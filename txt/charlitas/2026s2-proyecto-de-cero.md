# Antes
Muestro para dónde vamos: gestión de torneos de tenis. Vemos el enunciado un toque. Vemos lo que se llegó a implementar.

# Arrancamos
Vamos a ir monorepo. 
Creamos la estructura: /backend, /doc, /frontend.
En /doc meto enunciado.md.

# Qué modelo
Dado que MiniMax M2.5 no está más, sigo la recomendación de Claude de usar DeepSeek V4 Flash, le mandé high por temor a que max se hiciera demasiado lento.

# Comentarios iniciales 
El editor de la consola es choto, yo lo que hago es escribir los prompts en un editor de texto y pegarlos en la consola de OpenCode.

Actualícense al nuevo OpenCode quienes tengan una versión vieja. A mí me propuso actualizarme y le dije que sí nomás. Versión 1.18.15. Mucho mejor experiencia de usuario que el cuatri pasado.


# Arranco distinto
Mi nuevo primer prompt.

Necesito que te comportes como un Leader Técnico con una amplia experiencia en desarrollo en Node.js y con mucha experiencia en análisis de sistemas. Esto es crucial para ir trabajando en cada tarea que te solicite.
El objetivo general es desarrollar una aplicación Web responsiva que responda a los requerimientos que se explican en doc/enunciado.md. 
La arquitectura básica es: frontend y backend deployados en forma separada, aunque en un mismo repo dentro de las carpetas /frontend y /backend; comunicación via API REST.
Para empezar, te pido que a partir de un análisis de estos requerimientos, generes un documento inicial que describa: 
- las funcionalidades que deben desarrollarse para cumplir con lo que pide el enunciado, vinculando cada una con citas concretas del enunciado.
- un mapa inicial de páginas que sugerís para la app Web.
- un esquema inicial para los endpoints necesarios para soportar las funcionalidades necesarias.
   
Ufff tardó unos 6 minutos.

Se lo mandé también a Claude con Opus 1M, tardó unos 3/4 minutos. Los comentarios en ai-generated-docs/. Podemos parar un par de minutos para ver las diferencias.

Después pedí un foco en torneos, pidiendo recorte + detalle de páginas y endpoints, ir a detalle con datos / body / response, e incluir modelo de datos.

Tardó 13 minutos. Me doy cuenta que va por las opciones obvias, p.ej. páginas aparte para manejar parejas, tabla de relación entre pareja y jugador, se olvidó que las categorías son configurables.
Por otro lado, qué maravilla el gráfico de la BD.

Un par de prompts de ajuste (prompts 3 y 4). Los detalles de que las categorías tienen que tener los puntos, o que a los jugadores tal vez le falta data de ranking, los dejo para después. Relacionar esto con el valor que provee el producto.
Parte del prompt 3, y todo el prompt 4, surgen de imaginarme la experiencia de usuario. Acá se puede, una vez que se llegó a una comprensión básica, jugar en paralelo con el mockup de pantallas y el ir llegando a una especificación más detallada.

Los prompts tardaron 4 y 2.6 minutos respectivamente.

# Voy por FE primero
Al contrario de lo que había hecho el cuatri pasado.

El prompt 5 lo mandé derecho, sin plan, que arme una estructura inicial y después vemos.

Notable la cantidad de veces que se equivocó ... y se corrigió.

Atenti una cosa, esto me dijo OpenCode.
Nota: el scaffold de create-vite generó un template vanilla en vez de react-ts; lo reconstruí manualmente. Puedés correrlo con cd frontend && npm run dev. ¿Siguiente: las pantallas de detalle de torneo (inscripciones) o pasamos al backend?
Pueden especificar que use el template correcto, eso lo buscan en la doc de Vite.

Acá se puede mostrar el package.json y algo de código (que veremos en detalle en una clase específica).

*Muy importante*  
generar un .gitignore si no lo hace la IA, es **mega-incorrecto** incluir los node_modules en el repo. Ojo ahí.
Yo lo tuve que hacer en FE y también en BE. Conviene tenerlos separados.

*Una pavada que puede ser útil*  
La IA puede tener ganas de levantar el FE mediante npm run dev, y a veces no mata el proceso, eso es molesto porque después hay que encontrarlo y matarlo nosotros. Ahora lo mató, bien ahí. Siempre me olvido y le pregunto a la IA (que me hace vago, confieso).


# Pasamos al BE

Contar un toque la base, y cómo pruebo la BD / los endpoints.

Acá metimos un mínimo AGENTS.md.

Si da, podemos revisar el controller de torneos y matchar con las llamadas API.

Cómo levantar BE y FE -> mirar en package.json. Ver la colección de Insomnia que me armé ... también se le puede pedir a la IA que la arme, genera un JSON que se importa desde Insomnia (mostrar el del cuatri pasado).

Le pegamos una mirada al .env. En rigor, si la clave no es de desarrollo o no es compartida, no va en el repo.

Notable que el GET de torneos devuelve los datos de la categoría. Me pregunto si lo hubiera hecho así de no armar el mockup de FE antes.


# Conectamos

Acá sí pedí plan y lo peloteé un poco.

Notar que al conocer FE y BE, puede hacer solo la conexión, incluso se da cuenta de detalles sobre los query params del GET de torneos.

Ver comentario sobre filtrar en FE o en BE.

Mostrar network ... mencionar el debounce (que sólo sé que existe, no sé qué es ni cómo setearlo) para evitar que busque a cada teclazo.


# Hagamos algo en vivo

## Pantalla de detalle de torneo
Vamos desde el primer plan (tag 05), para mostrar cómo pedirle modificaciones.
Después del ajuste que pedí, todavía hay una cosa que no me gustó (Editar no debería estar habilitado si el torneo tiene inscripciones cerradas), la hago a mano (esto se puede ver con el tag 07).

## Otras ideas
- Desde el tag 03, GenerarJugadoresDto no está usado.
- Errores de compilación por campos no inicializados.


## Comentarios
Acá mostrar lo del consumo de tokens del contexto, el límite, y la posibilidad de compactar.


# Comentario lateral
A partir de este prompt (OK, en Claude pago), después de pelotear para entender qué plataformas puede convenir usar para deployar el ejemplo que estamos mostrando, le puse este prompt.

ok, let's go with this combination
- DB: Neon
- BE: Render
- FE: Vercel
Please prepare a document that I can download, including all the information I could need to actually make this work. Take into account that I'm not super smart regarding infrastructure/deploy stuff. Thanks!

Generó ai-generated-docs\deployment-guide-neon-render-vercel.md.


# Para la charla de React
Mostrar definición de AppShell con uso de Outlet.
Interesante el useEffect para cargar torneos en TorneosPage.tsx.