# Aplicación 2 - acceso de afiliados y grupo familiar
Mediante esta aplicación, los afiliados a la empresa y algunos miembros del grupo familiar pueden 
- Solicitar turnos de atención (de acuerdo a la disponibilidad que configura la empresa, ver aplicación 1).
- Gestionar reintegros.
- Abrir pedidos de autorización de prestaciones que deben ser autorizadas.
- Registrar recetas para las que se solicita cobertura por parte de la empresa.
- Consultar la cartilla de prestadores.

Los pedidos de reintegros, autorizaciones y recetas son revisados por los prestadores, esto forma parte del alcance de la aplicación 3.

## Registro de usuarios
Los afiliados, así como los miembros del grupo familiar que tengan al menos 16 años, se deben registrar en la aplicación, después de haber sido dados de alta por la empresa (ver aplicación 1). Para esta aplicación, la información sobre afiliados se carga directamente en la BD, y después la registración se implementa como parte de esta aplicación.  
Durante la registración, cada usuario elige una contraseña que le sirve para los accesos subsiguientes a la aplicación.

Una vez registrados, los usuarios pueden realizar operaciones (ver alcance en la introducción), y ver operaciones registradas, de acuerdo a estas reglas
- El afiliado puede ver sus operaciones y las de todos los integrantes del grupo familiar; puede registrar operaciones para sí y para los hijos menores de 18 años.
- El cónyuge puede ver y registrar operaciones para sí y para los hijos menores de 18 años.
- Los otros usuarios pueden ver y registrar operaciones solamente para sí mismos.

## Gestión de reintegros, autorizaciones y recetas
Se presenta al usuario un dashboard con información sobre los reintegros, autorizaciones y recetas que puede ver, teniendo en cuenta los estados de cada uno (ver explicación sobre estado de una operación en la aplicación 3).
En particular, debe ser posible acceder a las solicitudes
- Pendientes de procesamiento.
- Observadas.
- Rechazadas en la última semana.
- Aprobadas en la última semana.  

También es interesante ver la lista de las recetas, y dar información sobre qué medicamentos se recetaron, con cantidades totales para un período de tiempo.

Para las solicitudes observadas, el usuario tiene que escribir un texto. Cuando se graba este texto, la solicitud vuelve al estado “En análisis”.

Las solicitudes en estado “Recibido” se pueden modificar o eliminar, las otras no.

A continuación se detallan los datos que hay que registrar para cada tipo de solicitud.
### Datos de un reintegro
Hay que cargar
- Fecha de la prestación.
- Integrante (de acuerdo a las reglas indicadas en “Registro de usuarios”).
- Médico.
- Especialidad.
- Lugar donde fue atendido.
- Datos de la factura incluyendo: fecha, CUIT, valor total, persona a la que se le factura.
- Forma de pago del reintegro (cheque, efectivo, transferencia - indicando CBU).
- Observaciones.

Los datos deben ser coherentes con la información sobre prestadores (ver aplicación 1). Los datos sobre los médicos se cargan directamente en la BD (dado que su gestión está dentro del alcance de la aplicación 1), las especialidades son una lista conocida.

### Datos de una autorización
Hay que cargar
- Fecha prevista para la prestación.
- Integrante (de acuerdo a las reglas indicadas en “Registro de usuarios”).
- Médico.
- Especialidad.
- Lugar donde se realizará la prestación.
- Días de internación.
- Observaciones.

Los datos deben ser coherentes con la información sobre prestadores (ver aplicación 1). Los datos sobre los médicos se cargan directamente en la BD (dado que su gestión está dentro del alcance de la aplicación 1), las especialidades son una lista conocida.

### Datos de una receta
Hay que cargar
- Integrante (de acuerdo a las reglas indicadas en “Registro de usuarios”).
- Medicamento.
- Cantidad.
- Presentación (puede ser blister, capsulas, pastillas, inyectable, gotas entre otros).
- Observaciones.

## Gestión de turnos
Debe ser posible reservar un turno de atención médica, teniendo en cuenta la disponibilidad de turnos que configura la empresa, y que se describe dentro del alcance de la Aplicación 1. Para el desarrollo de la aplicación 2, la disponibilidad de turnos se carga directamente en la BD.

Obviamente, una vez reservado un turno, deja de estar disponible. En la reserva se indica para quién es, dentro de lo que puede hacer el usuario logueado.  
Una reserva de turno se puede cancelar hasta un día antes del mismo.  

Tiene que brindarse una consulta de turnos reservados, que puede o no unirse al dashboard de solicitudes mencionado más arriba. 

<!-- ## Cartilla.
Debe incluirse una funcionalidad de búsqueda de prestadores, con filtros por (al menos) código postal, especialidad, y apellido del médico. Los datos sobre los prestadores se cargan directamente en la BD (dado que su gestión está dentro del alcance de la aplicación 1). -->
