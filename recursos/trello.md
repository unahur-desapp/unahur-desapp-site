---
layout: default
---

# Cómo manejarse con Trello - detalles

## Tableros 
Como dijimos en [la página de recursos](./recursos-index), Les sugerimos que trabajen con **tres tableros**.
- Uno para el sprint actual.
- Uno para que quede registro de lo que se fue cerrando en cada sprint anterior.
- Uno para las tareas a futuro.

Les dejamos tableros donde se muestran las listas que proponemos para cada uno. Van los links.

- [Sprint actual](https://trello.com/b/PolRgqcs/desapp-2021-propuesta-de-tablero-trello-este-sprint).
- [Futuro](https://trello.com/b/7eN8Djgf/desapp-2021-propuesta-de-tablero-trello-futuro).
- [Pasado](https://trello.com/b/WWCyjTZq/desapp-2021-propuesta-de-tablero-trello-pasado).


### Sprint actual
Se propone incluir, en principio, estas listas.

1. **Hecho en este sprint**.  
Acá van las tareas definidas para el sprint actual, y que están terminadas e integradas.
1. **Para revisar o integrar**.  
Acá van las tareas definidas para el sprint actual, que la/s persona/s asignadas terminaron, y que están pendientes de revisión, o de integrar al branch de Git de integración.
1. **Estamos haciendo ahora**.  
Acá van las tareas en las que al menos una persona está trabajando en este momento.
1. **Lo que sigue**.  
Acá van las tareas candidatas a ser las próximas que agarre/n algune/s integrantes/s cuando terminen lo que están haciendo.
1. **Planificado para este sprint**.  
Acá van las tareas que se decidió hacer en este sprint, y que no caen en ninguna de las categorías anteriores.
1. **Para después - a ordenar**.  
Acá van las tareas que vamos descubriendo que hay que hacer después de este sprint, y que todavía no organizamos.

Si hay alguna tarea de este sprint que "explota" y se quiere ver aparte, vale crear una lista separada cargando sub-tareas. A veces es cómodo. Incluso, estas listas pueden "sobrevivir" durante varios sprints.


### Pasado
Este tablero tiene una lista por sprint, donde se indica qué tareas se hicieron en cada sprint.


### Futuro
Se propone incluir, en principio, estas listas.

1. **De acá a no mucho**.  
Acá van tareas que en principio deberían incluirse en el siguiente sprint, y en todo caso no postergarse mucho más.
1. **En algún momento**.  
Tareas que hay que hacer seguro antes del fin del proyecto, pero no tienen urgencia.
1. **Sería lindo**.  
Funcionalidades o chiches que sería lindo meterle, pero no son necesaries.
1. **Ideas**.  
Una bolsa con ideas y notas que podrán, o no, convertirse en tareas a futuro. P.ej. una idea puede convertirse en una tarea de conversar cierto tema con les usuaries, o de definir cierta mejora o funcionalidad.


## Flujo de tareas y sprints

OK, todo muy lindo, pero ... ¿cómo lo usamos, podés bajar un poco a tierra?  
Acá va un intento ... que obviamente es aproximado, después cada equipo puede hacer las adaptaciones o cambios que crea conveniente.  
Lo dejamos para que no arranquen de cero.


### Al principio de cada sprint
Primero se trabaja con el tablero de futuro, revisando la prioridad de las que están cargadas, y cargando nuevas tareas e ideas.  
Si quedó una lista de "a ordenar" del final del sprint anterior, es el momento de organizarla. 
Si hay tareas que no se sabe dónde ponerlas, se puede armar una lista de "no sabemos".

> **Atención**  
Una tarea puede ser _cualquier cosa_: pensar, definir, hablar de algo con usuaries, experimentar una tecnología, codear (claro), armar tests, hacer una demostración.  
No sean tímidos al definir tareas.

En algún momento del proceso, empezar a seleccionar las tareas para el sprint actual. Crear una lista donde vayan esas tareas.
Acá tenemos que dimensionar "cuánto entra" en un sprint. Para eso, es importante _considerar lo que fuimos aprendiendo en los sprints anteriores_, en cuánto/qué le pifiamos al planificar.  
En este punto, mirar el tablero de sprint actual, y revisar las tareas que quedaron del anterior, para no zarparnos con lo que definimos para el sprint.  

Cuando estemos, la lista de "tareas para el sprint actual" se mueve al tablero de "este sprint", y pasamos a trabajar en este tablero ... que debería estar bastante limpio (porque lo limpiamos al final del sprint anterior).  
Estas tareas van a la lista de "planificado para este sprint".

Después toca elegir las primeras tareas que se van a encarar, y asignarlas. Cada persona debería tener entre una y dos (o _excepcionalmente_ tres) tareas asignadas en "Estamos haciendo ahora". También vale ir cargando "Lo que sigue". El resto queda en "planificado para este sprint".  
Vale priorizar las tareas que queden en "planificado para este sprint", poniendo arriba las que se estima que conviene encarar primero.

> **Consejo**  
> Al ir poniendo tareas de desarrollo en "estamos haciendo ahora", definir ya el nombre del branch de Git, y anotarlo en la tarjeta.


### Durante el sprint
Las tareas se mueven "hacia la izquierda" en el tablero de "este sprint".
- cuando termino algo, lo muevo de "estamos haciendo ahora" a "a revisar o integrar", y me paso una a "estamos haciendo ahora".
- cuando termino de integrar algo que estaba en "a revisar o integrar"
  - si está para integrar, lo hago , y la tarea pasa a "hecho en este sprint", _arriba de todo_.
  - si no, la tarea "va para atrás", a "ahora", "lo que sigue", o "planificado", depende la prioridad y la carga de trabajo de les integrantes.
- cuando estamos un toque perdidos, agarramos tareas de la bolsa de "planificado para este sprint", y las movemos a "estamos haciendo ahora" o "lo que sigue". 
- es muy común que a medida que se va avanzando, se descubren nuevas tareas. Para cada tarea que aparece, hay que decidir si va en este sprint o más adelante. Si va para este sprint, se agrega en "planificado para este sprint". Si no, se agrega en "Para después - a ordenar".


### Al final del sprint
Primero "limpiamos": lo que esté a revisar/integrar, lo revisamos, y pasa a "hecho" o vuelve para atrás, igual que durante el sprint.

Después hacemos la retrospectiva: de lo que habíamos planificado ¿hicimos todo, casi todo, más o menos, más bien casi nada? ¿Qué pasó, cómo hacemos para que la próxima nos salga mejor?   
Junto con esto, decidimos si de lo que nos quedó, estamos seguros que lo vamos a hacer en el siguiente sprint, o no.
Lo que estamos seguros que va en este, lo movemos a "Planificado para este sprint".

Lo que quedó pendiente de este sprint y no estamos seguros que va en el siguiente, más lo que está en "Para después - a ordenar", hay que volcarlo al tablero de "futuro". Se puede poner en una lista provisoria de "a ordenar", que la vamos a limpiar al abrir el siguiente sprint.

Finalmente, lo que quedó en "hecho en este sprint", se mueve al tablero de "pasado".

La lista de "en este momento" debería tener cosas solamente si el final de sprint nos agarró en el medio de algo. La de "lo que sigue" yo la vaciaría, después se vuelve a armar al comienzo del siguiente sprint.



