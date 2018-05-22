# Ejercicios tema 3(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T3.1 Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

**Manipulación de tablas de enrutamiento en window**

ROUTE [-f] [-p] [-4|-6] comando [destino] [MASK máscara_red] [puerta_enlace]  [METRIC métrica] [IF interfaz]
   * -f    Borra las tablas de enrutamiento de todas las entradas de puerta de enlace. Si se usa junto con uno de los comandos, se borrarán las tablas antes de ejecutarse el comando.
   * -p    Cuando se usa con el comando ADD, hace una ruta persistente en los arranques del sistema. De manera predeterminada, las rutas no se conservan cuando se reinicia el sistema. 		Se pasa por alto para todos los demás comandos, que siempre afectan a las rutas persistentes apropiadas. Esta opción no puede utilizarse en Windows 95.
   * -4    Forzar el uso de IPv4.
   * -6    Forzar el uso de IPv6.
   *  comando es alguno de los siguientes:
        PRINT. Imprime una ruta
        ADD. Agrega una ruta
        DELETE. Elimina una ruta
        CHANGE. Modifica una ruta existente.  Solo se utiliza para cambiar la puerta de enlace o la métrica.
   * destino. Especifica el host.
   * MASK. Especifica que el siguiente parámetro es el valor de "máscara_red'.
   * máscara_red. Especifica un valor de máscara de subred para esta entrada de ruta. Si no se especifica, se usa de forma predeterminada el valor 255.255.255.255.
   * puerta_enlace. Especifica la puerta de enlace.
   * interfaz. El número de interfaz para la ruta especificada. Si no se proporciona intenta buscar la mejor interfaz para una puerta de enlace específica.
   * METRIC. Especifica la métrica; por ejemplo, costo para el destino.

Todos los nombres simbólicos usados para el destino se consultan en el archivo de base de datos de red, NETWORKS. Los nombres simbólicos para la puerta de enlace se consultan en el archivo de base de datos de nombre de host, HOSTS.
Si el comando es PRINT o DELETE, destino o puerta_enlace pueden ser un carácter comodín, (se especifica como un asterisco '*') o se puede omitir el argumento puerta_enlace.
Si destino contiene un carácter * o ?, se tratará como un modelo del shell y sólo se imprimirán las rutas de destino coincidentes. El carácter '*' coincide con cualquier cadena y '?' coincide con cualquier carácter. Ejemplos: 157.*.1, 157.*, 127.*, *224*.
La coincidencia de patrones sólo se permite en el comando PRINT.
Si MASK no es válido se genera un error, como cuando (DEST & MASK) != DEST

    Ejemplo-> route ADD 157.0.0.0 MASK 155.0.0.0 157.55.80.1 IF 1
    Error al agregar la ruta: El parámetro de máscara especificado no es válido. (Destino & Máscara) != Destino.

Ejemplos:
    - route PRINT Imprimire toda la tabla de enrutamiento

    - route PRINT -4 ->Imprime la tabla de enrutamiento con las rutas de IPv4.

    - route PRINT -6 -> Imprime la tabla de enrutamiento con las rutas de IPv6

    - route PRINT 157* ->Imprime lo que coincida con 157*

    - route ADD 157.0.0.0 MASK 255.0.0.0  157.55.80.1 METRIC 3 IF 2 ->Añade la ruta especificada con la metrica 3 y el interfaz 2

    - route ADD 3ffe::/32 3ffe::1

    - route CHANGE 157.0.0.0 MASK 255.0.0.0 157.55.80.5 METRIC 2 IF 2 ->Cambia una ruta existente

    - route DELETE 157.0.0.0 -> Borra la ruta

    - route DELETE 3ffe::/32 -> Borra la ruta


**Manipulación de tablas de enrutamiento en linux**

Mediante el comando route.
El comando route muestra la tabla de enrutamiento que reside en el kernel y también se usa para modificarla. La tabla que especifica cómo se enrutan los paquetes a un host se llama tabla de enrutamiento.

OPCIONES:
-n 	Muestra la tabla de enrutamiento en formato numérico [dirección IP]
-e 	Muestra la tabla de enrutamiento en formato hostname
add 	Añade una nueva ruta a la tabla de enrutamiento
del 	Elimina una ruta de la tabla de enrutamiento

    -host 	Indica que el objetivo es un host
    -gw 	Especifica el puerta de enlace del host o red objetivo
    -netmask 	Usado para especificar la máscara de subred del host o red de destino
    -dev 	Especifica el dispositivo o interfaz donde se enviarán los paquetes
    -reject 	Rechaza los paquetes enviados a una ruta o host particular

    EJEMPLO:
    1.Para mostrar la tabla de enrutamiento: route -n
    El comando anterior mostrará: 


![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/3.1.jpg)


    2.Para añadir ruta estática a una red en la tabla de enrutamiento:
    route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1 dev eth0 

![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/3.1.2.jpg)  

    3.Para eliminar una ruta de la tabla de enrutamiento:
    route del -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1 dev eth0


---

**Ejercicio T3.2 Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

**Windows**

    La Plataforma de filtrado de Windows (WFP) permite a los proveedores de software independientes (ISV) filtrar y modificar los paquetes de TCP/IP, supervisar o autorizar conexiones, filtrar tráfico protegido por protocolos de seguridad de internet (IPsec) y filtrar las llamadas a procedimiento remoto (RPC). 

    También en windows dispone de un firewall con el cual, podemos establecer un conjunto de reglas para bloquear y filtrar paquetes. Dicho servicio se puede utilizar mediante una interfaz gráfica.

**Linux**
  
  En Linux, el filtrado de paquetes está programado en el núcleo.Los núcleos de Linux han ido evolucionando y con él su firewall, cambiando su implementación
	en las sucesivas versiones. Así, actualmente se utiliza el módulo NetFilter como firewall de filtrado de paquetes, el cual, junto con la herramienta iptables
	 permite establecer las reglas de filtrado. El entornoNetfilter permite el filtrado de paquetes (ya sea con o sin estado), la traslación de direcciones y puertos
	(NAT /NAPT) y otras manipulaciones sobre el datagrama IP (packet mangling).

--- 

[No hay más ejercicios propuestos para este tema]

--- 

##  FIN ejercicios tema 3
