---
ID: 77
post_title: 'Antipatrones: aprendiendo de los errores de otros (II) #bdc11'
author: pbousan
post_date: 2011-12-14 13:22:44
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-ii-bdc11/
published: true
---
<p>Hace unas semanas os traje <a href="http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-I">la primera</a> parte de la charla sobre antipatrones que di en la Barcelona Developers Conference, en la que definimos los antipatrones como una soluci&oacute;n a un problema que genera consecuencias negativas. Adem&aacute;s, vimos que se pueden agrupar en antipatrones:</p>
<ul>
<li>De desarrollo</li>
<li>De arquitectura (o de dise&ntilde;o)</li>
<li>De gesti&oacute;n</li>
</ul>
<p>En esta segunda parte hablaremos sobre los antipatrones de arquitectura de software.</p>
<p>La definici&oacute;n de la&nbsp; arquitectura de una aplicaci&oacute;n es posiblemente la m&aacute;s dif&iacute;cil de todas las decisiones que se tienen que tomar en un proyecto, ya que afectar&aacute; en gran medida al &eacute;xito o fracaso de la aplicaci&oacute;n. Una arquitectura que no abarque toda la problem&aacute;tica de una soluci&oacute;n de software es tan peligrosa como otra que sea muy compleja y dif&iacute;cil de desarrollar.</p>
<p>Muchas veces las decisiones de dise&ntilde;o se toman sin conocer partes de la soluci&oacute;n que se quiere desarrollar y con muy poco tiempo; pero eso ya lo veremos en el pr&oacute;ximo cap&iacute;tulo de esta serie, cuando hablemos de los antipatrones de gesti&oacute;n de proyectos, de momento vamos a centrarnos en algunos de los antipatrones m&aacute;s conocidos de dise&ntilde;o o arquitectura (no son los &uacute;nicos, ten&eacute;is una lista <a href="http://en.wikipedia.org/wiki/Antipattern">aqu&iacute;</a>).</p>
<p>&nbsp;</p>
<p><b>Big Ball of Mud (Gran bola de lodo)</b></p>
<p><img src="/wp-content/uploads/2012/09/ball_of_mud.jpg" alt="Big ball of mud" style="margin-right: 5px;" width="200" align="left" height="150" /></p>
<p>Describe un sistema que no tiene una estructura bien definida. Las responsabilidades y la informaci&oacute;n se encuentran esparcidas por los elementos, a veces est&aacute;n compartidas y otras repetidas. Adem&aacute;s, es com&uacute;n que existan clases que nadie sabe qu&eacute; hacen, pero que se mantienen en el c&oacute;digo "por si acaso".</p>
<p>Este tipo de no-arquitectura es muy com&uacute;n en proyectos que llevan muchos a&ntilde;os de desarrollo, en los que han intervenido gran n&uacute;mero de personas y que nunca han tenido un responsable que indique el camino a seguir.</p>
<p>Rodrigo Corral suele referirse a este antipatr&oacute;n como "Gran Bola de mierda", y afirma, muy acertadamente que sobre una bola de mierda no se puede a&ntilde;adir nada. Como mucho, podr&aacute;s hacer otra peque&ntilde;a bola de mierda al lado de la antigua y rezar para que funcione.</p>
<p>&nbsp;</p>
<p><b>Yet another (useless) layer (&iexcl;Y otra capa m&aacute;s!)</b></p>
<p>Consiste en agregar otra capa m&aacute;s a una librer&iacute;a o framework con la excusa de intentar reducir el acoplamiento, pero normalmente las capas que se a&ntilde;aden son innecesarias ya que lo &uacute;nico que hacer es servir de envoltorio: tienen llamadas a m&eacute;todos de objetos que est&aacute;n en otras capas. Tambi&eacute;n es conocida como c&oacute;digo lasa&ntilde;a o musaka (dependiendo de si lleva pasta o berenjenas :P).</p>
<p>Este antipatr&oacute;n suele estar asociado a la moda arquitect&oacute;nica del momento. Por ejemplo, desde la publicaci&oacute;n del libro <a href="http://msdn.microsoft.com/es-es/architecture/default.aspx">Gu&iacute;a de Arquitectura N-Capas DDD .NET 4</a> por parte de Microsoft se ha iniciado una pol&eacute;mica entre los que pretenden seguir la arquitectura planteada en el libro a rajatabla y los que saben que es &uacute;nicamente una referencia para aplicaciones complejas (que curiosamente es lo que pone en la introducci&oacute;n del propio libro).</p>
<p>&nbsp;</p>
<p><b>Reinventing the Wheel (Reinventar la rueda)</b></p>
<p><img src="/wp-content/uploads/2012/09/reinventar-la-rueda.jpg" alt="Reinventing_the_wheel" style="margin-right: 5px;" width="200" align="left" height="200" /></p>
<p>Consiste en intentar solucionar un problema conocido con una soluci&oacute;n "ad hoc", inventada y desarrollada por nosotros y sin tener en cuenta los patrones de dise&ntilde;o, arquitect&oacute;nicos ni de ning&uacute;n tipo. La causa principal suele ser el desconocimiento y la soberbia. No es extra&ntilde;o encontrar un proyecto con su propia soluci&oacute;n de loggin, su propio ORM o su propio serializador de JSON.</p>
<p>El principal problema de reinventar la rueda es que se rompe con los est&aacute;ndares y es muy dif&iacute;cil de mantener, ya que se cumple con la regla de "si es para m&iacute;, no hace falta que lo documente". Adem&aacute;s, como es una soluci&oacute;n para salir del paso, tampoco tendr&aacute; tests unitarios, con lo que el conocimiento sobre qu&eacute; hace y c&oacute;mo lo hace se suele ir con la persona que lo implement&oacute;.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><b>Golden Hammer (Martillo de oro)</b></p>
<p><img src="/wp-content/uploads/2012/09/Golden_Hammer.jpg" alt="Golden_Hammer" style="margin-right: 5px;" width="92" align="left" height="200" /></p>
<p>El nombre de este anitpatr&oacute;n viene de la frase: "Si todo lo que tienes es un martillo, todos tus problemas se convertir&aacute;n en clavos". Se trata de intentar utilizar nuestra soluci&oacute;n favorita para TODOS los problemas. Se puede aplicar como antipatr&oacute;n de desarrollo como de dise&ntilde;o.</p>
<p>Un ejemplo muy gr&aacute;fico ser&iacute;a el de intentar aplicar una arquitectura CQRS para hacer un blog. En este caso, se trata claramente de una arquitectura innecesariamente compleja para lo que queremos hacer.</p>
<p>Este antipatr&oacute;n suele producirse cuando se quieren anticipar requerimientos futuros, ya que el cliente de momento no los tiene decididos o no ha pensado en ellos.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>&iquest;Qu&eacute; consecuencias tienen?</h2>
<p>Durante un tiempo una arquitectura deficiente no tiene m&aacute;s consecuencias que hacer la aplicaci&oacute;n poco mantenible, pero, &iquest;qu&eacute; pasa cuando empiece a tener problemas?</p>
<ol>
<li>El equipo est&aacute; acostumbrado a trabajar mal, no sigue buenas pr&aacute;cticas ni mejoran el c&oacute;digo existente.</li>
<li>La aplicaci&oacute;n tiene un &iacute;ndice de mantenibilidad que tiende a infinito, cualquier cambio es dif&iacute;cil y suele llevar asociado la generaci&oacute;n de nuevos bugs.</li>
<li>Los clientes ven que la aplicaci&oacute;n no funciona como ellos quieren, adem&aacute;s, hay nuevos bugs y se tarda mucho en solucionarlos. La relaci&oacute;n con el cliente se enturbia.</li>
<li>Volvemos al punto 1, pero con m&aacute;s presi&oacute;n.</li>
</ol>
<p>Jurgen Appelo lo explica perfectamente en esta presentaci&oacute;n: <a href="http://www.slideshare.net/jurgenappelo/agile-management-complexity-thinking" target="_blank">Complexity Thinking</a>.</p>
<p>&nbsp;</p>
<h2>&iquest;C&oacute;mo se solucionan?</h2>
<p>Lo que tienen en com&uacute;n estos 4 antipatrones es que nos encontramos en un proyecto que tiene una arquitectura o un dise&ntilde;o que no le corresponde. Hay que tratar cada situaci&oacute;n de una manera individualizada y podemos afrontar los cambios de dos formas: hacerlo todo de nuevo o refactorizar lo que hay.</p>
<p>La opci&oacute;n de hacerlo todo de nuevo es f&aacute;cil, pero tiene el problema de que no se ver&aacute;n resultados hasta que el proyecto est&eacute; avanzado. Y mientras avancemos habr&aacute; que seguir d&aacute;ndole soporte a la aplicaci&oacute;n tal y como est&aacute;. Adem&aacute;s, como la nueva versi&oacute;n no funcione, como m&iacute;nimo, 10 veces mejor que la actual, seremos el hazmerre&iacute;r de la empresa.</p>
<p>Refactorizar sobre lo que hay es mucho m&aacute;s complicado que hacerlo todo de nuevo, pero tiene la ventaja que se puede hacer de manera progresiva, planteando plazos en los que se implantar&aacute;n las mejoras y aprendiendo de nuestros errores. Scrum puede ser una buena ayuda para esto. Lo importante es no intentar abarcar todos los cambios a la vez, sino de manera gradual y planeada: primero plantear una arquitectura, despu&eacute;s cambiar el acceso a datos, lo siguiente agrupar la l&oacute;gica de negocio, ... refactorizar tanto a nivel de c&oacute;digo como de estructura.</p>
<p>Pero afrontar estos cambios conlleva dos problemas a&ntilde;adidos: la presi&oacute;n y la resistencia al cambio. Tendremos una presi&oacute;n superior a seguir haciendo lo de siempre, ya que tendremos que sacar mejores resultados en menos tiempo. Adem&aacute;s, tendremos que enfrentarnos a la resistencia al cambio dentro del propio equipo y de la organizaci&oacute;n. No es f&aacute;cil hacer que una organizaci&oacute;n trabaje de una forma diferente a la que est&aacute; acostumbra, pero sobre eso hablaremos m&aacute;s adelante, cuando tratemos los antipatrones de gesti&oacute;n de proyectos.</p>