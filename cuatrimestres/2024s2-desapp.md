---
layout: default
---


# Segundo cuatrimestre 2024 - Desarrollo de Aplicaciones

## Características generales
Esta cursada va a incluir 6 grupos, 3 grupos de 4 integrantes y 3 grupos de 5 integrantes, para cubrir las 27 personas inscriptas.

Es **muy** importante que cada grupo decida _en conjunto_ si va a seguir con PPS en el 1er cuatrimestre de 2025, o no. De esto depende cómo se encara cada proyecto, e incluso evaluaremos en algún caso si conviene que un proyecto lo lleva adelante un grupo que va a seguir con PPS o uno que no lo va a hacer.  
Si un grupo tiene la intención de seguir con el proyecto en 2025, pero alguno/s de sus integrantes no pueden inscribirse en PPS por correlativas, por favor háblenlo con los docentes.

Planteamos seis proyectos, todos relacionados con propuestas surgidas desde la Universidad, que están en distinto grado de avance:
- tres están muy avanzados, el objetivo en estos tres proyectos es dejar productos listos para ponerlos operativos, desplegarlos en algún recurso gratuito, y organizar pruebas experimentales.
- uno tiene un grado de desarrollo más humilde, el objetivo acá es agregar funcionalidades. Como es un proyecto de migración de una aplicación existente, en este caso las funcionalidades están claras.
- dos son para arrancarlos en este cuatrimestre.

> <hr/> 
> 
> ### ¿Proyecto empezado? ¡Es la vida misma!
> 
> En cuatro de los seis proyectos, el grupo va a estar agregando, y también modificando/corrigiendo, código que hicieron otros grupos en el pasado.
>
> Esto es _muy_ distinto a lo que vienen haciendo en los trabajos para las distintas materias, en las que siempre cada trabajo empieza de cero.
>
> Por otro lado, es _el escenario habitual_ en contextos laborales, sobre todo para quienes se insertan en la industria en posiciones de trainee o junior. Es muy improbable que te toque empezar un proyecto de cero, casi siempre hay que agarrar un proyecto hecho por otros, entender tanto el dominio como el código (y la infraestructura), y agregar/modificar/corregir.
>
> Quienes elijan estos proyectos, van a estar ejercitándose en contextos que seguramente se van a repetir en su trayectoria profesional.
> 
> <hr/>

## Cómo arrancar
Obviamente, lo primero es organizarse en grupos. Inmediatamente después, hay que definir de qué proyecto se encarga cada grupo.
Para esto le vamos a pedir a cada grupo que entregue un ranking de los seis proyectos, de mayor a menor de acuerdo al interés que tengan en hacer cada uno (primero el que más les interesa, último el que menos les gustaría). Eso nos lo mandan a los docentes, que nos fijamos la forma de hacerlos lo más felices (o menos infelices) posible a todos, y se comunican lo antes posible para que puedan arrancar.


Después, toca arrancar con el desarrollo. Para esto:
1. Antes que nada, hacer lo que se indica en la página de [tareas iniciales](../tareas-iniciales.md). <br/> **Atención** acá: la organización GitHub la tienen que crear _solamente_ los grupos que tomen proyectos que arrancan en esta cursada, o sea planillas de evaluación para enfermería y gestión de convocatorias de investigación. Para los otros proyectos (o sea sistema de sugerencias, pedidos de materiales,  gestión de equivalencias y control de gastos de subsidios), el grupo docente les va a dar acceso a los repositorios donde está el código sobre el que van a tener que aplicar los agregados y mejoras.
2. Después, seguir las instrucciones que corresponden al proyecto que hayan elegido.


## Proyectos
En resumen, tenemos estos proyectos.

