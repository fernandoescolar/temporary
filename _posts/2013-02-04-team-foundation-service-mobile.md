---
ID: 808
post_title: Team Foundation Service Mobile
author: fernandoescolar
post_date: 2013-02-04 10:56:21
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/team-foundation-service-mobile/
published: true
---
Hace unos días publicamos un artículo sobre <a href="http://www.dotnetodology.com/scrum-con-tfs/" target="_blank">cómo TFS nos puede ayudar en la gestión de proyectos con scrum</a>. En los comentarios, Francisco Calles señalaba una de las carencias de esta herramienta: la existencia de una aplicación para móviles. Así que aprovechando que han liberado la beta de los servicios <a href="https://tfsodata.visualstudio.com/" target="_blank">OData para Team Foundation Service</a>, os presentamos una pequeña herramienta que hemos desarrollado el equipo de ALM de la fundación <a href="http://www.techdencias.net" target="_blank">Techdencias</a>, del que algunos miembros de Programando en .Net formamos parte: <strong>TFS Mobile</strong>.

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/alm-techdencias-banner.png"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; margin-right: auto; border-width: 0px;" title="alm-techdencias-banner" alt="alm-techdencias-banner" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/alm-techdencias-banner_thumb.png" width="492" height="142" border="0" /></a>

Empezamos el desarrollo de TFS Mobile como un ejercicio de programación, un prototipo que quizá en un futuro pueda inspirar otro tipo de aplicaciones más completas. Pero para hacerlo más divertido pusimos unas normas básicas:
<ul>
	<li><strong>Aportar valor</strong>: la aplicación, debía ser un complemento al portal web de TFS, aportando información de una forma rápida y sencilla.</li>
	<li>Realizar una aplicación <strong>para dispositivos móviles</strong>, que se pudiera manejar bien en una pantalla pequeña y que reaccionara correctamente a pulsaciones realizadas con el dedo en la pantalla.</li>
	<li>Si queríamos aportar valor, no podíamos cerrarnos las puertas a diferentes dispositivos, por lo que además debía ser <strong>multiplataforma</strong>.</li>
	<li>Y la vía más rápida de conseguir estas características era desarrollar una aplicación usando las últimas tecnologías de <strong>javascript y html5</strong>.</li>
</ul>
Como resultado, si con nuestro teléfono móvil entramos en <a href="http://www.dotnetodology.com/tfs">http://www.dotnetodology.com/tfs</a>, podremos tener acceso al fruto de nuestro trabajo.
<h3>Guía de usuario</h3>
Antes de empezar a usar <a href="http://www.dotnetodology.com/tfs/" target="_blank">TFS Mobile</a>, tenemos que preparar nuestra cuenta de <strong>Team Foundation Service</strong>, para poder acceder a los servicios <strong>OData</strong>. Para ello nos dirigiremos a nuestro portal de TFS: <a href="http://[cuenta].visualstudio.com" target="_blank">http://[cuenta].visualstudio.com</a>.

Una vez nos hayamos autenticado y estemos en la página principal, en la parte superior derecha buscaremos nuestro nombre, y en el menú contextual que aparece después de pulsarlo, haremos clic en “My Profile”:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/step1.jpg"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; margin-right: auto; border-width: 0px;" title="step1" alt="step1" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/step1_thumb.jpg" width="252" height="124" border="0" /></a>

Entonces aparecerá una nueva ventana donde nos tendremos que dirigir a la página de “Credentials”, y allí deberíamos presionar el enlace “Enable alternate credentials”:

<a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/step2.jpg"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; margin-right: auto; border-width: 0px;" title="step2" alt="step2" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/step2_thumb.jpg" width="321" height="292" border="0" /></a>

Para terminar, tendremos que introducir un nombre de usuario y una contraseña en las cajas de texto que se mostrarán. Si todo ha ido bien, recibiremos un email de Microsoft informándonos de que hemos activado estas credenciales.

