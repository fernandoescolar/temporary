---
ID: 165
post_title: 'Gestión de excepciones con WCF &#8211; REST'
author: luisruizpavon
post_date: 2012-04-17 09:00:25
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/gestion-de-excepciones-con-wcf-rest/
published: true
---
Mi compañero <a title="@fernandoescolar" href="https://twitter.com/fernandoescolar" target="_blank">fernandoescolar</a> escribió un artículo muy interesante sobre la <a href="http://www.dotnetodology.com/gestion-de-excepciones-con-wcf" target="_blank">Gestión de excepciones con WCF</a> que te recomiendo leas para ponerte al día sobre buenas prácticas cuando trabajamos con servicios WCF, y a ráiz de leerlo me he acordado del problema que tuve el otro día desarrollando una API REST sobre WCF. ¿Que ocurre cuando nuestro servicio WCF es un endpoint REST (No SOAP) y lanzamos un FaultException&lt;T&gt;?

Lo primero de todo y antes de meternos en chicha, vamos a dar una pequeña descripción de que es REST para que nuestro lector no se pierda.

El acrónimo REST significa Representational State Transfer y apareció por primera vez en la tesis doctoral de Roy Thomas Fielding y es un sistema arquitectural para desarrollar servicios que solicitan y manipulan recursos utilizando los metodos estandar del protocolo HTTP: GET, POST, PUT y DELETE... frente a <a href="http://en.wikipedia.org/wiki/SOAP" target="_blank">SOAP</a> que es un protocolo mucho más complejo desde mi punto de vista.

Para ver un ejemplo de lo fácil que sería comunicarse con un API REST, veamos la siguiente tabla:

<img src="/wp-content/uploads/2012/10/rest.png" alt="" width="921" height="251" />

Simplemente, si queremos recuperar una lista de productos, bastaría con escribir en un navegador web la dirección <a href="http://miservidor/products">http://miservidor/products</a> y el servicio nos devolvería o bien en formato <a href="http://www.json.org/" target="_blank">JSON</a> o <a href="http://en.wikipedia.org/wiki/XML">XML</a> un listado de productos. Sí ahora le pregunto a usted lector ¿Me sabría construir un mensaje <a href="http://en.wikipedia.org/wiki/SOAP" target="_blank">SOAP</a> para esta misma acción? Lo más seguro es que la respuesta sea no, y este es un ejemplo muy sencillo, imagine una petición mucho más compleja añadiendole un filtrado y paginado...

Sí desde nuestro servicio REST lanzamos una excepción del tipo FaultException&lt;T&gt; nuestro servicio mostrará la siguiente página:

<img src="/wp-content/uploads/2012/10/error.png" alt="" width="512" height="303" />

El problema de esto, es que si un cliente JavaScript por ejemplo consume nuestra API REST se encontrará al procesar nuestro error con el contenido HTML de la página de error anterior, con lo cual no sabrá que ha ocurrido y se puede encontrar un poco perdido.

En los servicios REST, hay que jugar con los errores HTTP: 500, 401, 404, 201, 200... ya que es la manera correcta de infromar a los clientes del resultado de llamar a las operaciones de nuestra API. De esta manera y para que sirva de ejemplo, si invocamos la siguiente url:

<a href="http://miservidor/products">http://miservidor/products</a> con un POST y el producto, si todo es correcto, nuestra API deberá devolver el HTTP status code <a href="http://servererrorcodes.com/201-created/" target="_blank">201</a> indicando que se ha creado.

Sí quieres ver una lista extensa de códigos de estado HTTP, echale un vistazo a este enlace <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html">http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html</a>

Entonces <strong>¿Como hago para enviar a mi cliente un error HTTP que le aporte información y que pueda ser tratado de manera correcta?</strong>

En WCF, dispones de un conjunto de clases que nos permiten alterar la respuesta que se le va a enviar a nuestro cliente y la que a nosotros nos interesa para el ejemplo es:
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">public System.ServiceModel.Web.OutgoingWebResponseContext OutgoingResponse { get; }</pre>
</div>
Que básicamente nos permite acceder a la respuesta antes de que sea enviada al cliente, así pues, si en nuestro caso tenemos un método en nuestro servicio de productos un método para retornar un producto por su id y este no existe, REST nos dicta que deberíamos devolver un error HTTP 404 Not Found, para que nuestro cliente sepa que ese producto no existe, algo como esto:
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">public Product GetProductById(int id)
{
	var product =_products.SingleOrDefault(p =&gt; p.Id == id);

    if (product == null)
    {
        OutgoingWebResponseContext ctx=WebOperationContext.Current.OutgoingResponse;
        ctx.SetStatusAsNotFound(String.Format("El producto con id {0} no existe", id));
        ctx.SuppressEntityBody=true;
    }

    return product;
}</pre>
</div>
En este caso llamamos al método <a href="http://msdn.microsoft.com/en-us/library/system.servicemodel.web.outgoingwebresponsecontext.setstatusasnotfound.aspx" target="_blank">SetStatusAsNotFound</a> pasandole el mensaje correspondiente que lo que hace es enviar un <a href="http://en.wikipedia.org/wiki/HTTP_404" target="_blank">404</a> al cliente indicandole que es producto no existe. El código anterior también se puede escribir así:
<pre class="brush: csharp">public Product GetProductById(int id)
{
	var product =_products.SingleOrDefault(p =&gt; p.Id == id);

    if (product == null)
    {
        OutgoingWebResponseContext ctx=WebOperationContext.Current.OutgoingResponse;
        ctx.StatusCode = HttpStatusCode.NotFound;
        ctx.StatusDescription = String.Format("El producto con id {0} no existe", id);
        ctx.SuppressEntityBody=true;
    }

    return product;
}</pre>
Sí se produce una excepción inesperada, entonces podemos enviar un error 500 a nuestro cliente
<pre class="brush: csharp">public Product GetProductById(int id)
{
    try 
	{	        
		var product =_products.SingleOrDefault(p =&gt; p.Id == id);

        if (product == null)
        {
            OutgoingWebResponseContext ctx=WebOperationContext.Current.OutgoingResponse;
            ctx.SetStatusAsNotFound(String.Format("El producto con id {0} no existe", id));
            ctx.SuppressEntityBody=true;
        }

        return product;
	}
	catch (Exception ex)

	{
		OutgoingWebResponseContext ctx=WebOperationContext.Current.OutgoingResponse;
        ctx.StatusCode = HttpStatusCode.InternalServerError;
        ctx.StatusDescription = _localizationHelper.GetLocalizedLiteral("$Resources:api,api_genericerror_message");
        ctx.SuppressEntityBody=true;
	}
}</pre>
A continuación os muestro un ejemplo de llamada JavaScript donde podemos observar el HTTP status code de retorno de nuestro servicio REST cuando un elemento no existe:

<img src="/wp-content/uploads/2012/10/errorjs.png" alt="" width="800" height="399" />

Como habéis podido observar, ahora nuestra API comunica de manera correcta al cliente que la consume que está ocurriendo en todo momento y es su responsabilidad tratar dicho error en su aplicación.

Teníamos otra manera muy elegante de hacer esto, devolviendo errores JSON al cliente con el uso de WCF REST Starter Kit pero como podéis leer en <a href="http://www.codeplex.com/" target="_blank">Codeplex</a> que recientemente Microsoft <a href="http://aspnet.codeplex.com/wikipage?title=WCF%20REST" target="_blank">ha dejado de estar soportado</a> por las llegada de <a href="http://www.asp.net/web-api" target="_blank">ASP.NET MVC 4 WebAPI</a>

Espero que os haya gustado!!!

Hasta la próxima.