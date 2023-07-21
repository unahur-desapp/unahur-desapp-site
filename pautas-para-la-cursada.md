---
layout: default
---

# Pautas para la cursada

Se detallan algunos puntos que viene bien (creo) tener en cuenta.


## Antes que nada - condiciones de aprobación
Para aprobar cualquiera de las dos materias (o sea Desarrollo de Aplicaciones y PPS) tenemos condiciones grupales e individuales.

Las condiciones grupales son
- entregar en tiempo y forma las fichas de inicio y fin de sprint para cada sprint.
- realizar las reuniones de cierre de sprint para cada sprint, en las fechas indicadas en el cronograma que se publica en este mismo sitio para cada cuatrimestre. <br/> A partir del sprint 3 para Desarrollo de Aplicaciones, y en todos los sprints en PPS, estas reuniones incluyen la presentación de los avances sobre la aplicación corriendo.
- mantener el Trello actualizado durante la cursada.
- realizar la presentación final presencial que debe incluir una demo de la aplicación en vivo, y estar organizada a partir de un PPT o similar.
- para PPS se suman: un resumen que debe ser aprobado por el Consejo Directivo del Instituto de Ingeniería, y una carpeta que se presenta al jurado. Para los trabajos de PPS se arma un jurado que evalúa carpeta y presentación, y a partir de estos elementos se define la nota entre el jurado y los profesores. <br/> Van a encontrar ejemplos de carpeta en [esta página](./pautas-para-la-carpeta).

Las condiciones individuales son
- asistencia a todos los cierres de sprint salvo ausencia muy (pero muy) justificada. Esta asistencia puede ser virtual.
- asistencia a la presentación final, **ojo** esta es presencial para los alumnos (puede ser virtual para profes y/o jurado).
- **muy importante** <br> participación efectiva en el desarrollo, que se va a evaluar por cantidad y relevancia de los commits hechos por cada integrante en los repositorios de frontend y backend. O sea, quienes no tengan commits o tengan poquitos y/o poco relevantes, no van a aprobar la materia. <br/> Si trabajan en grupo (lo cual está perfecto), por favor roten quién hace los commits (un día uno, otro día otro).




