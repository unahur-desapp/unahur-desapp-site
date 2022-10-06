# Git

Juntamos en esta página/sección el material relacionado con Git.

## Las recetas para manejarnos en el trabajo en grupo
Dejamos acá escritas las "recetas" que recomendamos para el trabajo diario con repositorios de Git compartidos.


### Cuando empiezo una tarea
- `git checkout dev`
- `git pull`
- `git checkout -b <branch-de-mi-tarea>`

### Trabajo diario
**Cuando arranco**
- `git checkout dev`
- `git pull`
- `git checkout <branch-de-mi-tarea>`

**Mientras trabajo**  
`git commit`  
a cada rato. 

**Antes de salir de la compu**  
`git push`  
No le cambio el código a nadie a nadie porque pusheo en mi branch, y si rompo mi repo local, siempre está el respaldo en el repo remoto.

### Cuando termino una tarea
Acá tenemos dos variantes, usar `rebase` o usar `merge`.

Si usamos `rebase`:
- `git checkout dev`
- `git pull`
- `git checkout <branch-de-mi-tarea>`
- `git rebase dev`
- ... pruebo que sigue andando ...
- `git push -f`

Si usamos `merge`:
- `git checkout dev`
- `git pull`
- `git merge <branch-de-mi-tarea>`
- ... pruebo que sigue andando ...
- `git push`


## Material para leer
Dentro de la documentación/material educativo sobre Git, lo que me parece más claro es la [serie de tutoriales de Atlassian](https://www.atlassian.com/es/git/tutorials).  
De tierno que soy se los dejo en castellano.

También les dejo acá algo que escribí en otro contexto, y tal vez les sirva. Son varias páginas.

**OJO** - no arranca de cero, el material que sigue asume que ya lo básico lo tenés.

[Git - intro](./git/git-intro)

[Los 'lugares' de Git](./git/git-espacios)

[Un repo es una red de commits](./git/git-commits)

["Deshaciendo" o "modificando" cambios - reset, commit --amend, revert](./git/git-reset)

[Repositorios remotos](./git/git-remote)

[Sincronización de branches - merge y rebase](./git/git-synchro-merge-rebase)

[Pull requests](./git/pull-requests)

[Modelos de branches](./git/branch-models)

[Git - algunos extras](./git/git-extras)


