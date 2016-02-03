---
ID: 720
post_title: Scrum con TFS
author: fernandoescolar
post_date: 2013-01-23 09:13:27
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/scrum-con-tfs/
published: true
---
<p>En los últimos años estamos asistiendo a un cambio radical en la forma de gestionar los proyectos de desarrollo de software. Empieza a resultar extraño encontrar ofertas de trabajo en las que no se mencione scrum, o proyectos que empiecen en los que no se haya planteado el uso de metodologías ágiles. Pero de nada nos sirve una metodología, por muy buena que pueda ser, si perdemos más tiempo gestionando el proceso que programando. Por lo que nos vemos casi obligados a empezar a usar herramientas que nos ayuden con esta tarea. A lo largo de este artículo trataremos una de esas herramientas, que consideramos más potentes: TFS.</p> <h3>Team Foundation Server/Service</h3> <p>Las siglas TFS pueden significar Team Foundation Server o Team Foundation Service. En ambos casos se trata del mismo producto, pero en diferentes formas de distribución.</p> <p>Este software es la herramienta que nos ayudará con la gestión del ciclo de vida de aplicaciones (ALM), propuesta por Microsoft. TFS nos aportará una serie de utilidades que nos facilitarán la gestión de los procesos, el control de versiones del código fuente, el testing de aplicaciones, el deploy, y además nos aportará diferentes informes sobre todo esto.</p> <p>Las dos formas de distribución en las que podemos encontrar TFS hoy en día son:</p> <ul> <li><strong>On-premises</strong>: la modalidad de distribución de software tradicional que podemos instalar en nuestras propias máquinas, tantas veces como licencias hayamos adquirido. En resumen, la forma en la que siempre hemos comprado software, que recibe el nombre de <strong>Team Foundation Server 2012</strong>. </li></ul> <ul> <li><strong>Saas</strong>: que significa Software as a service, una modalidad de venta de un software que en lugar de instalarlo, lo utilizamos directamente sin preocuparnos por la infraestructura. Por lo general esto implica que ya no tendremos que realizar un desembolso económico grande para usar un producto, solo pagaremos por lo que consumamos. Esta versión recibe el nombre de <strong>Team Foundation Service</strong> y por ahora, permanece gratuita para equipos de hasta 5 miembros. </li></ul> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/TFS-Saas.png"><img title="TFS-Saas" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="TFS-Saas" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/TFS-Saas_thumb.png" width="589" height="143"></a></p> <p>Las diferencias entre ambas versiones sobre todo radican en que la versión on-premises permite la personalización de las plantillas de procesos y tiene una mejor herramienta de generación de informes. Pero para el proceso que vamos a describir a continuación es indiferente cual de estas utilizar.</p> <p>En los ejemplos que veremos a lo largo de este artículo hemos utilizado la versión Saas: Team Foundation Service. Para ello nos dirigimos primero a la página oficial: <a href="http://tfs.visualstudio.com" target="_blank">tfs.visualstudio.com</a>. Allí nos dimos de alta y creamos una nueva cuenta:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/singup.png"><img title="singup" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="singup" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/singup_thumb.png" width="566" height="339"></a></p> <p>En nuestro caso usamos el nombre de “programandonet” con una cuenta de Live ID que ya teníamos anteriormente. Una vez has finalizado el proceso, al entrar en: <u>misitio.visualstudio.com</u>, deberíamos encontrarnos algo parecido a esto:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/portal.png"><img title="portal" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="portal" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/portal_thumb.png" width="703" height="388"></a></p> <p>En nuestro caso ya tenemos algunos proyectos creados, pero si es la primera vez, para poder seguir los ejemplos, deberíamos crear un proyecto nuevo, presionando el botón de “New Team Project”, y usando la plantilla de scrum:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/new-project.png"><img title="new-project" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="new-project" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/new-project_thumb.png" width="517" height="440"></a></p> <p>Para poder entender mejor la plantilla de proceso que estamos usando, primero tendremos que definir la metodología que tenemos pensado usar: scrum.</p> <h3>¿Qué es scrum?</h3> <p>Podríamos definir <strong>scrum</strong> como un marco de trabajo, un conjunto de herramientas y protocolos a seguir con el fin de obtener un objetivo común: el éxito de un proyecto. Una metodología ágil que a pesar de estar enfocada en el desarrollo de software, es aplicable también a muchos otros campos como por ejemplo, el desarrollo de un vehículo de Formula 1.</p> <p>La idea de un desarrollo ágil se fundamenta en la reducción de riesgos basándose en la división de un gran problema en problemas más pequeños. Estas divisiones serán acometidas como proyectos en si mismas, que deberán ser desarrollados a lo largo de un corto espacio de tiempo. A este ciclo se le denomina iteración y está compuesto por las fases de: planificación, análisis, diseño, codificación, revisión y documentación. Una vez finalizamos una iteración, se realiza una retrospectiva de cómo han ido las cosas, y se empieza una nueva iteración con las mejoras que se han propuesto.</p> <p>Básicamente se asume que en un proyecto no todo va a ser como podemos pensar en un principio. Nos vamos a encontrar problemas no previstos y los requisitos van a cambiar con el paso del tiempo. Ante estos cambios lo único que podemos hacer es adaptarnos. Por esta razón dividimos el proyecto: para que las cosas que pueden ir mal vayan mal pronto, y así podamos ir afinando el proceso antes de que sea demasiado tarde.</p> <p>Dentro de scrum estas iteraciones reciben el nombre de <strong>sprints</strong> y suelen durar de 2 a 4 semanas. El objetivo de cada sprint es que al finalizarlo, el equipo haya conseguido un producto potencialmente entregable. Es decir, algo que funcione, que se pueda probar y sobre lo que se puedan proponer modificaciones.</p> <h3>Roles</h3> <p>Antes de comenzar a trabajar debemos definir los roles de los diferentes miembros del proyecto. Scrum divide en dos grandes grupos de participantes:</p> <p>Los <strong>comprometidos</strong> por el proyecto:</p> <ul> <li><strong>Product owner</strong>: representa a cliente, a las personas que han solicitado el producto resultante de este proyecto. Es quien marca los requisitos y gestiona la prioridad de estos. </li></ul> <ul> <li><strong>ScrumMaster</strong>: es la persona responsable de que el proceso de scrum se ejecute correctamente. Se asegura de que se respeten las reglas y aísla al equipo de cualquier influencia externa. No hay que confundir este rol con el de jefe de equipo o project manager. </li></ul> <ul> <li><strong>El equipo</strong>: es el grupo de personas que tiene la responsabilidad del desarrollo del producto. Se auto-organiza, por esa razón no existe ningún rol de líder o jefe. Por lo general debe ser multidisciplinario, un conjunto de no más de 8 personas que puedan abarcar todas las tareas que conlleva el proyecto: análisis, diseño, desarrollo, pruebas, … </li></ul> <p>Y los <strong>implicados</strong> con el proyecto;</p> <ul> <li><strong>Stakeholders</strong> (partes implicadas): Es esa gente que hace el proyecto posible, los implicados de alguna manera con el resultado del desarrollo. Los clientes, vendedores, usuarios finales… </li></ul> <ul> <li><strong>Administradores</strong>: Es la gente que se encuentra jerárquicamente por encima del proyecto. Los gerentes y managers que establecen el ambiente para el desarrollo. </li></ul> <p>En lo que respecta a la gestión que deberíamos realizar, solo serían relevantes los perfiles comprometidos con el proyecto. Para añadirlos a TFS lo primero que tendríamos que hacer es crear un equipo de trabajo. Para ello nos tendremos que dirigir al portal web principal de nuestro sitio de TFS (<u>misitio.visualstudio.com</u>), y dentro de este, al panel de configuración. Esto se hace presionando en el icono con forma de rueda, arriba a la derecha:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/configuration.png"><img title="configuration" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="configuration" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/configuration_thumb.png" width="218" height="44"></a></p> <p>Si no lo hemos hecho ya, nos aparecerá una pantalla para que seleccionemos el proyecto que queremos configurar. Y al seleccionarlo, veremos que automáticamente el sistema nos ha creado un equipo con el mismo nombre que nuestro proyecto. Al presionar sobre este equipo podremos gestionar los miembros del mismo:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/02/team-management.png"><img title="team-management" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; border-left: 0px; display: block; padding-right: 0px; margin-right: auto" border="0" alt="team-management" src="http://www.dotnetodology.com/wp-content/uploads/2013/02/team-management_thumb.png" width="725" height="316"></a></p> <p>En este caso, hemos añadido a todo nuestro equipo de desarrollo que está formado por 4 personas.</p> <p>Otra forma que tenemos de realizar esta operación es entrar en la página “home” (dashboard) de nuestro proyecto y fijarnos en el panel de equipo de nuestra derecha. Haciendo clic en “Manage all members…”:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/dashboard-team.png"><img title="dashboard-team" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="dashboard-team" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/dashboard-team_thumb.png" width="743" height="392"></a></p> <p>&nbsp;</p> <h3>El proceso</h3> <p>Como hemos comentado anteriormente, scrum es iterativo. Se divide en una serie de sprints que se van realizando hasta el momento en el que el proyecto se considera terminado. Una forma rápida de explicar el proceso sería el siguiente gráfico:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/scrum-proceso.png"><img title="scrum-proceso" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="scrum-proceso" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/scrum-proceso_thumb.png" width="589" height="294"></a></p> <p>Aquí se puede observar que todo el proceso se inicia con la recogida de requisitos, y terminará cuando el resultado del feedback proporcionado por las partes implicadas sea que el producto está terminado.</p> <h4>Gestión del backlog</h4> <p>Asumimos que ya están todos los roles preparados para empezar con el proyecto, o al menos ya tenemos una figura de Product Owner, el propietario del producto. Entonces es el momento de empezar a recopilar requisitos. El product owner, además de ser la voz de nuestro cliente, también debe ser la persona que ordene y priorice aquellas necesidades que el cliente le ha comunicado.</p> <p>Todos los requisitos relacionados con la aplicación, se recogen en un listado priorizado que recibe el nombre de pila de producto o <strong>Backlog</strong>. Y los elementos que encontramos en este backlog se denominan “<strong>user stories</strong>” o historias de usuario. Estas historias no son más que requisitos únicos, cortos, fácilmente redactarles, y que definen un requisito de forma rápida y en el propio lenguaje del usuario.</p> <p>Es muy común que una historia de usuario esté definida mediante la plantilla:</p> <blockquote> <p><em>As a [<font color="#000000"><strong>user</strong></font>] i want [<font color="#000000"><strong>something</strong></font>] so that [<strong>i can achieve that</strong>]</em></p></blockquote> <p>Donde los parámetros entre corchetes son sustituidos por el rol de la persona que lo solicita, qué es lo que le gustaría que pasará y cual el el objetivo que busca con dicho comportamiento.</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog.png"><img title="backlog" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="backlog" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog_thumb.png" width="760" height="310"></a></p> <p>Para la gestión del backlog, TFS nos ofrece dos herramientas que podremos encontrar en la sección “Work &gt; backlog”. Una es la lista de requisitos como una lista ordenada según prioridad, que podemos ver en la imagen anterior. Y la otra es en forma de tablero, en la que podremos ver visualmente la evolución de las historias de usuario:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog-board.png"><img title="backlog-board" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="backlog-board" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog-board_thumb.png" width="765" height="344"></a></p> <p>En adición, en la parte superior, conforme vayan desarrollándose los sprints, tendremos dos gráficas que nos darán un claro estado del proyecto y de la velocidad de nuestro equipo. Eso siempre y cuando se siga usando TFS en el resto de las fases.</p> <h4>Preparando el entorno</h4> <p>Antes de ponernos a programar, debemos definir nuestro marco de trabajo: responder preguntas como el tiempo del que dispone cada miembro de nuestro equipo, cuanto va a durar cada sprint inicialmente o qué tipo de especialidad tiene cada uno.</p> <p>Una vez tenemos respuesta a estas preguntas tendremos que introducir estos parámetros en el portal de nuestro proyecto de Team Foundation Server.&nbsp; Así pues, en la página principal del proyecto buscaremos a mano derecha la opción de “Configure schedule and iterations…”:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/administration-widget.png"><img title="administration-widget" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="administration-widget" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/administration-widget_thumb.png" width="273" height="160"></a></p> <p>Al&nbsp; hacer clic en esta opción aparecerá una ventana donde podremos decidir qué días tendrán lugar los próximos sprints:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/configure-iterations.png"><img title="configure-iterations" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="configure-iterations" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/configure-iterations_thumb.png" width="593" height="475"></a></p> <p>Tampoco deberíamos obsesionarnos con configurar todos los sprints, ya que la duración de los mismos podría cambiar si el equipo considerara que son, o demasiado breves, o demasiado largos. En este sentido recomendamos mantener consistente la duración y que por lo general tengamos entre ninguno y un solo cambio de duración de un sprint por proyecto. Pero no obstante, creemos que es mejor ir configurando todo sprint a sprint.</p> <p>Otro de los datos que serán muy útiles, sobre todo cuando nos encontramos con equipos multidisciplinares, es el cálculo de capacidades. Una vez tenemos definido el sprint, podemos seleccionarlo dentro de la pestaña “Work” e introducir para cada uno de los miembros del equipo, cual es la actividad que van a desarrollar, el tiempo que van a dedicar al trabajo por día y si tienen vacaciones durante el sprint:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/capacity-planning.png"><img title="capacity-planning" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="capacity-planning" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/capacity-planning_thumb.png" width="677" height="439"></a></p> <p>En realidad es una tarea que no nos tomará más de 10 minuto y a cambio, gracias a estos datos, más adelante, seremos capaces de medir el trabajo que podemos asumir a lo largo de un sprint.</p> <h4>Planificación del sprint</h4> <p>Para comenzar con las liturgias que engloban al equipo, está la reunión de planificación del sprint o “sprint planning”. El resultado de esta reunión debe ser un listado de tareas que se van a desempeñar a lo largo del sprint para conseguir un objetivo marcado.</p> <p>Al principio de la reunión, el product owner deberá explicar el backlog y proponer las historias de usuario más prioritarias. Y el equipo deberá realizar preguntas sobre las dudas que puedan surgir, evaluar estos requisitos y decidir cuales son los que se compromete a entregar a final de sprint.</p> <p>Desde la vista del product backlog del tfs podremos arrastrar los elementos que hemos planificado encima del sprint que les corresponda:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog-dragdrop.png"><img title="backlog-dragdrop" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="backlog-dragdrop" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/backlog-dragdrop_thumb.png" width="709" height="354"></a></p> <p>Y haciendo doble clic en la user story, podremos añadir comentarios con la información extra que recolectemos durante la exposición del product owner.</p> <p>Además de esto, el equipo deberá dividir las historias en tareas. Estas tareas serán estimadas (usando el poker planning, por ejemplo) y en algunos equipos hasta se auto-asignan según las cualidades de cada uno.</p> <p>Así que una vez hemos asignado los elementos del backlog al sprint actual, podemos hacer clic la etiqueta y añadir tareas que dependan de los requisitos. Haciendo doble clic en las tareas podremos añadir detalles sobre su implementación, las estimaciones e incluso a qué actividad se refiere:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/task-edition.png"><img title="task-edition" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="task-edition" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/task-edition_thumb.png" width="588" height="435"></a></p> <p>Lo interesante de asignar la actividad de una tarea es que automáticamente podremos ver en unas barras a la derecha si estamos excediendo el tiempo de trabajo de las personas dedicadas a esas actividades o por el contrario si podríamos comprometernos a realizar más trabajo.</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/capacity-bars.png"><img title="capacity-bars" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="capacity-bars" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/capacity-bars_thumb.png" width="171" height="402"></a></p> <p>Ahora ya tememos todo preparado para que el equipo empiece a trabajar…</p> <h4>Trabajo diario</h4> <p>Dentro de un sprint, dividimos el trabajo por días. El empezar la jornada, aunque algunos equipos lo dejan para el final del día, tiene lugar la daily meeting o standup meeting. Ambas nomenclaturas definen bien este tipo de reuniones ya que se realizan de forma diaria y los asistentes deben estar de pie. Esto responde a que esta reunión tiene que durar un máximo de 15 minutos, y si permaneciéramos sentados la gente se siente cómoda y es más fácil extenderse.</p> <p>A un daily meeting puede asistir cualquier persona interesada, pero solo tendrán voz los roles comprometidos por el proyecto: el equipo, el scrummaster y el product owner. Generalmente se hace una ronda en la que cada uno de los asistentes debe responder a tres preguntas:</p> <ul> <li>¿Qué hice ayer?  <li>¿Qué problemas encontré?  <li>¿Qué voy a hacer hoy? </li></ul> <p>Esto no se hace para controlar a las personas, si no para favorecer la comunicación entre los miembros del equipo. Casi todas las liturgias de scrum van dirigidas a este objetivo. Se sustenta en la premisa de que si hay buena comunicación, es más fácil que las cosas salgan bien.</p> <p>La ubicación de esta reunión debería ser todos los días la misma y a la misma hora, para que no exista duda alguna. Y sería interesante realizarla junto a la scrumboard. Esto es una tabla sobre la que vamos a ir gestionando las tareas del sprint, de la que ya nos habló Albert Cumplido en <a href="http://www.dotnetodology.com/el-taskboard-en-scrum/" target="_blank">este artículo</a>.</p> <p>Team Foundation Server nos proporciona un tablero virtual para scrum que encontraremos en las sección “Work &gt; board”:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/scrumboard.png"><img title="scrumboard" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="scrumboard" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/scrumboard_thumb.png" width="757" height="293"></a></p> <p>Como podemos observar automáticamente nos muestra el tablero del sprint actual y podemos agrupar las tareas por elemento del backlog o por miembro del equipo. La mejor parte de esta scrumboard virtual es que podemos ir moviendo las tareas y estas se irán actualizando en tiempo real. Eso si, en scrum, cuando una tarea se da por terminada (se han cumplido todos los requisitos de la definición de “hecho”), no puede volver atrás. Si por A o por B el desarrollo de esta tarea ha tenido unas consecuencias no esperadas, esto debería repercutir en la aparición de un bug o una nueva historia que subsane los problemas que hayamos generado.</p> <p>Otro de los artefactos relacionados con scrum en particular, y las metodologías ágiles en general, es el burn down chart. Una gráfica que podemos ver en la parte superior derecha de la scrumboard. Al hacer clic sobre ella podremos tener una vista ampliada, en la que se observarán mejor los detalles de la gráfica:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/burndown.png"><img title="burndown" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="burndown" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/burndown_thumb.png" width="520" height="404"></a></p> <p>Es importante que el equipo tenga clara esta gráfica, ya que nos muestra el estado actual del sprint. Si estamos muy por encima de la línea de tendencia ideal es que vamos con retraso y si estamos por debajo, podría significar que hemos sobre-estimado el esfuerzo de las tareas.</p> <p>Pero para que TFS nos muestre todos estos datos de una forma correcta, es necesario que el equipo vaya actualizando las tareas día a día. Y el control de código fuente junto con el Team Explorer de Visual Studio, nos van a ayudar.</p> <p>Bastará con que dentro de Visual Studio, cuando un programador vaya a realizar un checkin, asocie mediante drag ‘n drop, una tarea. Esto se realiza en el panel de “Peding Changes” de la ventana de “Team Explorer”:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/associate-workitem-checkin.png"><img title="associate-workitem-checkin" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="associate-workitem-checkin" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/associate-workitem-checkin_thumb.png" width="753" height="294"></a></p> <p>El punto negativo y que podría resultar tedioso es que el esfuerzo que le hemos dedicado a la tarea, deberemos introducirlo manualmente. Con respecto a este tema, una práctica muy útil es que antes de irnos a casa, cada miembro del equipo debe ser responsable de haber actualizado sus tareas y la scrumboard. O al menos si sería necesario hacerlo antes de cada daily meeting.</p> <p>En scrum no se aceptan tareas con una estimación de duración de más de una jornada de trabajo. Si así fuera, se debería dividir en varias tareas más pequeñas. Por lo que todos los días deberá haber movimiento en la scrumboard.</p> <p>El último punto del trabajo a tener en cuenta desde el punto de vista de TFS sería el Continuous Integration, que tendría lugar con la ayuda de la configuración de los procesos de build. Aunque este punto, quizá lo podamos tratar en un futuro con mucho más detalle.</p> <h4>Revisión del sprint</h4> <p>Una vez hemos llegado a la fecha de finalización del sprint, nos encontramos en el momento de la revisión del trabajo realizado. Tanto si hemos terminado todas las tareas como si no, se deberá informar y apuntar, para tenerlo en cuenta en posteriores sprints.</p> <p>En el proceso de revisión es necesario involucrar a todos lo roles definidos en el proceso de scrum, tanto los implicados como los comprometidos. Se presentará el producto tal y como está en ese momento. Se responden preguntas y se admiten sugerencias.</p> <p>La forma que nos provee TFS de recolectar el feedback de las partes interesadas del proyecto es la herramienta “Microsoft Feedback Client for TFS 2012”. Todo el proceso comienza con la petición de este feedback.</p> <p>Si nos dirigimos a la página “home” de nuestro proyecto de Team Foundation Service, encontraremos en el widget de “Activities”, una opción llamada “Request Feedback”. Al pulsarla, se abrirá una nueva ventana donde se nos permitirá rellenar los detalles de esta petición:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/request-feedback.png"><img title="request-feedback" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="request-feedback" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/request-feedback_thumb.png" width="630" height="523"></a></p> <p>Los tres detalles que nos permite rellenar son: los invitados a dar feedback, la forma de acceder a la aplicación para poder probarla y los elementos que deben tener más en cuenta, por ser los objetivos principales del sprint, a la hora de revisar.</p> <p>El resultado de enviar esta petición será un email a cada uno de los stakeholders especificados, donde se le informará de todo. En este email además encontraremos un enlace para descargar la herramienta de feedback de Microsoft de forma gratuita.</p> <p>Después de instalar el “Microsoft Feedback Client”, al ejecutarlo, lo primero que nos pedirá es la conexión con el TFS:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedbackclient-tfs-connection.png"><img title="feedbackclient-tfs-connection" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="feedbackclient-tfs-connection" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedbackclient-tfs-connection_thumb.png" width="596" height="438"></a></p> <p>Acto seguido la aplicación nos pedirá que abramos la demo de prueba, siguiendo las instrucciones que especificamos anteriormente. Y después irá pasando por todos los elementos que indicamos que se debían revisar, para que el usuario pueda añadir comentarios, capturas de pantalla, notas de voz, …</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedback.png"><img title="feedback" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="feedback" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedback_thumb.png" width="241" height="586"></a></p> <p>Después de enviar el feedback, podremos acceder a él desde el portal de TFS, “Work &gt; work items &gt; Feedback”:</p> <p><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedback-view.png"><img title="feedback-view" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin-left: auto; display: block; padding-right: 0px; border-top-width: 0px; margin-right: auto" border="0" alt="feedback-view" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/feedback-view_thumb.png" width="757" height="340"></a></p> <p>Es muy recomendable que la reunión de revisión sea en persona y con todos los roles a la vez. No obstante, de cualquier forma, también es muy recomendable usar la herramienta de feedback para poder almacenar en TFS todos los datos y así poderlos revisar con más calma. Tanto si la persona que reporta está o no en la reunión.</p> <h4>Retrospectiva&nbsp; del sprint</h4> <p>La última reunión que tiene lugar en a lo largo de un sprint es la retrospectiva. Una vez tenemos el feedback, esta vez reuniremos al scrummaster y el equipo, aunque el product owner puede estar invitado de oyente.</p> <p>A lo largo de esta reunión se debatirán temas como la gráfica de burn down, la velocidad del equipo, las cosas que han ido bien en el sprint, que podría haber ido mejor y lo más importante: que cosas se van a hacer de forma diferente, buscando sacar el mejor resultado, en el siguiente sprint.</p> <p>En esta reunión será muy importante manejar todos los datos que hemos ido recolectando con TFS, e incluso almacenar un resumen con las conclusiones de la reunión también dentro del sistema. De esta forma todo quedará archivado y accesible por todos los miembros del equipo.</p> <p>Es la reunión donde más partido sacaremos a TFS de todas.</p> <p>Al finalizar esta reunión deberemos volver al primer paso del proceso y volver a empezar con el siguiente sprint. Eso si, esta vez habiendo retroalimentado el proceso con la experiencia del sprint anterior.</p> <h3>Conclusiones</h3> <p>Aún sabiendo que scrum varía en cada equipo que se aplica, hemos intentado exponer un proceso lo más aséptico que hemos podido, para observar la potencia de TFS.</p> <p>Hemos de reconocer que <strong>scrum</strong> nos parece un escenario muy bueno para el desarrollo de software. Y en este sentido, tanto <strong>Team Foundation Server 2012</strong> como <strong>Team Foundation Service</strong> han demostrado ser dos herramientas muy completas que nos ayudarán mucho con la gestión del proceso.</p> <p>Todo esto a pesar de que muchos más detalles sobre la personificación del proceso, se nos han quedado en el tintero, como por ejemplo: las builds, la entrega continua, la integración continua, los code reviews o la potencia de las herramientas de testing.</p> <p>Nosotros lo hemos probado y hemos llegado a la conclusión de que nos gusta. Si aún no lo has hecho, te invitamos a que uses una cuenta gratuita de <a href="http://tfs.visualstudio.com" target="_blank">Team Foundation Service</a>, y durante el próximo sprint, realices un seguimiento en paralelo con esta herramienta, para que saques tus propias conclusiones.</p>