---
ID: 181
post_title: >
  ¿Cómo enfrentarnos a código heredado
  (legacy code)?
author: pbousan
post_date: 2012-06-12 12:21:29
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/como-enfrentarnos-a-codigo-heredado-legacy-code/
published: true
---
Quien más y quien menos seguro que alguna vez se ha encontrado con un proyecto de mantenimiento, evolución o migración de una aplicación existente. Es lo que comúnmente se conoce como <em>"código heredado"</em> (o legacy code en inglés). El concepto de "herencia" tiene mucho que ver con lo que nos presentó <a href="https://twitter.com/fernandoescolar" target="_blank">@fernandoescolar</a> en su artículo sobre <a href="http://www.dotnetodology.com/deuda-tecnica">deuda técnica</a>. Cuanto menor sea la deuda técnica del proyecto, más sencillo resultará solventar sus bugs, evolucionarlo o migrarlo hacia otra arquitectura y/o plataforma.

Por desgracia, cuanto mayor sea esa deuda, más difícil resultará trabajar y evolucionar el proyecto. Lo peor de esta situación es que resulta complicado justificar ante el "cliente" (sobre todo, cuantos menos conocimientos técnicos tenga) el tiempo que tardemos en realizar pequeños cambios o solucionar bugs. Son muy habituales frases como: "Pero si ya está todo hecho", "La lógica está en el código (o peor, en la base de datos)", "Son dos pequeños cambios sin importancia",...
<h3>El edificio de cartón-piedra</h3>
No es intención de este artículo generalizar situaciones, pero basándome en mis propias experiencias y en las de compañeros de profesión, podemos decir que es complicado explicar y hacer entender que el mantenimiento de una aplicación se tiene que tratar con el mismo rigor y gestionar igual que un proyecto que se hace desde 0.

Como a veces es difícil hacernos entender en un lenguaje muy técnico, existen metáforas como las de la deuda técnica. Pero aun así, ésta puede no resultar adecuada. Podemos utilizar un símil un poco más visual para referirnos a un proyecto heredado, para intentar explicar mejor lo complejo que resulta abordarlo:

<img style="display: block; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/torres.jpg" width="175" height="200" />

Cuando heredamos un proyecto (ya sea una persona sola o un equipo) es como cuando alguien hereda o compra un edificio de oficinas y nos contratan para acondicionarlo. Si el edificio está en perfecto estado, tiene buenos cimientos, una instalación eléctrica bien pensada y planificada, plantas bien distribuidas y está hecho con buenos materiales, se podrán hacer los cambios necesarios de manera rápida y fácil y así tener a nuestro cliente listo para usarlo. Será suficiente con pintar, actualizar algunas zonas y comprar mobiliario nuevo.

Pero si lo que se ha comprado es un decorado de cine, muy bonito y vistoso... pero de cartón piedra, detrás del cual sólo hay una caseta de obra en la que duermen un vagabundo y su perro.

&nbsp;
<div style="line-height: 70px; vertical-align: middle;"><img style="display: inline; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10//movie.jpg" width="210" height="170" /> <strong><span style="font-size: 90px;">+</span></strong><img style="display: inline; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/caseta.jpg" width="210" height="170" /><strong><span style="font-size: 70px;">= WTF!!</span></strong></div>
&nbsp;

Y nos contratan para que le añadamos dos pisos más y un parking... Es evidente que tendremos un problema: el comprador no sabrá nada sobre el decorado, es más, estará convencidísimo de que lo que había adquirido era un edificio perfectamente acabado. Nadie de los vendedores sabrán nada sobre la caseta de obra, y mucho menos qué hacen el vagabundo y su perro viviendo en ella. Todo el mundo se lavará las manos pero seguirán pidiendo los dos pisos y el parking.

Será entonces cuando tendremos que hacer entender que es necesario deshacerse de la caseta de obra, tirar el decorado, excavar los cimientos, hacer una estructura sólida y a partir de ahí, planear cuántos pisos podemos construir y a qué precio.

