# Introducción
La Empresa **Medicina Integral** ha abierto sus puertas y está captando nuevos afiliados para vender sus productos de Medicina Prepaga. Estos productos involucran la atención de los afiliados y sus grupos familiares, por parte de prestadores de servicios médicos que tienen relación con la empresa.  
Para soportar la relación con los afiliados y con los prestadores, la empresa se propone el desarrollo de las tres aplicaciones que describimos más adelante. Cada una de estas aplicaciones cubre las interacciones con distintos actores: una para la administración de la empresa, otra para los afiliados, y una tercera para los médicos prestadores de servicios.

En principio, las tres aplicaciones deberían formar un todo coherente. Esto no es obligatorio a los efectos de las cursadas, pero sí puede ser una alternativa a explorar por grupos que quieran experimentar un desarrollo a escala mayor. En lo que sigue, las referencias a otras aplicaciones dentro del enunciado de una de ellas, deberán ser reemplazadas por la carga directa de datos (mediante scripts que los insertan en la BD).

## Pequeño glosario
Es importante destacar que se encontrarán con términos del ámbito de la atención médica, a continuación describimos algunos.

### Afiliado y grupo familiar
Llamamos _afiliado_ a cada persona que firman contratos con la empresa.  
En el contrato se proveen servicios de salud al afiliado y a su _grupo familiar_ que puede incluir: un cónyuge, uno o varios hijos/as, y uno o más familiares a cargo. El afiliado forma parte del grupo familiar, es su _titular_.

### Prestador, prestación
Llamamos _prestador_ a cada profesional o centro médico que brinda servicios de salud a través de la empresa. Para el caso de los centros médicos, se registran por separado el centro y cada uno de los médicos que trabajan en el mismo.  
Llamamos _prestación_ a cada servicio que un afiliado o miembro de grupo familiar recibe por intermedio de la empresa.

### Situación terapéutica
Una _situación terapéutica_ consiste en una dolencia o situación que se da de forma crónica. Por ejemplo, una mujer embarazada, una discapacidad, o una persona que ha tenido un acv o dolencia cardiaca crónica.  
Una situación terapéutica se puede cargar por un tiempo limitado o ilimitado, es decir que tiene una fecha desde obligatoria y una fecha hasta no obligatoria.  
Hay que registrar las situaciones terapéuticas de cada integrante del grupo familiar de un afiliado. Las que se conozcan en el momento de dar el alta al integrante del grupo familiar se registran en ese momento por parte del personal administrativo de la empresa, esto es parte del alcance de la aplicación 1. Las que se producen después las registra el médico que las detecta, eso es parte de la aplicación 3.

### Reintegros, autorizaciones, recetas
Para algunas prestaciones, el afiliado paga por anticipado todo el costo o parte del mismo, y después puede pedirle a la empresa que le restituya el importe pagado. A esto se le llama un _reintegro_.  
A su vez, algunas prestaciones (p.ej. ciertas operaciones) deben ser autorizadas por la empresa <u>antes</u> de realizarse. El sistema a desarrollar debe contemplar el manejo de estas _autorizaciones_.
Por último, como resultado de una prestación, un prestador puede emitir _recetas_ cuyo costo será cubierto por la empresa. El procesamiento de estas recetas también entra dentro del dominio del sistema.

### Dashboard
Varios ítems del enunciado hacen referencia a “dashboards”. Un dashboard es una interface en la que se presenta información consolidada: cantidades, casos especiales (p.ej. las últimas X actualizaciones), alertas, etc..  
Queda a criterio de cada grupo decidir qué información incluir en cada dashboard y cómo organizarla gráficamente.  
Se recomienda consultar a Google / ChatGPT / análogos al respecto.