Ahora si que podemos dirigirnos a la página principal de TFS Mobile: <a href="http://www.dotnetodology.com/tfs">http://www.dotnetodology.com/tfs</a>, donde se solicitarán nuestras credenciales:
<p align="center"><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/login1.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="login1" alt="login1" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/login1_thumb.png" width="187" height="244" border="0" /></a> <a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/login2.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="login2" alt="login2" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/login2_thumb.png" width="171" height="244" border="0" /></a></p>
<p align="left">En este punto puede ser que aparezca un formulario para introducir nuestras credenciales, o por el contrario, que al pulsar sobre “AUTHENTICATE”, el navegador nos pida que introduzcamos las credenciales. En este último caso, el nombre de usuario será el nombre de nuestra cuenta de TFS, una contra barra y el nombre de usuario que introdujimos en el paso anterior: cuenta\usuario. Y en la contraseña deberemos introducir la asociada a nuestro nombre de usuario.</p>
<p align="left">Una vez hayamos introducido las credenciales correctas podremos acceder al listado de nuestros proyectos:</p>
<p align="left"><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/projects.png"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; margin-right: auto; border-width: 0px;" title="projects" alt="projects" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/projects_thumb.png" width="258" height="207" border="0" /></a></p>
<p align="left">Al pulsar sobre cualquiera de ellos se mostrará el elemento seleccionado en la parte superior y un listado de opciones a elegir para poder navegar en la información de TFS:</p>
<p align="left"><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/categories.png"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; margin-right: auto; border-width: 0px;" title="categories" alt="categories" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/categories_thumb.png" width="262" height="252" border="0" /></a></p>
<p align="left">Cada elección que vayamos haciendo se irá acumulando debajo del logotipo, y para volver a la pantalla de selección, como se trata de una aplicación en javascript, no tendremos que pulsar el botón volver, simplemente tendremos que volver a pulsar sobre la selección que hicimos. Por ejemplo, para cambiar de proyecto deberíamos pulsar en el nombre del proyecto que seleccionamos anteriormente:</p>
<p align="center"><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/categories2.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="categories2" alt="categories2" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/categories2_thumb.png" width="244" height="235" border="0" /></a> <span style="font-size: 120px;">&gt;&gt;</span><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/projects1.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="projects" alt="projects" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/projects_thumb1.png" width="244" height="196" border="0" /></a></p>
<p align="left">Las opciones disponibles hoy en día son:</p>

<ul>
	<li>
<div align="left"><strong>Changesets</strong>: podemos ver un listado con los últimos cambios que se han realizado en el código fuente, su número, el comentario y quien lo realizó.</div></li>
	<li>
<div align="left"><strong>Builds</strong>: contiene la información sobre el resultado de los últimos procesos de build y su resultado: se añade un cuadrado rojo o verde en dependencia de si fue exitoso o no.</div></li>
	<li>
<div align="left"><strong>Build Definitions</strong>: nos muestra un listado de las builds que están configuradas para el proyecto.</div></li>
	<li>
<div align="left"><strong>Queries</strong>: nos mostrará un listado de todas las ‘queries’ que tengamos almacenadas en nuestra cuenta para este proyecto y al navegar sobre ellas, veremos el listado de ‘workitems’ seleccionados. Al pulsar sobre un workitem, podremos ver detalles del mismo.</div></li>
</ul>
<p align="left">Algunas capturas de la aplicación:</p>
<p align="center"><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/builds.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="builds" alt="builds" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/builds_thumb.png" width="180" height="244" border="0" /></a> <a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/queries.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="queries" alt="queries" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/queries_thumb.png" width="178" height="244" border="0" /></a> <a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/workitems.png"><img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="workitems" alt="workitems" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/workitems_thumb.png" width="180" height="244" border="0" /></a></p>
<p align="left">Como podemos deducir, si creamos una buena serie de consultas, tendremos acceso desde nuestro móvil a una información muy completa. Pero si quisiéramos realizar tareas más complejas, tendremos que ir a un ordenador y entrar en el portal de TFS o usar Visual Studio.</p>

<h3>Desarrollo</h3>
Para aquellos que tengan interés en cómo hemos realizado esta aplicación vamos a hacer un resumen de las tecnologías y estrategias que hemos llevado a cabo.

Lo primero que debemos decir es que la aplicación ha se distribuye en javascript y html5, usando como backend los servicios OData de TFS.

