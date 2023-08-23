---
layout: default
---


# Segundo cuatrimestre de 2023 - Desarrollo de Aplicaciones

## Características generales
Esta cursada va a incluir 4 grupos, con 5 personas en cada grupo.

De acuerdo a la experiencia del año pasado, en la que casi todos quienes cursaron Desarrollo de Aplicaciones siguieron con la PPS en el cuatrimestre siguiente, vamos a suponer que al menos dos de los cuatro grupos van a seguir con PPS.

Planteamos cuatro proyectos, dos están pensados para empezarlos con Desarrollo de Aplicaciones y seguirlos con PPS en el 1er cuatrimestre de 2024, los otros dos paraa cerrarlos en principio en este cuatrimestre, aunque también se pueden plantear continuaciones.


## Muy importante - avisamos de entrada
Los grupos que sigan PPS van a tener que retomar en marzo de 2024 lo que lleguen a hacer este año.  
Por eso es **súper** importante que dejen todo anotado: los resultados del relevamiento, el detalle de los siguientes pasos, el código claro y documentado, y por qué no con algún test.

## Cómo arrancar
Obviamente, lo primero es organizarse en grupos. Inmediatamente después, hay que definir de qué proyecto se encarga cada grupo; sobre esto vamos a hablar en la primer reunión.

Después, toca arrancar con el desarrollo. Para esto:
1. Antes que nada, hacer lo que se indica en la página de [tareas iniciales](../tareas-iniciales.md).
2. Después, seguir las instrucciones que corresponden al proyecto que hayan elegido.


## Proyectos
A continuación describimos cada uno de los cuatro trabajos propuestos, indicando para cada uno si está pensado para continuarlo en PPS o bien si es para cerrarlo en el cuatrimestre de Desarrollo de Aplicaciones.


