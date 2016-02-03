---
ID: 110
post_title: Windows Azure Connect
author: Quiqu3
post_date: 2012-02-06 10:00:12
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/azure-connect/
published: true
---
<p>Este es mi primer art&iacute;culo en programandonet.com, aunque espero que no el &uacute;ltimo. En esta ocasi&oacute;n me gustar&iacute;a hablaros de Windows Azure Connect, uno de tantos servicios que nos ofrece el portal de Windows Azure.</p>
<p></p>
<p>Antes de continuar con Azure Connect, voy a hablaros un poco de Windows Azure, para los que no est&eacute;is al d&iacute;a sobre temas de Cloud Computing.</p>
<p></p>
<p>Windows Azure es la plataforma de Cloud Computing de Microsoft, en dicha plataforma se nos ofrece una gran variedad de servicios, entre estos est&aacute;n el hospedaje de aplicaciones, Bases de Datos Sql, bases de datos no relacionales, maquinas virtuales, Cache, Service bus y muchos m&aacute;s.</p>
<p></p>
<p>Ahora vayamos un poco m&aacute;s all&aacute; de Windows Azure y hablemos un poco del Cloud Computing. A grandes rasgos definimos el Cloud Computing, como el sistema de ofrecer servicios a trav&eacute;s de internet. Para explicarlo mejor pondr&eacute; un ejemplo pr&aacute;ctico que es esto de ofrecer servicios a trav&eacute;s de internet.</p>
<p></p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/windows_azure-1.jpg" alt="" height="341" width="525" align="middle" /></p>
<h3>Por ejemplo</h3>
<p></p>
<p>En una empresa se suelen tener servidores (en una sala o no :P), a estos nos referimos cuando servidores On-premise, son esos a los que tenemos acceso a ellos f&iacute;sicamente.</p>
<p></p>
<h2>&iquest;Que problem&aacute;tica tiene hoy en d&iacute;a tener los servidores On-Premise?</h2>
<p></p>
<p>Como problema t&eacute;cnico ninguno, pero si hablamos de costes, es diferente ya que tener servidores puede llegar a ser muy caro. El hardware, licencias, empleados de IT todo esto sube el precio por cada servidor. Es ah&iacute; donde reside una de las mejores ventajas del Cloud Computing.Tienes servidores en la nube, donde solo pagas 'x &euro;' por cada hora que est&aacute;n encendidos, ya no tienes que pensar en licencias, mantenimiento, instalar actualizaciones del sistema (a no ser que sea que lo necesitas). Todo esto es una ventaja muy grande para las empresas y m&aacute;s en los tiempos en los que de lo primero que prescinde una empresa es la tecnolog&iacute;a.</p>
<p></p>
<p>A priori ninguna, ya que nosotros seguiremos teniendo accesibles todos los aspectos de nuestra m&aacute;quina, solo que ser&aacute; en remoto.</p>
<p></p>
<h2>&iquest;Que es Windows Azure Connect?</h2>
<p></p>
<p>Azure Connect, es un servicio de la plataforma de Azure que nos permite configurar una VPN, entre las m&aacute;quinas que tenemos hospedadas en la nube y las que tenemos en local.</p>
<p></p>
<p>Antes de continuar me gustar&iacute;a definir muy brevemente que es una VPN (Virtual Private Network). Tal y como dice su nombre, una VPN, es una red virtual privada, que une 2 o m&aacute;s puntos que se encuentran en diferentes redes y las conecta de forma segura.</p>
<p></p>
<h3>Podr&iacute;amos tener</h3>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/VPN.png" alt="" height="364" width="805" align="middle" /></p>
<p>Una VPN permite que una aplicaci&oacute;n que tenemos hospedada en nuestra central de Barcelona pueda consumir una base de datos que tenemos en la sede de Paris de forma segura, sin tener que estar as&iacute; en la misma red.</p>
<p></p>
<h2>Una nube h&iacute;brida es mejor que ninguna</h2>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/02/HYBRID-CLOUD-esp.jpg" alt="" height="428" width="428" align="middle" /></p>
<p>No todo es tan bonito como parece cuando hablamos de migrar todo a la nube, ya que cuando llega el momento de hablar con nuestro responsable, nos dice que no se pude invertir ahora mismo en todo ese I+D que se tiene que hacer para migrar todos los servicios de una empresa.</p>
<p></p>
<p>O incluso cuando conseguimos que si nos dejen hacer todo ese I+D, la c&uacute;pula superior tiene miedo de no tener los datos en Local, ya que se pueden perder por internet..</p>
<p></p>
<p>Es ah&iacute; cuando nace el termino de nube hibrida. Nosotros conseguimos tener aplicaciones en la nube y nuestras bases de datos en nuestras salas de servidores o la inversa, nuestra aplicaci&oacute;n esta instalada en local pero consume datos de la nube.</p>
<p></p>
<p>En este segundo caso no tenemos problemas, ya que se puede configurar que el acceso &uacute;nicamente modificando las reglas del firewall de Windows Azure.</p>
<p>&iquest;Que pasa en el primer caso cuando tenemos una aplicaci&oacute;n publicada en la nube y queremos consumir los datos que tenemos en otro punto fuera de esta?.</p>
<p></p>
<p>Ah&iacute; es donde entra la VPN que nos configuramos con Windows Azure, ya que siguiendo los paso que a continuaci&oacute;n vamos a detallar no tendremos ning&uacute;n problema.</p>
<p></p>
<h3>Si miramos este esquema:</h3>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/connect.png" alt="" height="300" width="588" align="middle" /></p>
<p>En este esquema podemos ver de forma visual la problem&aacute;tica del caso 1.</p>
<p></p>
<h2>Como configurar Azure Connect</h2>
<p></p>
<p>Lo primero que debemos saber es cual de nuestros proyectos tiene que tener una VPN con uno de nuestros servidores. Una vez esto, vamos al portal de Windows Azure, una vez all&iacute;:</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/menuAzure.png" alt="" height="525" width="212" align="middle" /></p>
<p>Vemos el men&uacute; de la izquierda de nuestro portal, lo primero que tenemos que hacer ir a la &uacute;ltima secci&oacute;n "Red virtual", all&iacute; nos encontramos con las siguientes opciones:</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/azureconnectmenu.png" alt="" height="124" width="285" align="middle" /></p>
<p>Aqu&iacute; podemos ver que tenemos 2 opciones activadas:</p>
<p></p>
<ul>
<li>Instalar extremo local: Esta opci&oacute;n es la que nos va a permitir configurar la parte de las m&aacute;quinas On-premise.</li>
</ul>
<p></p>
<ul>
<li>Obtener token de activaci&oacute;n: Esta opci&oacute;n es la que nos permite configurar la VPN dentro del servicio queremos publicar en Azure.</li>
</ul>
<p></p>
<p>Pulsamos en esta &uacute;ltima, y una nueva venta aparece para darnos la opci&oacute;n de copiar en token:</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/popup.png" alt="" height="267" width="611" align="middle" /></p>
<p>Ahora solo tenemos que copiar este token, y dirigirnos a nuestra soluci&oacute;n de Visual Studio.</p>
<p></p>
<p>Una vez all&iacute;, vamos a las propiedades del role de nuestra soluci&oacute;n:</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/vsconfig.png" alt="" height="287" width="802" align="middle" /></p>
<p>Y en la pesta&ntilde;a de "Virtual Network" pegamos el token que con anterioridad hemos copiado del portal de Windows Azure. &Uacute;nicamente con este paso, al publicar la soluci&oacute;n en la nube, nuestra soluci&oacute;n ya instalar&aacute; todo lo necesario para que este extremo tenga la VPN configurada.</p>
<p></p>
<p>Ahora el siguiente paso a seguir, es configurar las m&aacute;quinas On-premise, que queremos que se puedan comunicar de forma segura con nuestro servicio de la nube. Para ello, volvemos al portal de Windows Azure y est&aacute; vez pulsamos en el primer enlace (Instalar extremo local).</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/azureconnectmenu.png" alt="" height="124" width="285" align="middle" /></p>
<p>Al pulsar en esta opci&oacute;n volveremos a ver una nueva pantalla, en la que nos permitir&aacute; copiar un link personalizado para instalar la configuraci&oacute;n de nuestra VPN, en las maquinas locales.</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/tokenlocal.png" alt="" height="249" width="611" align="middle" /></p>
<p>Ahora lo &uacute;nico que tenemos que hacer es copiar el link, y abrirlo en un IE (Internet explorer), sino ver&eacute;is un mensaje en diciendo que el navegador no es compatible.</p>
<p></p>
<p>Una vez esto, descargaremos un fichero autom&aacute;ticamente, que al ejecutarlo, iniciaremos el proceso de instalaci&oacute;n del cliente de Azure Connect.</p>
<p><img src="/wp-content/uploads/2012/09/Captura.PNG" alt="" height="442" width="566" align="middle" /></p>
<p>Una vez instalado, nos tenemos que volver a dirigir al portal de Windows Azure, esta vez para configurar un grupo dentro de nuestra Red privada.</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/menuroles2.png" alt="" height="120" width="290" align="middle" /></p>
<p>Ahora pulsamos en el bot&oacute;n de Crear grupo, al hacerlo como en las otras opciones del men&uacute;, se abrir&aacute; una venta para crear el grupo.</p>
<p><img style="display: block; margin-left: auto; margin-right: auto;" src="/wp-content/uploads/2012/09/roels.png" alt="" height="385" width="565" align="middle" /></p>
<p>Aqu&iacute; lo &uacute;nico que tenemos que hacer es dar un nombre al grupo y agregar las maquinas On-Premise y los servicios que hemos publicado en Windows Azure.</p>
<p></p>
<p>Al pulsar en crear, autom&aacute;ticamente todas las maquinas, est&eacute;n en local o en la nube se ver&aacute;n entre ellas.</p>
<p></p>
<p>&iexcl;Listo! Tenemos montada una VPN entre nuestras maquinas On-Premise y nuestras maquinas de la nube.</p>
<p></p>
<h2>Conclusiones sobre Windows Azure Connect</h2>
<p></p>
<p></p>
<p>Desde mi punto de vista es un servicio con una gran utilidad ya que nos permite de una forma f&aacute;cil, poder montar una VPN, a un coste asequible y en muy poco tiempo.</p>
<p></p>
<p>Adem&aacute;s con la problem&aacute;tica que hoy en d&iacute;a muestran muchas empresas con tener sus datos fuera de la oficina, este servicio nos libera de la problem&aacute;tica de configurar la VPN entre la aplicaci&oacute;n y la BBDD sin tener que tirar de m&aacute;s hardware ni grandes especialistas en redes.</p>
<p></p>
<p>Otro de los usos que le podemos dar, es para montarnos un entorno para realizar pruebas de carga contra aplicaciones web que tenemos publicadas en internet.</p>
<p></p>
<p>Esta ultima utilidad ser&aacute; mi siguiente post :D</p>
<p></p>