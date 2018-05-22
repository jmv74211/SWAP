# Ejercicios tema 4(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T4.1 Buscar información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja webde unas prestaciones similares**

No he encontrado dicha información, dado que la tendencia en la actualidad es utilizar granjas web, y las especificaciones técnicas que he leído de los mainframe no vienen en términos de hardware. Sin embargo, he encontrado un artículo en el que la NASA ha reemplazado su último mainframe debido a lo siguiente:

Los primeros computadores comerciales, como el IBM 701, tuvieron un gran calado dentro del ámbito gubernamental y solían instalarse en instalaciones de investigación vinculadas a la defensa militar estadounidense o en centros de investigación. Poco a poco, estos mainframes que eran capaces de procesar gran cantidad de datos comenzaron a encontrar su lugar en el seno de las empresas (transacciones bancarias, contabilidad, nóminas, etc) pero siempre siguieron vinculadas a la investigación y al cálculo numérico gracias a su capacidad de proceso, su fiabilidad, soporte y robustez y, sobre todo, su orientación a transacciones. Sin embargo, el transcurrir de los años ha ido dejando paso a otras tecnologías (virtualización, supercomputación, etc) que han ido dejando a un lado a los grandes mainframes para dar paso a grandes granjas de sevidores. La NASA, originalmente, también disponía de mainframes que, poco a poco, se han ido sustituyendo por otros dispositivos y, el pasado sábado, la Agencia Espacial apagó el último mainframe que tenía en activo.

"Los mainframes, honestamente, no son tan malos y tienen su lugar. Cosas como la virtualización, los hipervisores, los thin clients son algo que nos una novedad para los que usamos mainframes pero sí que son una tendencia para las nuevas generaciones".

**Referencias**

[https://hipertextual.com/2012/02/la-nasa-apaga-ultimo-mainframe]

--- 

**Ejercicio T4.2 Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros.** 

Podemos ver como el precio varía desde los 4000$ hasta los 58000$ de un modelo a otro, mejorando las siguientes características.
 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.2.jpg)


En este caso podemos ver una comparativa entre unos modelos u otros aunque no muestra el precio debido a no disponibilidad de ellos.
 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.2.2.jpg)


**Referencias**

[https://kemptechnologies.com/server-load-balancing-appliances/product-matrix.html/

[https://www.barracuda.com/products/loadbalancer/models/compare/1?models=642,840,841,842]

---

**Ejercicio T4.3: Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.**

En la hoja de especificaciones técnicas de los balanceadores de carga barracuda podemos encontrarnos los siguientes datos:

• Balanceo de carga de capas 4 y 7
• Compatibilidad con IPv6/IPv4
• Alta disponibilidad activo/pasivo
• Balanceo de carga predeterminado
  –Round Robin
  –Round Robin ponderado
  –Least connection
• Balanceo de carga adaptable 
mediante carga de CPU, carga 
de URL y sesiones de terminal
• Persistencia de sesiones y 
grupos de servicios
• Health check y monitorización del 
estado del servido



Para más información
[https://assets.barracuda.com/assets/docs/dms/Barracuda_Load_Balancer_ADC_DS_ES.pdf]

---

**Ejercicio T4.4: Instala y configura en una máquina virtual el balanceador ZenLoadBalancer**

**Definición:**

Zen load Balancer es un Balanceador de carga de licencia Open Source, es un software con una interfaz gráfica de configuración. Tiene una versión libre y una versión de pago que incluye el mantenimiento del balanceador.

**Instalación:**

Para empezar la isntalación podemos descargarnos la iso de desde su página oficial
http://www.zenloadbalancer.com/community/downloads/ y una vez la tengamos descargada instalamos como si fuera la instalación de un sistema operativo, zen load balancer esta integrado en una iso con debian squeeze.

Cuando se inicia la instalación nos sale como si estuviéramos instalando una máquina normal:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.1.jpg)

Continuamos con la instalación normal hasta que nos pida que le introduzcamos la IP de la máquina que vayamos a utilizar, normalmente en un distro de linux cualquiera intentaría coger por DHCP pero en este caso la introduciremos manualmente para que quede siempre con esa IP y facilite la configuración. Después esto la instalación es típica de una instalación de linux.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.3.jpg)

**Acceso al panel web.**

Una vez terminada la instalación debemos de irnos al navegador web y poner la dirección IP que hemos puesto antes pero debemos de acceder mediante “https” y por el puerto “444”como por
ejemplo:

https://192.168.130.24:444/

El usuario y la contraseña por defecto son “admin” y “admin”.

Un a vez que accedemos por el navegador, vemos que nos aparecen unas gráficas que es información sobre es uso del balanceador, memoria, carga, trafico de red o las granjas de servidores.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.4.jpg)

