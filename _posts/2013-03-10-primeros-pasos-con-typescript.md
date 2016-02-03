---
ID: 898
post_title: Primeros pasos con TypeScript
author: pbousan
post_date: 2013-03-10 20:07:36
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/primeros-pasos-con-typescript/
published: true
---
JavaScript ha pasado en los últimos años de ser un lenguaje que únicamente se utilizaba para añadir funcionalidad gráfica y validaciones a las webs, a ser usado para fines que hasta ahora no nos podríamos imaginar: se pueden hacer aplicaciones para Windows 8 con <a href="http://msdn.microsoft.com/es-es/library/windows/apps/br211385.aspx" target="_blank">WinJS</a>, hacer aplicaciones de servidor con <a href="http://nodejs.org/" target="_blank">Node.js</a>, controlar una Kinect con <a href="http://kinect.childnodes.com/" target="_blank">KinectJS</a>, hacer aplicaciones para casi cualquier smartphone con <a href="http://phonegap.com/" target="_blank">PhoneGap</a>, programar un Arduino con <a href="http://www.schillmania.com/projects/arduino-js/" target="_blank">arduino.js</a>, …

Este aumento en su utilización ha provocado que casi cualquier programador (tanto de front-end como de back-end) tenga en algún momento la necesidad de usar JavaScript en aplicaciones cada vez más grandes y complejas. Para ello se pueden utilizar las miles de librerías que existen actualmente y que proporcionan soluciones a problemas muy concretos (como <a href="http://harvesthq.github.com/chosen/" target="_blank">Chosen.js</a>) o que nos permiten utilizar patrones de una forma muy sencilla (como <a href="http://knockoutjs.com/" target="_blank">Knockout</a> para MVVM o <a href="http://backbonejs.org/" target="_blank">Backbone</a> para MVC).

Para un desarrollador que esté acostumbrado a utilizar lenguajes orientados a objetos, como C# o Java, le puede resultar difícil abandonar las técnicas aprendidas: herencia, polimorfismo, patrones de diseño, ... y adaptarse a JavaScript. Es entonces cuando se nos plantean dos opciones: adaptarnos a JavaScript o que JavaScript se adapte a nosotros.

Si se elige el primer camino, existen fantásticos documentos, como este de Addy Osmani: <a href="http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/" target="_blank">Essential JS Design Patterns</a>, con el que podremos aprender a utilizar nuestra experiencia en OOP y patrones para así hacer un código Javascript más mantenible y reutilizable.

Para la segunda opción, tenemos la posibilidad de utilizar lenguajes como <a href="http://coffeescript.org/" target="_blank">CoffeScritp</a>, <a href="http://www.dartlang.org/" target="_blank">Dart</a> o el recientemente lanzado <a href="http://www.typescriptlang.org/" target="_blank">TypeScript</a>, sobre el que hablaremos en este artículo, que generarán JavaScript a partir de lenguajes orientados a objetos.

&nbsp;
<h2>¿Qué aporta TypeScript?</h2>
TypeScript es fruto del trabajo de <a href="http://en.wikipedia.org/wiki/Anders_Hejlsberg" target="_blank">Anders Hejlsberg</a>, uno de los creadores de C# (además de padre de Turbo Pascal y arquitecto jefe de Delphi) y pretende ayudar a los equipos de programación a definir interfaces entre componentes de software y reducir los conflictos de nomenclatura mediante la organización del código en módulos que se pueden cargar de forma dinámica.

Pero a diferencia de Coffescript o Dart, TypeScript es un superconjunto de JavaScript que genera JavaScript.

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/Typescript.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; margin-left: 0px; display: inline; padding-right: 0px; margin-right: 0px; border-width: 0px;" title="Typescript" alt="Typescript" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/Typescript_thumb.png" width="310" height="255" border="0" /></a>

Por tanto, si ya conocemos JavaScript, no tendremos ningún problema para utilizar TypeScript. La curva de aprendizaje de este nuevo lenguaje será realmente suave, pudiendo conseguir grandes resultados desde el principio. Además, al ser JavaScript, TypeScript nos permite seguir utilizando todas las librerías que conocemos hasta ahora (JQuery, Backbone, Knockout, ...)

Hay que destacar también que TypeScript es un proyecto Open Source, y se puede descargar su código fuente (además de varios ejemplos) desde aquí: <a title="http://typescript.codeplex.com/" href="http://typescript.codeplex.com/">http://typescript.codeplex.com/</a>Actualmente se encuentra en la versión 0.8.3, y como podéis ver en este <a title="TypeScript Roadmap" href="http://typescript.codeplex.com/wikipage?title=Roadmap&amp;referringTitle=Home" target="_blank">roadmap</a> en la versión final (1.0) estará completamente alineado con la versión 6 de ECMAScript.