| Nombre | Grado de avance |
| --- | --- | 
| Control de gastos de subsidios | Muy avanzado |
| Solicitudes de equivalencia | Muy avanzado |
| Pedidos de materiales al laboratorio | Muy avanzado |
| Sistema de sugerencias de cursada y acompañamiento académico | Poco avanzado |
| Registro de evaluaciones de enfermería | Para arrancar |
| Gestión de convocatorias de investigación | Para arrancar |

A continuación, damos una descripción de cada uno, contando de qué se trata, y los pasos iniciales que proponemos (después de los de arriba, claro).


### 1. Control de gastos de subsidios

La UNAHUR (como es común en las universidades públicas argentinas) destina una parte (pequeñita) de su presupuesto para actividades de investigación.  
Para asignar estos fondos, se organizan convocatorias en las cuales grupos de docentes hacen propuestas de trabajos a realizar. Se forma un jurado que elige cuáles de los proyectos propuestos son elegidos para que la Universidad los financie, y qué monto se destina a cada proyecto. Esto se conoce como subsidio a un grupo de docentes/investigadores.

Con los fondos que se le asignan mediante un subsidio, cada grupo de docentes/investigadores compra bienes, contrata servicios, financia viajes de intercambio o presentación de resultados, y paga los gastos de inscripción a congresos y publicación de artículos.
La Universidad debe aprobar cada gastos, y después tiene que llevar un control, recibiendo copia de la factura correspondiente.

La Secretaría de Investigación propuso implementar una aplicación que informatice la gestión de los gastos de subsidios. En el marco de cursadas anteriores, se llegó a implementar las funcionalidades principales pedidas por la Secretaría, con un buen grado de avance.  
Esta es la [carpeta](../adjuntos/gastos-de-subsidios-2023s2.pdf){:target="_blank"} presentada por el grupo que trabajó sobre este proyecto en 2023.

Los objetivos del grupo que tome este proyecto van a ser:
- Agregar algunas funcionalidades faltantes, alguna es sencilla, otras tienen lo suyo.
- Agregar algunos detalles a las funcionalidades existentes.
- Actualizar el stack tecnológico del frontend, tomando como base el template que se encuentra en este sitio.
- Configurar un storage en cloud para los archivos adjuntos que tiene que manejar la aplicación.
- Desplegar el producto en algún servicio público, y acompañar a la Secretaría en la realización de pruebas preliminares de uso. Registrar las modificaciones y agregados que se detecten como necesarios para dejar operativo el producto. En la medida de lo posible, implementar estas modificaciones y agregados, y generar versiones sucesivas del producto.
- Montar la estructura para implementar tests unitarios, e implementar algunos. Idealmente tanto BE como FE.

En principio, el stakeholder para este proyecto es Juan Pedrosa, el secretario de Investigación. Probablemente él delegará el seguimiento a alguna persona del plantel de la Secretaría.


#### Instrucciones particulares para arrancar

Leer la carpeta del equipo que trabajó en este proyecto en 2023 (que próximamente va a estar disponible en este sitio). Entender el dominio y las funcionalidades implementadas.

Clonarse los repos con el código existente, darles `npm install`.

Instalarse PostgreSQL. Crear una BD para el proyecto y configurarla desde el archivo `.env.development` del BE. Ejecutar las tareas `npm run db:init` y `npm run db:seed` en el proyecto de BE, para definir la base y cargar algunos datos iniciales.

Levantar BE y FE (`npm start` en ambos casos), navegar para entender un poco de qué se trata, relacionar con lo que se leyó en la carpeta.

Conversar con los docentes sobre una primera lista de funcionalidades a agregar o modificar.


#### Un poco más adelante
Cuando se sientan seguros con la aplicación y el dominio, solicitar una reunión con el stakeholder, mostrarle lo que está hecho, plantearle las funcionalidades planteadas por los docentes de Desarrollo de Aplicaciones, y refinar los pasos a seguir.


### 2. Solicitudes de equivalencia
Como sabemos bien, las carreras de Informática tienen una enorme popularidad. Además de una gran alegría, esto trae el desafío de gestionar la gran masa de estudiantes.  

