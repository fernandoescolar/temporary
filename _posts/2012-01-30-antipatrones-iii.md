---
ID: 102
post_title: 'Antipatrones: aprendiendo de los errores de otros (y III) #bdc11'
author: pbousan
post_date: 2012-01-30 13:42:00
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/antipatrones-iii/
published: true
---
<p>Tras el de <a href="http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-I">desarrollo</a> y el de <a href="http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-ii-bdc11">arquitectura</a>, en este tercer y &uacute;ltimo post sobre antipatrones nos vamos a centrar en los referentes a gesti&oacute;n de proyectos. Tal vez se traten de los m&aacute;s da&ntilde;inos para el buen resultado de un proyecto. Una aplicaci&oacute;n llena de c&oacute;digo spaghetti o con una arquitectura mal dise&ntilde;ada, seguramente es capaz de funcionar de una manera m&aacute;s o menos decente, al menos durante un periodo corto de tiempo.</p>
<p>Pero un proyecto mal gestionado tiene muchos n&uacute;meros para ser un fracaso, e incluso no llegar a ver nunca la luz. Seg&uacute;n <a href="http://www.galorath.com/wp/software-project-failure-costs-billions-better-estimation-planning-can-help.php">varios estudios</a> casi el 70% de los proyectos de software son un fracaso, provocando sobrecostes de cientos de billones de euros al a&ntilde;o. De estos, entre el 60 y el 80% son atribuibles directamente a una pobre toma de requerimientos, mala planificaci&oacute;n y gesti&oacute;n deficiente.</p>
<p>Veamos algunos ejemplos de antipatrones de gesti&oacute;n de proyectos que est&aacute;n bastante relacionados entre s&iacute;:</p>
<p><b>Smoke and Mirrors (Humo y espejos)</b></p>
<p>El nombre de este antipatr&oacute;n viene de los trucos que usan los ilusionistas para hacernos ver cosas que no existen (quien haya visto la pel&iacute;cula <a href="http://www.filmaffinity.com/es/film686978.html">El Ilusionista</a> tendr&aacute; una imagen muy clara de lo que hablo. El que no la haya visto, se la recomiendo). Se trata de vender como acabado un producto o funcionalidad que no est&aacute; implementado o ni tan siquiera dise&ntilde;ado. El cliente asumir&aacute; que est&aacute; finalizado y, l&oacute;gicamente, querr&aacute; tenerlo lo antes posible. Otro nombre para este antipatr&oacute;n ser&iacute;a: "Los powerpoints no compilan".</p>
<p>&nbsp;</p>
<p><b>Fire Drill (Simulacro de incendios)</b></p>
<p><img src="/wp-content/uploads/2012/09/fire_drill.jpg" alt="Fire Drill" style="margin-right: 5px;" width="200" align="left" height="150" /></p>
<p>Los gestores esperan hasta el &uacute;ltimo momento para permitir que los desarrolladores empiezen con el dise&ntilde;o y la implementaci&oacute;n de la aplicaci&oacute;n. Una vez empezado solicitan resultados inmediatos.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><b>Mushroom Management (Gesti&oacute;n Champi&ntilde;&oacute;n)</b></p>
<p><img src="/wp-content/uploads/2012/09/mushroom.jpg" alt="Mushroom" style="margin-right: 5px;" width="200" align="left" height="150" /></p>
<p>Sucede cuando se tiene a los desarrolladores como champi&ntilde;ones, en la oscuridad y alimentados con fertilizante. Cuando est&aacute;n listos, se cuecen y enlatan. La interacci&oacute;n con los clientes o usuarios finales est&aacute; prohibida, no s&oacute;lo todos los requerimientos llegan a trav&eacute;s del jefe de proyecto o analista de turno, sino que cualquier duda tiene que pasar tambi&eacute;n por ellos. Esto provoca que la comunicaci&oacute;n sea un factor que retrasa la toma de decisiones y la realizaci&oacute;n de acciones.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><b>Hero Cult (Cultura del h&eacute;roe)</b></p>
<p><img src="/wp-content/uploads/2012/09/overtime2.jpg" alt="Hero Cult" style="margin-right: 5px;" width="200" align="left" height="150" /></p>
<p>Siempre hay un "h&eacute;roe" que haciendo infinitas horas de m&aacute;s es capaz de sacar un proyecto adelante. El problema es cuando estas horas de m&aacute;s se entienden como lo normal y se requiere que todo el equipo las haga.Hay que entrar antes que el jefe y salir despu&eacute;s que &eacute;l. Por supuesto, cuando se acercan las fechas de entrega se pide otro esfuerzo m&aacute;s. Los desarrolladores se quedan hasta altas horas de la madrugada. La aplicaci&oacute;n se llena de errores por las prisas y la falta de sue&ntilde;o y empiezan los roces entre compa&ntilde;eros.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&iquest;Qu&eacute; provocan estos antipatrones?</h2>
<p>Desarrolladores cansados, haciendo horas para intentar llegar a un plazo imposible, pele&aacute;ndose entre s&iacute; y sin conocer los requisitos reales del cliente, lo que van a provocar son otros anitpatrones:</p>
<ul>
<li>C&oacute;digo de copia y pega para interntar salir del paso (Copy-Paste Programming y Spaghetti Code)</li>
<li>Arquitecturas sin definici&oacute;n porque no hay tiempo para acabarlas (Big Ball of Mud)</li>
<li>Uso de la primera soluci&oacute;n que tengamos a mano aunque no sea la m&aacute;s adecuada (Golden Hammer)</li>
<li>...</li>
</ul>
<p>Estoy seguro que muchos de los que est&aacute;is leyendo estas l&iacute;neas habr&eacute;is vivido alg&uacute;n proyecto de este tipo porque, para nuestra desgracia, es la forma "normal" en que muchas empresas de software gestionan sus proyectos. Este tipo de proyectos no s&oacute;lo acarrea sobrecostes para el cliente, que se quedar&aacute; con una aplicaci&oacute;n hecha con prisas y llena de errores, mala imagen de la empresa que la ha desarrollado. Adem&aacute;s, tendr&aacute; un alto precio para el equipo de desarrolladores ya que perder&aacute; a alguno de sus componentes porque se habr&aacute; "quemado" en el camino. Se podr&iacute;a decir que se trata de un fracaso en todos los aspectos.</p>
<h2>&iquest;C&oacute;mo evitar llegar a este punto?</h2>
<p>La soluci&oacute;n a estos antipatrones tiene que surgir de la implicaci&oacute;n de los desarrolladores desde las primeras fases de los proyectos. Incluso en las pre-ventas tendr&iacute;a que haber un experto en tecnolog&iacute;a para dar su opini&oacute;n sobre si lo que solicita el cliente es viable desde el punto de vista t&eacute;cnico y contando con las habilidades de los desarrolladores que se tiene en plantilla.</p>
<p>Una vez que ese experto diese el visto bueno, existen varias opciones para continuar:</p>
<ul>
<li>que un equipo peque&ntilde;o de desarrolladores monte un prototipo, y a partir de &eacute;ste fijar el dise&ntilde;o e implementaci&oacute;n y estimar la duraci&oacute;n del proyecto sobre ese prototipo.</li>
<li>utilizar SCRUM para hacer un desarrollo basado en entregables peri&oacute;dicos y con el cliente implicado desde el principio y dando feedback.</li>
</ul>
<p>Pero para poder llevar un proyecto a buen termino es necesario un buen EQUIPO de desarrolladores. Ese equipo tiene que estar equilibrado, cohesionado y debe poder trabajar en un buen ambiente. Con esto me refiero a que la carga de trabajo sea razonable y respetando los horarios de los trabajadores.</p>
<p>Tal vez las soluciones parezcan ut&oacute;picas o poco realistas, pero si la forma de hacerlo no sirve, habr&aacute; que probar otra. Como dijo una vez Albert Einstein: "Locura es hacer la misma cosa una y otra vez esperando obtener diferentes resultados".</p>
<p>Nota: No me gustar&iacute;a acabar el post sin mencionar <a href="http://jummp.wordpress.com/">el blog de jummp</a>, en el que, entre otras cosas, se habla mucho y muy bien sobre antipatrones. Os lo recomiendo :)</p>