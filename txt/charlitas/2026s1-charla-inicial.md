# Intro
Situación particular, cambio violento del contexto
- Argentina
- mundo
- IA

Conclusión:  
posta piensen bien si de verdad este es el oficio que eligen, y en todo caso, no estaría en absoluto de más combinar con un oficio relacionado con las cosas que se tocan.


# Este cuatri
Antes que cada grupo genere (o intente generar) aplicaciones construidas con herramientas IA-powered, decidimos adelantarnos y proponer esta modalidad desde el grupo docente.  
O sea, vamos por una estrategia "full-IA".  

Hoy les vamos a mostrar un entorno 100% gratuito que les alentamos a usar. En algunas pruebas que fuimos haciendo, parece funcionar correctamente. Si les queda corto, sepan que tienen la alternativa de Claude Code, asumiendo un costo de 180 lucas aprox por 5 meses. Es lo que usamos Hernán y yo, y es un caño garantizado.

Tomamos este giro convencidos de que les va a ayudar a posicionarse respecto de las habilidades que se están popularizando en estos meses, y van a ser cada vez más solicitadas/relevantes.  
Dicho de otra forma, la apuesta es a darles herramientas que los ayuden a ponerse adelante de lo que pide el mercado.

Para que siga siendo un desafío, sabiendo que el uso de herramientas basadas en IA acelera en varias veces el desarrollo, subimos mucho la vara de lo que pedimos. Algo de detalle sobre esto después.


# Cómo es esto de desarrollar "con IA"
Modelo + herramienta. Uno escribe prompts en una herramienta, que le pasa el prompt a un modelo, el modelo genera texto (es lo que hacen los modelos), la herramienta graba los archivos que correspondan.

Si esperan escribir tres prompts y tener la app lista para entregar, lamento decepcionarlos. Hice una prueba el sábado pasado, me tomó 18 prompts, y más o menos 5 horas, llegar hasta la primera pantalla (que se puede mostrar). 

En un ratito vamos a los detalles operativos. Quiero antes mencionar algunos conceptos que creo que garpa mucho tener en cuenta
- Plan, la idea es que primero le pedís un plan, te genera un .md, lo mirás, peloteás hasta que te convence el plan, le pedís que lo ejecute, recién ahí genera código.
- Contexto: cuanto más información de contexto le demos, mejor van a ser los resultados. La información de contexto se guarda en archivos .md que conviene incluir en el repo. Y podemos pedirle a la misma herramienta que los vaya alimentando. Ejemplos rápidos de contexto: usá los colores de la paleta de MUI, guardá las llamadas API en la carpeta /services, generar tests en tal carpeta, los jugadores se ordenan por orden alfabético. 
- Mirar el código que genera, no vale que el código sea una roña porque "igual lo mantiene la IA". Ejemplo del FE inicial. También la simplificación de modelo.
- Posta, ir despacio, y sobre todo, ser uno el que marca el ritmo de desarrollo, no dejarse acelerar por planes súper ambiciosos que propone la IA. En nuestra experiencia, si le pedís que haga un desarrollo grande de una, lo va a hacer, pero con un montón de falencias.
- Acostúmbrense a usar la IA no solamente para generar el código, sino también para la UI y la documentación, y para las consultas técnicas. A mí que no me acuerdo ni si es includes o contains me ahorra bocha de tiempo.


# Un poco de contrato de cursada
Cinco sprints, reunión de cierre de sprint de 50 minutos, a la que tienen que llegar afilados. Tienen que
- hacer show de avance.
- responder preguntas que le vamos a hacer para que nos demuestren que un poco miraron el código que genera.
- a partir del sprint 2, presentar documentación, que vamos a ir especificando.

A su vez, les vamos a dar consignas para el trabajo en el siguiente sprint, que incluye la documentación que esperamos que produzcan.

Los dominios son *grandes*, no se duerman, si lo van llevando y le toman el ritmo al trabajo con IA (que es el objetivo principal de esta cursada) van a llegar bien, pero nooooo seeeeee confíen.

Contar un poco de qué se tratan los proyectos.


# Interactuando con OpenCode - un poco de hands-on
Cómo se fue refinando el plan.
Probar que ejecute el plan refinado, podríamos arrancar de etapa_1.1 y darle a los prompts 8 y 9.
