---
ID: 126
post_title: >
  Creando HTML Helpers personalizados en
  ASP.NET MVC 3
author: luisruizpavon
post_date: 2012-02-12 11:15:58
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/creando-html-helpers-personalizados-en-asp-net-mvc-3/
published: true
---
Gracias al equipo de <a href="http://www.programandonet.com" target="_blank">programandonet.com</a> por ofrecerme otro sitio donde poder compartir mi conocimiento con la comunidad. Voy a ir escribiendo cosas acerca de <a href="http://www.asp.net/mvc" target="_blank">ASP.NET MVC</a> y como podemos customizarlo poco a poco, motores de vistas, controladores, modelos, testing, integración continua, despliegues, herramientas... Para empezar a abrir boca, voy a empezar por hablar de los<a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank"> HTML Helpers de ASP.NET MVC</a>, espero que os guste!
<h2>Introducción a HTML Helpers</h2>
Básicamente y sin enrollarnos mucho en una definición compleja de que es un <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank">HTML Helper</a>, podríamos decir que es un método que devuelve una cadena de texto y esta cadena de texto puede ser lo que nosotros queramos, desde etiquetas HTML, scripts...

Así pues la principal ventaja de usar <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank">Html Helpers</a> en <a href="http://www.asp.net/mvc" target="_blank">ASP.NET MVC</a> es claramente el evitar tener que estar escribiendo etiquetas de HTML,scripts... continuamente en nuestras vistas. En <a href="http://www.asp.net/mvc" target="_blank">ASP.NET MVC</a> tenemos una amplia lista de Helpers como por ejemplo los 2 que os muestro a continuación:

<img src="/wp-content/uploads/2012/10/tabla.png" alt="" width="631" height="114" />

Como podemos observar, al usar el método TextBox() lo que  devuelve es un string con el HTML necesario para mostrar una caja de texto de HTML estándar.

Si queréis ver la lista completa de HTMLHelpers mira este <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank">enlace</a> de la <a href="http://msdn.microsoft.com" target="_blank">MSDN</a>

Vista esta pequeña introducción, vamos a crear nuestro propio HTML Helper el cual mostrará un DateTime en formato relativo como lo hace Twitter, Facebook… y para ello vamos a usar una librería de <a title="jQuery" href="http://jquery.com/" target="_blank">jQuery</a> llamada <a href="http://timeago.yarp.com/" target="_blank">timeago</a>.

<img src="/wp-content/uploads/2012/10/twitter.png" alt="" width="516" height="202" />
<h2>Introducción a Timeago y como hacer el trabajo manualmente sin Helpers</h2>
<a href="http://timeago.yarp.com/">Timeago</a> es un plugin de <a href="http://jquery.com/">jQuery</a> que actualizara automáticamente (Cada x tiempo) nuestras fechas a un formato relativo como lo hacen las principales redes sociales.

Una vez <a href="http://timeago.yarp.com/jquery.timeago.js">descargado</a>, vamos a ver como hacer el trabajo de forma manual en nuestra aplicación y luego lo trasladaremos a un HTML Helper para ver como nos evitará la tediosa tarea de estar escribiendo todo este código cada vez que queramos usarlo en nuestras aplicaciones web.

Lo primero que tendríamos que hacer para que <a href="http://timeago.yarp.com/" target="_blank">timeago</a> funcione en nuestras aplicaciones <a href="http://www.asp.net/mvc" target="_blank">ASP.NET MVC</a> es añadir el fichero js a nuestra carpeta de es scripts y añadir una referencia a dicho fichero en nuestra pagina maestra, que se encuentra en (<strong>Shared/_Layout.cshtml</strong>):
<pre class="brush: js">&lt;script type="text/javascript" src="jquery.timeago.js"&gt;&lt;/script&gt;</pre>
<strong>Nota:</strong> No incluyo el de <strong>jquery-version.min.js</strong> porque el layout ya lo incluye por defecto cuando creamos un proyecto de <a href="http://www.asp.net/mvc" target="_blank">ASP.NET MVC</a>, de no ser así, lo añadimos:
<pre class="brush: js">&lt;script src="@Url.Content("~/Scripts/jquery-x.x.x.min.js")" type="text/javascript"&gt;&lt;/script&gt;</pre>
El siguiente paso es hacer un attach de timeago al DOM, y para ello podemos hacerlo con el siguiente código insertándolo también en nuestra master page y así lo tendremos disponible en todas nuestras vistas:
<pre class="brush: js">jQuery(document).ready(function () {
            jQuery("abbr.timeago").timeago();
        });</pre>