## Qué es lo que hay que construir
Una aplicación Web, que idealmente que tenga una salida a celular, o al menos cuidar un poco que la UI sea [responsive](https://www.w3schools.com/css/css_rwd_intro.asp).


## Cómo documentar los requerimientos
Se recomienda fuertemente que los acuerdos que se establezcan con les stakeholders / usuaries se basen en pantallas y flujos de navegación. Eso es, creo, lo que mejor sitúa a gente que no es del gremio en qué puede esperar de una app.

Se pueden armar user stories ... en forma gráfica, mostrando la sucesión de pantallas que van a ir apareciendo.

En la primer reunión que tuvimos se mencionó (creo) una descripción general (no me acuerdo cómo la llamaron) ... OK si no ocupa más de media carilla / 2K de texto.

Un documento viejo, pero que puede servir, es la lista de requerimientos, una lista de bullets con lo que se espera de la aplicación, donde cada bullet no lleva más de un renglón o dos.


## Tiempos
Se recomienda **mucho-mucho** pensar en un proyecto anual, o sea que se desarrolla durante dos cuatrimestres; involucrando Desarrollo de Aplicaciones en un primer cuatrimestre y la PPS en el siguiente.  
Al final del primer cuatrimestre hay que hacer un corte y una presentación, de ahí sale la nota de Desarrollo de Aplicaciones. Los requerimientos sobre este corte los vamos a ir definiendo a medida que avance el cuatrimestre.

El desarrollo se **tiene** que organizar en sprints, esto no es optativo. 
En principio, un sprint dura tres semanas. Si algún grupo necesita, se pueden acelerar los sprints, o sea hacerlos de menos de tres semanas; nunca de más de tres semanas.  
- Al _principio_ de cada sprint se establecen los objetivos, qué se espera que esté hecho o avanzado o definido o lo que sea al final del sprint.
- Al _final_ de cada sprint se hace una evaluación de qué se logró y qué no, se trata de entender por qué no se llegó a lo que no se llegó, y a partir de estos elementos, se planifica el siguiente.

El corte de un sprint a otro coincide con el día y hora del encuentro semanal. En el encuentro de esa semana se hace el análisis de fin-de-sprint, y si es necesario, se fija otro encuentro en esa misma semana para definir el alcance del siguiente.

La definición y evaluación de cada sprint forma parte de la evaluación de la materia.

> **Nota**  
En la página de [recursos](./recursos/recursos-index), están las fichas de principio y fin de string que hay que llenar, junto con ejemplos.  
En los [detalles sobre uso del Trello](./recursos/trello), se detalla cómo proceder al principio y al final de cada sprint respecto de las tareas definidas.

## Para llevar la organización del desarrollo
Se propone usar [Trello](https://trello.com/), una herramienta de manejo de tareas liviana y sencilla, basada en listas de tareas.
Se va a proponer una organización para el proyecto Trello, eso va a aparecer en este sitio en breve.

Una alternativa es llevar los issues en el mismo repo de GitHub que el código. Voy a intentar armar un ejemplo.

Otra alternativa es [JIRA](https://www.atlassian.com/es/software/jira) ... pero no sé si tiene versión en-la-nube. Es más completo, y (bastante) más pesado.


## Guía para organizarse - priorizar la funcionalidad específica
Ponerle foco a la funcionalidad, a lo que le interesa a les usuaries, más que a las cuestiones técnicas.

Se recomienda ir del front hacia el back, se puede empezar con un back fake (que devuelva valores fijos o con una variación mínima) que ayude a establecer la API. 

Las cuestiones no ligadas a la funcionalidad específica, como autenticación/autorización, **no** se encaran al principio.  
Si quieren manejar desde el principio interfaces diferenciadas por roles, pueden: definir un atributo `rol` en la UI, y URLs separadas para cada rol, que definan el valor del atributo y ruteen, p.ej. `/admin`, `/docente`, `/alumno`.


## Arquitectura de software
Se proponen estas definiciones iniciales
- frontend y backend separados. Si el back se pone muy gordo, se puede evaluar partirlo en varios (micro)servicios.
- comunicación con una API HTTP, el front le hace requests al back. JSON para la representación de información en los payloads de requests y responses.
- basar tanto frontend como backend en JavaScript (JS) o TypeScript (TS).

Para el **frontend**, se propone hacerlo en JS y basarlo en React. Entre los [recursos](./recursos) incluimos un repositorio que pueden usar de base.

Para el **backend**, se pueden elegir dos cosas.
1. si usar una base SQL o bien MongoDB con Mongoose.
1. si hacerlo en JS o en TS.

Esto nos da cuatro combinaciones: SQL/JS, SQL/TS, Mongo/JS, Mongo/TS.

Para la combinación SQL/JS, incluimos un repositorio que pueden usar de base en la página de [recursos](./recursos).

Para experimentar con TS, se propone usar el framework [NestJS](https://nestjs.com/). En la página de [First steps](https://docs.nestjs.com/first-steps) se explica cómo instalarlo.   
Nest resuelve en forma sencilla la integración, tanto con [Mongoose](https://docs.nestjs.com/techniques/mongodb) como con [TypeORM](https://docs.nestjs.com/techniques/database), un ORM que es (creo) más feliz que Sequelize, y que se lleva muy bien con TS.

Si quieren usar la combinación Mongo/JS ... hablemos sobre cómo hacer.

Se pueden proponer otras opciones ... pero se pierde el soporte docente.


### Atención - evolución de la BD
No olvidar el tema de las _migraciones_ de BD, para que no sea un garronazo el mantenimiento de la BD a medida que avanzan en el proyecto. Esto sobre todo para bases SQL.


## Organización del código
En repositorios GIT. Se recomienda tener dos repos, uno para el backend y otro para el frontend. Se puede usar [GitHub](https://github.com/) (les van a resultar más fáciles algunas tareas) o [GitLab](https://gitlab.com/) (repos privados infinitos gratis), también existe [BitBucket](https://bitbucket.org/product) pero no se recomienda.  
En cualquier caso, tienen que incluir a su docente asignado para que al menos pueda ver el repo y hacerle comentarios.

**No vale** trabajar en un único branch. Se recomienda manejarse con estos branches.
- uno `master` que sólo se actualiza cuando hay cosas nuevas que se pueden mostrar a un usuarie.
- uno `dev` que es la base del desarrollo.
- uno para cada tarea que se defina. Estos branches salen de `dev` y se mergean a `dev`.

Vale trabajar con [Pull Requests](https://yangsu.github.io/pull-request-tutorial/) para mergear a `dev`. 


## Actividades
Vamos a tener una sesión semanal, para la reunión de fin de sprint cuando corresponda, para revisar la marcha y resolver dudas las otras.  
Está la intención de ir mechando charlas sobre temas que les vienen bien para el proyecto, eso lo vamos a ir reflejando en [la página de actividades](./actividades).