Un aspecto que le genera mucho trabajo administrativo a la Universidad es la gestión de las solicitudes de equivalencia.  
¿Qué es una solicitud de equivalencia? Un pedido que puede hacer unx estudiante que aprobó materias en otra Universidad, de que se las reconozcan como equivalentes en contenidos con materias del plan de estudios de la carrera que está haciendo en la UNAHUR. Si el pedido es aceptado, entonces al/a la estudiante se le dan por aprobadas las materias UNAHUR que se aceptan como "equivalentes" a las que el/la solicitante aprobó en otro lado.

Fernando Puricelli solicitó hace un tiempo, el desarrollo de una aplicación que permita organizar la información de los trámites de equivalencia. 
En el marco de cursadas anteriores, se llegó a implementar las funcionalidades principales pedidas por Fernando.  
Esta es la [carpeta](../adjuntos/equivalencias-2023s2.pdf){:target="_blank"} presentada por el grupo que trabajó sobre este proyecto en 2023.

Los objetivos del grupo que tome este proyecto van a ser:
- Agregar una funcionalidad faltante, que describimos abajo.
- Encriptar las claves, que hoy están planas en la BD.
- Actualizar el stack tecnológico del frontend, tomando como base el template que se encuentra en este sitio.
- Configurar un storage en cloud para los archivos adjuntos que tiene que manejar la aplicación (ver si esto ya está previsto en el proyecto que van a recibir).
- Desplegar el producto en algún servicio público, y acompañar a Fernando en la realización de pruebas preliminares de uso. Registrar las modificaciones y agregados que se detecten como necesarios para dejar operativo el producto. En la medida de lo posible, implementar estas modificaciones y agregados, y generar versiones sucesivas del producto.
- Montar la estructura para implementar tests unitarios, e implementar algunos. Idealmente tanto BE como FE.

La principal funcionalidad nueva es que se pueda mantener un status de materias con equivalencias que, al menos en principio, la UNAHUR va a aceptar. Esto surge de los trámites ya estudiados y definidos.  
Pongamos un ejemplo inventado. Supongamos que una estudiante pide que se le reconozcan Organización de Computadoras y Redes de Computadoras, porque aprobó Arquitectura de Computadoras 1, 2 y 3 en la Universidad de la Gran Montaña, y la UNAHUR, después de analizar el pedido, decide aceptarlo.
Unos meses después viene otro estudiante, que aprobó las mismas materias en la Universidad de la Gran Montaña, y también solicita que le reconozcan Organización de Computadoras y Redes de Computadoras. La UNAHUR no va a volver a hacer la evaluación que ya hizo, en principio se puede suponer que la solicitud se va a aceptar.  

Lo que se busca con esta funcionalidad es llevar el registro de qué "esquemas de pedidos de equivalencia" ya fueron aceptados.  
Esta información tiene que estar disponible para el directivo que esté evaluando la solicitud.  
También se desea que elx estudiante que está cargando una solicitud, pueda consultar a partir de las materias que trae aprobadas de otras Universidades, cuáles materias podría pedir y que (en principio) le van a ser reconocidas.

En principio, el stakeholder para este proyecto es Fernando Puricelli. Probablemente él delegará el seguimiento a alguna persona del plantel del Instituto de Ingeniería o del área de Informática.


#### Instrucciones particulares para arrancar

Leer la carpeta del equipo que trabajó en este proyecto en 2023 (que próximamente va a estar disponible en este sitio). Entender el dominio y las funcionalidades implementadas.

... más información en breve ...


### 3. Pedidos de materiales al laboratorio
En varias materias de las carreras del instituto de Biotecnología (y tal vez también Salud) se hacen clases prácticas en laboratorios, en las cuales lxs estudiantes tienen hacer experimentos. 
Para estos experimentos, la Universidad provee: 
- _equipos_, p.ej. un aparato que rota tubos de ensayo a gran velocidad para producir cierto efecto en la muestra que se les pone.
- _materiales_, p.ej. los tubos de vidrio.
- _reactivos_, que son sustancias que se usan para producir los efectos que se miden en el experimento.

