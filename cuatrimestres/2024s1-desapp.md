---
layout: default
---


# Primer cuatrimestre 2024 - Desarrollo de Aplicaciones

## Características generales
Esta cursada va a incluir 5 grupos, 3 grupos de 4 integrantes y 2 grupos de 5 integrantes, para cubrir las 22 personas inscriptas.

Es **muy** importante que cada grupo decida en conjunto si va a seguir con PPS en el 2do cuatrimestre o no. De esto depende cómo se encara cada proyecto, e incluso evaluaremos en algún caso si conviene que un proyecto lo lleva adelante un grupo que va a seguir con PPS o uno que no lo va a hacer.

Planteamos cinco proyectos, de los cuales dos están relacionados con propuestas surgidas desde la Universidad, una es una propuesta nueva que podría ser de interés siempre dentro del ámbito de la Universidad, y las otras dos son ajenas al ámbito universitario, fueron pensadas por nosotros docentes porque nos parecen dominios interesantes.  
Estamos abiertos a escuchar propuestas adicionales que surjan desde los grupos.  




## Cómo arrancar
Obviamente, lo primero es organizarse en grupos. Inmediatamente después, hay que definir de qué proyecto se encarga cada grupo; sobre esto vamos a hablar en la primer reunión.

Después, toca arrancar con el desarrollo. Para esto:
1. Antes que nada, hacer lo que se indica en la página de [tareas iniciales](../tareas-iniciales.md).
2. Después, seguir las instrucciones que corresponden al proyecto que hayan elegido.


## Proyectos
A continuación describimos cada uno de los cinco trabajos propuestos.


### Cuaderno de laboratorio orientado a estudiantes
Un cuaderno de laboratorio es el soporte donde un investigador que hace experimentos (de física, química, etc.) anota en detalle toda la información relacionada con cada experimento: qué se busca, qué pasos se van a seguir, qué materiales y equipos se usan, las observaciones durante o después de cada paso al ejecutar el experimento, y las conclusiones.

Desde hace un tiempo (digamos un par de décadas) el uso de cuadernos de laboratorio electrónicos (o sea informatizados) es cada vez más común. Esto se puede hacer tanto con herramientas genéricas (planillas de cálculo, documentos de texto, repositorios de documentación, wikis, etc.) como con productos de software específicos.

El objetivo es ir evolucionando hacia un producto orientado específicamente a las necesidades de actividades de laboratorio realizadas en un contexto educativo, en concreto como TPs que hacen alumnos universitarios (y eventualmente también de escuelas secundarias técnicas).  
En un futuro feliz y promisorio, esto se va a enganchar con otro proyecto sobre el que se está avanzando (en este cuatrimestre lo va a continuar un grupo de PPS) que es el software de gestión de pedidos a los laboratorios de docencia, y en uno aún más copado también con los datos que provee SIU-Guaraní; por eso, vamos a hacer un recorte de funcionalidades que no se pisen con lo que pueden proporcionar otros sistemas.  

Se propone continuar con un proyecto comenzado durante el 2do cuatrimestre de 2023 por un grupo que cursó Desarrollo de Aplicaciones. 
Más abajo detallamos algunas funcionalidades para arrancar a pensar el desarrollo.  

El stakeholder para este proyecto es Carlos Lombardi.

#### Instrucciones particulares para arrancar
Crear, dentro de la orga de Github que armaron para la cursada, los repos de frontend y backend haciendo _forks_ de los repositorios que tienen el trabajo hecho hasta ahora. Para ver cómo hacer forks, mirar [la página del primer cuatrimestre de 2023](../cuatrimestres/2023s1.md), sección "Cómo arrancar".

Estas son las URL de los repositorios que hay que forkear.
- Back: https://github.com/DesApp-2023c2-Grupo4/cuaderno-de-laboratorio-back .
- Front: https://github.com/DesApp-2023c2-Grupo4/cuaderno-de-laboratorio-front .

Instalarse Mongo, que es la BD que usa el BE para persistir la información.

Después de clonar y hacer `npm install` al back, se puede ejecutar  
`node ./config/insertardatosmock.js`  
para tener algunos datos iniciales en la BD Mongo.


#### Warnings

Usar Node seguro < 20 (en 20 no anda), tal vez < 18. Yo (Carlos) lo hice andar con Node 14.

En `src/components/Comision.jsx` en el front, hay que cambiar el valor de la const `profesorId` por un id de profe válido en la BD.


#### Primeras tareas
Lograr que ande lo que está implementado, y tal vez limpiar un poquito el código.
Primeros focos respecto de esto
- Edición básica de un TP: que se vean  la consigna y los grupos, poder editar (sin grupos) y eliminar.
- Hacer andar la edición de grupos de un TP.
- Poder acceder a la edición de grupos desde la edición de un TP.
- Separar los cursos en anteriores (los que fecha fin < hoy), y actuales (fecha fin >= hoy).

