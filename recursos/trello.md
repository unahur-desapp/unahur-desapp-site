---
layout: default
---

# Cómo manejarse con Trello - detalles

## Tablero 
Como dijimos en [la página de recursos](./recursos-index), Les sugerimos que trabajen con un tablero.  
En este tablero van a tener varias listas correspondientes a las tareas del sprint actual, más para cada sprint terminado, una lista con las tareas terminadas en ese sprint para que quede registro.

[Este link](https://trello.com/b/PolRgqcs/desapp-2021-propuesta-de-tablero-trello-este-sprint) es un tablero donde les dejamos las listas que proponemos. Obviamente, la lista "Terminado en el sprint _n_" hay que replicarla para cada sprint que se va terminando.


## Listas que proponemos
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
1. **Terminado en el sprint _n_**.  
De estas vamos a tener una por sprint. A fin de cada sprint, creamos la lista correspondiente y movemos las tareas que estén en "Hecho en este sprint".

Si hay alguna tarea de este sprint que "explota" y se quiere ver aparte, vale crear una lista separada cargando sub-tareas. A veces es cómodo. Incluso, estas listas pueden "sobrevivir" durante varios sprints.



## Flujo de tareas y sprints

OK, todo muy lindo, pero ... ¿cómo lo usamos, podés bajar un poco a tierra?  
Acá va un intento ... que obviamente es aproximado, después cada equipo puede hacer las adaptaciones o cambios que crea conveniente.  
Lo dejamos para que no arranquen de cero.


### Al principio de cada sprint
Primero se trabaja con la lista de "Para después - a ordenar", más lo que haya quedado en "Lo que sigue" y "Planificado para este sprint", que son cosas que se pensaron para el sprint que acaba de terminar, pero no se hicieron.
Primero, revisar la prioridad de las tareas que estén cargadas, y cargando nuevas tareas e ideas.  

> **Atención**  
Una tarea puede ser _cualquier cosa_: pensar, definir, hablar de algo con usuaries, experimentar una tecnología, codear (claro), armar tests, hacer una demostración.  
No sean tímidos al definir tareas.

Durante este proceso se seleccionan las tareas que se van a encarar en el sprint actual. Moverlas a "Planificado para este sprint".  
Acá tenemos que dimensionar "cuánto entra" en un sprint. Para eso, es importante _considerar lo que fuimos aprendiendo en los sprints anteriores_, en cuánto/qué le pifiamos al planificar. 
También tenemos que tener en cuenta las tareas que no terminamos, o sea las que están en "Para revisar e integrar" y "Estamos haciendo ahora".

> **Recordar**  
_Junto con esto_ hay que completar [la ficha de principio de sprint](https://docs.google.com/document/d/19Ghm0d92Ur7GU5TC7PJJTEzz6suKjtMgPQkwh62Deg0).

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
> **Recordar**  
_antes_ de arrancar, llenar la [ficha de fin de sprint](https://docs.google.com/document/d/1NAKfgXVUJa0fN4u3FcdQ4xhzzqh4h4ySt8RWc1XBslg).  


Primero "limpiamos": lo que esté a revisar/integrar, lo revisamos, y pasa a "hecho" o vuelve para atrás, igual que durante el sprint.

Después hacemos la retrospectiva: de lo que habíamos planificado ¿hicimos todo, casi todo, más o menos, más bien casi nada? ¿Qué pasó, cómo hacemos para que la próxima nos salga mejor?   
Junto con esto, decidimos si de lo que nos quedó, estamos seguros que lo vamos a hacer en el siguiente sprint, o no.
Lo que estamos seguros que va en este, lo movemos a "Planificado para este sprint".

Lo que quedó pendiente de este sprint y no estamos seguros que va en el siguiente, lo movemos a "Para después - a ordenar".

Finalmente, crean la lista "Terminado en el sprint _número del sprint que terminó_", y le mueven lo que esté en "Hecho en este sprint"; esta última lista tiene que quedar limpia.

La lista de "en este momento" debería tener cosas solamente si el final de sprint nos agarró en el medio de algo. 



