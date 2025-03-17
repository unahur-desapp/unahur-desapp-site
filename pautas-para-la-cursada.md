---
layout: default
---

# Pautas para la cursada

Se detallan algunos puntos que viene bien (creo) tener en cuenta.

## Antes que nada - condiciones de aprobación

Para aprobar cualquiera de las dos materias (o sea Desarrollo de Aplicaciones y PPS) tenemos condiciones grupales e individuales.

Las condiciones grupales son

- entregar en tiempo y forma las fichas de inicio y fin de sprint para cada sprint.
- realizar las reuniones de cierre de sprint para cada sprint, en las fechas indicadas en el cronograma que se publica en este mismo sitio para cada cuatrimestre. <br/> A partir del sprint 2 para Desarrollo de Aplicaciones, y en todos los sprints en PPS, estas reuniones incluyen la presentación de los avances sobre la aplicación corriendo.
- mantener el Trello actualizado durante la cursada.
- realizar la presentación final presencial basada en una demo de la aplicación en vivo, y estar organizada a partir de un PPT o similar.
- para PPS se suman: un resumen que debe ser aprobado por el Consejo Directivo del Instituto de Ingeniería, una carpeta que se presenta al jurado, y una PPT o similar que debe ser parte de la presentación final. Para los trabajos de PPS se arma un jurado que evalúa carpeta y presentación, y a partir de estos elementos se define la nota entre el jurado y los profesores. <br/> Van a encontrar ejemplos de carpeta en [esta página](./pautas-para-la-carpeta).

Las condiciones individuales son

- asistencia a todos los cierres de sprint y participación (o sea, en los cierres de sprint todos tienen que hablar), salvo ausencia muy (pero muy) justificada. Esta asistencia puede ser virtual. Quien no tiene una participación activa en una actividad, es como si no hubiera asistido.
- asistencia a la presentación final, **ojo** esta es presencial para los alumnos (puede ser virtual para profes y/o jurado). En la presentación final también tienen que hablar todos.
- **muy importante** <br> participación efectiva en el desarrollo, que se va a evaluar por cantidad y relevancia de los commits hechos por cada integrante en los repositorios de frontend y backend. O sea, quienes no tengan commits o tengan poquitos y/o poco relevantes, no van a aprobar la materia. <br/> Si trabajan en grupo (lo cual está perfecto), por favor roten quién hace los commits (un día uno, otro día otro). A este respecto es válido, si un commit lo hicieron entre varios, que en el comentario pongan "hecho en conjunto con X, Y y Z", aparte del que registra el commit claro.

## Dinámica de la cursada

El desarrollo se **tiene** que organizar en sprints, esto no es optativo.
En principio, un sprint dura tres semanas. Si algún grupo necesita, se pueden acelerar los sprints, o sea hacerlos de menos de tres semanas; nunca de más de tres semanas.

- Al _principio_ de cada sprint se establecen los objetivos, qué se espera que esté hecho o avanzado o definido o lo que sea al final del sprint.
- Al _final_ de cada sprint se hace una evaluación de qué se logró y qué no, se trata de entender por qué no se llegó a lo que no se llegó, y a partir de estos elementos, se planifica el siguiente.

El corte de un sprint a otro coincide con el día y hora del encuentro semanal. En el encuentro de esa semana se hace el análisis de fin-de-sprint, y se habla del alcance del siguiente, que después el grupo tiene que plasmar en la ficha de inicio.

La definición y evaluación de cada sprint forma parte de la evaluación de la materia.

> **Nota**  
> En la página de [recursos](./recursos/recursos-index), están las fichas de principio y fin de sprint que hay que llenar, junto con ejemplos.  
> En los [detalles sobre uso del Trello](./recursos/trello), se detalla cómo proceder al principio y al final de cada sprint respecto de las tareas definidas.

### Manejo de grupo

Los docentes _no_ vamos a inmiscuirnos con la relación entre lxs integrantes de cada grupo. Podemos hacer quejas sobre el comportamiento de un integrante y tomarlas en cuenta para la evaluación que hacemos del funcionamiento del grupo, pero no vamos a intervenir ni intentar resolver cuestiones dentro de un grupo. Lo intentamos con nuestra mejor voluntad en cursadas anteriores, con un resultado muy malo.

Los grupos **no** se pueden separar una vez comenzada la cursada. Se puede intentar, sin promesas, hacer cambio de grupo hasta la primer semana del sprint 2, después no.

## Qué es lo que hay que construir

