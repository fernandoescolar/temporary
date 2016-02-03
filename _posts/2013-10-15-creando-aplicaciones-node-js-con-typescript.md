---
ID: 984
post_title: >
  Creando aplicaciones Node.js con
  TypeScript
author: pbousan
post_date: 2013-10-15 09:42:26
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/creando-aplicaciones-node-js-con-typescript/
published: true
---
<strong>Aviso:</strong> este artículo fue publicado originalmente en <a title="Node Hispano" href="http://www.nodehispano.com/2013/04/creando-aplicaciones-node-js-con-typescript-parte-1-nodejs/" target="_blank">Node.js Hispano</a>.
&nbsp;

TypeScript es la respuesta de Microsoft a la necesidad de crear aplicaciones web robustas y mantenibles utilizando JavaScript. Esto lo consigue mediante:
<ul>
	<li>Código más homogéneo y mantenible</li>
	<li>Comprobación estática de tipos (opcional y de momento sólo con Visual Studio)</li>
	<li>Object Oriented Programming: clases, herencia e interfaces</li>
	<li>Separation of Concerns (SoC): mediante la organización del código en módulos que se pueden cargar de forma dinámica</li>
</ul>
A diferencia de otros lenguajes que compilan JavaScript, como pueden ser Dart o CoffeScript, TypeScript es un superconjunto de JavaScript, por lo que en esencia es JavaScript.

<img alt="" src="http://www.dotnetodology.com/wp-content/uploads/2013/03/Typescript_thumb.png" />

Por tanto, si ya conocemos JavaScript, no tendremos ningún problema para utilizar TypeScript. La curva de aprendizaje de este nuevo lenguaje será realmente suave, pudiendo conseguir grandes resultados desde el principio. Además, al ser JavaScript, TypeScript nos permite seguir utilizando todas las librerías que conocemos hasta ahora (JQuery, Backbone, Knockout, …)

Hay que destacar también que TypeScript es un proyecto Open Source, y se puede descargar su código fuente (además de varios ejemplos) desde aquí: <a href="http://typescript.codeplex.com/">http://typescript.codeplex.com/</a> Actualmente se encuentra en la versión 0.8.3, y como podéis ver en este <a href="http://typescript.codeplex.com/wikipage?title=Roadmap&amp;referringTitle=Home" target="_blank">roadmap</a>, en la versión final (1.0) estará completamente alineado con la versión 6 de ECMAScript, que traerá de serie alguna de las novedades que implementa TypeScript,

Existen varias formas de utilizar este nuevo lenguaje. La primera sería con proyectos creados con Visual Studio 2012 y el plugin de TypeScript. La segunda, que será sobre la que desarrollemos este artículo, es utilizar el paquete de Node.js y alguno de los IDEs que lo soporta (Sublime Text, Vim, Emacs,...). Para este artículo hemos decidido utilizar Sublime Text, ya que es uno de los que se integra mejor con TypeScript, exceptuando Visual Studio. En este link tenéis los pasos para <a href="http://www.andrewrowland.com/article/display/typescript-sublime-text-integration/" target="_blank">utilizar TypeScript en Sublime Text</a> tanto el syntax highlighter como la forma de crear una System Build que compile TypeScript:

Instalar el paquete de TypeScript para Node.js

<code>npm </code><code>install</code> <code>-g typescript</code>

Para instalar el syntax highlighter, que te puedes descargar desde <a href="http://www.interoperabilitybridges.com/media/155452/typescript_support_for_sublime_text.zip" target="_blank">este link</a>, sólo hace falta copiar el fichero <em>typescript.tmplanguage</em> en tu directorio de paquetes de Sublime Text.

Y sólo falta añadir un Build System para que compile los ficheros TypeScript. Para ello, abrimos Sublime Text, y en <strong>Tools –&gt; Build System –&gt; New Build System</strong>, añadir lo siguiente:
<pre class="csharpcode">{
<span class="str">"selector"</span>: <span class="str">"source.ts"</span>,
<span class="str">"cmd"</span>: [<span class="str">"tsc.cmd"</span>, <span class="str">"$file"</span>],
<span class="str">"file_regex"</span>: <span class="str">"^(.+?) \\((\\d+),(\\d+)\\): (.+)$"</span>
}</pre>
&nbsp;