OData es el nombre que recibe el <a href="http://www.odata.org/" target="_blank">Open Data Protocol</a>, un protocolo web que sirve para consultar y actualizar la información que manejamos mediante una combinación de tecnologías como HTTP, AtomPub o Json. Podemos encontrar la especificación de los servicios concretos de TFS en <a title="https://tfsodata.visualstudio.com/" href="https://tfsodata.visualstudio.com/">https://tfsodata.visualstudio.com/</a>.

Para poder consumir datos de este servicio hemos utilizado una librería de javascript conocida como <a href="http://datajs.codeplex.com/" target="_blank">datajs</a>, que nos permite consumir datos de un servicio OData de una forma fácil. Básicamente hemos creado un servicio que realiza peticiones, implementando el patrón <strong>Promise</strong> con la ayuda del objeto “Deferred” de la librería <a href="http://jquery.com/" target="_blank">jQuery</a>:
<pre class="brush: js">var tfservice = (function() {
    function request(url) {
        var deferred = $.Deferred();

        OData.read({ requestUri: url, timeoutMS: 90000 }, function (data) {
            deferred.resolve(data);
        }, function (err) {
            deferred.reject(err);

            if (err.message == 'Invalid user or password.') {
                alert(err.message + ' Maybe you should clear the browser cache or open this page in a new browser window.');
                location.reload(true);
            }
            else {
                alert(err.message);
            }
        });

        return deferred.promise();
    }

    OData.defaultHttpClient.enableJsonpCallback = true;

    return {
        request: request
    };
})();</pre>
Ya podíamos acceder a los datos, y para poder mantener nuestro código fácilmente y bien estructurado, nos decidimos por el patrón <strong>Model-View-ViewModel</strong>, sirviéndonos de la ayuda de <a href="http://knockoutjs.com/" target="_blank">knockout</a>.

En este punto del desarrollo optamos por usar <a title="TypeScript" href="http://www.typescriptlang.org/" target="_blank">TypeScript </a>para resolver un problema engorroso de javascript: la herencia. Si vamos a crear objetos de tipo ViewModel nos gustaría crear una herencia de objetos para no tener que codificar todo el rato lo mismo, y esta jerarquía es más simple desarrollarla con TypeScript. Lo primero que hicimos fue crear la base de nuestros objetos ViewModel:
<pre class="brush: java">class ViewModel { 
    public shouldShow: ObservableBool;
    public isLoading: ObservableBool;
    constructor(public tfservice: ITfservice) { 
        this.shouldShow = ko.observable(false);
        this.isLoading = ko.observable(false);
    }
}</pre>
Y después fuimos heredando en el resto:
<pre class="brush: java">class LoginViewModel extends ViewModel {
    // ...
}
class CollectionViewModel extends ViewModel {
    // ...
}
class ProjectsViewModel extends CollectionViewModel { 
    // ...
}
// ...</pre>
La peculiaridad que tiene TypeScript al usarlo junto con knockout es que no podremos declarar los métodos de la forma estándar:
<pre class="brush: java">class CollectionViewModel extends ViewModel {
    // ...
    public selected: ObservableAny;

    public isSelected(model: any) {
        return this.selected() == model;
    }
    // ...
}</pre>
Para no tener problemas, knockout requiere que declaremos los métodos de nuestras clases como variables y que las definamos en el constructor:
<pre class="brush: java">class CollectionViewModel extends ViewModel {
    // ...
    public selected: ObservableAny;
    public isSelected: (item: any) =&gt; bool;

    constructor() {
    	this.isSelected = (model: any) =&gt; this.selected() == model;
    }
    // ...
}</pre>
La idea era crear un ViewModel de aplicación que gestionara los ViewModels que habíamos creado en TypeScript. Pero antes de eso surgió el problema de comunicar todos los ViewModels unos con otros. Algo que resolvimos con <a href="http://www.dotnetodology.com/patrones-de-diseno-mediator/" target="_blank">el patrón <strong>Mediator</strong> que ya comentamos en programandonet</a>. Así que en la base de los objetos ViewModel añadimos en el constructor un parámetro que representara el mediador:
<pre class="brush: java">class ViewModel { 
    public shouldShow: ObservableBool;
    public isLoading: ObservableBool;
    constructor(public mediator: IMediator, public tfservice: ITfservice) { 
        this.shouldShow = ko.observable(false);
        this.isLoading = ko.observable(false);
    }
}</pre>
De esta forma podríamos publicar mensajes o registrarnos para escucharlos:
<pre class="brush: java">// escuchamos los mensajes de tipo 'action name'
this.mediator.register('action name', data =&gt; alert(data));
// enviamos un mensaje de tipo 'action name'
this.mediator.notify('action name', data);</pre>
Una vez teníamos toda esta estructura, volvimos a programar con javascript y creamos el ViewModel general que contendría al resto:
<pre class="brush: js">var ApplicationViewModel = function (mediator, tfservice) {
    var self = this;
    var httpLoginBrowser = navigator.userAgent.indexOf('MSIE') &gt;= 0 || navigator.userAgent.indexOf('iPhone') &gt;= 0 || navigator.userAgent.indexOf('Android') &gt;= 0;

    self.LoginContext = new LoginViewModel(mediator, tfservice, httpLoginBrowser);
    self.ProjectsContext = new ProjectsViewModel(mediator, tfservice);
    self.CategoriesContext = new CategoriesViewModel(mediator);
    self.QueriesContext = new QueriesViewModel(mediator, tfservice);
    self.ItemsContext = new ItemsViewModel(mediator, tfservice);
};