### Pedidos para laboratorio - para continuar en PPS
Entre 2022 y 2023, un grupo de Desarrollo de Aplicaciones + PPS implementó una primera versión de una aplicación para automatizar la gestión de los pedidos que reciben quienes se encargan de cuidar los laboratorios de docencia, donde se indica qué elementos se necesitan para cada clase que se lleva a cabo en uno de estos laboratorios.  
Este desarrollo tiene de particular que los datos se guardan en una base de documentos [MongoDB](https://www.mongodb.com/).

Esta es [la carpeta](../adjuntos/pedidos-de-laboratorios-2023s1.pdf){:target="_blank"}.

Los repos de código de frontend y backend los encuentran en [https://github.com/orgs/Des-app-2022-C2/repositories](https://github.com/orgs/Des-app-2022-C2/repositories).

El objetivo es hacer todo lo necesario para que la aplicación quede operativa en el ámbito de la Universidad.

A grandes rasgos, las tareas necesarias son:
1. Entender el dominio y la aplicación, tener andando la aplicación en sus entornos locales.
1. Hablar con lxs encargadxs de laboratorios, que ya hablaron con el grupo que hizo la primera implementación, para entender qué más hace falta para tener un producto que se pueda usar. A este respecto, tenemos varias ideas de funcionalidades a agregar que detallamos aparte.
1. Implementar lo que se decida.
1. Subir la aplicación, front y back, de alguna forma que permita que lxs encargadxs de laboratorios, u otros actores de la Universidad, puedan usarla.
1. Escribir la documentación necesaria para que la gente de Sistemas de la Universidad pueda desplegar la aplicación en los equipos que maneja.

#### Instrucciones particulares para arrancar
Crear, dentro de la orga de Github que crearon, los repos de frontend y backend haciendo _forks_ de los repositorios que tienen el trabajo hecho hasta ahora. Para ver cómo hacer forks, mirar [la página del cuatrimestre pasado](../cuatrimestres/2023s1.md), sección "Cómo arrancar".

#### Posibles funcionalidades a agregar
- ABM de materiales / reactivos / equipos.
- Soporte para las actividades de preparación de lo que se necesita para una reserva. En particular, que la gente del labo pueda marcar cuando la preparación está terminada. También sería bueno que se pueda ir anotando qué es lo que no hay, y eventualmente con qué se reemplaza. También dejar la posibilidad de registrar otras notas. Y todo esto se tiene que poder ver asociado al pedido.
- Reporte de actividades planificadas para un laboratorio, o para el conjunto de los laboratorios.
- Agregar horario de la actividad asociada a cada pedido. Cuando esto esté, validar que no haya superposición horaria cuando se asigna laboratorio a un pedido.
- Reportes de utilización de materiales / reactivos / equipos, y de intensidad de uso de equipos / materiales (para ir previendo qué puede tener sentido comprar a futuro).
- Agregar PDF con la hoja de seguridad de cada reactivo.


### Entorno de programación de robots - para continuar en PPS
Se trata de dar los primeros pasos para armar un entorno gráfico para la programación de robots educativos. Los robots están siendo desarrollados por otro grupo dentro del ámbito de la Universidad, ahora para darle las instrucciones tienen una botonera, se apunta a poder programarlos desde una app Web.  
Para tener una idea de los robots, encontré [este video de Youtube](https://www.youtube.com/watch?v=6cs-LPd8j0s). La gente que lleva adelante el desarrollo del robot nos indicó [este video público para quien tiene el link](https://drive.google.com/file/d/1xKwIUHoya_uqAoti1-yHai5fBhHguw-i/view).

Para tener una idea de entorno de programación gráfica para educación, pueden chusmear [Pilas Bloques](https://pilasbloques.program.ar/), un producto muy lindo hecho en Argentina.  
----- **Atención** _sobre esto_ -----  
por las primeras conversaciones que tuvimos con la gente que lleva adelante el desarrollo del robot, lo que se pretende es distinto.

En este proyecto vamos a centrarnos, al menos en principio, en la interfaz gráfica; no vamos a apuntar a transmitir los programas definidos a los robots.

Este proyecto va a tener una primer fase de análisis para definir el alcance de una primer versión a implementar. Para eso se les va a dar el contacto de una persona que está trabajando con los robots dentro de la Universidad, para que les cuente las capacidades de estos robots y cómo se imaginan que sería su programación. Es muy importante que estudien el funcionamiento de Pilas Bloques y eventualmente de otras propuestas p.ej. [Alice](http://www.alice.org/) o [Scratch](https://scratch.mit.edu/), para poder proponer ideas y evaluar las que puedan tener las personas de la Universidad con quienes van a hablar.  
También les podemos conseguir el contacto de gente que participa en el desarrollo de Pilas Bloques, que les pueden tirar una onda importante.

Creemos que este proyecto es a la vez muy interesante y bastante desafiante.


#### Instrucciones particulares para arrancar
Siendo este un trabajo que arranca de cero, los repos a agregar dentro de la orga Github se generan a partir de los repos semilla linkeados en [la página de recursos](../recursos/recursos-index.md).  


### Programación de carteleras - cierra en el cuatrimestre de Desarrollo de Aplicaciones

La propuesta es implementar una aplicación que permita configurar qué se muestra en las pantallas que están en los pasillos de la Universidad, aburriéndose de no ser usadas. La idea es que estas pantallas sirvan como carteleras que muestren la asignación de aulas, eventos de interés para la comunidad académica, o mensajes en general que quiera difundir la Universidad.

A grandes rasgos, este proyecto involucra a grandes rasgos
- Especificar la ubicación de cada pantalla, para esto conviene agregar algunos conceptos que permitan "zonificar" el espacio de la Universidad (edificio / piso / sector / aulas / tal vez otros).
- Definir los contenidos a mostrar.
- Especificar en qué pantallas queremos que se muestren (esto relacionado con su ubicación, p.ej. "todas las pantallas del 1er piso del edificio Malvinas"), y cuándo. Para esto hay que modelar lo que haga falta para permitir flexibilidad en el "cuándo": rango de días, rango de horas, cuántos segundos/minutos se muestra.

El stakeholder para este proyecto es Cristian Schiffino.

#### Instrucciones particulares para arrancar
Siendo este un trabajo que arranca de cero, los repos a agregar dentro de la orga Github se generan a partir de los repos semilla linkeados en [la página de recursos](../recursos/recursos-index.md).  


### Cuaderno de laboratorio orientado a estudiantes - cierra en el cuatrimestre de Desarrollo de Aplicaciones

Un cuaderno de laboratorio es el soporte donde un investigador que hace experimentos (de física, química, etc.) anota en detalle toda la información relacionada con cada experimento: qué se busca, qué pasos se van a seguir, qué materiales y equipos se usan, las observaciones durante o después de cada paso al ejecutar el experimento, y las conclusiones.

Desde hace un tiempo (digamos un par de décadas) el uso de cuadernos de laboratorio electrónicos (o sea informatizados) es cada vez más común. Esto se puede hacer tanto con herramientas genéricas (planillas de cálculo, documentos de texto, repositorios de documentación, wikis, etc.) como con productos de software específicos.

Este proyecto apunta a dar algunos pasos en la dirección de desarrollar un cuaderno de laboratorio electrónico que apunte específicamente a las necesidades de los TPs que hacen alumnos universitarios (y eventualmente también de escuelas secundarias técnicas).

En un futuro feliz y promisorio, esto se va a enganchar con el software de gestión de pedidos a los laboratorios de docencia, y en uno aún más copado también con los datos que provee SIU-Guaraní; por eso, vamos a hacer un recorte de funcionalidades que no se pisen con lo que pueden proporcionar otros sistemas.  
Por el mismo motivo, el backend tiene que manejar los datos en una base de documentos MongoDB.  
Más abajo detallamos algunas funcionalidades para arrancar a pensar el desarrollo.  

El stakeholder para este proyecto es Carlos Lombardi.

#### Instrucciones particulares para arrancar
Siendo este un trabajo que arranca de cero, los repos a agregar dentro de la orga Github se generan a partir de los repos semilla linkeados en [la página de recursos](../recursos/recursos-index.md).  
Al repo de backend hay que modificarlo al principio, para conectar con MongoDB en lugar de una BD relacional. Para esto hable con su docente amigo.

#### Funcionalidades para arrancar
- Modelado en la BD de alumnos, materias y cursos (no incluir el ABM porque posiblemente esta información se pueda obtener desde el SIU-Guaraní).
- ABM de TPs para un curso. Cada TP puede ser individual o grupal, si es grupal el docente puede asignar mínimo y máximo de estudiantes por grupo. Cada TP puede tener varias secciones, cada una con un nombre.
- Asignación de grupos para cada TP, se puede copiar del TP anterior.
- El estudiante/grupo puede cargar notas y adjuntos para cada sección.
- El docente puede ver las notas y adjuntos que cargó cada estudiante/grupo.


## Grupos

### Grupo 1 - va a seguir con PPS
Magalí Acosta  
Rodrigo Nahuel Chiapparo  
Angel Cutri  
Brenda Micaela Denhoff  
Laura Pereyra  

**Trabajo asignado**: Entorno de programación de robots


### Grupo 2 - va a seguir con PPS
Gabriel de Rivas  
Leandro de Rivas  
Claudio Molina  
Cristian Damián Vitola  
Nicolás Ramírez  

**Trabajo asignado**: Pedidos de materiales para el laboratorio


### Grupo 3
Enzo Alarcón  
Valentino Chiappanni  
Lucián Coniglio  
Luciano Ezequiel Garegnani  
Tomás Benjamín Vásquez  

**Trabajo asignado**: Programación de carteleras


### Grupo 4
Facundo Ariel Cichero Ríos  
Agustín Fiordalisi  
Pablo Ezequiel Lopes Ferrao  
Ezequiel Pereira  
Gisela Daiana Tamburro  

**Trabajo asignado**: Cuaderno de laboratorio orientado a estudiantes


## Cronograma 

| Fecha | Es presencial | Actividad |
| --- | --- | --- |
| 10/08 | No | Presentación / objetivos / armado de equipos / selección de trabajos. |
| 17/08 | No | <b>1er Sprint - planning</b> <br/> |
| 24/08 | No | Metodología agile / Relevamiento / análisis inicial. |
| 31/08 | No | Figma <br/> Seguimiento |
| 07/09 | No | <b>1er Sprint - review<b><br/><b>2do Sprint - planning<b> |
| 14/09 | No | React - parte 1. |
| 21/09 | No | Seguimiento |
| 28/09 | No | <b>2do Sprint - review<b><br/><b>3er Sprint - planning<b> |
| 05/10 | No |  React - parte 2. <br/> Manejo de branches. |
| 12/10 | No | Seguimiento |
| 19/10 | No | <b>3er Sprint - review</b><br/><b>4to Sprint - planning</b> |
****| 26/10 | No | Seguimiento |
| 02/11 | No | Backend. |
| 09/11 | No | <b>4to Sprint - review<b><br/><b>5to Sprint - planning<b> |
| 16/11 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Práctica presentación presencial</span> | 
| 23/11 | No | Seguimiento |
| 30/11 | No | <b>5to Sprint - review<b> |
| 07/12 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Presentación presencial</span> |