Los docentes realizan pedidos de reserva de laboratorio, en los que indican qué equipos, materiales y reactivos se necesitan, y en qué cantidades. Con esta información, el personal de laboratorio designa en cuál de los laboratorios de docencia de la UNAHUR se desarrolla la clase, y organiza la provisión de los elementos necesarios.

El equpo que gestiona los laboratorios solicitó hace ya un tiempo, una aplicación que permita gestionar estos pedidos de materiales, en lugar de las idas y vueltas de mails con los docentes más anotaciones en algún Excel u hoja para registrar las reservas.

En cursadas anteriores se avanzó mucho con este proyecto, interactuando activamente con personal de laboratorio, y llegando a una versión que tal vez esté bastante cerca de quedar operativa.  
Esta es la [carpeta](../adjuntos/pedidos-de-materiales-2024s1.pdf){:target="_blank"} presentada por el grupo que trabajó sobre este proyecto en el segundo cuatrimestre de 2023 y primero de 2024.

Los objetivos para el grupo que siga con este trabajo son:
- Documentar y mejorar la implementación de algunos aspectos en los que la implementación es bastante difícil de seguir.
- Migrar el frontend de react-scripts a vite, tomando como base el template que se encuentra en este sitio.
- Hacer algunos refactors que mejoren la legibilidad del código.
- Agregar opciones de configuración.
- Arreglar algunos bugs.
- Revisar el circuito de un pedido, y agregar lo que haga falta para que sea realmente usable.
- Agregar reportes y filtros de la info que maneja la aplicación.
- Desplegar el producto en algún servicio público, y acompañar al personal de laboratorio en la realización de pruebas preliminares de uso. Registrar las modificaciones y agregados que se detecten como necesarios para dejar operativo el producto. En la medida de lo posible, implementar estas modificaciones y agregados, y generar versiones sucesivas del producto.

Los stakeholders para este proyecto son Paloma Martínez Ponce y Marco Ruiz.

#### Instrucciones particulares para arrancar

Leer la carpeta del equipo que trabajó en este proyecto en 2023 (que próximamente va a estar disponible en este sitio). Entender el dominio y las funcionalidades implementadas.

Clonarse los repos con el código existente, darles `npm install`.

Instalarse MongoDB, o usar Atlas (el servicio cloud gratuito de Mongo). Configurar el acceso a la BD desde el proyecto de backend, seteando la variable de ambiente `URI_MONGO` en el archivo `.env` en el proyecto de backend.

Agregar un documento en la colección de usuarios, con estas características (salvo `contrasenia`, `admin`, `editor`, `rol` y `__v`, en los otros atributos pueden poner el valor que quieran. Incluso no es necesario que el id de usuario sea `admin`, aunque esto se recomienda).  
**¡¡Atención!!** - fíjense que dni y matricula son _números_, eso tiene que ser así.
```
{
    _id: ObjectId("66b4fd973c67f8681c1b01fe"),
    usuario: 'admin',
    contrasenia: '$2b$10$TrsBSx5JPJx8U9gQazlrF.4JMKEQ6dglANaWIUU3U8Wq2mkP6xdG6',
    nombre: 'Aymará',
    apellido: 'Rocamora',
    dni: 88778877,
    matricula: 333444,
    admin: true,
    email: 'aymara.rocamora@notamail.com',
    editor: false,
    __v: 0,
    rol: 'lab'
}
```
La clave de este usuario es 123123. Esto está contado en la carpeta del equipo que trabajó en este proyecto en 2023.

