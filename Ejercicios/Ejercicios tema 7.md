# Ejercicios tema 7(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T7.1: ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de dos discos de 100 GB y 100 GB?**

Dado que el nivel RAID 0 es el conjunto dividido, el tamaño de unidad total será la suma de las unidades. En este caso

Tam = 100GB + 100GB = **200GB**

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de tres discos de 200 GB cada uno?** 

Tam = 3 * 200GB = **600GB**

---

**Ejercicio T7.2: ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1a partir de dos discos de 100 GB y 100 GB?** 

Dado que el nivel RAID 1 es el conjunto espejo, el tamaño de unidad total será la mitad de la suma de los discos, ya que debemos de duplicar la información. En este caso:

Tam = (100GB + 100GB) /2 = **100GB**

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de tres discos de 200 GB cada uno?** 

Suponiendo que replicamos la información en todos los discos:

Tam = (3*200GB) /3 = **200GB**


---

**Ejercicio T7.3: Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.**

El sistema de almacenamiento en red (NAS) se ha convertido en una solución muy popular entre las empresas para guardar los datos.


Gracias, entre otras cosas, a su coste asequible, mínima carga de gestión por parte del usuario y prestaciones adicionales.


Un servidor NAS (Network Area Storage) o sistema de almacenamiento conectado en red, comparte su capacidad de almacenamiento a través de la red haciendo uso de un sistema operativo optimizado para dar acceso con los protocolos CIFS, NFS, FTP o TFTP.


Un servidor SAN (Storage Area Network) son redes especializadas de almacenamiento de datos de alta velocidad que emplean la tecnología Fiber Channel (FC) o iSCSI para conectar servidores con discos de almacenamiento.

**Características**

-El rendimiento de NAS se ve afectado por su dependencia de la propia red de área local (LAN) de la empresa, mientras que SAN, utiliza una red dedicada, normalmente mediante fibra a 10G, sin afectar al rendimiento de la LAN.


-En un servidor SAN, el sistema de ficheros está ubicado en el lado del cliente, mientras que en un NAS, reside en el lado del almacenamiento.


-En una cabina de almacenamiento SAN, los recursos pueden ser gestionados de forma centralizada y el espacio puede ser reubicado en función de las necesidades, pudiendo ser accedido por múltiples servidores simultáneamente, con un procesamiento muy rápido.


[http://rcg-comunicaciones.com/mejor-sistema-de-almacenamiento-en-red/]


**Configurar en una máquina virtual un servidor NFS. Montar desde otra máquina virtual en la misma subred la carpeta exportada y comprobar que ambas pueden acceder a la misma para lectura y escritura.**


Para realizar estas configuraciones, tanto la del cliente como la del servidor, he seguido el tutorial disponible en la siguiente página web: https://www.howtoforge.com/nfs-server-on-ubuntu-14.10


He configurado el servidor nfs en mi máquina virtual llamada nfs, y el cliente en la máquina llamada nfs.


Tras realizar todos los pasos indicados en el tutorial, desde la máquina cliente he creado un archivo de prueba. Como se puede comprobar en la siguiente imagen, dicho archivo de prueba se ha almacenado en el servidor nfs, y lo podemos abrir desde el cliente.


![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/7.4.jpg)


--- 

##  FIN ejercicios tema 7