ko.applyBindings(new ApplicationViewModel(mediator, tfservice));</pre>
Para terminar, diseñamos las vistas en <strong>HTML5</strong>, usando secciones para mostrar los datos expuesto por cada uno de los ViewModels:
<pre class="brush: xml">&lt;section id="projects" data-bind="with:ProjectsContext, visible: ProjectsContext.shouldShow"&gt;
    &lt;h1 data-bind="text: title, visible: selected() === null"&gt;&lt;/h1&gt;
    &lt;div id="projects-list" data-bind="foreach: items"&gt;
        &lt;button data-bind="visible: $parent.isVisible($data), text: $data.Name, click: $parent.select, css: { selected: $parent.isSelected($data) }"&gt;&lt;/button&gt;
    &lt;/div&gt;
    &lt;div data-bind="if: isLoading" class="loading"&gt;&lt;img alt="Loading..." src="Images/loading.gif"/&gt;&lt;/div&gt;
&lt;/section&gt;</pre>
<h3>Feedback</h3>
Esperamos que esta aplicación se entienda como lo que es, un experimento o prueba de concepto... En ningún caso es una herramienta completa y lista para producción. Pero ha sido muy emocionante desarrollar este primer proyecto junto con el equipo de <a href="http://www.techdencias.net" target="_blank">Techdencias</a>. Y creemos que es una buena carta de presentación para el grupo de ALM que hemos formado.

Lo que si que nos gustaría pedir a los lectores es que, los que hayan usado la aplicación nos retornaran un feedback sobre las cosas que les han gustado o cuales podríamos mejorar.
<h3>Enlaces de interés</h3>
Como hemos mencionado muchos conceptos y librerías a lo largo del documento, nos gustaría cerrar este artículo con un resumen de los enlaces a las librerías y sites que han ido apareciendo:
<ul>
	<li><strong>OData</strong>: <a title="OData" href="http://www.odata.org/" target="_blank">http://www.odata.org/</a></li>
	<li><strong>TFS OData</strong>: <a title="TFS OData Service" href="https://tfsodata.visualstudio.com/" target="_blank">https://tfsodata.visualstudio.com/</a></li>
	<li><strong>jQuery</strong>: <a title="jquery" href="http://jquery.com/" target="_blank">http://jquery.com/</a></li>
	<li><strong>Datajs</strong>: <a title="datajs" href="http://datajs.codeplex.com/" target="_blank">http://datajs.codeplex.com/</a></li>
	<li><strong>Knockout</strong>:<a title="knockoutjs" href=" http://knockoutjs.com/" target="_blank"> http://knockoutjs.com/</a></li>
	<li><strong>TypeScript</strong>: <a title="TypeScript" href="http://www.typescriptlang.org/" target="_blank">http://www.typescriptlang.org/</a></li>
	<li><strong>TFS Mobile</strong>: <a title="TFS Mobile" href="http://programandonet.com/tfs/" target="_blank">http://programandonet.com/tfs/</a></li>
</ul>