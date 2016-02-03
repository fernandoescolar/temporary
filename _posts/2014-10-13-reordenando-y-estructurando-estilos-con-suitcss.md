---
ID: 1243
post_title: >
  Reordenando y estructurando estilos con
  SuitCSS
author: Jhon Marmolejo
post_date: 2014-10-13 11:29:49
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/reordenando-y-estructurando-estilos-con-suitcss/
published: true
---
<span style="line-height: 1.5em">Antes que nada me presento, me llamo Jhon Marmolejo y llevo en el mundo de desarrollo de software usando tecnología .NET poco más de 8 años. En los últimos años he ido orientando mi carrera a la parte de FrontEnd pero sin dejar de lado la parte de BackEnd. Agradezco la oportunidad que me ha dado el equipo de programandoNET de poder colaborar en el blog. </span>

<span style="line-height: 1.5em">Uno de los temas que más me fastidia de la parte FrontEnd de las aplicaciones, es la falta de orden y estándar para la nomenclatura y acoplamiento que hay en los archivos CSS de una aplicación. Entre las cosas que me molestan podemos consideras las siguientes:</span>
<ul>
	<li><span style="line-height: 1.5em">Aplicaciones con infinidad de archivos CSS o con una cantidad gigantesca de líneas de código(muchas de estas ya existentes en selectores que hacen lo mismo).</span></li>
</ul>
<a href="http://www.dotnetodology.com/wp-content/uploads/2014/10/estilo.png"><img class="size-full wp-image-1246 aligncenter" alt="estilo" src="http://www.dotnetodology.com/wp-content/uploads/2014/10/estilo.png" width="229" height="272" /></a>
<ul>
	<li>Archivos css que se machacan entre ellos ya sea por usar selectores de elementos o porque los selectores en un archivo CSS ya existen en otros archivo CSS. Veamos un ejemplo.</li>
</ul>
<br />
Tenemos dos archivos css:
<br />
<strong>Estilo1.css</strong>
<pre class="brush: css">
.label {
    font-family: 'Monotype Corsiva';
    color:red;
}
</pre>
<br />
<strong>Estilo2.css</strong>
<pre class="brush: css">
.label {
    font-family:'Comic Sans MS';
}
</pre>
<br />
Y un archivo html
<br />
<pre class="brush: html">
    <div id="header">
        <span class="label">Mi cabecera</span>
    </div>
    <div id="mainBody">
        <span class="label">Nombre: </span>
        <br />
        <span class="label">Dirección:</span>
        <br />
        <span class="label">Teléfono:</span>
    </div>
</pre>
<br />
Ahora, si a este archivo html le referenciamos el archivo Estilo1.css, el resultado es el siguiente:
<br />
<a href="http://www.dotnetodology.com/wp-content/uploads/2014/10/img12.png"><img src="http://www.dotnetodology.com/wp-content/uploads/2014/10/img12-300x104.png" alt="img1" width="300" height="104" class="aligncenter size-medium wp-image-1276" /></a>
<br />
Y si sólo referenciamos el segundo css Estilo2, el resultado sería el siguiente:
<br />
<a href="http://www.dotnetodology.com/wp-content/uploads/2014/10/img21.png"><img src="http://www.dotnetodology.com/wp-content/uploads/2014/10/img21-300x102.png" alt="img2" width="300" height="102" class="aligncenter size-medium wp-image-1277" /></a>
<br />
¿Y que pasaría si referenciamos estos dos archivos a la vez? Estilo1.css y Estilo2.css en ese mismo orden. El resultado sería el siguiente:
<br />
<a href="http://www.dotnetodology.com/wp-content/uploads/2014/10/img3.png"><img src="http://www.dotnetodology.com/wp-content/uploads/2014/10/img3-300x100.png" alt="img3" width="300" height="100" class="aligncenter size-medium wp-image-1279" /></a>
<br />
Como puedes ver en la imagen, el resultado es una mezcla de los archivos CSS. Esto puede generarte dolores de cabeza al no entender porque el estilo de tu página ha cambiado de la noche a la mañana, y créeme, pasa!! Muchas veces el equipo de desarrollo crea selectores de clase repetidos en diferentes archivos css porque no sabia que ya existía una clase así o porque simplemente no se dignó a buscar antes. 
<br />
Felizmente existe un estándar para la nomenclatura de estilos que me parece muy interesante y esta teniendo acogida por parte de muchos desarrolladores. Se trata de <a href="http://suitcss.github.io/" target="_blank">SuitCSS</a>, un proyecto de GitHub que aparte de ser un preprocesador de estilos pretende establecer un estándar para nombrar a nuestros selectores de clases en nuestras hojas de estilos. En este artículo nos centraremos en la parte del estándar que define SuitCSS, dejando el tema del preprocesado para otros artículos en el que también hablaremos de otros preprocesadores conocidos como Sass o Less.
<br />
SuitCSS pretende establecer un estándar para la nomenclatura de nuestros selectores de clase de dos maneras:

<strong>
.namespace-ComponentName-descendentName--modifierName.is-stateName {...}
.u-utilityName {...}
</strong>
<br />
<br />
<br />
Empecemos explicando el primer caso:
<br />
<strong><u>.namespace-ComponentName-descendentName--modifierName.is-stateName {...}</u></strong>
<br />
<br />
<b><span style="color: #0b5394">.namespace:&nbsp;</span></b>SuitCSS pretende que empecemos nombrando nuestras clases con un namespace. Aunque este parámetro es <b>opcional</b>, se recomienda utilizarlo para tener que evitar conflictos con otros archivos css. Esto debe ser escrito en Camel Case.<br />
<br /></div>
<div>
<span style="color: #0b5394;font-weight: bold">-ComponentName: </span>Es el nivel más alto de nuestro componentes. Si nos guiamos a la nueva estructura que propone HTML5, acá se podría declarar los elementos header, section, article, footer, etc. Esto debe ser escrito en Pascal Case.<br />
<br />
<b><span style="font-size: x-small">Archivo CSS usando el namespace y ComponentName juntos</span></b><pre class="brush: css">
.main-Header{...}
.main-Footer{...}