Levantar BE y FE. Para el BE, simplemente `npm start`.
Para el FE, setear las variables de instancia `REACT_APP_API_URL` con la URL donde levantó el BE (que por defecto es `http://localhost:3001`) y `REACT_APP_USER` con un nombre cualquiera, pero tiene que estar. Después, `npm start`.

Una vez BE y FE levantados, navegar el FE para entender un poco de qué se trata, relacionar con lo que se leyó en la carpeta. 
Se recomienda hacer lo siguiente:
- Entrando como el admin que crearon, cargar al menos: una usuario de perfil laboratorio, un usuario de perfil docente, un equipo, un material y un reactivo.
- Entrar con el usuario de perfil docente, cargar un pedido.
- Entrar con el usuario de perfil laboratorio, ver el pedido.

Conversar con los docentes de Desarrollo de Aplicaciones sobre una primera lista de funcionalidades a agregar o modificar.


#### Un poco más adelante
Cuando se sientan seguros con la aplicación y el dominio, solicitar una reunión con la stakeholder (o quien ella designe), mostrarle lo que está hecho, plantearle las funcionalidades planteadas por los docentes, y refinar los pasos a seguir.


### 4. Sistema de sugerencias de cursada y acompañamiento académico
Desde la comunidad de Informática se desarrolló una aplicación que genera y envía en forma masiva mails con sugerencias de cursada y otras acciones, donde el contenido está personalizado para cada estudiante a partir de los datos de su trayectoria académica.

El objetivo en el cual se inscribe este proyecto es realizar una nueva implementación de esta aplicación, tomando como base este stack tecnológico:
- Para el FE: React 18, Material UI 5, React Router 6, y Vite (en lugar de Create React App). Estas son las herramientas de base del nuevo template de FE.
- Para el BE: Express o Nest.js, y Mongoose. 
- BD: Mongo.

En el primer cuatrimestre de 2024, un grupo de Desarrollo de Aplicaciones comenzó con el desarrollo, implementando exitosamente la edición de varios elementos de configuración. Para el BE, este grupo eligió Express y JavaScript como lenguaje de programación.

La propuesta para el grupo que tome este proyecto es 
- Completar la edición de la configuración, lo que implica: 
  - agregar una pantalla, 
  - completar otra que tiene una implementación parcial faltando una parte bastante compleja, 
  - agregar características que falta integrar en algunas pantallas ya implementadas.
- Desplegar el producto en algún servicio público para que el stakeholder lo pueda usar sin levantarlo desde su compu, y mostrárselo a otros actores de la Universidad.
- Montar la estructura para implementar tests unitarios del backend, e implementar algunos.

El grupo puede, si así lo elige, migrar el BE a Nest.js sobre TypeScript; sería una buena oportunidad para aprender un lenguaje nuevo.

El stakeholder para este proyecto es Carlos Lombardi.

**Importante**  
Como este proyecto consiste en la migración de una aplicación que está funcionando, debemos respetar la estructura de la BD, que está en Mongo. 


#### Instrucciones particulares para arrancar

Clonarse los repos con el código existente, darles `npm install`.

Instalarse MongoDB, o usar Atlas (el servicio cloud gratuito de Mongo). Configurar el acceso a la BD desde el proyecto de backend, y cargar los datos iniciales (los detalles se los va a dar el stakeholder).

Levantar BE (`npm start`) y FE (`npm run dev`), navegar para entender un poco de qué se trata.

Estudiar las funcionalidades de configuración, que van a ser las primeras en migrarse. Para esto el stakeholder les puede hacer una demostración y después enviarles screenshots.

Conversar con el stakeholder sobre las funcionalidades y características a agregar.


### 5. Registro de evaluaciones de enfermería
En varias materias de la carrera de Enfermería, los alumnos tienen que simular acciones que realizan sobre personas (p.ej. control de signos vitales), para lo que se utilizan biosimuladores, que son dispositivos de uso específicamente educativo. También se evalúan otras acciones de preparación (p.ej. lavado de manos). Los docentes observan el desempeño de cada estudiante, y a partir de esto llenan planillas en las que se evalúan distintos aspectos. 