Y por ultimo, añadimos la siguiente etiqueta html en nuestra página Index.cshtml:
<pre class="brush: html">&lt;abbr class="timeago" title="2008-07-17T09:24:17Z"&gt;July 17, 2008&lt;/abbr&gt;</pre>
Que será transformado por timeago en algo como esto:
<div id="CodeDiv" dir="ltr">
<pre class="brush: xml">&lt;abbr class="timeago" title="July 17, 2008"&gt;3 years ago&lt;/abbr&gt;</pre>
</div>
¿Cual es el principal problema de todo esto?

Pues tenemos 2, el primero es que si queremos reutilizar este código en otra aplicación tendremos que volver a escribirlo y esto conlleva además que podamos cometer algún error de sintaxis al escribirlo de nuevo y volvernos locos horas y horas viendo donde está fallando. Sí lo escribimos una vez, lo probamos y funciona, será mejor reutilizar un par de métodos sencillos y tipados en C# que nos ahorrarán tiempo y problemas. Vamos a verlo!
<h2>Creando nuestro propio HTML Helper</h2>
Nuestra tarea comienza aquí y lo primero para crear un HTML Helper es crear una clase, que en este caso llamaremos <strong>TimeagoExtensions</strong> y que tendrá que ser estática, porque para crear un HTML Helper tendremos que hacer uso de los <a href="http://msdn.microsoft.com/es-es/library/bb383977.aspx" target="_blank">métodos de extensión de c#</a>, que básicamente lo que nos van a permitir es agregar métodos a una clase existente sin tener que heredar de ella o modificar la clase original, que en este caso es <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank">HtmlHelper</a>
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">public static class TimeagoExtensions
{

}</pre>
</div>
Ahora vamos a añadir nuestro primer método de extensión para registrar el script en nuestra vista. El parámetro html de tipo <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper.aspx" target="_blank">HtmlHelper</a> con el modificador <a href="http://msdn.microsoft.com/en-us/library/dk1507sz(v=vs.80).aspx" target="_blank">this</a> por delante sirve para decir la clase a la que queremos añadir este método extensor:
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">public static MvcHtmlString RegisterScriptTimeAgo(this HtmlHelper html)
{
    var script = String.Format(@"&lt;script src=""{0}"" type=""text/javascript""&gt;&lt;/script&gt;
                                    &lt;script type=""text/javascript""&gt;
                                        jQuery(document).ready(function() {{
                                            jQuery(""abbr.timeago"").timeago();
                                        }});
                                    &lt;/script&gt;", 
                    UrlHelper.GenerateContentUrl("~/Scripts/jquery.timeago.js", 
                                                    html.ViewContext.HttpContext));

    return MvcHtmlString.Create(script);
}</pre>
</div>
A continuación vamos con el segundo método. Este método recibe un <strong>DateTime</strong> con él se va a generar la etiqueta html a la que timeago aplicara la transformación relativa:
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">public static MvcHtmlString TimeAgo(this HtmlHelper html,
                                    DateTime dateTime)
{
    var tagBuilder = new TagBuilder("abbr");
    tagBuilder.SetInnerText(String.Format("{0:MMMM d, yyyy}", dateTime));
    tagBuilder.AddCssClass("timeago");
    tagBuilder.Attributes.Add("title", String.Format("{0:s}Z", dateTime));
    return MvcHtmlString.Create(tagBuilder.ToString());
}</pre>
</div>
Aquí podemos ver una nueva clase <a href="http://msdn.microsoft.com/en-us/library/system.web.mvc.tagbuilder.aspx" target="_blank">Tag Builder</a> que usaremos en nuestros HTML Helpers para construir de manera sencilla tags HTML. En este caso estamos construyendo la etiqueta HTML tal cual nos dice la documentación de <a href="http://timeago.yarp.com/" target="_blank">timeago</a> y que escribimos manualmente en el ejemplo anterior.

Otra cosa muy importante es que el atributo <strong>title</strong> tiene el valor de la fecha formateado en <a href="http://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>