Esta metáfora nos puede servir para describir un proyecto con una arquitectura deficiente (más bien inexistente), mal estructurado, sin documentación y sin responsables a los que poder preguntar sobre las decisiones tomadas. (Seguro que más de uno ha esbozado una sonrisa recordando aquel proyecto en el que se encontró una caseta de obra tras una fachada grandiosa).

Lo que intento explicar es que afrontar un proyecto heredado con prisas y sin planificación es la principal causa para volver a repetir los errores cometidos en un principio. Es lo que se suele conocer como proyecto “sumidero”, una aplicación por la que han pasado muchos programadores, han hecho los cambios que les han pedido, pero no se han preocupado de lo que se va a encontrar el que venga detrás.
<h3>¿Por donde empiezo?</h3>
Cuando eres un desarrollador sin mucha experiencia y afrontas un proyecto con código heredado, la tendencia es a tocar lo mínimo posible y a suponer que lo que hay hecho estará bien. Es un comportamiento natural ya que nadie quiere ser el responsable de "romper" algo que estaba funcionando. Así que lo normal suele ser hacer cambios superficiales e intentar salir airoso.

Si eres un desarrollador medianamente experimentado, ya habrás desarrollado tu "olfato" para detectar problemas. Es lo que Ken Beck definió como "Code Smell", sobre lo que también nos habló <a href="https://twitter.com/fernandoescolar" target="_blank">@fernandoescolar</a> en su anterior <a href="http://www.dotnetodology.com/deuda-tecnica">artículo</a>, y consiste en indicadores superficiales que denotan problemas más profundos. Por ejemplo, al abrir una solución en Visual Studio, un programador con experiencia puede detectar de un vistazo la falta de estructura o la desorganización en los proyectos. Esto, en sí mismo, no es un indicativo de que la aplicación tenga algún problema, pero ya <em>huele</em> a que lo puede tener. O al menos, es un síntoma de que será difícil de mantener.

En ambos casos, estaremos dependiendo del <em>instinto</em> de la persona (o equipo) encargado de mantener el software para que lleven la tarea a buen término. Pero esta capacidad para detectar problemas tampoco nos asegura que vamos a hacer las cosas bien.

Ahora veremos cómo plantear una aproximación más eficaz para lidiar con código heredado.
<h3><strong>TRAZA UN PLAN</strong></h3>
Existen varios libros sobre el tema de mantener código legado en los que se presentan planes y tácticas para llevar a cabo estos procesos. Por ejemplo, el "Object-Oriented Reengineering Patterns" [1], presenta la siguiente guía de pasos a seguir:

<img style="display: block; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/legacy.bmp" width="420" height="360" />

Como se puede ver en la imagen, no se empieza a mantener la aplicación hasta que se tiene un conocimiento importante de qué hace. Esto es fundamental, ya que empezar a modificar el código de una aplicación tal cual esté, suele llevar a cometer los mismos errores que cometió el equipo original.

Aunque no sigamos exactamente esta guía, sí que es importante trazar algún plan de acción e intentar no desviarnos de él, a no ser que haya causas justificadas. Nuestra propuesta de plan de acción es la siguiente:
<ul>
	<li>Reconocimiento del terreno</li>
	<li>Establece el alcance</li>
	<li>Crea tu red de seguridad</li>
	<li>Métricas de código: detecta la deuda técnica</li>
	<li>Establece tareas y prioriza</li>
	<li>Manos a la obra</li>
</ul>
<h3>Reconocimiento del terreno</h3>
Lo primero que deberíamos hacer es tener una pequeña entrevista con la persona responsable de la aplicación que vamos a heredar. En esta entrevista tendremos que obtener la información básica sobre el proyecto: ¿cuál es su fin?, ¿cómo encaja con el resto de las aplicaciones de la empresa/departamento?, ¿qué nivel de criticidad tiene?,...