**Configuración del Cluster.**

Como tenemos dos servidores con el balanceador de carga por motivos de alta desponibilidad, debemos de configurar un cluster entre ellos para que trabajen como uno y si se cae uno de los dos pueda seguir trabajando y el sistema siga funcionando. Si nos fijamos vemos como en la parte superior nos dice que no tenemos configurado el cluster, esto es porque Zen Load Balancer recomienda de que haya mas de un balanceador por precaución. En primer lugar nos vamos al menú de configuración y hacemos clic en Settings > Cluster.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.5.jpg)

Hacemos clic en “crear una nueva IP virtual”, a partir de que tengamos el cluster funcionando accederemos a esta IP y no a las físicas de las máquinas.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.6.jpg)

Guardamos la configuración y volvemos a hacer clic en “settings > cluster” y seleccionamos la IP virtual que acabamos de crear.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.7.jpg)

Pinchamos en “Save IP” e iniciamos la configuración del cluster y rellenamos el siguiente formulario.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.8.jpg)

Cuando guardamos la configuración se nos desglosa automáticamente mas opciones que tenemos que rellenar, como la contraseña de ROOT del otro servidor y el tipo de cluster que lo podremos que ambos sean maestro.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.9.jpg)

Luego volvemos a cargar y ya no nos aparecerá el mensaje que nos aparecía antes en la parte superior de la página.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.10.jpg)

**Creación de las Granjas.**

Ya hemos configurado el cluster entre los dos nodos de balanceadores, ahora lo que debemos de hacer es configurar las granjas de servidores a las cuales los balanceadores enviaran las peticiones. Estas granjas consisten en agrupar los servidores por los servicios que van a dar. En primer lugar lo que debemos de hacer es irnos al menú de arriba y hacer clic en “Manage” >“Farms”:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.11.jpg)

A continuación escribimos el nombre de la granja que vamos a crear y el perfil que va a tener dicha granja (http, udp, tcp, etc).

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.12.jpg)

Hacemos clic en “Save & continue” nos aparecerá nuevo campos de texto a rellenar en el cual especificamos la IP Virtual que hemos creado anteriormente y especificamos el puerto por el que irá el tráfico.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.13.jpg)

Ahora nos aparecerá que la granja ha sido creada correctamente y nos muestra información sobre la misma.

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.14.jpg)

A continuación vamos a hacer clic en el botón de editar que se encuentra en acciones y nos aparecerá la configuración de la granja que podemos modificar como queramos. Nos vamos al final y hacemos clic en “Add service” después de poner el nombre del nuevo servicio:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.15.jpg)

Nos aparecera un cuerpo nuevo en la página en el cual añadiremos los servidores (IP’s) que vamos a usar. Como podemos ver no permite elegir el tipo de persistencia de sesión, que podrá ser por IP, cookies url, etc. En este caso escogeremos por cookie:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.16.jpg)

Luego nos vamos para abajo y en acciones añadimos un nuevo servidor real que ya tengamos preparado para este fin, poniendo la IP y el puerto que va a usar, también podemos elegir el “timeout” y el “weight” pero lo dejaremos en blanco por el momento, luego hacemos clic en guardar y realizamos esto tantas veces como servidores queramos añadir:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.17.jpg)

Una vez agregado todos los servidores debemos de reiniciar la granja como se nos indica en en la parte superior de la pagina del balanceador:

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.18.jpg)

**Prueba de funcionamiento.**

Por ultimo lo que tenemos que hacer es irnos al nevegador y poner la IP virtual con la que trabaja el balanceador o el dominio si lo hemos metido en DNS

 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.19.jpg)
 ![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.4.20.jpg)


**Referencias**

