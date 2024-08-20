# Control de gastos de subsidios

## Contexto y objetivos
La UNAHUR (como es común en las universidades públicas argentinas) destina una parte (pequeñita) de su presupuesto para actividades de investigación.  
Para asignar estos fondos, se organizan convocatorias en las cuales grupos de docentes hacen propuestas de trabajos a realizar. Se forma un jurado que elige cuáles de los proyectos propuestos son elegidos para que la Universidad los financie, y qué monto se destina a cada proyecto. Esto se conoce como subsidio a un grupo de docentes/investigadores.

Con los fondos que se le asignan mediante un subsidio, cada grupo de docentes/investigadores compra bienes, contrata servicios, financia viajes de intercambio o presentación de resultados, y paga los gastos de inscripción a congresos y publicación de artículos.
La Universidad debe aprobar cada gastos, y después tiene que llevar un control, recibiendo copia de la factura correspondiente.

La Secretaría de Investigación propuso implementar una aplicación que informatice la gestión de los gastos de subsidios. 

### Stakeholder
En principio, el stakeholder para este proyecto es Juan Pedrosa, el secretario de Investigación. Probablemente él delegará el seguimiento a alguna persona del plantel de la Secretaría.

## Estado del proyecto
En el marco de cursadas anteriores, se llegó a implementar las funcionalidades principales pedidas por la Secretaría, con un buen grado de avance.  
Esta es la [carpeta](../adjuntos/gastos-de-subsidios-2023s2.pdf){:target="_blank"} presentada por el grupo que trabajó sobre este proyecto en 2023.

## Objetivos preliminares para segundo cuatrimestre 2024 y primer cuatrimestre 2025

Planteamos tareas técnicas, un par de bugs, y varias tareas que agregan o mejoran funcionalidades.  
Las tareas técnicas se consensúan con los docentes, los bugs se arreglan y ya, las cuestiones funcionales se consensúan con el stakeholder.

### Tareas técnicas
- Actualizar el stack tecnológico del FE al nuevo template, o sea: vite / react 18 / mui 5 / react router 6.
- Definir y usar un storage externo para los archivos adjuntos (facturas de compra). Este storage puede ser algún recurso de cloud, o la misma BD. Pero no vale almacenar los adjuntos dentro del servidor que va a alojar el BE. <br/> Hay una tercera opción que nunca probé, pero la tiro por las dudas: usar un repo Git (para lo cual hay que hacer un commit + push ante cada archivo que se sube).
- Agregar algo de unit test, al menos en backend.

### Bugs
- En el rol investigador, si se elige la opción "Proveedores", se lanzan continuamente consultas a `GET /proveedores`.
- En el BE, si se manda mal un dato en el POST /api/compras, mandar status 400 en lugar de 404.

### Funcionalidades a agregar/mejorar/modificar
- Implementar la edición de los combos que aparecen en la creación de proyectos (tipo, organismo, agrupamiento de I+D, convocatoria).
- Permitir modificar o dar de baja una compra desde el rol investigador - sólo si está en estado pendiente.
- Permitir consulta de detalle de una compra desde el rol investigador.
- Mostrar gráfico detalle de presupuesto de un proyecto para el rol administrador (ahora está solamente para el rol investigador).
- Completar administración de usuarios, está sólo el alta.
- Mostrar el rol del usuario logueado (administrador o investigador).
- Definir si en un proyecto director y codirector también tienen que ser usuarios.
- Implementar la administración de documentos de normativas.
- En el gráfico de torta, separar cada rubro en aprobado+pendiente por un lado, remanente por otro. O sea, en lugar de 6 colores que sean 12.
- Validar en el FE, alta de compras, que el CAE tiene que ser un número.
- Verificar las validaciones en el alta de proyectos. En particular: permite fin anterior al inicio, sólo permite números en número expediente / número resolución / número proyecto.


## Instrucciones particulares para arrancar

### Entender el dominio
Leer la carpeta del equipo que trabajó en este proyecto en 2023, que está linkeada arriba en esta página. Entender el dominio y las funcionalidades implementadas.

### Inicializar los repos de código remoto y local
Hacer los fork (ver instrucciones [en esta página](../../creacion-repos-de-codigo.md)) de los repositorios con el código existente, en la organización de GitHub correspondiente al grupo. Los repositorios base que deben forkear son estos:
- Backend: https://github.com/unahur-desapp/control-gastos-subsidios-backend 
- Frontend: https://github.com/unahur-desapp/control-gastos-subsidios-frontend

Una vez creados los fork, en el equipo de cada integrante:
- Clonar los dos repos apenas creados (o sea los forks).
- **Importante** <br/> Para los dos repositorios, moverse al branch `inicio-c2-2024`.
- En ambos repos, ejecutar `npm install` para cargar las librerías.

### Configurar la BD y la carpeta de archivos subidos
Instalarse PostgreSQL. Crear una BD para el proyecto y configurarla desde el archivo `.env.development` del BE. Ejecutar las tareas `npm run db:init` y `npm run db:seed` en el proyecto de BE, para definir la base y cargar algunos datos iniciales.

Crear una carpeta `uploads` dentro del raíz del proyecto backend. Ahí van a ir a parar las facturas que se suban para cada nueva compra.

### Levantar BE y FE
Alcanza con `npm start` en ambos casos.

### Después
Entre los datos iniciales hay cuatro usuarios, en particular `azurduy` que es administrador, y `artigas` que es investigador. La clave de los dos es 123456.

Utilizando estos dos usuarios, navegar la aplicación para entender un poco de qué se trata, relacionar con lo que se leyó en la carpeta. En particular recomendamos.
- Entrar con `artigas`. Tiene un proyecto solo, elegirlo. Mirar el presupuesto. Cargar tres compras.
- Entrar con `azurduy`. Elegir el proyecto donde se cargó la compra (es el de "Desarrollo de software para la monitorización..."). Aprobar una compra, rechazar otra. Cargar un proyecto, incluir a `artigas` entre los usuarios responsables.
- Volver a entrar con `artigas`. Ahora debería tener dos proyectos. Elegir el que ya estaba, ver los cambios en el presupuesto. Elegir el nuevo.

Conversar con los docentes sobre la lista provisional de tareas que aparece más arriba.


## Un poco más adelante
Cuando se sientan seguros con la aplicación y el dominio, solicitar una reunión con el stakeholder, mostrarle lo que está hecho, plantearle las funcionalidades planteadas por los docentes de Desarrollo de Aplicaciones, y refinar los pasos a seguir.
