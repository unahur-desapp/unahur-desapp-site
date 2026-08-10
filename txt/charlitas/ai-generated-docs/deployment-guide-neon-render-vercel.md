# Deployment Guide — NestJS + React/Vite + Postgres

**Stack:** Neon (database) → Render (backend) → Vercel (frontend)

This guide assumes you know how to build the app but not much about infrastructure. Every step is spelled out. Total time for a first deploy: **60–90 minutes**. After that, deploys are automatic on `git push`.

---

## Table of contents

1. [How the pieces fit together](#1-how-the-pieces-fit-together)
2. [Before you start](#2-before-you-start)
3. [Part A — Database on Neon](#3-part-a--database-on-neon)
4. [Part B — Prepare the NestJS code](#4-part-b--prepare-the-nestjs-code)
5. [Part C — Deploy the backend to Render](#5-part-c--deploy-the-backend-to-render)
6. [Part D — Prepare the React/Vite code](#6-part-d--prepare-the-reactvite-code)
7. [Part E — Deploy the frontend to Vercel](#7-part-e--deploy-the-frontend-to-vercel)
8. [Part F — Close the loop (CORS)](#8-part-f--close-the-loop-cors)
9. [Troubleshooting](#9-troubleshooting)
10. [Pre-lecture checklist](#10-pre-lecture-checklist)
11. [Appendix — environment variable reference](#11-appendix--environment-variable-reference)
12. [Appendix — costs and limits](#12-appendix--costs-and-limits)

---

## 1. How the pieces fit together

```
   Browser
      │
      │  https://my-app.vercel.app
      ▼
┌─────────────────┐
│     VERCEL      │   Static files (HTML/JS/CSS) built from your Vite project.
│   (frontend)    │   No server. Just files on a CDN.
└─────────────────┘
      │
      │  fetch("https://my-api.onrender.com/...")
      ▼
┌─────────────────┐
│     RENDER      │   Your NestJS app running as a real Node process
│    (backend)    │   in a container, 24/7 (with a nap on the free plan).
└─────────────────┘
      │
      │  postgresql://...neon.tech/...
      ▼
┌─────────────────┐
│      NEON       │   Managed Postgres. Sleeps when idle, wakes in ~1s.
│   (database)    │
└─────────────────┘
```

**Three separate services, three separate dashboards.** They only know about each other through **environment variables** — strings you paste from one dashboard into another.

That's genuinely the whole concept. If you understand that, the rest is clicking buttons in the right order.

### The order matters

Deploy **bottom-up**, because each layer needs a URL from the one below it:

1. **Neon first** → gives you a `DATABASE_URL`
2. **Render second** → you paste `DATABASE_URL` in; it gives you an API URL
3. **Vercel third** → you paste the API URL in; it gives you a site URL
4. **Back to Render** → paste the site URL in as `FRONTEND_URL` (for CORS)

Step 4 is the loop-closer that trips people up. Don't skip it.

---

## 2. Before you start

### Checklist

- [ ] Code is pushed to **GitHub** (all three platforms deploy from a Git repo)
- [ ] `package-lock.json` is **committed** in both backend and frontend (needed for `npm ci`)
- [ ] `.env` files are in `.gitignore` — never commit secrets
- [ ] The app runs locally with `npm run start:dev` / `npm run dev`
- [ ] Accounts: [neon.com](https://neon.com), [render.com](https://render.com), Vercel (you have this)

### One repo or two?

Both work. Note which one you have, because it changes one setting later:

| Layout | What to set |
|---|---|
| **Two repos** (`my-app-api`, `my-app-web`) | Nothing special. Root Directory stays empty. |
| **One repo** (`/backend`, `/frontend`) | Set **Root Directory** = `backend` on Render, `frontend` on Vercel. |

A monorepo is fine and arguably nicer for a course — one repo for students to clone.

### A note on secrets

You will be copying database passwords around. Rules:

- Secrets live in **`.env` locally** (gitignored) and in the **platform dashboard** in production.
- Never in the code, never in a commit, never in a screenshot during the lecture.
- Commit a `.env.example` with the *names* but fake values, so students know what's needed.

---

## 3. Part A — Database on Neon

### A.1 Create the project

1. Go to [neon.com](https://neon.com) → **Sign up** (GitHub login is fastest, no credit card).
2. **Create a project**:
   - **Name**: `demo-project` (or your course name)
   - **Postgres version**: leave the default
   - **Region**: **Europe (Frankfurt)** — you're in Italy, and Render also offers Frankfurt. Keeping both in the same region keeps queries fast. ⚠️ **You cannot change the region later**, so get this right.
3. Click **Create**.

That's it — you have a Postgres database. It took 5 seconds because Neon doesn't provision a server; it just gives you a database.

### A.2 Grab the connection string

On the project dashboard there's a **Connection string** box. It looks like:

```
postgresql://neondb_owner:npg_AbCd1234@ep-cool-name-a1b2c3-pooler.eu-central-1.aws.neon.tech/neondb?sslmode=require
```

Copy it into a scratch file. Note two things:

- **`-pooler`** in the hostname — this is the *pooled* connection. **Use this one for your app.** It lets many connections share a few real ones, which matters because Render restarts your service and each restart opens new connections.
- **`?sslmode=require`** at the end — Neon requires encrypted connections. Keep this. If you drop it you'll get a confusing SSL error.

There's a toggle in the Neon UI to show the **direct** (non-pooled) string. You only need it if you use **Prisma** (see below). For TypeORM, the pooled string is fine everywhere.

### A.3 Test it before going further

Best 30 seconds you'll spend. Put the string in your **local** `.env` and run the backend locally against the cloud database:

```bash
# backend/.env
DATABASE_URL="postgresql://neondb_owner:npg_...@ep-...-pooler.eu-central-1.aws.neon.tech/neondb?sslmode=require"
```

```bash
npm run start:dev
```

If the app boots and can query, your database half is **done and proven**. Any error later is Render's fault, not Neon's — which massively narrows down debugging.

> **Tip for the lecture:** Neon has a **Branches** feature — instant copies of your database. You could keep a `main` branch with clean demo data and a `dev` branch you're free to break. Nice thing to show off, and it costs nothing.

---

## 4. Part B — Prepare the NestJS code

Five small changes. Do them all before deploying; each one prevents a specific failure.

### B.1 Listen on the right port and interface

**This is the #1 cause of "deploy succeeded but the site is down."** Render assigns a port via the `PORT` environment variable and expects you to listen on it, on all network interfaces.

```ts
// src/main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // CORS — see B.2
  const allowedOrigins = (process.env.FRONTEND_URL ?? '').split(',').filter(Boolean);
  app.enableCors({
    origin: allowedOrigins.length ? allowedOrigins : true,
    credentials: true,
  });

  // Render provides PORT. 3000 is the local fallback.
  const port = process.env.PORT ?? 3000;
  await app.listen(port, '0.0.0.0'); // 0.0.0.0, NOT localhost
}
bootstrap();
```

Why `'0.0.0.0'`: inside a container, `localhost` means "only reachable from inside this container." Render's router is outside, so it never gets in and eventually times out. `0.0.0.0` means "accept connections from anywhere."

### B.2 CORS

Browsers block a page on `my-app.vercel.app` from calling `my-api.onrender.com` unless the API explicitly says it's allowed. That's what `enableCors` above does.

`FRONTEND_URL` will be set on Render **after** Vercel gives you a URL (Part F). Until then the fallback `origin: true` allows everything, which is fine while you're setting things up.

**Gotchas:**
- **No trailing slash.** `https://my-app.vercel.app` ✅ — `https://my-app.vercel.app/` ❌
- Include `https://`, not just the domain.
- Vercel preview deployments get random URLs (`my-app-git-feature-you.vercel.app`). If you need those too, comma-separate them, or use a regex origin.

### B.3 Database connection with SSL

**TypeORM** (`app.module.ts`):

```ts
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    ConfigModule.forRoot({ isGlobal: true }),
    TypeOrmModule.forRoot({
      type: 'postgres',
      url: process.env.DATABASE_URL,
      ssl: { rejectUnauthorized: false }, // required by Neon
      autoLoadEntities: true,
      synchronize: false,   // ⚠️ see below
      migrationsRun: true,  // apply pending migrations at boot
      migrations: ['dist/migrations/*.js'],
    }),
  ],
})
export class AppModule {}
```

**Prisma** (`schema.prisma`) — Prisma needs *both* strings: pooled for queries, direct for migrations.

```prisma
datasource db {
  provider  = "postgresql"
  url       = env("DATABASE_URL")        // the -pooler string
  directUrl = env("DIRECT_URL")          // the non-pooled string
}
```

> **`synchronize: true` — turn it off.**
> It's convenient locally (schema auto-updates from your entities), but in production it can silently drop columns and take your demo data with it. Use migrations. If you're teaching, `synchronize: false` + migrations is the professional habit worth passing on.

### B.4 Health check endpoint

Gives Render something cheap to ping, and gives *you* a URL to test that doesn't touch the database — so you can tell "app is down" apart from "database is down."

```ts
// src/app.controller.ts
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get('health')
  health() {
    return { status: 'ok', timestamp: new Date().toISOString() };
  }
}
```

### B.5 Scripts and Node version

```jsonc
// package.json
{
  "engines": {
    "node": ">=20.0.0"          // stops Render picking an old Node
  },
  "scripts": {
    "build": "nest build",
    "start:prod": "node dist/main",
    // if using TypeORM migrations:
    "migration:run": "typeorm-ts-node-commonjs migration:run -d ./src/data-source.ts"
  }
}
```

Make sure `@nestjs/cli` and `typescript` are in **`dependencies`**, not `devDependencies`, *or* that your build command installs dev dependencies. Render runs `npm ci` which installs both by default — but if you've set `NODE_ENV=production` it will skip devDependencies and the build will fail with `nest: not found`. Simplest fix: don't set `NODE_ENV=production` on Render, or move the build tools to `dependencies`.

### B.6 Seed some demo data

For a live demo, an empty screen is a bad look. Write a seed script and run it once after deploying:

```ts
// src/seed.ts — run with: npx ts-node src/seed.ts
```

You can run it locally pointed at the Neon `DATABASE_URL` — it's the same database Render will use. No need to run it on Render at all.

---

## 5. Part C — Deploy the backend to Render

### C.1 Create the service

1. [render.com](https://render.com) → sign up with GitHub → **New +** → **Web Service**
2. Connect your GitHub account, pick the repository
3. Fill in the form:

| Field | Value |
|---|---|
| **Name** | `my-app-api` → becomes `https://my-app-api.onrender.com` |
| **Region** | **Frankfurt (EU Central)** — same region as Neon |
| **Branch** | `main` |
| **Root Directory** | *empty* if backend-only repo; `backend` if monorepo |
| **Runtime** | Node |
| **Build Command** | `npm ci && npm run build` |
| **Start Command** | `npm run start:prod` |
| **Instance Type** | **Free** |

### C.2 Add environment variables

Scroll to **Environment Variables** → **Add Environment Variable**:

| Key | Value |
|---|---|
| `DATABASE_URL` | the Neon pooled connection string |
| `NODE_VERSION` | `20` |
| `FRONTEND_URL` | leave empty for now — you'll fill it in Part F |

Do **not** add `PORT`. Render sets it automatically, and overriding it breaks things.

### C.3 Health check path

Under **Advanced** (or Settings after creation), set **Health Check Path** to `/health`. Render uses this to know when your service is actually ready.

### C.4 Deploy

Click **Create Web Service**. The first build takes 3–8 minutes — watch the log stream. You want to end with a line like `Nest application successfully started` and then **Your service is live 🎉**.

### C.5 Verify

```bash
curl https://my-app-api.onrender.com/health
# {"status":"ok","timestamp":"..."}
```

Then hit an endpoint that reads from the database. If that works, your backend and database are **both** confirmed working. Write the URL down.

> **⚠️ The free plan sleeps.** After 15 minutes with no traffic, Render shuts the service down. The next request takes **30–60 seconds** while it boots — which is an eternity in front of a classroom. Mitigations, in order of preference:
> 1. **Open the app 5–10 minutes before you present.** Free, reliable, zero setup. Just remember to do it.
> 2. **Upgrade to Starter ($7/month)** for the month of the course. No sleeping. If the demo matters, this is $7 well spent.
> 3. A cron pinger (UptimeRobot etc.) hitting `/health` every 10 minutes. Works, but burns your monthly instance hours and is against the spirit of the free tier.

---

## 6. Part D — Prepare the React/Vite code

### D.1 The one thing to understand about Vite env vars

**Vite bakes environment variables into the JavaScript bundle at build time.** They are not read when the page loads — they're already hardcoded in the compiled file.

Consequences:

- Variables **must** start with `VITE_` or Vite ignores them entirely.
- Changing a variable in the Vercel dashboard does nothing until you **redeploy**.
- **Never put secrets in `VITE_` variables.** Anyone can open DevTools and read them. API base URLs are fine. API *keys* are not.

### D.2 Wire up the API URL

```bash
# frontend/.env.local  (gitignored)
VITE_API_URL=http://localhost:3000
```

```bash
# frontend/.env.example  (committed — documents what's needed)
VITE_API_URL=
```

```ts
// src/lib/api.ts
const API_URL = import.meta.env.VITE_API_URL;

if (!API_URL) {
  throw new Error('VITE_API_URL is not set — check your .env file');
}

export async function apiFetch(path: string, options?: RequestInit) {
  const res = await fetch(`${API_URL}${path}`, {
    ...options,
    headers: { 'Content-Type': 'application/json', ...options?.headers },
  });
  if (!res.ok) throw new Error(`API error ${res.status}`);
  return res.json();
}
```

Search your codebase for any remaining hardcoded `http://localhost:3000` and replace it. Leftovers are a classic — everything works until one page silently fails in production.

### D.3 SPA routing fix

If you use React Router: `https://my-app.vercel.app/products` works when you click a link, but **404s when someone refreshes the page**. Vercel looks for a file called `products` and doesn't find one.

Create `vercel.json` in the frontend root:

```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

This says "whatever the path, serve index.html and let React Router figure it out."

**Do this even if you don't think you need it.** Refreshing a deep link is exactly the kind of thing that happens during a live demo.

---

## 7. Part E — Deploy the frontend to Vercel

You already know Vercel from your Next.js project. Two differences for a Vite app.

### E.1 Import the project

1. Vercel dashboard → **Add New** → **Project** → import the repo
2. **Framework Preset**: Vercel should detect **Vite**. If it says "Other," set it to Vite manually.
3. **Root Directory**: empty for a frontend-only repo, `frontend` for a monorepo
4. Build settings (usually auto-filled correctly):
   - Build Command: `npm run build`
   - Output Directory: **`dist`** ← *this is the Vite difference. Next.js uses `.next`; Vite uses `dist`.* If Vercel guessed wrong you'll get a blank page or a build error.
   - Install Command: `npm install`

### E.2 Environment variable

Before deploying, expand **Environment Variables**:

| Key | Value | Environments |
|---|---|---|
| `VITE_API_URL` | `https://my-app-api.onrender.com` | Production, Preview, Development |

No trailing slash — your `apiFetch` adds the path.

### E.3 Deploy

Click **Deploy**. A Vite build takes about a minute. You'll get `https://my-app.vercel.app`.

Open it. Expect one of two things:

- ✅ It works → go to Part F to lock down CORS
- ❌ A **CORS error** in the browser console → that's expected, Part F fixes it

Either way, write down your Vercel URL.

---

## 8. Part F — Close the loop (CORS)

The final connection: telling the backend which frontend is allowed to call it.

1. Render dashboard → your service → **Environment**
2. Edit `FRONTEND_URL`:
   ```
   https://my-app.vercel.app
   ```
   No trailing slash. Include `https://`.
3. **Save Changes** — Render redeploys automatically (~2 minutes)
4. Reload your Vercel site. Everything should now work end to end.

If you want preview deployments to work too, comma-separate them:

```
https://my-app.vercel.app,https://my-app-git-dev-you.vercel.app
```

### Alternative: skip CORS entirely

If CORS keeps fighting you, there's a trick: have Vercel proxy API calls, so the browser thinks everything is on one domain and CORS never applies.

`vercel.json`:

```json
{
  "rewrites": [
    { "source": "/api/:path*", "destination": "https://my-app-api.onrender.com/:path*" },
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

Then set `VITE_API_URL=/api` and redeploy. Order matters — the API rule must come first.

Trade-off: it's a nice trick to show students, but it hides what's happening. For teaching purposes the explicit CORS version is more honest about how browsers actually work. Keep this as your escape hatch.

---

## 9. Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| Render build succeeds, then **"Timed out waiting for port"** | Listening on `localhost` or a hardcoded port | `app.listen(process.env.PORT ?? 3000, '0.0.0.0')` |
| **`nest: not found`** during build | `NODE_ENV=production` skipped devDependencies | Remove that env var, or move `@nestjs/cli` to `dependencies` |
| **`Cannot find module '/app/dist/main'`** | Build didn't run, or wrong Root Directory | Check Build Command is `npm ci && npm run build`; check Root Directory matches your folder |
| **`no pg_hba.conf entry ... no encryption`** | Missing SSL | Keep `?sslmode=require` in the URL **and** `ssl: { rejectUnauthorized: false }` in TypeORM |
| **`sorry, too many clients already`** | Using the direct Neon string | Switch to the `-pooler` connection string |
| Browser: **"blocked by CORS policy"** | `FRONTEND_URL` wrong/missing/trailing slash | Part F. Check the exact origin in the error message matches exactly |
| **First request takes ~50 seconds**, then it's fast | Free plan cold start | Expected. Warm it up before the lecture |
| Frontend shows **blank white page** | Wrong Output Directory | Should be `dist` for Vite |
| **404 on page refresh** but links work | Missing SPA rewrite | Add `vercel.json` rewrites (D.3) |
| `import.meta.env.VITE_API_URL` is **undefined** | Missing `VITE_` prefix, or not redeployed after adding it | Rename the variable; redeploy |
| Changed env var on Vercel, **nothing happened** | Vite bakes vars at build time | Deployments → ⋯ → **Redeploy** |
| API works in Postman, **fails in browser** | Almost always CORS | Check the browser console, not the network tab alone |
| Tables don't exist | Migrations never ran | Run them locally against `DATABASE_URL`, or set `migrationsRun: true` |

### General debugging method

Test each layer in isolation, bottom-up:

1. **Database:** run the backend *locally* against the Neon URL. Works? Database is fine.
2. **Backend:** `curl https://my-app-api.onrender.com/health`. Works? Backend is fine.
3. **Backend + DB:** `curl` an endpoint that queries data. Works? Connection is fine.
4. **Frontend:** if 1–3 pass and the browser still fails, it's **CORS or the wrong `VITE_API_URL`**. Nearly always.

The **Logs** tab in Render is where the real error message lives. Read it before guessing.

---

## 10. Pre-lecture checklist

**The day before:**

- [ ] Full run-through: open the site, click every path you'll demo
- [ ] Demo data seeded and looking presentable
- [ ] ⚠️ **Check the Neon project is active** — if you haven't touched it in a while, open the dashboard and run a query
- [ ] Both URLs bookmarked
- [ ] Consider $7 Render Starter for the month — removes the cold-start risk entirely

**10 minutes before:**

- [ ] **Open the Vercel URL to wake the Render service** — then wait for it to fully load
- [ ] Load a page that hits the database (wakes Neon too)
- [ ] Have the Render Logs tab open in a background tab, in case you need to explain an error live
- [ ] Zoom your browser to ~125% for readability

**Have a plan B:** a screen recording of the working app, or the app running locally in a second window. If the internet fails in the room, you still have a demo.

---

## 11. Appendix — environment variable reference

### Backend (Render)

| Variable | Example | Notes |
|---|---|---|
| `DATABASE_URL` | `postgresql://...-pooler.../neondb?sslmode=require` | From Neon. Use the **pooled** one |
| `DIRECT_URL` | `postgresql://.../neondb?sslmode=require` | Prisma only. Non-pooled |
| `FRONTEND_URL` | `https://my-app.vercel.app` | For CORS. No trailing slash |
| `NODE_VERSION` | `20` | Pins the Node version |
| `PORT` | — | ❌ Don't set. Render provides it |

### Frontend (Vercel)

| Variable | Example | Notes |
|---|---|---|
| `VITE_API_URL` | `https://my-app-api.onrender.com` | Must start with `VITE_`. Public — no secrets. Redeploy after changing |

### Local development (`.env`, gitignored)

```bash
# backend/.env
DATABASE_URL="postgresql://...-pooler...neon.tech/neondb?sslmode=require"
FRONTEND_URL="http://localhost:5173"
PORT=3000

# frontend/.env.local
VITE_API_URL=http://localhost:3000
```

Note you can point your local backend at the **same Neon database** — one less thing to install, and students can share a database if you want. (For real projects, use a separate Neon branch per developer.)

---

## 12. Appendix — costs and limits

| Service | Free tier | Watch out for | Paid |
|---|---|---|---|
| **Neon** | 0.5 GB storage, 100 compute-hours/month per project. Permanent — doesn't expire. Sleeps after 5 min idle, wakes in ~1s | Nothing serious for a demo | ~$19/mo |
| **Render** | Web service: 512 MB RAM, 750 hours/month | **Sleeps after 15 min → 30–60s cold start.** Also: the free *Postgres* expires after 30 days — irrelevant for you, since you're using Neon | $7/mo removes sleeping |
| **Vercel** | Generous for static sites | Nothing for this use case | — |

**Total: €0.** Optionally €7/month for Render Starter during the course to eliminate cold starts.

> Free-tier terms change often — all three companies have adjusted theirs in the past year. If something in this table doesn't match what you see, trust the dashboard.

### Why this stack, in one line each (useful for the lecture)

- **Neon** — Postgres that costs nothing when idle, and whose free tier doesn't expire out from under a months-long course.
- **Render** — runs your NestJS app as a normal long-lived Node process, which is what a Nest app actually wants to be. No serverless workarounds.
- **Vercel** — a compiled Vite app is just static files; this is the best possible way to serve static files, and you already know it.

The transferable lesson for your students isn't the three brand names — it's the shape: **static frontend / stateful backend / managed database, connected by environment variables.** Swap in any provider and the diagram is identical.