Una aplicación Web, que idealmente que tenga una salida a celular, o al menos cuidar un poco que la UI sea [responsive](https://www.w3schools.com/css/css_rwd_intro.asp).

## Cómo documentar los requerimientos

Se recomienda fuertemente que los acuerdos que se establezcan con les stakeholders / usuaries se basen en pantallas y flujos de navegación. Eso es, creo, lo que mejor sitúa a gente que no es del gremio en qué puede esperar de una app.

Se pueden armar user stories ... en forma gráfica, mostrando la sucesión de pantallas que van a ir apareciendo.

En la primer reunión que tuvimos se mencionó (creo) una descripción general (no me acuerdo cómo la llamaron) ... OK si no ocupa más de media carilla / 2K de texto.

Un documento viejo, pero que puede servir, es la lista de requerimientos, una lista de bullets con lo que se espera de la aplicación, donde cada bullet no lleva más de un renglón o dos.

## Para llevar la organización del desarrollo

Se propone usar [Trello](https://trello.com/), una herramienta de manejo de tareas liviana y sencilla, basada en listas de tareas.
Se va a proponer una organización para el proyecto Trello, eso va a aparecer en este sitio en breve.

Una alternativa es llevar los issues en el mismo repo de GitHub que el código.

Otra alternativa es [JIRA](https://www.atlassian.com/es/software/jira) ... pero no sé si tiene versión en-la-nube. Es más completo, y (bastante) más pesado.

## Guía para organizarse - priorizar la funcionalidad específica

Ponerle foco a la funcionalidad, a lo que le interesa a les usuaries, más que a las cuestiones técnicas.

Se recomienda ir del front hacia el back, se puede empezar con un back fake (que devuelva valores fijos o con una variación mínima) que ayude a establecer la API.

Las cuestiones no ligadas a la funcionalidad específica, como autenticación/autorización, **no** se encaran al principio.  
Si quieren manejar desde el principio interfaces diferenciadas por roles, pueden: definir un atributo `rol` en la UI, y URLs separadas para cada rol, que definan el valor del atributo y ruteen, p.ej. `/admin`, `/docente`, `/alumno`.

## Arquitectura de software

El proyecto tiene que responder a estos dos principios:

1. frontend y backend separados. Si el back se pone muy gordo, se puede evaluar partirlo en varios (micro)servicios.
1. comunicación con una API HTTP, el front le hace requests al back. JSON para la representación de información en los payloads de requests y responses.

Se recomienda fuertemente, y se da soporte para, basar tanto frontend como backend en JavaScript (JS) o TypeScript (TS).

Para el **frontend**, se propone basarlo en React. Entre los [recursos](./recursos) incluimos un repositorio que pueden usar de base, basado en JS.

Para el **backend**, se pueden elegir dos cosas.

1. si usar una base SQL o bien MongoDB con Mongoose.
2. si hacerlo en JS o en TS.

Esto nos da cuatro combinaciones: SQL/JS, SQL/TS, Mongo/JS, Mongo/TS.

Para la combinación SQL/JS, incluimos un repositorio que pueden usar de base en la página de [recursos](./recursos).

Para experimentar con TS, se propone usar el framework [NestJS](https://nestjs.com/). En la página de [First steps](https://docs.nestjs.com/first-steps) se explica cómo instalarlo.  
Nest resuelve en forma sencilla la integración, tanto con [Mongoose](https://docs.nestjs.com/techniques/mongodb) como con [TypeORM](https://docs.nestjs.com/techniques/database), un ORM que es (creo) más feliz que Sequelize, y que se lleva muy bien con TS.

Si quieren usar la combinación Mongo/JS ... hablemos sobre cómo hacer.

Se pueden proponer otras opciones ... pero se pierde el soporte docente.

### Atención - evolución de la BD

No olvidar el tema de las _migraciones_ de BD, para que no sea un garronazo el mantenimiento de la BD a medida que avanzan en el proyecto. Esto sobre todo para bases SQL.

## Organización del código

En repositorios GIT, creando dos repos, uno para el backend y otro para el frontend. Se puede usar [GitHub](https://github.com/) (les van a resultar más fáciles algunas tareas) o [GitLab](https://gitlab.com/) (repos privados infinitos gratis), también existe [BitBucket](https://bitbucket.org/product) pero no se recomienda.  
En cualquier caso, tienen que incluir a todos los docentes para que al menos puedan ver el repo y hacerle comentarios.

**No vale** trabajar en un único branch. Se recomienda manejarse con estos branches.

- uno `main` que sólo se actualiza cuando hay cosas nuevas que se pueden mostrar a un usuarie.
- uno `dev` que es la base del desarrollo.
- uno para cada tarea que se defina. Estos branches salen de `dev` y se mergean a `dev`.

Vale trabajar con [Pull Requests](https://yangsu.github.io/pull-request-tutorial/) para mergear a `dev`.

## Actividades

Vamos a tener una sesión semanal, para la reunión de fin de sprint cuando corresponda, para revisar la marcha y resolver dudas las otras.  
Está la intención de ir mechando charlas sobre temas que les vienen bien para el proyecto, eso lo vamos a ir reflejando en [la página de actividades](./actividades).