&nbsp;
<h2>SHOW ME THE CODE</h2>
Para utilizar TypeScript tenemos dos opciones:

- Instalar el paquete de TypeScript para Node.js y un IDE como Sublime Text, Vim o Emacs. En <a title="Aplicaciones NodeJS con TypeScript" href="http://www.nodehispano.com/2013/04/creando-aplicaciones-node-js-con-typescript-parte-1-nodejs/" target="_blank">este artículo</a> podemos ver cómo hacerlo con Sublime Text.

o

- Instalar el <a href="http://www.microsoft.com/en-us/download/details.aspx?id=34790" target="_blank">plugin para Visual Studio 2012</a>  que sirve para cualquiera de sus <a href="http://www.microsoft.com/visualstudio/esn/downloads" target="_blank">versiones</a>, incluso las Express.

En este artículo usaremos la segunda opción, dejando la primera para un futuro artículo en el que veremos características más avanzadas del lenguaje.

&nbsp;
<h4>Hola Mundo!!</h4>
Una vez instalado el plugin podemos ver que tenemos una nueva opción en las plantillas de proyecto:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts2.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts2" alt="ts2" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts2_thumb.png" width="647" height="396" border="0" /></a>

&nbsp;

Cuando la seleccionamos, se genera un proyecto que ya contiene algunos archivos con código Typescript.

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts3.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts3" alt="ts3" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts3_thumb.png" width="244" height="222" border="0" /></a>

Podemos observar que existe un fichero con extensión .ts (TypeScript), del que cuelga otro con extensión .js (JavaScript). Esto se debe a que nuestro código TypeScript genera código JavaScript, que será el que en última instancia utilizaremos en nuestras aplicaciones, ya que a día de hoy no existe ningún navegador o motor que interprete TypeScript nativamente.

Con el plugin instalado, cuando abrimos el fichero app.ts se nos abre automáticamente su fichero JavaScript relacionado. Por ejemplo, si ponemos un <em>alert</em> para mostrar el texto “Hola Mundo!!” cuando se ejecute el evento <em>onload</em> del objeto <em>window</em>:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts4.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts4" alt="ts4" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts4_thumb.png" width="587" height="140" border="0" /></a>

Vemos que el código generado (derecha) es exactamente igual que el que hemos escrito (izquierda). Esto es porque, como comentamos anteriormente, TypeScript es JavaScript. Podemos utilizar la sintaxis que ya conocemos para la mayoría de nuestro código. Y utilizar las novedades de TypeScript sólo cuando las necesitemos realmente.

&nbsp;
<h4>Clases y herencia</h4>
Uno de los mayores aportes de TypeScript es su facilidad para declarar clases. Además, nos permite generar un código homogéneo para toda la aplicación, evitando así la mezcla de alguna de las <a href="http://www.phpied.com/3-ways-to-define-a-javascript-class/" target="_blank">3 formas de declarar clases</a> que existen en Javascript.

Por ejemplo, el siguiente código definimos un usuario de nuestra aplicación. Como vemos, es una clase muy simple donde declaramos dos propiedades y un método.
<pre class="csharpcode"><span class="kwrd">class</span> User {
    name: <span class="kwrd">string</span>;
    age: number;

    constructor () {}

    play(song: <span class="kwrd">string</span>) {
        console.log(<span class="str">'User: '</span> + <span class="kwrd">this</span>.name + <span class="str">' plays song: '</span> + song);
    }
}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

El anterior código en TypeScript genera el siguiente en JavaScript:
<pre class="csharpcode"><span class="kwrd">var</span> User = (<span class="kwrd">function</span> () {
    <span class="kwrd">function</span> User() {
    }
    User.prototype.play = <span class="kwrd">function</span> (song) {
        console.log(<span class="str">'User: '</span> + <span class="kwrd">this</span>.name + <span class="str">' plays song: '</span> + song);
    };
    <span class="kwrd">return</span> User;
})();</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

Podemos comprobar que es un muy buen código JavaScript. Veamos cómo podemos instanciar un objeto de nuestra clase User:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts5.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts5" alt="ts5" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts5_thumb.png" width="386" height="195" border="0" /></a>

El Intellisense de Visual Studio ya nos detecta que existe una clase User y nos muestra sus métodos y propiedades:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts6.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts6" alt="ts6" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts6_thumb.png" width="244" height="140" border="0" /></a>

Además, al definir el tipo de cada propiedad, nos avisará en caso cuando no asignemos el tipo adecuado, aquí el tipado estático en TypeScript:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts7.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts7" alt="ts7" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts7_thumb.png" width="357" height="107" border="0" /></a>

