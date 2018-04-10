# Práctica 3: Balanceo de carga
## Autor: Jonathan Martín Valera

Software utilizado:  

- Virtualización: VirtualBox -- Versión 5.2.8 r121009 (Qt5.6.2)
- Sistemas operativos: Ubuntu-16.04.4-server-amd64
- UbuntuServer1: 192.168.1.10
- UbuntuServer2: 192.168.1.20
- Cliente: 192.168.1.30
- Balanceador: 192.168.1.100
- Adaptador de red: Bridge

En primer lugar vamos a descargar el software de balanceo de carga. Empezaremos con NGINX. Para su instalación usamos la orden:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/1.jpg)

---

Tras se instalado, procedemos a editar su fichero de configuración. En primer lugar se comprueba si existe:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/2.jpg)

---

Como hemos comprobado, no existe ningún el archivo **/etc/nginx/conf.d/default.conf** por lo que procedemos a crearlo:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/3.jpg)

---

Añadimos la lista de servidores junto con sus IP´s, junto con la siguiente configuración. Por defecto se utiliza el algoritmo de balance Round-robin(por turnos):

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/4.jpg)

---

Para comprobar el correcto balanceo de los servidores, se va a editar el fichero index.html de cada servidor, y se mostará una información descriptiva sobre el servidor que está respondiendo a la petición, por ejemplo, se mostará su nombre.

Contenido del servidor 1

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/6.jpg)

Contenido del servidor 2

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/7.jpg)

---

Posteriormente, iniciamos el servicio con la siguiente orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/5.jpg)

---

La primera vez que iniciamos el servicio nginx e intentamos acceder desde el cliente al balanceador nos mostrará lo siguiente:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/7.1.jpg)

---

Si se nos muestra este mensaje, significa que nginx está funcionando como servidor web y no como balanceador. Para cambiar esto, debemos de editar el archivo **/etc/nginx/nginx.conf** y comentar la siguiente línea:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/8.jpg)

---

A continuación reiniciamos el servicio nginx mediante la siguiente orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/9.jpg)

---

Finalmente, enviamos las peticiones desde el cliente y comprobamos que cada servidor responderá a nuestra petición alternativamente (siguiendo el algoritmo Round-robin):

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/10.jpg)

---

En el caso de que quisiéramos asignar una carga diferente a cada servidor, podríamos asignarle un peso a cada uno de ellos. Para ello, volvemos a editar las siguientes líneas en el archivo de configuración **/etc/nginx/conf.d/default.conf**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/11.jpg)

---

En este caso, le hemos asignado el doble de carga al servidor 2 (weight=2), por lo que de cada 3 peticiones, el servidor 1 responderá a una de ellas, mientras que el servidor 2 responderá a dos de ellas. Para comprobar su correcto funcionamiento, realizamos las peticiones desde la máquina cliente y verificamos que esto se cumple.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/12.jpg)

---

También aplicar un balanceo por IP, de forma que todo el tráfico que venga de una IP se sirva durante toda la sesión por el mismo servidor final. Para ello, editamos las siguientes líneas del archivo de configuración **/etc/nginx/conf.d/default.conf** :

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/13.jpg)

---

Ahora podemos comprobar que siempre está respondiendo el mismo servidor al cliente, puesto que el cliente posee una única dirección IP.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/14.jpg)

---

A partir de la versión 1.2 de nginx ya es posible utilizar conexiones con keepalive entre el  nginx  y  los  servidores  finales,  de  forma  que  se  realice  una conexión  con  una persistencia de múltiples peticiones HTTP en lugar de abrir una conexión nueva cada vez. Para especificar esto, editamos el archivo de configuración ** /etc/nginx/conf.d/default.conf ** y modificamos las siguientes líneas:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/15.jpg)

---
---

Ahora vamos a probar otro software de balanceo. En este caso vamos a utilizar **Haproxy**. Empezamos instalándolo con la orden: **sudo apt-get install haproxy**


Tras instalarlo, voy a hacer una copia de seguridad del archivo de configuración, para proceder a configurarlo tranquilamente.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/16.jpg)

---

A continuación editamos el fichero de configuración **/etc/haproxy/haproxy.cfg**:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/17.jpg)

---

Para ejecutarlo, debemos de comprobar que no haya ningún otro servicio utilizando el puerto 80, para ello podemos comprobar qué servicios se está ejecutando en dicho puerto mediante la orden: sudo netstat -tulpn | grep :80 . En este caso, podemos observar que nginx está utilizando dicho puerto, por lo que procedemos a pararlo y a iniciar el servicio haproxy

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/17.1.jpg)

---

Para verificar el correcto balanceo, desde la máquina cliente procedemos a realizar peticiones al servidor, y vemos que cada servidor nos responde alternativamente.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/19.jpg)

---
---

Por último lugar, vamos a realizar una comparación del rendimiento entre estos sofware de balanceo, midiendo los tiempos obtenidos variando el número de peticiones lanzadas desde el cliente.

Esta comprobación se va a realizar mediante la utilidad **Apache Benchmark**. Para instalarla utilizamos la orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/20.jpg)

---

Una vez instalada, podemos realizar 1000 peticiones de forma que se realicen concurrentemente de 10 en 10 al servidor de balanceo mediante la orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/22.1.jpg)

---

Tras ejecutar esa orden, se obtiene la siguiente salida:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/23.jpg)

---

Como hemos podido comprobar, las 1000 peticiones se ha realizado en un tiempo de 0,579 segundos.

Para realizar diversas comprobaciones, y automatizar dicha tarea, se ha realizado un pequeño script que almacena en un fichero el tiempo obtenido desde las 1.000 peticiones hasta las 20.000 con un incremento de 1.000.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/24.jpg)

---

Tras realizar dicho script, le damos permisos de ejecución y procedemos a ejecutarlo:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/25.jpg)

---

A continuación se va a mostrar algunos de los resultados obtenidos:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/26.jpg)

---

Finalmente, tras realizar dicho test tanto para el software de balanceo **NGINX** como para **HAPROXY**, comparamos dichos tiempos y lo representamos mediante una gráfica:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/27.jpg)

---

Podemos concluir con dichos resultados, que para una gran cantidad de peticiones el software de balanceo **HAPROXY** funciona con un **mayor rendimiento**

---
---
## TAREA EXTRA Y OPTATIVA ##

Como tarea adicional y optativa, he instalado un tercer software de balanceo. Dicho software se llama **Pound**.

En primer lugar procedemos a instalarlo mediante la orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/28.jpg)

---

A continuación editamos su archivo de configuración **/etc/pound/pound.cfg** y añadimos lo siguiente:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/29.jpg)
![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/30.jpg)

---

Tras realizar esto, iniciamos el servicio:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/31.jpg)

---

Y comprobamos que se está ejecutando en el puerto 80

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/32.jpg)

---

Posteriormente, realizamos las peticiones desde la máquina cliente y comprobamos que nos responden ambos servidores:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/33.jpg)

---

Por último, se ha realizado la prueba de rendimiento con Apache Benchmark, y hemos comparado los tiempos con los demás softwares de balanceo. Hemos obtenido tiempos superiores, por lo que podemos decir que con dicha configuración tanto **HAPROXY** como **NGINX** tienen **mejor rendimiento**.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_3/Imágenes/34.jpg)

---

##  FIN PRÁCTICA 3
