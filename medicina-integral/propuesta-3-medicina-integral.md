# Aplicación 3 - prestadores
Mediante esta aplicación, los prestadores realizarán el procesamiento de las solicitudes de reintegros, autorizaciones y recetas registradas por los afiliados (esto es parte del alcance de la aplicación 2).  
También debe ser posible gestionar las situaciones terapéuticas de los afiliados y miembros de grupo familiar, registrando las novedades que ocurren después del alta.  
Finalmente, se debe brindar una visualización de los turnos reservados para el prestador, y de la historia clínica de un afiliado o miembro de grupo familiar.

Cada médico puede procesar las solicitudes de reintegros y autorizaciones que le corresponden. Los centros médicos pueden procesar las solicitudes de reintegros y autorizaciones de los médicos que forman parte de su personal. Todos los prestadores pueden procesar cualquier receta.

**Importante**:  
los datos sobre los prestadores, afiliados y sus grupos familiares se cargan directamente en la BD (dado que su gestión está dentro del alcance de la aplicación 1). Idem para reintegros, autorizaciones, recetas y turnos solicitados (cuya gestión pertenece al alcance de la aplicación 2).  
Respecto de prestadores, afiliados y grupo familiar, tener en cuenta solamente los datos necesarios para desarrollar la funcionalidad de esta aplicación. P.ej. las direcciones de los afiliados y de los prestadores no importan, la composición del grupo familiar de un afiliado y si un prestador es médico o centro médico sí. Los horarios de atención de un prestador se pueden descartar, dado que vamos a trabajar directamente con las agendas de turnos.

## Workflow de solicitudes
Se deberá implementar un workflow con cambios de estados en donde los mismos deben quedar registrados, y en donde los estados serán:
- Recibido.
- En análisis.
- Observado.
- Aprobado.
- Rechazado.

Cuando una solicitud pasa a “en análisis”, los pasos siguientes solamente los puede dar el usuario que realizó este cambio de estado. Cuando pasa a “observado”, queda habilitada para que el afiliado (o miembro de grupo familiar) agregue comentarios, como se indica en el alcance de la Aplicación 2.

Al observar o rechazar un trámite, se deberá cargar el motivo.

## Gestión de las solicitudes
Al prestador se le debe presentar una bandeja de entrada con las solicitudes que puede procesar. El diseño de esta bandeja de entrada se deja a criterio del equipo de desarrollo.  
Seguro tiene que ser fácil visualizar las solicitudes en análisis y observadas. 

Asociado a esta bandeja de entrada, implementar un dashboard con información sobre las solicitudes pendientes y resueltas (una solicitud queda resuelta cuando pasa al estado aprobada o al estado rechazada). Es interesante ver la evolución de cantidades de solicitudes procesadas por día o semana.

## Gestión de situaciones terapéuticas
Primero hay que seleccionar un afiliado, buscándolo por número de afiliado, apellido o teléfono.  
La aplicación muestra las situaciones terapéuticas de todo el grupo familiar del afiliado, separándolas por integrante. El prestador puede
- Modificar la fecha de finalización de una situación.
- Dar de baja una situación.
- Dar de alta una situación.

## Consulta y gestión de turnos asignados
Se le presenta al prestador un calendario con los turnos solicitados por los afiliados (ver aplicación 2). 
Para centros médicos, se muestra el calendario para una especialidad, que el operador elige previamente.

El prestador puede ingresar notas asociadas a un turno, que pasan a engrosar la historia clínica de la persona atendida. 
<!-- Además de esto, puede dar de alta nuevas solicitudes, con los mismos datos indicados en la Aplicación 1; estas solicitudes también quedan asociadas al turno. -->

## Consulta de historias clínicas
Seleccionando un afiliado o miembro del grupo familiar, se debe poder visualizar la historia clínica, pudiendo filtrar sólo las notas tomadas por el prestador que está haciendo la consulta, o todas.