Con esto tendremos suficiente para identificar los puntos críticos de la aplicación. Por ejemplo, no es lo mismo una aplicación que sirva para que un alumno de instituto vea sus notas, que otra para que un cirujano consulte el historial del paciente que tiene en la mesa de operaciones.

Una vez hecho esto, deberíamos conocer cómo funciona, de manera rápida, el software que vamos heredar. Alguien que domine el uso de la aplicación debería hacernos una demostración de su funcionalidad. Es deseable que esta demo nos la haga un usuario antes que un desarrollador. Todos sabemos que los desarrolladores evitarán las acciones más propensas a producir un fallo.
<h3>Establece el alcance</h3>
Este es un punto muy importante sobre todo para la motivación de la persona o el equipo que va a responder por el proyecto. Es necesario tener una idea clara de qué se quiere hacer con la aplicación para establecer cuanto puede durar el proceso.

Hablando en plata, a nadie le gusta "limpiar la basura de otros", y menos hacerlo durante mucho tiempo. Así que es necesario establecer si se trata de mantenimiento puro (resolución de bugs), evolución y adición de nuevas funcionalidades, migración a otra plataforma, o una mezcla de algunos de estos procesos.
<h3>Crea tu red de seguridad</h3>
Con toda la información obtenida en las fases anteriores, ya podemos empezar con el código. Pero antes de empezar a modificarlo, deberemos evitar <em>romper</em> algo. La mejor forma de evitar esto es apoyarse en pruebas unitarias: es una forma de probar que un determinado bloque de código fuente, funciona correctamente. Y pruebas de integración, que comprueban que los diferentes artefactos funcionan correctamente unos con otros. Así que si la aplicación no tiene este tipo de tests, antes de empezar a solucionar nada, hay que crearlos. Durante el proceso de creación de test es buen momento para establecer la lógica de negocio, y tal vez nos encontremos con errores o incongruencias que nos ahorrarán trabajo posterior. Además, estos test nos servirán como parte de la documentación para nuestro cliente, sobre todo si hacemos <a href="http://gemini.udistrital.edu.co/comunidad/grupos/arquisoft/fileadmin/Estudiantes/Pruebas/HTML%20-%20Pruebas%20de%20software/node55.html">pruebas de aceptación</a>, cuyo objetivo es validar que un sistema cumple con el funcionamiento esperado y permitir al usuario de dicho sistema que determine su aceptación, desde el punto de vista de su funcionalidad y rendimiento.
<h3>Métricas de código: detecta la deuda técnica</h3>
Para poder medir la deuda técnica, es necesario hacer una auditoría inicial de código fuente: Varios programadores deberían analizar el código, calcular métricas,… Para esto viene muy bien, complementariamente al estudio, herramientas como Sonar o el Code Analysis (FxCode), Code Metrics del Visual Studio o Simian para detectar código repetido. En próximos artículos hablaremos más en profundidad sobre las métricas de código, pero podemos decir que con ellas podremos medir la mantenibilidad (dificultad para realizar el mantenimiento) del código, su complejidad y el nivel de profundidad en la jerarquía de objetos. Estos valores nos servirán para conocer un poco más a qué nos estamos enfrentando.
<h3>Establece tareas y prioriza</h3>
Con las conclusiones del estudio del código se debería crear una lista de tareas a desarrollar, priorizarlas y analizar su impacto. A partir de estos datos podríamos ser capaces de asegurar el ROI (Retorno de Inversión), eligiendo correctamente el momento de llevarlas a cabo. Ya que si tienes que mantener la aplicación y evolucionarla; por ejemplo, no puedes dejar un mes un bug prioritario bloqueado por pagar deuda técnica.

Los análisis de pago de deuda técnica se basan en <a href="http://c2.com/cgi-bin/wiki?FirstLawOfProgramming">la primera ley de la programación de Ward Cunningham</a>, que indica que: “Reducir la calidad, incrementa el tiempo de desarrollo.”, y queda gráficamente representado como la curva de costo:

<img style="display: block; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/curva.png" width="420" height="360" />

