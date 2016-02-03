---
ID: 201
post_title: >
  Subir ficheros a través de un servicio
  REST WCF
author: luisruizpavon
post_date: 2012-07-10 16:23:46
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/subir-ficheros-en-un-servicio-rest-wcf/
published: true
---
Siguiendo con la temática de WCF, voy a escribir un par de artículos relacionados con las subida de archivos a través de un API REST WCF y al mismo tiempo aprovecharé para escribir otro acerca de como evitar el límite de 64Kb de subida que nos impone WCF, sin usar el fichero de configuración web.config.

El otro día tuve que modificar un API REST en WCF para soportar subida de ficheros a través de dispositivos móviles como iPad, iPhone...y  se pudiesen subir imagenes tomadas con la cámara. Al principio no tenía muy claro como construir la url del recurso, dado que tenía que subir dicha a imagen de un grupo que se correspondía con un sitio de SharePoint que a su vez tenía una biblioteca de documentos compartidos. El verbo lo tenía claro "POST" y al final decidí usar <strong>/Groups/{id}/Upload/{filename}</strong> que creo que es bastante descriptiva.

Esto traducido a un servicio REST con WCF quedaría asíen nuestro contrato (Interfaz):
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">[OperationContract,
    WebInvoke(UriTemplate = "/Groups/{id}/Upload/{file}",
    ResponseFormat = WebMessageFormat.Json)]
AttachmentsDTO UploadFile(string id, string file, Stream stream);</pre>
</div>
Básicamente lo que hacemos, es traducir los parámetros del UriTemplate a parámetros de nuestro método (Id del Grupo y nombre del archivo con su extensión) y a su vez añadir un <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.aspx" target="_blank">Stream</a> que será el contenido del fichero a subir y que vendrá en el POST, y como valor de retorno le devolvemos al cliente un objeto DTO con la información del fichero que se ha subido (Su Id, su url...).

Una vez que tenemos nuestro contrato, vamos a implementarlo. Para ello os voy a poner directamente el código que sube dicho fichero a la libraría de SharePoint y discutimos algunos temas:
<div id="CodeDiv" dir="ltr">
<pre class="brush: csharp">var buffer = new byte["TAMAÑO DEL BUFFER"];

using (var memoryStream = new MemoryStream())
{
    int bytesRead;
    while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) &gt; 0)
    {
        memoryStream.Write(buffer, 0, bytesRead);
    }

    var list = SPUtility.GetLocalizedString("$Resources:shareddocuments_Title", "core",
                                            (uint)SPContext.Current.Web.Locale.LCID);

    var urlOfFile = SPUrlUtility.CombineUrl(SPUrlUtility.CombineUrl(web.Url, list), file);

    using (new HandleEventFiring())
    {
        web.AllowUnsafeUpdates = true;
        var uploaded = web.Files.Add(urlOfFile, memoryStream.ToArray(), new SPFileCollectionAddParameters { Overwrite = true });
        web.AllowUnsafeUpdates = false;
        attachment = new Attachment(file, uploaded.ServerRelativeUrl, file);
    }
}</pre>
</div>
Lo primero que os puede llamar la atención es el literal <strong>"TAMAÑO DEL BUFFER"</strong> que podríamos saber haciendo esto <strong>stream.Lenght</strong> ¿Verdad? Pues no, en este caso esto levantará una excepción del tipo NotSupportedException porque la propiedad del <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.aspx" target="_blank">Stream</a> <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.canseek" target="_blank">CanSeek</a> es false. Echa un vistazo a <a href="http://stackoverflow.com/questions/3373579/stream-length-throws-notsupportedexception" target="_blank">StackOverflow</a>.

Entonces, no nos queda más remedio que no sabiendo de antemano su longitud, tengamos que ir leyendo el contenido del <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.aspx" target="_blank">Stream</a> que recibimos y en mi caso usar un <a href="http://msdn.microsoft.com/en-us/library/system.io.memorystream.aspx" target="_blank">MemoryStream</a> para almacenarlo y despues pasar su contenido a la función Add.

Una vez hemos implementado nuestro método para añadir el fichero a la librería de SharePoint, solo nos falta probarlo, y para ello vamos a hacer uso de <a href="http://www.fiddler2.com/fiddler2/" target="_blank">Fiddler</a>, un debugger http que nos permitirá simular/analizar todo el tráfico entre el cliente y el servidor de una manera muy sencilla como se muestra en la siguiente imagen:

<img src="/wp-content/uploads/2012/10/upload1.png" alt="" width="812" height="589" />

Destacar, que <a href="http://www.fiddler2.com/fiddler2/" target="_blank">Fiddler</a> nos permite hacer attach de un fichero de nuestro disco y montarnos toda la petición que se va a hacer al servidor (Podemos reutilizar toda esta información para crear un cliente en C# haciendo uso de HttpWebRequest y simularlo nosotros) Además, podéis observar que el Content-Type del Request Header que envíamos es <strong>multipart/form-data </strong>de ahí que recibamos el <a href="http://msdn.microsoft.com/en-us/library/system.io.stream.aspx" target="_blank">Stream</a> en nuestro servicio.

Ejecutamos la petición:

<img src="/wp-content/uploads/2012/10/upload2.png" alt="" width="816" height="592" />

Y como podemos observar, el fichero se ha añadido a la librería y ya tenemos la información necesaria para tratarla en el cliente.

Como os comentaba al principio, existe una limitación de subida de 64Kb que podemos configurar en el fichero web.config de nuestra aplicación, pero que en mi caso no lo contemplo, si puedo ahorrarme ficheros de configuración lo prefiero y más aún si estoy trabajando en una granja de SharePoint de N servidores. En el siguiente artículo veremos como podemos hacer esto vía código.

Un saludo y espero que os haya gustado! Acepto críticas, comentarios, mejoras...