Ahora vayamos con la herencia. Para heredar de nuestra clase User, simplemente definimos otra clase que la extienda:
<pre class="csharpcode"><span class="kwrd">class</span> RegisteredUser extends User {
    play(song: <span class="kwrd">string</span>) { 
        super.play(song);
        <span class="kwrd">this</span>.AddPoints(10);
    }

    <span class="kwrd">private</span> AddPoints(<span class="kwrd">value</span>: number) { 
        console.log(<span class="str">'User: '</span> + <span class="kwrd">this</span>.name + <span class="str">' obtains '</span> + <span class="kwrd">value</span>.toString() + <span class="str">' points.'</span>);
    }
}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

Esta nueva clase <em>RegisteredUser</em>, además ejecuta el método play() a través de una llamada a su clase padre: super.play(song); y añade la funcionalidad de llamar a un método que es exclusivo de esta subclase: AddPoints(). Podemos observar que a este método le hemos añadido el modificador <strong>private</strong>, lo que provoca que no pueda ser llamado desde fuera de la propia clase:

&nbsp;

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts8.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="ts8" alt="ts8" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/ts8_thumb.png" width="479" height="123" border="0" /></a>

Esta es otra de las novedades de TypeScript, permite definir el alcance de los métodos y propiedades de una clase. Facilitando así que sólo expongamos los elementos de una clase que nos interesen.

&nbsp;
<h4>Interfaces</h4>
TypeScript permite declarar interfaces para definir el contrato de las clases que vamos a utilizar, abstrayéndonos de su implementación. Estas interfaces no tienen ningún reflejo en el código compilado en JavaScript, ya que no es soportado por el lenguaje.

Un ejemplo muy típico es el de una clase Logger que almacenará el log de la aplicación. De de momento no sabemos cómo lo vamos a utilizar, por ejemplo, podemos mostrar un mensaje con un alert o por consola. Pero sí sabemos que tendrá un método que escriba en algún sitio. Con esta información podemos definir la interface ILogger, que tendrá un método write, y ya nos ocuparemos de la implementación.

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;
<pre class="csharpcode"><span class="kwrd">interface</span> ILogger { 
    write: (msg: <span class="kwrd">string</span>) =&gt; <span class="kwrd">void</span>;
}

<span class="kwrd">class</span> Logger implements ILogger {}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

Cuando intentemos que se genere el código JavaScript, se producirá un error de compilación ya que la clase no implementa el método write. Veamos un par de clases que sí implementan la interface:

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;
<pre class="csharpcode"><span class="kwrd">interface</span> ILogger { 
    write: (msg: <span class="kwrd">string</span>) =&gt; <span class="kwrd">void</span>;
}

<span class="kwrd">class</span> ConsoleLogger implements ILogger {
        write(msg) { console.log(msg); }
 }

<span class="kwrd">class</span> AlertLogger implements ILogger { 
    write(msg) { alert(msg); }
}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

Y ahora otra forma de implementar el constructor para que reciba un parámetro que decida qué tipo de <em>Logger</em> vamos a utilizar:

&nbsp;
<pre class="csharpcode">var LoggerMode = {
    Console : 1,
    Alert : 2
}

<span class="kwrd">interface</span> ILogger { 
    write: (msg: <span class="kwrd">string</span>) =&gt; <span class="kwrd">void</span>;
}

<span class="kwrd">class</span> Logger implements ILogger {
    <span class="kwrd">private</span> writer: any;

    constructor (<span class="kwrd">public</span> mode: number = LoggerMode.Console) { 
        <span class="kwrd">switch</span> (<span class="kwrd">this</span>.mode) { 
            <span class="kwrd">case</span> LoggerMode.Console:
                <span class="kwrd">this</span>.writer = (msg: <span class="kwrd">string</span>) =&gt; console.log(msg);
                <span class="kwrd">break</span>;

            <span class="kwrd">case</span> LoggerMode.Alert:
                <span class="kwrd">this</span>.writer = (msg: <span class="kwrd">string</span>) =&gt; alert(msg);
        }
    }

    write(msg) { <span class="kwrd">this</span>.writer(msg); }
 }

window.onload = () =&gt; {
    var logger = <span class="kwrd">new</span> Logger(LoggerMode.Alert);
    logger.write(<span class="str">"Hola Mundo!"</span>);
};</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;
<h4>Módulos</h4>
El código que hemos hecho hasta ahora está todo en el mismo fichero. De momento no nos hemos preocupado de la mantenibilidad, pero cuando el proyecto crece y crean muchas clases, y éstas son desarrolladas por diferentes personas, se hace imprescindible separar las declaraciones, para ello utilizaremos los módulos.

&nbsp;