La curva de costo de cambio demuestra que los diseños de alta calidad, simples y fáciles de seguir pueden costar más al principio, pero representarán una deuda técnica inferior más adelante; las modificaciones y las adiciones que deban hacerse posteriormente al código serán menos costosas. En la curva de calidad (roja), podrá observar que el costo inicial es superior, pero con el tiempo se vuelve previsible. La curva rápida (azul) muestra un costo inferior al principio, pero con el tiempo el desarrollo, mantenimiento y costo total de un producto y su código se hacen más costosos.

Herramientas como Scrum y Kanban pueden ser muy buenos aliados a la hora de priorizar, asignar y mantener el control sobre las tareas. Como dijimos al principio del artículo, es fundamental tratar estos proyectos como si fuesen un desarrollo desde 0, de otra forma caeremos en peticiones continuas de nuevas mejoras o bugs que no tienen prioridad y se van pisando unos a otros (normalmente, dependiendo de lo fuerte que griten los clientes).

<img style="display: block; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/kanban.jpeg" width="424" height="339" />

<a href="https://twitter.com/#!/bmegias">@bmegias</a> me demostró en un proyecto cómo un tablero Kanban mejora sustancialmente el seguimiento de la resolución de bugs en una aplicación que está en producción.
<h3>Manos a la obra</h3>
Ya es momento de atacar el código: tendremos los tests que asegurar que no rompemos nada, hemos detectado los problemas y tenemos tareas para solucionarlos, pero nos falta lo más importante... saber cómo vamos a proceder.

Un equipo experimentado intentará basarse en el conocimiento adquirido para, aplicando principios como los SOLID, patrones de diseño y técnicas de Extreme programming como la integración continua, TDD y Pair Programming, avanzar rápidamente en la adaptación del código una estructura más sólida y mantenible.

Pero, un equipo con menos experiencia se puede encontrar perdido en este punto, y es aquí donde entran las técnicas de <a href="http://www.refactoring.com/">refactorización</a>: disciplina de restructurar código existente, alterando su estructura interna, pero sin cambiar su comportamiento.

Hay dos libros fundamentales en este aspecto: "Refactoring: Improving the Design of Existing Code"[2] y "Refactoring To Patterns"[3]. Existen más libros en el mercado, pero estos 2 tienen una particularidad, los autores mantienen un listado más o menos actualizado de técnicas de refactoring, veamos unos ejemplos de lo que nos proponen:

- <a href="http://www.refactoring.com/catalog/replaceConstructorWithFactoryMethod.html">Remplazar un constructor por un método Factory</a>

- <a href="http://refactoring.com/catalog/replaceConditionalWithPolymorphism.html">Remplazar lógica condicional con polimorfismo</a>

El estudio de los principios SOLID, patrones de diseño y estas técnicas pueden ser un buen punto de partida para afrontar un proyecto heredado para un equipo sin rumbo.

<img style="display: block; margin-left: auto; margin-right: auto;" alt="" src="/wp-content/uploads/2012/10/refactor.jpg" width="300" height="330" />

Por supuesto, este plan debe ser aceptado por el "cliente", ya que muchos de los puntos se refieren a tareas de análisis y planificación. Es necesario hacer entender que estas tareas son imprescindibles para dotar al proyecto de la calidad que obviamente le falta, mejorar la mantenibilidad del código y hará mucho más sencillo las siguientes evoluciones de la aplicación.

<strong>Bibliografía</strong>

[1]"Object-Oriented Reengineering Patterns" de Oscar Nierstrasz, Stéphane Ducasse y Serge Demeyer. ISBN-10: 395233412X | ISBN-13: 978-3952334126

[2] "Refactoring: Improving the Design of Existing Code" de Martin J Fowler, Kent Beck, John Brant, William Opdyke y Don Roberts. ISBN-10: 0201485672 | ISBN-13: 978-0201485677

[3] "Refactoring to Patterns" de Joshua Kerievsky. ISBN-10: 0-321-21335-1 | ISBN-13: 978-0-321-21335-8