[https://titaniumsystem.es/2016/01/zen-load-balancer/]

---

**Ejercicio T4.5:Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?**

**Redirección HTTP:** Este metodo se puede usar avisando al usuario que cambiaste de servidor o que la url ha cambiado y llevarlo a la url correcta, podemos dar un tiempo de recarga cambiando el valor de content.

**Redirección con PHP:** Al redireccionar con PHP el usuario puede que no note que lo llevaste a otra página, siempre y cuando sea de tu mismo dominio, la redirección con este método puede y sera más segura para ti y tu sitio web pero para los usuarios puede ser más intrusiva ya que no se les esta avisando del rediereccionamiento, sobre todo si los llevas a una página que podría ser desconocida.

**Redireccionar con JavaScript:** A pesar que se realiza del lado del cliente, puede llegar a danos menos problemas si no tenemos acceso al servidor o nuestro sitio web es muy sencillo y no deseamos usar las etiquetas metas, podemos hacer el redireccionamiento con un retraso usando funciones adicionales.

Creo que el mejor método de redireccionamiento sería con **PHP**, porque puede ser el más seguro, y el más rápido entre servidores.

---

**Ejercicio T4.6 Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario.**

La IANA es la responsable de coordinar el espacio de direcciones IP a nivel mundial. Hoy en día existen 2 tipos principalmente: IPs de versión 4 e IPs de versión 6.

En la web de la IANA se puede encontrar el espacio de direcciones y su estructura en IPv6 . Como ejemplo:

El espacio de direcciones 2000::/3 está destinado a direcciones unicast globales.
Existen otros espacios de direcciones para multicast,  direccuibes unicast locales y para enlaces locales.

Las direcciones se asignan jerárquicamente. En general:

La IANA reparte bloques IP entre los diferentes registros de internet regionales o RIR. Existen 5 englobados por continentes. Para España, el RIR de referencia es el RIPE NCC.
En segundo lugar las RIR reparten bloques de IP a los proveedores de servicio o ISP. Podemos ver la lista de miembros (local internet registries) asociados a RIPE en España
En última estancia, los ISP reparten las direcciones IP a los usuarios finales.

Como curiosidad, en la propia página del RIPE podemos introducir una IP pública y conocer, entre otros datos, a que ISP pertenece. También podemos ver un mapa de geolocalización de las IP de la red al que pertenece la nuestra.

![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/4.6.1.jpg)]

Por lo visto parecen bloques destinados a la zona del levante Español. Pertenece a un bloque asignado al operador de /14, que daría espacio para más de 260.000 direcciones.

**Código PHP para detectar la zona geográfica.**

    function locateIp($ip){

        $d = file_get_contents("http://iplocationtools.com/ip_query.php?ip=$ip&output=raw");

        if (!$d)

            return false; // error al abrir conexion

        $d= explode(",",$d);

        if ($d[1] != 'OK')

            return false; // codigo de estatus no valido

        $country_code = $d[2];

        $country_name = $d[3];

        $region_name = $d[5];

        $city = $d[6];

        //$zippostalcode = $answer->ZipPostalCode;

        $latitude = $d[8];

        $longitude = $d[9];

        // Devuelve datos como array

        return array('latitude' => $latitude, 'longitude' => $longitude, 'city' => $city, 'region_name' => $region_name, 'country_name' => $country_name, 'country_code' => $country_code, 'ip' => $ip);
    }


**Para obtener la IP del visitante.**

    function getIP(){

        if( isset( $_SERVER['HTTP_X_FORWARDED_FOR'] )) $ip = $_SERVER['HTTP_X_FORWARDED_FOR'];

        else if( isset( $_SERVER ['HTTP_VIA'] ))  $ip = $_SERVER['HTTP_VIA'];

        else if( isset( $_SERVER ['REMOTE_ADDR'] ))  $ip = $_SERVER['REMOTE_ADDR'];

        else $ip = null ;

        return $ip;
}


**// Para obtener la IP del propio servidor**


    function ownIP(){

         $ip= file_get_contents('http://myip.eu/');

         $ip= substr($ip,strpos($ip,'<font size=5>')+14);

         $ip= substr($ip,0,strpos($ip,'<br'));

         return $ip;
    }
 

**Referencias**

[http://digitta.com/2009/04/codigo-php-para-mostrar-la-ubicacion-de.html]
[https://danitic.wordpress.com/2018/03/29/como-se-reparten-las-direcciones-ip/]

---

**Ejercicio T4.7:Buscar información sobre métodos y herramientas para implementar GSLB.s**

**Global Server Load Balancing (GLSB)**
Se trata de una serie de técnicas para distribuir la carga entre varios centros de datos. De esta forma evitamos retrasos en las comunicaciones por las distancias entre el usuario y el servidor. Además, debido a la redundancia, si un centro falla, el tráfico se redirige a otro centro de datos.
Hay varias implementaciones posibles, con mayor o menor complejidad:
 - Uso del sistema de DNS
 - Redirección HTTP
 - GSLB basado en DNS
 - GSLB usando protocolos de enrutamiento

**Referencias**

[http://swap-ugr.blogspot.com.es/2015/03/tema-4-de-teoria-balanceo-de-carga.html]

---

[No hay más ejercicios propuestos para este tema]

--- 

##  FIN ejercicios tema 4
