# Ejercicios tema 5(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T5.1: Buscar información sobre cómo calcular el número de conexiones por segundo**

Para calcular el número de conexiones por segundo es necesario saber el **número máximo de solicitudes por segundo**, y el **número máximo de conexiones permitidas por segundo**. Para obtener dicha información, podemos instalar un módulo llamado **HttpStubStatusModule** y acceder a dicha información a través de: **http://ip.address.here/nginx_status**

Un ejemplo sería el siguiente: 

- Número máximo de solicitudes = 21897888
- Número máximo de conexiones permitidas = 9582571 

El número de conexiones por segundo sería 21897888/9582571 = **2.28**


Referencias [https://www.cyberciti.biz/faq/nginx-see-active-connections-connections-per-seconds/]

--- 


**Ejercicio T5.2 Ejercicio: Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP.**

Tras instalar wireshark en una máquina virtual, y realizar una petición HTTP con la orden curl desde una máquina cliente con IP= 192.168.1.30 hacia el servidor web con IP=192.168.1.10.

Podemos observar que wireshark ha capturado el tráfico generado, y observar que primero se ha generado una petición GET mediante el protocolo HTTP 1.1, a continuación el servidor web ha enviado el contenido HTML con un código 200 de OK.


![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/5.2.jpg)

--- 


**Ejercicio T5.3 Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.**

Para empezar, podemos comenzar utilizando las clásicas de Linux: 


-**top** : Muestra un resumen del estado de nuestro sistema y la lista de procesos que se están ejecutando. Con ella podemos comprobar datos como:


- Tiempo de actividad y carga media del sistema
- Tareas
- Estados de la CPU
- Memoria física
- Memoria virtual


-**vmstat** : Vmstat es un comando que nos permite obtener un detalle general de los procesos, E/S, uso de memoria/swap, estado del sistema y actividad del CPU. Es esencial para entender que esta pasando en tu sistema, detectar cuellos de botella, etc..


-**netstat** : Es una herramienta de la línea de comandos para controlar las conexiones de red entrantes y salientes, así como la visualización de las tablas de enrutamiento, las estadísticas de la interfaz, etc 


Otras herramientas:


- Visualización de procesos: **ps**. El comando ps nos muestra información detallada de los procesos del sistema, pudiendo filtrar por usuarios y detalles de procesos. Las opciones mas usuales de utilizar pueden ser aux o fax , indicando la opción a junto con x para incluir todos los procesos, y las opciones f y u que se utilizan para seleccionar la visualización en árbol o detallada, respectivamente. 


- Visualización del disco: **df, iotop**. Para la monitorización del disco contamos con varios comandos, dependiendo de lo que queramos observar. Para visualizar el uso del disco tenemos el comando df , aunque también podemos sacar una visión mas amigable de esto con el comando discus . Si lo que queremos visualizar es el I/O del disco podemos utilizar el comando iotop , que nos muestra los procesos del sistema y su trabajo de interrupción en el disco. 


- Visualización de ficheros y servicios: **lsof**. En este apartado hablaré del comando lsof que nos permite mostrar los ficheros abiertos asociados tanto a procesos como a servicios (sockets, tuberías, etc). Un ejemplo de ello es el comando lsof -i , que permite ver los sockets abiertos que tenemos en el sistema. Si ejecutamos lsof sobre un fichero o directorio, podremos ver si éste esta siendo ocupado por algún proceso. 


... Para más información visitar la web: https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/


**Referencias:**

- [https://geekytheory.com/funcionamiento-del-comando-top-en-linux]

- [https://storm.malditainternet.com/wp/2011/05/usando-y-entendiendo-vmstat/]

- [https://openwebinars.net/blog/3-formas-de-monitorizar-servidores-linux/]

--- 

##  FIN ejercicios tema 5