Y con esto ya podemos compilar los fichero TypeScript (con extensión .ts) en sus correspondientes JavaScript simplemente presionando <strong>Ctrl+B</strong>
<h2></h2>
<h2>MANOS A LA OBRA</h2>
Vamos a desarrollar una aplicación muy básica: el sistema de puntuaciones de un juego. Que está basado uno de los ejemplos disponibles en el repositorio de TypeScript en Codeplex (<a href="http://www.typescriptlang.org/Samples/#ImageBoard)">http://www.typescriptlang.org/Samples/#ImageBoard)</a>, en la que utilizaremos una serie de paquetes Node que harán nuestro trabajo más sencillo:
<ul>
	<li><a href="http://expressjs.com/" target="_blank">ExpressJS</a> para articular la estructura de la aplicación</li>
	<li><a href="https://github.com/mongodb/node-mongodb-native" target="_blank">Node-MongoDB</a> para conectar con la base de datos</li>
	<li><a href="http://jade-lang.com" target="_blank">JadeJS</a> como motor de gestión de vistas</li>
</ul>
Para este ejemplo es necesario, además de Node.js, tener MongoDB instalado, si no lo tenéis, podéis seguir estos pasos para <a href="http://docs.mongodb.org/manual/installation/" target="_blank">instalar MondoDB</a> en vuestro equipo.

Crearemos una estructura muy sencilla de directorios que nos permita tener las diferentes "capas" de la aplicación separadas, ya que usaremos una arquitectura MVC, tenéis disponible todo el código de este artículo en <a href="https://github.com/pbousan/welovejs/tree/master/Sample5" target="_blank">este repositorio de Github</a> . Pero analicemos un poco los ficheros que necesitamos:

/node_modules
/public
-- /stylesheets
/routes
-- index.ts
/views
-- index.jade
-- newscore.jade
-- layout.jade
app.ts
db.ts
express.d.ts
mongodb.ts
node.d.ts
package.json

Lo primero que haremos será crear el fichero de definición de paquetes para poder instalarlos. Este será nuestro package.json:
<pre class="csharpcode">{
    <span class="str">"name"</span>: <span class="str">"application-name"</span>
  , <span class="str">"version"</span>: <span class="str">"0.0.1"</span>
  , <span class="str">"private"</span>: <span class="kwrd">true</span>
  , <span class="str">"dependencies"</span>: {
      <span class="str">"express"</span>: <span class="str">"2.5.8"</span>
      , <span class="str">"ejs"</span>: <span class="str">"&gt;= 0.5.0"</span>
      , <span class="str">"jade"</span>: <span class="str">"&gt;= 0.0.1"</span>
      , <span class="str">"mongodb"</span>: <span class="str">"&gt;= 1.0.0"</span>
  }
}</pre>
&nbsp;

Y los instalamos con la instrucción:

<span style="font-family: 'Courier New';">npm install</span>

Con lo que veremos que se añaden los paquetes necesarios a nuestra carpeta node_modules.

A continuación vamos a editar el fichero principal de la aplicación, en nuestro caso será <strong>app.ts</strong>, que la extensión sea <em>.ts</em> indica que se trata de un fichero con código TypeScript. En este fichero es donde usaremos ExpressJS para establecer el enrutamiento que aceptará nuestra aplicación. Para una guía de uso de Express Framework os recomiendo <a href="http://www.nodehispano.com/2012/05/guia-de-uso-de-express-framework-para-nodejs/" target="_blank">esta de Javier Viola</a>, en este artículo nos centraremos en la implementación con TypeScript.

Antes de nada, debemos añadir las referencias de lo que vamos a utilizar, esto en TypeScript se hace con la siguiente línea:
<pre class="csharpcode">///&lt;reference path=<span class="str">'node.d.ts'</span> /&gt;</pre>
Los ficheros con extensión <em>*.d.ts</em> indican que dicho fichero tendrá la definición de elementos (módulos, interfaces, clases, variables globales y funciones) que necesita TypeScript para importarlos a la hora de compilarlos. Una vez compilado el código TypeScript estos ficheros ya no se vuelven a utilizar. Por tanto, igual que los ficheros <em>.ts</em>, no es necesario que se desplieguen en los servidores de producción.

<strong>Nota:</strong> la extensión .d.ts es una convención y puede que nos encontremos ficheros de definiciones sin ella, ya que no es obligatoria. Estos ficheros de definición son mantenidos por la comunidad de desarrolladores ya que, como comentaba antes, TypeScript es un proyecto Open Source.

Una vez referenciado el fichero de definiciones que nos permite trabajar con el paquete de Node, procedemos a importar los módulos que utilizaremos en nuestra aplicación:
<pre class="csharpcode">import http = module(<span class="str">"http"</span>)
import url = module(<span class="str">"url"</span>)
import routes = module(<span class="str">"./routes/index"</span>)
import db = module(<span class="str">"./db"</span>)
import express = module(<span class="str">"express"</span>)</pre>
Creamos una instancia del objeto <em>express</em> y procedemos a configurarlo. Podemos ver como con TypeScript las funciones anónimas pasan a ser "() =&gt;{}", luego veremos cómo quedan tras compilar:
<pre class="csharpcode">var app = express.createServer();

<span class="rem">// Configuration</span>
app.configure(() =&gt; {
  app.set(<span class="str">'views'</span>, __dirname + <span class="str">'/views'</span>);
  app.set(<span class="str">'view engine'</span>, <span class="str">'jade'</span>);
  app.use(express.bodyParser());
  app.use(express.methodOverride());
  app.use(express.<span class="kwrd">static</span>(__dirname + <span class="str">'/public'</span>));
});

app.configure(<span class="str">'development'</span>, () =&gt; {
  app.use(express.errorHandler({ dumpExceptions: <span class="kwrd">true</span>, showStack: <span class="kwrd">true</span> }));
});

app.configure(<span class="str">'production'</span>, () =&gt; {
  app.use(express.errorHandler());
});</pre>
Ahora asignamos las rutas al que aceptará nuestra aplicación. Como dijimos anteriormente será algo muy sencillo y simplemente tendremos la opción de hacer llamadas GET, que devuelve la lista completa de puntuaciones, y un POST para añadir nuevos elementos. Empecemos sólo con el GET:
<pre class="csharpcode"><span class="rem">// Routes</span>
app.get(<span class="str">'/'</span>, routes.index);

app.listen(3000, function(){
    console.log(<span class="str">"Demo Express server listening on port %d in %s mode"</span>, 3000, app.settings.env);
});

export var App = app;</pre>
Para comprobar que todo está correcto, compilamos el fichero <strong>app.ts</strong> y obtenemos su correspondiente fichero JavaScript:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_Sublime_1.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="NodeTS_Sublime_1" alt="NodeTS_Sublime_1" src="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_Sublime_1_thumb.png" width="778" height="417" border="0" /></a>

Vamos a crear un fichero con el nombre <strong>index.ts</strong>, que se trataría de nuestro "Controlador" dentro de nuestra carpeta <em>/routes</em> y añadimos el siguiente código:
<pre class="csharpcode"><span class="rem">// Importamos los módulos que vamos a utilizar</span>
import express = module(<span class="str">"express"</span>)
import db = module(<span class="str">"../db"</span>)

<span class="rem">// Y exponemos un método que devuelva los elementos de la tabla "highscores".</span>
export function index(req: express.ExpressServerRequest, res: express.ExpressServerResponse){
    db.getScores(function(scores) {
        res.render(<span class="str">'index'</span>, { title: <span class="str">'Highscores'</span>, scores: scores })
    });
};</pre>
Como vemos, hacemos referencia al módulo "<em>db</em>" y llamamos a un método <em>getScores</em>. Esto lo hacemos así para separar el acceso a datos del sistema de rutas y de la generación de las vistas.

&nbsp;
<h3>Accediendo a la base de datos</h3>
Editamos el fichero <strong>db.ts</strong> y añadimos aquí el código que accede a nuestra base de datos MongoDB. Para ello, importamos el módulo de mongodb y creamos una instancia de la clase mongodb, establecemos la conexión con la base de datos y la abrimos:
<pre class="csharpcode">import mongodb = module(<span class="str">'mongodb'</span>);

var server = <span class="kwrd">new</span> mongodb.Server(<span class="str">'localhost'</span>, 27017, {auto_reconnect: <span class="kwrd">true</span>}, {})
var db = <span class="kwrd">new</span> mongodb.Db(<span class="str">'highscores'</span>, server);
db.open(function() {});</pre>
Una vez abierta la conexión, definimos una clase que describe los objetos que esperamos enviar/recibir de la colección "highscores". Esta es una de las ventajas de utilizar TypeScript, que nos permite definir y trabajar con clases, e indicar el tipo de los parámetros de nuestras funciones.
<pre class="csharpcode">export <span class="kwrd">class</span> Score {
    _id: <span class="kwrd">string</span>;
    user: <span class="kwrd">string</span>;
    score : number;
}</pre>
Ahora podremos definir las funciones que expone este módulo. Veremos que hay ciertos elementos nuevos con respecto a una definición en JavaScript.
<pre class="csharpcode">export function getScores(callback: (scores: Score[]) =&gt; <span class="kwrd">void</span>) {

    db.collection(<span class="str">'scores'</span>, function(error, scores_collection) {
        <span class="kwrd">if</span>(error) { console.error(error); <span class="kwrd">return</span>; }
        scores_collection.find({}).toArray(function(error, scoresobj) {
           <span class="kwrd">if</span>(error) { console.error(error); <span class="kwrd">return</span>; }
           callback(scoresobj);
        });

    });
}</pre>
La primera la vemos en los parámetros, estamos indicando que tendremos un callback, que será de tipo <em>void</em> (esto es, que no devuelve nada) la cual recibirá una lista de objetos de tipo <em>Score</em> (la clase que acabamos de definir). Este callback será la función anónima que acabamos de definir en el módulo index:
<pre class="csharpcode">(scores) =&gt; {
        res.render(<span class="str">'index'</span>, { title: <span class="str">'Highscores'</span>, scores: scores })
}</pre>
El resto de una función es la típica que provee el módulo de mongoDB. Pero ya podemos ver la facilidad con la que podríamos cambiar el servidor al que nos conectamos o incluso el repositorio de datos...

&nbsp;
<h3>Definiendo las vistas</h3>
Gracias a JadeJS podemos cambiar el aspecto de la UI de una forma muy sencilla. En nuestro caso sólo vamos a definir una vista en la que mostrar la lista de puntuaciones. Para ello creamos 2 ficheros: <strong>layout.jade</strong> para tener unos elementos comunes e <strong>index.jade</strong> para mostrar la lista:

<strong>layout.jade</strong>
<pre class="csharpcode">!!!
html
  head
    title ImageBoard
    link(rel=<span class="str">'stylesheet'</span>, href=<span class="str">'http://cachedcommons.org/cache/960/0.0.0/stylesheets/960.css'</span>)
    link(rel=<span class="str">'stylesheet'</span>, href=<span class="str">'/stylesheets/style.css'</span>)
  body
    #header.container_12
      script(src=<span class="str">'http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js'</span>)
    #container.container_12!= body</pre>
<strong>index.jade</strong>
<pre class="csharpcode">h1= title
p Welcome to #{title}

ul
- each score <span class="kwrd">in</span> scores
  li
    b= score.user + <span class="str">" "</span> + score.score</pre>
No es intención de este artículo explicar cómo utilizar Jade, pero vemos que podemos recorrer de una forma muy sencilla una lista de elementos, en nuestro caso la clasificación de puntuaciones, y mostrarlas en una página.

Si desde Sublime Text compilamos el fichero <strong>app.ts</strong> podremos ver cómo se generan todos los ficheros JavaScript que serán los que utilice nuestra aplicación. Gracias a la Build Definition que hemos creado anteriormente, no es necesario hacerlo por cada fichero <em>.ts</em>, sino que se hace automáticamente para todos los que necesitamos. Y ya podemos arrancar la aplicación:

<span style="font-family: 'Courier New';">node app.js</span>

y abrimos un navegador para ver el resultado:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_1.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="NodeTS_1" alt="NodeTS_1" src="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_1_thumb.png" width="508" height="224" border="0" /></a>

Podemos ver que la página se renderiza correctamente pero no nos muestra ningún resultado, esto es normal puesto que no tenemos ningún registro en nuestra colección MongoDB. Vamos a hacer una página para insertar registros.
<h3>Añadiendo más funcionalidades</h3>
Siguiendo el mismo proceso que antes, lo primero que hacemos es modificar nuestro fichero de aplicación (<strong>app.ts</strong>) para añadir dos métodos nuevos, un GET que cargue un formulario y un POST para insertar los datos:
<pre class="csharpcode">app.get(<span class="str">'/scores/newscore'</span>, (req, res) =&gt; {
    routes.newscoreget(req, res);    
});

app.post(<span class="str">'/scores/newscore'</span>, (req, res) =&gt; {
   routes.newscorepost(req, res);
});</pre>
Definimos los nuevos métodos en nuestro fichero <strong>index.ts</strong>:
<pre class="csharpcode">export <span class="kwrd">function</span> newscoreget(req: express.ExpressServerRequest, res: express.ExpressServerResponse){
     res.render(<span class="str">'newscore'</span>,{});   
};

export <span class="kwrd">function</span> newscorepost (req: express.ExpressServerRequest, res: express.ExpressServerResponse){
    <span class="kwrd">var</span> newscore = <span class="kwrd">new</span> db.Score()
    newscore.user = req.param(<span class="str">'user'</span>);
    newscore.score = req.param(<span class="str">'score'</span>);
     db.addScore(newscore, (r) =&gt; {
        res.redirect(<span class="str">'/'</span>);
    });
};</pre>
Como vemos, el primero únicamente renderiza el formulario y es le segundo método el que llamará a nuestro módulo de acceso a datos. En este segundo método utilizamos un objeto de la clase <em>Score</em> que hemos definido en otro módulo, que será lo que pasemos como parámetro al método addScore. Veamos cómo implementamos este método:
<pre class="csharpcode">export <span class="kwrd">function</span> addScore(newscore : Score, callback: (result: any)=&gt; <span class="kwrd">void</span>){
    db.collection(<span class="str">'scores'</span>, <span class="kwrd">function</span>(error, scores_collection) {
        <span class="kwrd">if</span> (error) { console.error(error); <span class="kwrd">return</span>; }
        scores_collection.insert({<span class="str">"user"</span> : newscore.user, <span class="str">"score"</span> : newscore.score },
            (error, result) =&gt; {
                <span class="kwrd">if</span>(error) { console.error(error); <span class="kwrd">return</span>; }
                callback(result);
            })
        });
}</pre>
Gracias a que utilizamos una clase de TypeScript, podemos ver sus propiedades cuando las necesitemos:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_Sublime_2.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="NodeTS_Sublime_2" alt="NodeTS_Sublime_2" src="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_Sublime_2_thumb.png" width="634" height="156" border="0" /></a>

Y por último, creamos la vista <strong>newscore.jade</strong> con el formulario en el que añadimos el usuario y la puntuación:
<pre class="csharpcode">form( method=<span class="str">"post"</span>)
   div
       br
       div
           span.inputtitle User name :
           input(type=<span class="str">"text"</span>, name=<span class="str">"user"</span>)
       br
       div
           span.inputtitle Score :
           input(type=<span class="str">"text"</span>, name=<span class="str">"score"</span>)
       br
       #editScoreSubmit
           input.button(type=<span class="str">"submit"</span>, value=<span class="str">"Save Score"</span>)</pre>
&nbsp;

Y modificamos nuestra vista principal para añadirle un botón que llame a nuestra recién creada vista:
<pre class="csharpcode">h1= title
p Welcome to #{title}

ul
- each score <span class="kwrd">in</span> scores
  li
    b= score.user + <span class="str">" "</span> + score.score
br
form( action=<span class="str">"/scores/newscore/"</span>, method=<span class="str">"get"</span>)
    div
        #newScoreSubmit
            input.button(type=<span class="str">"submit"</span>, value=<span class="str">"New Score"</span>)</pre>
&nbsp;

Volvemos a compilar el fichero <strong>app.ts</strong> y arrancamos la aplicación, si todo ha ido bien ya podremos acceder al formulario para añadir puntuaciones:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_2.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="NodeTS_2" alt="NodeTS_2" src="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_2_thumb.png" width="427" height="208" border="0" /></a>

Y ver el resultado en la página principal:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_4.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="NodeTS_4" alt="NodeTS_4" src="http://www.dotnetodology.com/wp-content/uploads/2013/04/NodeTS_4_thumb.png" width="501" height="273" border="0" /></a>
<h2></h2>
<h2>RESUMIENDO</h2>
Este pequeño ejemplo nos ha servido para ver cómo se puede hacer una aplicación web con NodeJS y TypeScript con una buena estructura, el código bien organizado y siguiendo el patrón MVC. Esto nos permite que, si la aplicación es muy grande, el trabajo se pueda repartir entre diferentes personas/grupos de manera muy sencilla.