---
ID: 206
post_title: >
  Modificar programáticamente el tamaño
  de subida de ficheros en un servicio
  REST WCF
author: luisruizpavon
post_date: 2012-07-19 13:22:45
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/modificar-programaticamente-el-tamano-de-subida-de-ficheros-en-un-servicio-rest-wcf/
published: true
---
<p>En mi anterior <a href="http://www.dotnetodology.com/subir-ficheros-en-un-servicio-rest-wcf">art&iacute;culo</a>, vimos como podemos subir ficheros a un servidor a trav&eacute;s de un servicio REST WCF. Vimos que exist&iacute;a una restricci&oacute;n de subida del tama&ntilde;o del fichero de 64Kb y os comentaba, que esto se pod&iacute;a modificar tocando el fichero web.config, pero tambi&eacute;n os comentaba que en mi caso no era factible esa opci&oacute;n. As&iacute; pues vamos a ver como podemos hacerlo program&aacute;ticamente. La restricci&oacute;n de subida de archivos tiene su l&oacute;gica, evitar <a href="http://en.wikipedia.org/wiki/Denial-of-service_attack" target="_blank">ataques de denegaci&oacute;n de servicio</a> (DoS).</p>
<h3>&iquest;Por donde empezamos?</h3>
<p>Lo primero que necesitamos es poder acceder a las propiedades de configuraci&oacute;n que nos permitir&aacute;n cambiar este tama&ntilde;o de subida. S&iacute; buscamos en la documentaci&oacute;n de WCF, podemos ver que el Binding tiene estas 2 propiedades:</p>
<p><a href="http://msdn.microsoft.com/en-us/library/system.servicemodel.basichttpbinding.maxbuffersize" target="_blank">BasicHttpBinding<span xmlns="">.</span>MaxBufferSize</a></p>
<p><a href="http://msdn.microsoft.com/en-us/library/system.servicemodel.basichttpbinding.maxreceivedmessagesize.aspx" target="_blank">BasicHttpBinding<span xmlns="">.</span>MaxReceivedMessageSize</a></p>
<p>En las que podemos establecer el tama&ntilde;o en bytes del buffer y del tama&ntilde;o m&aacute;xiximo del mensaje. En mi caso, he establecido el mismo&nbsp;tama&ntilde;o a las 2 propiedades.</p>
<p>Vale! Ya tenemos claro que hay que modificar estas propiedades para modificar la restricci&oacute;n del tama&ntilde;o de subida, pero...</p>
<h3>&iquest;Donde las cambiamos?</h3>
<p>Buena pregunta, para ello vamos a tener que implementar nuestra factor&iacute;a heredando de la que corresponda en cada caso, yo como uso SharePoint, tengo que usar <strong>MultipleBaseAddressWebServiceHostFactory </strong>que es la que se usa para crear servicios REST en SharePoint.</p>
<h3>&iquest;Por qu&eacute; tengo que implementar&nbsp;mi propia factor&iacute;a?</h3>
<p>Porque necesitamos&nbsp;interceptar cuando la factor&iacute;a abre los endpoints y as&iacute; poder configurar su binding&nbsp;y cambiar estas propiedades o sino no funcionar&aacute;, por ejemplo, si intentas hacer esto con un Custom&nbsp;Behavior no lo conseguir&aacute;s ;)</p>
<p>A continuaci&oacute;n os muestro las clases que he tenido que crear. Lo pirmero es hererdar de <strong>MultipleBaseAddressWebServiceHostFactory </strong>y sobreescribir el m&eacute;todo <strong>CreateServiceHost </strong>para poder crear nuestro propio ServiceHost:</p>
<div dir="ltr" id="CodeDiv">
<pre class="brush: csharp">public class CustomMultipleBaseAddressWebServiceHostFactory : MultipleBaseAddressWebServiceHostFactory
{
    protected override ServiceHost CreateServiceHost(Type serviceType, Uri[] baseAddresses)
    {
        return new CustomMultipleBaseAddressWebServiceHost(serviceType, baseAddresses);
    }
}</pre>
</div>
<p>&nbsp;A continuaci&oacute;n del c&oacute;digo de nuestro ServiceHost que hereda de <strong>MultipleBaseAddressWebServiceHost:</strong></p>
<div dir="ltr" id="CodeDiv">
<pre class="brush: csharp">public class CustomMultipleBaseAddressWebServiceHost : MultipleBaseAddressWebServiceHost
{
    public CustomMultipleBaseAddressWebServiceHost(Type serviceType, params Uri[] baseAddresses) : 
        base(serviceType, baseAddresses)
    {

    }

    protected override void OnOpening()
    {
        base.OnOpening();

        foreach (var endpoint in Description.Endpoints)
        {
            var binding = endpoint.Binding;

            if (binding is WebHttpBinding)
            {
                var web = binding as WebHttpBinding;
                web.MaxBufferSize = TAMA&Ntilde;O EN BYTES;
                web.MaxReceivedMessageSize = TAMA&Ntilde;O EN BYTES;
            }
        } 
    }
}</pre>
</div>
<p><br />Al tratarse de un servicio REST, estoy comprobando que el binding sea WebHttBinding (Estamos exponiendo nuestro servicio por peticiones HTTP y no por mensajes&nbsp;SOAP)&nbsp;y en ese caso establezco el tama&ntilde;o en bytes oportuno (Cuidado con el tama&ntilde;o que se le da, ya hablamos antes que todos estos valores sirven para evitar ataques Dos).</p>
<p>Por &uacute;ltimo falta decirle a nuestro servicio que utilice nuestra factor&iacute;a:</p>
<div dir="ltr" id="CodeDiv">
<pre class="brush: xml">&lt;%@ ServiceHost Language="C#" Debug="true"
    Service="..., ..., Version=1.0.0.0, Culture=neutral, PublicKeyToken=784c41e972d0ad71"  
    Factory="....CustomMultipleBaseAddressWebServiceHostFactory, ..., Version=1.0.0.0, Culture=neutral, PublicKeyToken=784c41e972d0ad71" %&gt;</pre>
</div>
<p>Con esto nuestro servicio ya ha superado la restricci&oacute;n de los 64Kb impuesta por WCF! pero recordad, aunque parezca pesado, no poner un tama&ntilde;o muy grande o podemos sufir ataques DoS.</p>
<p>Hasta aqu&iacute; los post dedicados a la subida de ficheros. Espero que os haya resultado interesante.</p>