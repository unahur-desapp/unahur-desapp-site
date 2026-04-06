---
layout: default
---

# Trabajo Práctico: Gestión de laboratorios de docencia

El objetivo de la aplicación a construir es la gestión de los turnos y recursos de los laboratorios de biología y química de la Universidad que se utilizan para docencia. 
La Universidad tiene varios laboratorios, que están en distintos edificios.
Cada actividad que se realiza en un laboratorio puede conllevar 
- la necesidad de trabajar con determinados equipos (p.ej. centrífugas, incubadoras, espectofotómetros).
- el uso de ciertos materiales (p.ej puntas de pipetas, tubos de ensayo, placas de cultivo).
- la aplicación de ciertos reactivos (p.ej. ácido nítrico, sales, colorantes).

Los docentes solicitan el uso de un laboratorio para una clase, indicando las necesidades de equipos, materiales y reactivos, o bien las actividades que se van a realizar, a partir de las cuales la aplicación obtiene los requerimientos.
Para que el pedido pueda ser satisfecho, tiene que haber un laboratorio libre para el lapso de tiempo de la clase, donde entre la cantidad de alumnos del curso. Además, tiene que haber disponibilidad de los equipos, que son escasos y podrían estar asignados a otras tareas, fuera de funcionamiento o en mantenimiento. P.ej. si para una clase se necesitan dos centrífugas, la Universidad tiene tres, y al momento de la clase hay dos ya reservadas para otras actividades, el pedido no puede satisfacerse. A esto debe sumarse que hay algunos equipos que por sus características no pueden moverse de un edificio a otro.
Otra razón para no poder satisfacer un pedido es que el stock de alguno/s de los materiales que se requieren no alcance para lo que se necesita en la clase. P.ej. si para una clase hacen falta 30 tubos de ensayo de un determinado tamaño, y la Universidad al momento tiene sólo 20, entonces el pedido no puede ser satisfecho.

Todos los pedidos son evaluados por una persona del equipo de gestión de laboratorios. La aplicación debe indicar si hay requisitos que no pueden satisfacerse, y en tal caso cuáles son. Esto genera un diálogo entre el equipo y los docentes de la materia, durante el cual el pedido puede sufrir modificaciones por parte de cualquiera de estos actores. Debe llevarse registro de las modificaciones hechas sobre cada pedido.

Finalmente, un pedido se acepta o se rechaza. Si se acepta, además de quedar reservados los equipos para el horario de la clase más una hora antes y media después, se generan tareas de preparación de materiales y reactivos. Los materiales se acondicionan y se ponen en los carritos que van a ir al aula. Algunos reactivos requieren preparación a partir de sustancias más básicas, otros se compran directamente, en todo caso hay que ponerlos también en los carritos. A su vez, algunas actividades requieren otras tareas de acondicionamiento del aula. La aplicación debe generar y mantener los check-list de tareas de preparación. 
Luego de la clase, deben registrarse los eventuales desperfectos en equipos, y descarte de materiales.

Deben proporcionarse vistas que permitan al personal visualizar el uso de los diversos laboratorios en un día.

La aplicación debe llevar registro del stock de materiales, reactivos y sustancias básicas que se usan para generar reactivos.

Otro aspecto relevante son las estadísticas de uso de equipos (importantes para los mantenimientos periódicos), descarte de materiales (por rotura, fin de vida útil u otros motivos) y de consumo de reactivos y sustancias básicas.