Recientemente se acercaron docentes de la carrera de Enfermería, a sugerir el desarrollo de una aplicación que simplifique el manejo de estas planillas.  
Lo que se está buscando es una aplicación en la que lxs docentes puedan cargar las evaluaciones, y después se genere algún tipo de reporte a partir de los resultados, como el estado de aprobación de cada estudiante, o la necesidad de repetir alguna de las acciones evaluadas.

En una primera aproximación, las funcionalidades iniciales del proyecto son:
- Generar los modelos de evaluación, cada modelo tiene un título, una cantidad de preguntas (cada pregunta puede valer uno o más puntos), y un porcentaje mínimo de aprobación (llamado "exigencia"). Las preguntas pueden venir separadas en grupos, donde cada grupo tiene un subtítulo. Los docentes podemos suministrar algunos ejemplos, y seguramente lxs stakeholders otros.
- Registrar cursos, cada curso con una lista de estudiantes y otra de docentes. Indicar cuáles de los modelos de evaluación se van a usar en cada curso.
- Registrar la evaluación de unx estudiante para uno de los modelos incluidos en el curso. Indicar quién es el docente que evalúa.
- Ver las evaluaciones registradas en formatos que serán a conversar con lxs stakeholders.

Lxs usuarixs de esta aplicación son lxs docentes, más algún usuario administrador que cargue los modelos y los cursos; al menos en principio, lxs estudiantes no acceden.

Los stakeholders de este proyecto son Daniela Saldivia y Hugo Bonda Pacheco, docentes de la carrera de Enfermería.


**Aclaración importante**  
El software que vamos a comenzar a implementar en esta cursada es parte de un proyecto más grande, que incluye el diseño y fabricación de biosimuladores, y otros elementos. Para organizar este proyecto se está generando una empresa desde la Universidad, y se está diseñando cuidadosamente el producto que se va a vender, estudiando sus diferenciales positivos respecto de alternativas existentes.  
Si este proyecto es exitoso, vamos a estar contribuyendo a una iniciativa que puede ser muy reconocido en la Universidad.


#### Instrucciones particulares para arrancar.
Este es un proyecto que arranca de cero. Por lo tanto, se empieza por ... entender el dominio, armar una primer serie de prototipos gráficos en Figma, pingponearla primero con los docentes y después con lxs stakeholders. Si quieren, en paralelo se pueden ir armando los repos de FE y BE, el de FE a partir del template que está en este sitio (a menos que elijan ir por un camino distinto del que le proponemos), el de BE dependiendo de la opción que definan.  
Vale absolutamente arrancar con el FE para ir dándole forma a la interacción con lxs usuarixs, definiendo datos mock; y empezar con el BE cuando tengan una idea un poco más estable.


### 6. Gestión de convocatorias de investigación
Este proyecto complementa de algún modo, el que describimos arriba sobre gestión de gastos de subsidios. Como contamos ahí, la Universidad genera convocatorias a las cuales se presentan los grupos de docentes que requieren financiamiento.   
Además del manejo de gastos, cada proyecto elegido en una convocatoria debe presentar informes, seguro uno al final, posiblemente uno o más intermedios, que son llamados "informes de avance". Todos estos informes son evaluados por jurados designados por la Universidad.

La Secretaría de Investigación propone este proyecto, cuyo objetivo es gestionar las convocatorias, desde que la Universidad las abre, hasta que se cierran con la evaluación del informe final.

