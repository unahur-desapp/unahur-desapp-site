# Aplicación 1 - administración de _Medicina Integral_
El propósito de esta aplicación es manejar la información relacionada con:
- Afiliados, incluyendo el grupo familiar de cada uno.
- Prestadores, incluyendo la configuración de turnos médicos disponibles para cada prestador. 
Esta aplicación será utilizada por el personal administrativo de la empresa.

A continuación, detalle sobre las funcionalidades que se esperan de esta aplicación.

## Alta de afiliados y grupo familiar
Debe ser posible crear grupos familiares, indicando los datos que siguen para cada integrante:
- Tipo documento
- Nro documento
- Nombre
- Apellido
- Fecha nacimiento
- Teléfono (puede tener más de un teléfono)
- Mail (puede tener más de un mail)
- Dirección (puede tener más de una dirección)
- Parentesco (Es el parentesco dentro del grupo familiar. Titular, cónyuge, hijo o familiar a cargo)
- Situaciones terapéuticas (pueden tener más de una, debe ser cargada de una lista de situación terapéuticas disponibles).
- Plan Médico (se selecciona desde un listado ejemplo 210, 310, 410, 510 o Bronce, Plata, Oro, Platino).

El equipo de desarrollo determinará qué validaciones hay que aplicar a la carga de un afiliado y de su grupo familiar.

También debe ser posible cargar nuevos integrantes a un grupo familiar existente, o modificar todos los datos excepto las situaciones terapéuticas (recordemos que la carga de situaciones terapéuticas que se descubren después que la persona se inscribe se hacen en la aplicación 3).  
Asimismo, se podrán dar de baja afiliados (lo que da de baja en forma automática a todo el grupo familiar), o integrantes individuales. 

Ofrecer una búsqueda de grupos familiares o integrantes por apellido, fecha de nacimiento, dirección o número de credencial (ver acá abajo).

### Consecuencias
Al realizar el alta de un grupo familiar, se deberá generar el nro de afiliado que será un número de 7 dígitos, y un número de integrante, en donde los integrantes irán desde 01 a 99 automáticamente. Ejemplo, el afiliado Pedro Gómez tendrá el número 0000001 y será el integrante 01. El hijo de Pedro Gómez tendrá el número de afiliado igual al padre pero el integrante 02, dado que integran el mismo grupo familiar.   
Por lo tanto, Pedro Gómez tendrá la credencial 0000001-01, y su hijo la 0000001-02.

El alta de un integrante o de todo un grupo familiar, puede ser con vigencia pasada o con vigencia futura. O sea, el 1ro de mayo se puede cargar un grupo familiar o integrante para que entre en vigencia el 1ro de junio, y también para el 1ro de abril.  
En forma análoga, se puede registrar la baja de un grupo familiar o integrante para que se ejecute en una fecha futura, p.ej. se carga la carga el 1ro de mayo para que se haga efectiva el 1ro de julio, o sea que el grupo familiar o la persona deje de tener cobertura a partir del 1ro de julio.

## Prestadores
Implementar un CRUD (alta / baja / modificación / consulta) de prestadores, teniendo en cuenta estos datos.
- Nro cuil o cuit.
- Nombre completo.
- Especialidades (puede tener más de una especialidad y debe ser cargada de una lista de especialidades).
- ¿Es un centro médico o un profesional independiente?
- ¿Integra centro médico? (sólo para profesionales- por sí, deberá indicar cuál)
- Teléfono (puede tener más de un teléfono)
- Mail (puede tener más de un mail)
- Dirección (puede tener más de una dirección) - cada una de estas direcciones es un lugar de atención asociado al prestador.
- Horarios de atención (se deberá cargar por cada lugar de atención).

Los horarios de atención definen en qué momentos de una semana el prestador puede recibir consultas. P.ej. de lunes a jueves de 8 a 13, lunes de 15 a 19, o martes y jueves de 8 a 12. Un prestador puede tener, para cada uno de sus lugares de atención asociado, más de un horario de atención.  
La eventual separación de estos horarios en distintas especialidades (p.ej. los lunes cardiología y los miércoles neumología) se especifica en las agendas de turnos, ver acá abajo. 

Ofrecer búsqueda por CUIT/CUIL, nombre, código postal, especialidad, día de atención (p.ej. prestadores que atiendan los miércoles) o cualquier combinación.

## Definición de agendas de turnos
Dentro de esta aplicación también está la carga de la _agenda de turnos_ de cada prestador. Cada agenda de turnos se refiere a un prestador, una especialidad y un lugar de atención. Se definen horarios (análogo a horarios de atención), y duración de cada turno en minutos.  
P.ej. para la doctora Tita Merello, la especialidad cardiología y el lugar de atención Avenida Vergara 1908, se definen turnos de media hora los lunes de 9 a 12, con lo cual van a quedar definidos 6 turnos de atención semanales.

Obviamente estas definiciones deben ser coherentes con la información sobre prestadores (ver punto anterior), respecto de la especialidad, el lugar de atención, y horarios de atención. En el ejemplo anterior, para que la definición de turnos sea válida:
- Cardiología está entre las especialidades que atiende la Dra. Tita Merello. 
- Avenida Vergara 1908 tiene que estar definido como lugar de atención de la Dra..
- Entre los horarios de atención de la Dra. para ese lugar de atención, tiene que haber alguno que cubra lunes de 9 a 12, p.ej. lunes de 8 a 14, lunes y miércoles de 9 a 18, etc..

Implementar un CRUD de agendas de turnos, incluyendo filtros por prestador y especialidad.

## Otras consultas
Además de las consultas indicadas en los ítems anteriores, implementar consultas que permitan obtener la información que se detalla a continuación.
- Alta de afiliados por periodos (o sea entre fecha y fecha).
- Alta de prestadores por periodo.
- Cantidad de prestadores por especialidad y por código postal.
- Reporte de situaciones terapéuticas por afiliado (considerando el grupo familiar de cada afiliado).
- Prestadores sin agendas de turnos cargadas.
- Horarios de atención de un prestador que no tiene turnos definidos.

