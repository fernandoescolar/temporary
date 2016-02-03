---
ID: 53
post_title: 'Antipatrones: aprendiendo de los errores de otros (I) #bdc11'
author: pbousan
post_date: 2011-11-30 11:30:23
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-i/
published: true
---
Después la charla que hice sobre antipatrones en la Barcelona Developers Conference, en la que quedaron muchos temas por hablar, me he decidido a escribir una serie de posts sobre el tema.

Empezaremos por definir los antipatrones, enfrentándolos con los patrones de diseño. También mostraremos su utilidad y algunos ejemplos.

&nbsp;
<h2>Patrones vs. Antipatrones</h2>
Normalmente cuando hablas de antipatrones la gente los asocia con los patrones de diseño, pero no están del todo relacionados, veamos porqué:

Un patrón de diseño es una solución reusable a problemas comunes de diseño de software. No se trata de un diseño finalizado que pueda ser plasmado directamente en código, sino que es la descripción o plantilla de cómo solucionar un problema que puede ser utilizada en muchas situaciones diferentes.

Por su parte, un antipatrón describe una solución a un problema que genera consecuencias negativas. Suele ser el resultado de un manager o un desarrollador que no conoce nada mejor, que no tiene suficiente conocimiento o experiencia solucionando un problema o que ha aplicado un patrón perfectamente válido en un contexto erróneo.

La diferencia se explica mucho mejor con un ejemplo:

Un patrón sería el Factory method pattern, que dice: Define una interface para crear un objeto, pero permite a las subclases que decidan qué clase instanciar. Sólo dice qué tiene que hacerse, pero el cómo lo deja en manos de quien lo vaya a implementar.

<img src="/wp-content/uploads/2012/09/300px-FactoryMethod.svg_.png" alt="FactoryMethodPattern" width="200" height="118" />

Un antipatrón sería la "God Class": un objeto que controla todos los demás objetos del sistema y ha crecido más allá de toda lógica para convertirse en la clase que hace de todo. Aquí la clave está en el “ha crecido más allá de toda lógica”, esto quiere decir que tal vez en un principio la clase estaba justificada y cumplía su objetivo, pero se ha deteriorado de tal forma que ha convertido el sistema en inmantenible.

&nbsp;
<h2>Los Antipatrones no salvarán tu vida, pero la harán más fácil</h2>
Por muy poco conocimiento que tengamos de programación nos daremos cuenta que una God Class es una mala idea, pero, ¿cómo llega alguien a hacer algo así? En el libro <a href="http://www.amazon.com/AntiPatterns-Refactoring-Software-Architectures-Projects/dp/0471197130" target="_blank">"<em>Anti-patterns: Refactoring software, Architectures and Projects in Crisis</em>"</a> se identifican 7 causas principales:

<img src="/wp-content/uploads/2012/09/antipatterns.jpg" alt="Antipatterns" width="120" height="200" />
<ul>
	<li>Prisa</li>
	<li>Apatía</li>
	<li>Estrechez de miras</li>
	<li>Pereza</li>
	<li>Avaricia</li>
	<li>Ignorancia</li>
	<li>Soberbia</li>
</ul>
Se podría decir que estos son los 7 pecados del desarrollo del software y tarde o temprano nos los encontraremos, en el equipo en el que trabajamos o en nosotros mismos. Por eso es importante conocer los antipatrones, porque el primer paso para solucionar un problema es identificarlo y eso es justamente lo que hacen los antipatrones, identificar malas prácticas en el desarrollo, la arquitectura, la gestión de proyectos de software e incluso en cómo se organizan las empresas.

Pero, ¿para qué quiero aprender cosas que están mal?

Principalmente para tratar de evitarlas. Los antipatrones exponen la verdad sobre la industria del software: está plagada de defectos, indefiniciones, contradiciones y falsas promesas. Los proyectos son caóticos, impredecibles y dañinos para las carreras de quienes participan en ellos, por lo que es mejor identificar los posibles problemas antes que lleguen a ser imposibles de resolver. Porque lo mejor de los antipatrones es que no se quedan en definir un problema, sino que muestran soluciones a estos problemas.

&nbsp;
<h2>Algunos ejemplos</h2>
Es muy difícil abarcar todos los antipatrones que se han documentado (que no quiere decir que son todos los que existen), como muestra en estos enlaces podréis encontrar listados más o menos completos de antipatrones detectados:

<a href="http://c2.com/cgi/wiki?AntiPatternsCatalog" target="_blank">Antipatterns Catalog en c2.com</a>
<a href="http://en.wikipedia.org/wiki/Antipattern" target="_blank">Antipatterns en wikipedia</a>

Pero vayamos con algunos ejemplos de antipatrones de desarrollo y en próximos posts hablaremos de los de arquitectura y de organización.

Supongamos que nos acaba de contratar una gran empresa para formar parte de un equipo en el que se hace el mantenimiento de las aplicaciones internas. El equipo está formado por seniors (más por años de trabajo que por conocimiento) que llevan gran parte de su carrera en la empresa, utilizando las mismas tecnologías y con poca formación. ¿Qué nos espera al ver el código?

<strong>Spaghetti Code (o spaghetti con albóndigas)</strong>
El código no tiene una estructura de clases definidas sino que se van haciendo las que se le ocurre a cada programador cuando las necesita. Esto deriva en código repetido, poco cohesionado y normalmente muy acoplado.

<strong>Cut-And-Paste Programming</strong>
Mucha gente es lo que entiende cuando hablan de reutilizar código: coger un trozo de código que funciona (el acceso a datos, control de excepciones, ...) y copiarlo donde lo necesites. Cuando se trata de aplicaciones de escritorio o web se llegan a copiar incluso la interfaz completa y ya se quitará lo que sobre.

Tendremos código muy difícil de mantener (si algo falla o se modifica, el mismo cambio hay que hacerlo en muchos sitios diferentes) y de testear (porque realmente funciona, pero suele hacer mucho más de lo que debería).

&nbsp;
<h2>¿Qué solución hay para esto?</h2>
Estos son 2 casos muy claros de antipatrones que se deben más que nada a la ignorancia y/o la pereza, normalmente combinados con una buena dosis de prisa. La solución no es fácil, ya que consiste en “obligar” al equipo a trabajar de una forma más correcta, siguiendo los principios de la <a href="http://en.wikipedia.org/wiki/Object-oriented_programming" target="_blank">OOP</a>, los <a href="http://en.wikipedia.org/wiki/Solid_%28object-oriented_design%29" target="_blank">principios SOLID</a> y otros como <a href="http://en.wikipedia.org/wiki/Don%27t_repeat_yourself" target="_blank">DRY</a> y <a href="http://en.wikipedia.org/wiki/YAGNI" target="_blank">YANGI</a>. Algo más avanzado sería utilizar TDD (Fernando nos explica muy bien sus ventajas en <a href="http://www.dotnetodology.com/tdd-en-entornos-net-bdc11" target="_blank">este post</a>).

Y por supuesto, mucha refactorización:

<img src="/wp-content/uploads/2012/09/keep-calm-and-refactor-your-code.jpg" alt="KeepCalmAndRefactor" width="172" height="200" />

Continúa con <a href="http://www.dotnetodology.com/antipatrones-aprendiendo-de-los-errores-de-otros-ii-bdc11">la segunda parte</a> de este artículo.