<strong>utils.ts</strong> -&gt; Como queremos utilizar la clase <em>Logger</em> en diferentes puntos de nuestro código necesitamos que sea visible fuera de este fichero. Para ello, expondremos lo que consideremos necesario, como puede ser el "enumerado"  <em>LoggerMode</em>, la interface <em>ILogger</em> y la clase <em>Logger</em>. Sólo se expondrán los elementos que se indiquen explícitamente con la palabra <strong>export</strong>.
<pre class="csharpcode">module App.Utils { 

  export  var LoggerMode = {
        Console : 1,
        Alert : 2
    }

     export <span class="kwrd">interface</span> ILogger { 
        write: (msg: <span class="kwrd">string</span>) =&gt; <span class="kwrd">void</span>;
    }

    export <span class="kwrd">class</span> Logger implements ILogger {
        <span class="kwrd">private</span> writer: any;

        constructor (<span class="kwrd">public</span> mode: number = LoggerMode.Console) { 
            <span class="kwrd">switch</span> (<span class="kwrd">this</span>.mode) { 
                <span class="kwrd">case</span> LoggerMode.Console:
                    <span class="kwrd">this</span>.writer = (msg: <span class="kwrd">string</span>) =&gt; console.log(msg);
                    <span class="kwrd">break</span>;

                <span class="kwrd">case</span> LoggerMode.Alert:
                    <span class="kwrd">this</span>.writer = (msg: <span class="kwrd">string</span>) =&gt; alert(msg);
            }
        }

        write(msg) { <span class="kwrd">this</span>.writer(msg); }
     }
}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

<strong>user.ts</strong> -&gt; Utilizamos la clase Logger. Vemos como en la primera línea le indicamos que existe una referencia al fichero utils.ts y con ello podemos crear una instancia de la clase Logger igual que si lo tenemos definido en el mismo fichero.

&nbsp;
<pre class="csharpcode"><span class="rem">/// &lt;reference path="utils.ts" /&gt;</span>

module App.Management { 
    export <span class="kwrd">class</span> User {
        <span class="kwrd">private</span> logger: App.Utils.ILogger;

        constructor (<span class="kwrd">public</span> name : <span class="kwrd">string</span>, <span class="kwrd">public</span> age: number) {
            <span class="kwrd">this</span>.logger = <span class="kwrd">new</span> App.Utils.Logger(App.Utils.LoggerMode.Alert);
        }

        play(song: <span class="kwrd">string</span>) {
            <span class="kwrd">this</span>.logger.write(<span class="str">'User: '</span> + <span class="kwrd">this</span>.name + <span class="str">' plays song: '</span> + song);
        }
    }
}</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>&nbsp;

<strong>app.ts</strong> -&gt; Es nuestro punto de arranque, y hace referencia a user.ts, pero como vemos, no tenemos por ningún sitio referencia a la clase <em>Logger</em>, hemos conseguido desacoplar las clases y que cada una se encargue de gestionar sus propias referencias.
<pre class="csharpcode"><span class="rem">/// &lt;reference path="user.ts" /&gt;</span>

window.onload = () =&gt; {
    var user = <span class="kwrd">new</span> App.Management.User(<span class="str">"Pablo"</span>, 33);
    user.play(<span class="str">"Welcome to the Jungle"</span>);
};</pre>
&nbsp;

<style type="text/css"><!--
.csharpcode, .csharpcode pre { font-size: small; color: black; font-family: consolas, "Courier New", courier, monospace; background-color: #ffffff; /*white-space: pre;*/ } .csharpcode pre { margin: 0em; } .csharpcode .rem { color: #008000; } .csharpcode .kwrd { color: #0000ff; } .csharpcode .str { color: #006080; } .csharpcode .op { color: #0000c0; } .csharpcode .preproc { color: #cc6633; } .csharpcode .asp { background-color: #ffff00; } .csharpcode .html { color: #800000; } .csharpcode .attr { color: #ff0000; } .csharpcode .alt { background-color: #f4f4f4; width: 100%; margin: 0em; } .csharpcode .lnum { color: #606060; }
--></style>En próximos artículos veremos cómo utilizar <a title="RequireJS" href="http://requirejs.org/" target="_blank">require.js</a> para que la carga de estos módulos sea dinámica, consiguiendo cargar los módulos cuando sea necesario.
<h2></h2>
<h2>Resumiendo</h2>
Cómo hemos visto en estos ejemplos básicos, TypeScript proporciona…

- Código más homogéneo y mantenible
- Comprobación estática de tipos
- OOP: clases, herencia
- Interfaces
- Módulos

&nbsp;

Tenéis disponibles todos los ejemplos de este artículo en la siguiente dirección: <a title="TypeScript samples" href="https://github.com/pbousan/welovejs" target="_blank">https://github.com/pbousan/welovejs</a>

Y aquí la charla que dimos @pbousan y @fernandoescolar en <a title="We love JS" href="http://welovejs.es/">We love JS</a>

<iframe style="border: 1px solid #CCC; border-width: 1px 1px 0; margin-bottom: 5px;" src="http://www.slideshare.net/slideshow/embed_code/17114707" height="356" width="427" allowfullscreen="" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>