En el FE, unificar Material UI en la versión 5, mover todos los usos de componentes de la versión 4 a la 5.


#### Primeras funcionalidades a agregar
- Entrar como alumno, ver los cursos en los que estoy anotado. Entrar en un curso, ver los TPs, para cada TP grupal con quiénes estoy. <br/> Si se quiere arrancar con esto antes del login, se puede armar una ruta `/alumno` con un id de alumno fijo.
- Como profe, cargar un informe para cada alumno o grupo (depende si el TP es individual o grupal).
- Vista para el profe, para cada TP quién cargó y quién no, acceder a los informes.
- Agregar imágenes a los informes.
- Que el profe pueda indicar una devolución y una nota para cada entrega.
- En paralelo a todo esto, login. Arranquemos con uno fácil, sin pwd ni validación ni nada, sólo para poder saber quién está accediendo.


#### Posible tarea técnica
Migrar el FE a Vite en lugar de Create React App. Para esto se puede volcar la funcionalidad implementada sobre el nuevo template de FE.


### Sistema de sugerencias de cursada y acompañamiento académico
Desde la comunidad de Informática se desarrolló una aplicación que genera y envía en forma masiva mails con sugerencias de cursada y otras acciones, donde el contenido está personalizado para cada estudiante a partir de los datos de su trayectoria académica.

El objetivo de este proyecto es realizar una nueva implementación de parte de esta aplicación, tomando como base un stack tecnológico actualizado, en concreto utilizando:
- para el FE: React 18, Material UI 5, React Router 6, y Vite (en lugar de Create React App). Estas son las herramientas de base del nuevo template de FE.
- para el BE: Nest.js y Mongoose. Queda a elección del grupo si usar JavaScript o TypeScript como lenguaje de programación.

El stakeholder para este proyecto es Carlos Lombardi.

**Importante**  
Como este es un proyecto que está operativo, debemos respetar la estructura de la BD, que está en Mongo. 


#### Instrucciones particulares para arrancar
Dentro de la orga de Github que armaron para la cursada, crear el repo de FE a partir del template que publicamos en este sitio, y el de BE siguiendo las instrucciones en el sitio de Nest.js.

Instalar mongodb.

Estudiar las funcionalidades de configuración, que van a ser las primeras en migrarse. Para esto el stakeholder les puede hacer una demostración y después enviarles screenshots.


#### Un poco más adelante

Instalar mongoose en el proyecto de BE. Buscar la documentación al respecto en el sitio de Nest.js.

Integrar en el proyecto de BE los modelos de BD que hay que respetar, y generar data inicial. Coordinar esto con el stakeholder.


### Intercambio de avisos para una comunidad
Se trata de crear una aplicación que facilite la publicación de avisos dentro de una comunidad, p.ej. la de lxs estudiantes de informática de la UNaHur.

Para una versión base, se plantean las siguientes funcionalidades.

1. crear un usuario y verificarlo.
2. elegir temas que me interesan.
3. ver los avisos publicados.
4. recibir notificaciones (browser o app mobile).
5. hacer una pregunta sobre un aviso.
6. publicar un aviso asociado a una categoria. un aviso una categoria. puedo agregar palabras clave.
7. responder una consulta sobre un aviso.
8. dar de baja un aviso.

A partir de la versión demarcada por los ítems anteriores, se puede sumar potencialidad e interés mediante los siguientes agregados. 

9.  analizar spam y contenido apropiado (spam usando p.ej. akismet, temática, adultos, etc, info sensible como números de celular; considerar el uso de IA).
10. búsquedas "inteligentes". Para ello, puede ser útil utilizar una plataforma de búsqueda como p.ej. Elastic Search o Apache Solr.
11. sugerir avisos relacionados. Aquí también puede intervenir alguna herramienta que explota IA.
12. usuarios moderadores.
13. comunidades (usuarios amigos).
14. integración con carteleras.

El stakeholder para este proyecto es Miguel Carboni.


#### Instrucciones particulares para arrancar
En este caso no hay restricciones para el stack tecnológico, queda a decisión del grupo de acuerdo a lo que se indica en la página de pautas para la cursada.


### Venta de tickets para eventos
El product Owner del equipo soclita un producto de venta de tickets para eventos. El objetivo del mismo es poder dar de alta eventos, realizar la búsqueda y las ventas de los tickets, sabiendo que cada lugar puede tener distintas configuraciones y capacidades (por ejemplo, campo parado, campo vip, campo vip numerado, platea sin numerar, etc)
Se requerirán estadísticas para el administrador.
El usuario final deberá poder registrarse, loguearse, y consultar sus transacciones, descargar sus tickets y vincular los mismos a personas.
Se toma por ejemplo sitios como platea net, ticketek y otros.