.popup-Header{...}
.popup-Footer{...}
</pre>
</div>
<b><span style="font-size: x-small">Página HTML</span></b>
<pre class="brush: html">
<header class="main-Header">
   ...
   ...
</header>
<footer class="main-Footer">
   ...
   ...
</footer>
</pre>
<br />
<span style="color: #0b5394;font-weight: bold">-descendantName: </span>Es la parte del componente al cual aplicaremos el estilo. Por ejemplo podría ser un &lt;figure&gt; que esta dentro de un &lt;header&gt;. Esto debe ser escrito en Camel Case.<br />
<br />
<b><span style="font-size: x-small">Archivo CSS&nbsp;</span></b>
<pre class="brush: css">
.main-Header{...}
.main-Header-figure {....}
</pre>
<b><span style="font-size: x-small">Página HTML</span></b>
<pre class="brush: html">
<header class="main-Header">   
   <figure class="main-Header-figure">
      ...
      ...
   </figure>
</header>
</pre>
<br />
<span style="color: #0b5394;font-weight: bold">--modifierName: </span>Esta clase nos permite modificar el elemento base de una cierta forma, un ejemplo sería un estilo determinado a un botón por defecto, o los campos de texto que son obligatorios de llenar. Esto debe ser escrito en Camel Case.<br /><br />
<b><span style="font-size: x-small">Archivo CSS&nbsp;</span></b>
<br />
<pre class="brush: css">
.main-Header{...}
.main-Header-figure {....}
.main-Header-button {....}
.main-Header-button--default {....}
</pre>
<b><span style="font-size: x-small">Página HTML</span></b>
<pre class="brush: html">
<header class="main-Header">   
   <figure class="main-Header-figure">
      ...
      ...
   </figure>
   <button class="main-Header-button--default" id="btnAceptar" value="Aceptar"></button>
   <button class="main-Header-button" id="btnCancelar" value="Cancelar"></button>
</header>
</pre>
<br />
<span style="color: #0b5394;font-weight: bold">.is-stateName:&nbsp;</span>Esta clase&nbsp;nos permite indicar un estado que puede tener un determinado elemento, como habilitado, deshabilitado, seleccionado, etc. Esta clase se escribe con un punto al inicio, lo cual indica que es una clase aparte y que puede ser reutilizada por diferentes elementos,<b> pero es recomendable</b> tenerlo dentro del mismo ámbito del componente por temas de orden y para facilitar luego el uso de preprocesadores. Esta clase se debe escribir en Camel Case también.<br />
<br />
<b><span style="font-size: x-small">Archivo CSS&nbsp;</span></b>
<pre class="brush: css">
.main-Header{...}
.main-Header-figure {....}
.main-Header-button {....}
.main-Header-button--default {....}
.main-Header-button--default.disabled {....}
.main-Header-button--default.enabled {....}
</pre>
<b><span style="font-size: x-small">Página HTML</span></b>
<pre class="brush: html">
<header class="main-Header">   
   <figure class="main-Header-figure">
      ...
      ...
   </figure>
   <button class="main-Header-button--default disabled" id="btnAceptar" value="Aceptar"></button>
   <button class="main-Header-button" id="btnCancelar" value="Cancelar"></button>
</header>
</pre>
<br />
Por último hablaremos del segundo caso:<br />
<br />
<br />
<strong><u>.u-utilityName</code><span>&nbsp;{...}</u></strong><br />
<br />
<br />
<span style="color: #0b5394;font-weight: bold">.u-utilityName: </span>Esta clase está pensada para crear estilos globales. El nombre de la clase debe empezar con u seguido de un guión, lo cual nos permite indicar que será un utilitario capaz de aplicar estilos a muchos elementos. Nos puede ser util para establecer estilos para cosas comunes en toda la aplicación, como los tag de title, h1, h2 o para indicar un tipo de posicionamiento o alineación. La idea es que sea una clase que contengan estilos comunes en la aplicación. Debe ser escrito también en Camel Case.<br />
<br />
<b><span style="font-size: x-small">Archivo CSS</span></b>
<pre class="brush: css">
.main-Header{...}
.main-Header-figure {....}
.main-Header-button {....}
.main-Header-button--default {....}
.main-Header-button--default.disabled {....}
.main-Header-button--default.enabled {....}
.u-title {...}
.u-buttons {...}
</pre>
<b><span style="font-size: x-small">Página HTML</span></b>
<pre class="brush: html">
<header class="main-Header">   
   <title class="u-title">Hola</title>
   <figure class="main-Header-figure">
      ...
      ...
   </figure>
   <button class="main-Header-button--default disabled u-buttons" id="btnAceptar" value="Aceptar"></button>
   <button class="main-Header-button  u-buttons" id="btnCancelar" value="Cancelar"></button>
</header>
</pre>
<br />
<br />
Como podemos ver SuitCSS viene a poner orden en la manera en como declarar las clases de estilos en nuestras páginas html. Hace uso del selector por clases y es una manera ordenada y clara de ver los documentos. Sería genial que los desarrolladores empiecen a usar este tipo de estándar de nomenclatura para que el mantenimiento de estilos esté más controlado. Espero les sirva, hasta la próxima :)<br />
<br /></div>