En una primera aproximación, podemos pensar en el siguiente flujo de eventos que la aplicación tiene que manejar
1. La Secretaría crea convocatorias, define un período de inscripción (p.ej. del 10 de noviembre al 9 de diciembre de 2025). Cada convocatoria tiene un texto que define la Secretaría, este texto puede tener títulos y un poco de formato.
2. Durante el período en que la convocatoria está abierta, los grupos de docentes se inscriben, para esto tienen que cargar una serie de datos (que puede ser bastante extensa) y documentos adjuntos (plan de trabajo, y CV de los docentes).
3. Eventualmente, la Secretaría puede extender el plazo de presentación de una convocatoria (continuando con el ejemplo anterior, extender la fecha límite de presentación hasta el 18 de diciembre).
4. Cuando se cierra el período de inscripción, hay que acercar las propuestas al jurado. 
5. El jurado hace una evaluación (hay que ver si es general o una por propuesta).
6. A partir de la evaluación del jurado, la Secretaría define cuáles de los proyectos salieron elegidos y qué monto se le otorga a cada uno.
7. Los grupos con proyectos adjudicados producen los informes de avance y finales, que también tienen plazos de entrega, que también se pueden prorrogar.
8. La Secretaría gira los informes a los jurados, que emiten un dictamen, acá seguro uno por cada proyecto.

Sobre esto la Secretaría, seguro, va a querer poder ver para una convocatoria: las propuestas presentadas, los dictámenes de los jurados, cuáles de las propuestas fueron elegidas. Después respecto de la entrega de informes, para cada instancia (informe de avance o final) cuáles de los grupos lo entregaron y a cuáles les falta entregar.

Esto se complementa con consultas: de convocatorias futuras / abiertas / en evaluación / en curso (o sea que empezó el período en el que los grupos tienen que hacer lo que dijeron y pueden usar los fondos disponibles) / finalizadas. También presentaciones filtradas por docente, por departamento, y posibles etc..

Igual que para el proyecto de gestión de gastos de subsidios, el stakeholder inicial para este proyecto es Juan Pedrosa, el secretario de Investigación. Probablemente él delegará el seguimiento a alguna persona del plantel de la Secretaría.


#### Instrucciones particulares para arrancar.
Al ser este un proyecto que arranca de cero, vale lo mismo que indicamos para el de evaluaciones de enfermería, que repetimos por las dudas.  
Se empieza por ... entender el dominio, armar una primer serie de prototipos gráficos en Figma, pingponearla primero con los docentes y después con lxs stakeholders. Si quieren, en paralelo se pueden ir armando los repos de FE y BE, el de FE a partir del template que está en este sitio (a menos que elijan ir por un camino distinto del que le proponemos), el de BE dependiendo de la opción que definan.  
En este caso también, vale absolutamente arrancar con el FE para ir dándole forma a la interacción con lxs usuarixs, definiendo datos mock; y empezar con el BE cuando tengan una idea un poco más estable.




## Grupos

... a designar ...



## Cronograma 

| Fecha | Es presencial | Actividad |
| --- | --- | --- |
| 15/08 | No | Presentación / objetivos / armado de equipos / selección de trabajos / Figma. |
| 22/08 | No | <b>1er Sprint - planning</b> <br/> |
| 29/08 | No | React - parte 1. |
| 05/09 | No | Seguimiento. |
| 12/09 | No | <b>1er Sprint - review<b><br/><b>2do Sprint - planning<b> |
| 19/09 | No | Metodología agile / Relevamiento / análisis inicial. |
| 26/09 | No | Seguimiento. |
| 03/10 | No | <b>2do Sprint - review<b><br/><b>3er Sprint - planning<b> |
| 10/10 | No |  Backend. |
| 17/10 | No | Seguimiento. |
| 24/10 | No | <b>3er Sprint - review</b><br/><b>4to Sprint - planning</b> |
| 31/10 | No | React parte 2. |
| 07/11 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Presentación presencial medio término</span> | 
| 14/11 | No | <b>4to Sprint - review<b><br/><b>5to Sprint - planning<b> |
| 21/11 | No | Manejo de branches. <br/> |
| 28/11 | No | <b>5to Sprint - review<b> |
| 05/12 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Presentación final presencial</span> |