Se definirán estadísticas mas adelante.

Es posible que se requiera la generación de una fila virtual de ingreso.

El stakeholder para este proyecto es Cristian Schiffino.


#### Instrucciones particulares para arrancar
En este caso no hay restricciones para el stack tecnológico, queda a decisión del grupo de acuerdo a lo que se indica en la página de pautas para la cursada.


### Alquiler de autos
El objetivo es armar una aplicación que le sirva a una organización que alquila autos, para organizar su flota de autos, registrar los alquileres y los pagos, y realizar estadísticas.  
En principio la aplicación es sólo para uso del personal de la agencia, la posibilidad de que un cliente pueda registrar una operación la dejamos para más adelante.

El stakeholder para este proyecto es Carlos Lombardi.


#### Instrucciones particulares para arrancar
En este caso no hay restricciones para el stack tecnológico, queda a decisión del grupo de acuerdo a lo que se indica en la página de pautas para la cursada.


#### Algunas funcionalidades a implementar
Registro de un nuevo alquiler, que implica:
- Ingresar fecha, hora y lugar de retiro y devolución.
- Permitir al usuario elegir un auto de los que maneja la agencia, dentro de los que estén disponibles en el período indicado para el alquiler.
- Cambiar el precio standard para el auto, por uno particular para el alquiler.
- Registrar nombre y apellido, teléfono y e-mail de la persona que alquila.

Agenda con eventos de entrega y recepción de autos en cada día.

Registro de auto no disponible por reparaciones o chequeos.

Manejo del pago de cada alquiler, permitiendo pagos parciales.

Estadísticas por auto y por cliente.



## Grupos

### Grupo 1
Matías Crisnejo  
Ignacio Fazah Beiroa  
Pablo Lopes Ferrao  
Marcos Macagna  
Nahuel Monje  

**Trabajo asignado**:  
Alquiler de autos

### Grupo 2
Gabriel Bianglino  
Enzo Colocho  
José Luis Farías  
Aldana Gómez  
Lucila Portillo Zuccotti  

**Trabajo asignado**:  
Intercambio de avisos para una comunidad

### Grupo 3
Marcos Monescao  
Julieta Noguera  
Agustín Otero  
César Augusto Pacheco  

**Trabajo asignado**:  
Cuaderno de laboratorio orientado a estudiantes

### Grupo 4
Lucas Bonadeo  
Hernán Marcelo Coniglio  
Matías Müller  
Mauricio Enrique Pintos  

**Trabajo asignado**:  
Venta de tickets para eventos

### Grupo 5
Damián Bruque López  
Javier Morales  
Patricio Rearte  
Cristian Vitola  

**Trabajo asignado**:  
Sistema de sugerencias de cursada y acompañamiento


## Cronograma 

| Fecha | Es presencial | Actividad |
| --- | --- | --- |
| 04/04 | No | Presentación / objetivos / armado de equipos / selección de trabajos / Figma. |
| 11/04 | No | <b>1er Sprint - planning</b> <br/> |
| 18/04 | No | Metodología agile / Relevamiento / análisis inicial. |
| 25/04 | No | <b>1er Sprint - review<b><br/><b>2do Sprint - planning<b> |
| 02/05 | No | React - parte 1. <br/> Seguimiento. |
| 09/05 | No | Manejo de branches. <br/> Seguimiento. |
| 16/05 | No | <b>2do Sprint - review<b><br/><b>3er Sprint - planning<b> |
| 23/05 | No |  React - parte 2. <br/> Seguimiento. |
| 30/05 | No |  Backend. <br/> Seguimiento. |
| 06/06 | No | <b>3er Sprint - review</b><br/><b>4to Sprint - planning</b> |
| 13/06 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Presentación presencial medio término</span> | 
| 20/06 | <span style="font-weight: bold; color: #f57c00">----</span> |  <span style="font-weight: bold; color: #f57c00">Feriado</span> |
| 27/06 | No | <b>4to Sprint - review<b><br/><b>5to Sprint - planning<b> |
| 04/07 | No | Seguimiento |
| 11/07 | No | <b>5to Sprint - review<b> |
| 18/07 | <span style="font-weight: bold; color: crimson">Sí</span> | <span style="font-weight: bold; color: crimson">Presentación final presencial</span> |

En las clases con tema y seguimiento, apuntamos en dar el tema de 18.00 a 19.45, y dejar espacio para seguimiento a partir de las 20.00, paralelizando entre los docentes para cubrir más grupos.