Bueno pues ya tenemos nuestro HTML Helper listo para ser usado en nuestras vistas, así que vamos a añadir una pequeña entrada al <a href="http://msdn.microsoft.com/en-us/library/aa306178.aspx" target="_blank">web.config</a> que esta en la carpeta de las vistas para que dispongamos de nuestros métodos extensores en el intellisense de Visual Studio:

<img src="/wp-content/uploads/2012/10/webconfig.png" alt="" width="303" height="298" />

Lo editamos con algún editor tipo <a href="http://en.wikipedia.org/wiki/Notepad_(software)" target="_blank">notepad</a> o <a href="http://notepad-plus-plus.org/" target="_blank">notepad++</a> e insertamos nuestro namespace donde se encuentran nuestro helpers (En mi caso MvcApplication1.Helpers):
<div id="CodeDiv" dir="ltr">
<pre class="brush: xml">&lt;system.web.webPages.razor&gt;
  &lt;host factoryType="System.Web.Mvc.MvcWebRazorHostFactory, System.Web.Mvc, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" /&gt;
  &lt;pages pageBaseType="System.Web.Mvc.WebViewPage"&gt;
    &lt;namespaces&gt;
      &lt;add namespace="System.Web.Mvc" /&gt;
      &lt;add namespace="System.Web.Mvc.Ajax" /&gt;
      &lt;add namespace="System.Web.Mvc.Html" /&gt;
      &lt;add namespace="System.Web.Routing" /&gt;
      &lt;add namespace="MvcApplication1.Helpers" /&gt;
    &lt;/namespaces&gt;
  &lt;/pages&gt;
&lt;/system.web.webPages.razor&gt;</pre>
</div>
Y en nuestras vistas ya los tenemos disponibles en el intellisense de Visual Studio como os muestro en la imagen:

<img src="/wp-content/uploads/2012/10/visualstudio.png" alt="" width="412" height="260" />

Entonces para terminar con nuestro ejemplo, vamos a nuestra pagina maestra <strong>_Layout.cshtml</strong> en la carpeta <strong>Shared</strong> y añadimos la llamada al método RegisterScriptTimeAgo()
<div id="CodeDiv" dir="ltr">
<pre class="brush: xml">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;@ViewBag.Title&lt;/title&gt;
    &lt;link href="@Url.Content("~/Content/Site.css")" rel="stylesheet" type="text/css" /&gt;
    &lt;script src="@Url.Content("~/Scripts/jquery-1.5.1.min.js")" type="text/javascript"&gt;&lt;/script&gt;
    @Html.RegisterScriptTimeAgo()
&lt;/head&gt;
&lt;body&gt;</pre>
</div>
En la vista <strong>Home/Index.cshtml</strong> ponemos el siguiente código:
<div id="CodeDiv" dir="ltr">
<pre class="brush: xml">@model IEnumerable&lt;MvcApplication1.Models.Message&gt;

@{
    ViewBag.Title = "Home Page";
}

&lt;h2&gt;timeago&lt;/h2&gt;
&lt;ul&gt;
    @foreach (var item in Model)
    {
        &lt;li&gt;
            &lt;p&gt;@item.Text&lt;/p&gt;
            @Html.TimeAgo(item.Created)
        &lt;/li&gt;
    }
&lt;/ul&gt;</pre>
</div>
Ejecutamos nuestra aplicación y el resultado es el siguiente:

<img src="/wp-content/uploads/2012/10/resultado.png" alt="" width="387" height="373" />

<strong>Nota:</strong> El tiempo de refresco de fechas es por defecto un minuto y lo refleja la variable (refreshMillis: 60000).

El código html generado por el método <strong>RegisterScriptTimeAgo</strong>:

<img src="/wp-content/uploads/2012/10/scritptimeago.png" alt="" width="606" height="184" />

Y por la ejecución del script de timeago:

<img src="/wp-content/uploads/2012/10/scritptimeago2.png" alt="" width="594" height="289" />

A partir de ahora es tarea del lector profundizar mas en el tema y como no empezar a crear sus propios HTML Helpers. Hasta la próxima!

<a href="https://skydrive.live.com/redir.aspx?cid=90f54d9ff9d3f9ea&amp;resid=90F54D9FF9D3F9EA!546&amp;parid=90F54D9FF9D3F9EA!465" target="_blank">Descarga el código de ejemplo</a>