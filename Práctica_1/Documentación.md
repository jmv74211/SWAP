# Práctica 1: Preparación de las herramientas
## Autor: Jonathan Martín Valera

Software utilizado:  

- Virtualización: VirtualBox -- Versión 5.2.8 r121009 (Qt5.6.2)
- Sistemas operativos: Ubuntu-16.04.4-server-amd64


Tras la instalación de las dos máquinas virtuales, se ha configurado las interfaces de red para que se puedan comunicar. Para ello, el adaptador de red se ha configurado en modo **Bridge**, con las siguientes direcciones:

- UbuntuServer1: 192.168.56.10
- UbuntuServer2: 192.168.56.20

Dichos Ubuntu servers constan de los servicios LAMP Y OpenSSH Server.

Para comprobar la conectividad entre las máquinas, se ha realizado una conexión SSH de prueba entre ambas.

**Conexión SSH desde el server 1 al server 2**

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_1/Imágenes/ssh.jpg)

**Conexión SSH desde el server 2 al server 1**

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_1/Imágenes/ssh2.jpg)  


Una vez comprobada las conexiones, comprobamos que el estado del servicio apache:

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_1/Imágenes/apacheServerStatus.jpg)

Como prueba adicional, se va a crear un archivo HTML para probar el servicio web

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_1/Imágenes/pruebaHTML.jpg)

Finalmente, se comprueba en la segunda máquina el servicio web proporcionado por la primera

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_1/Imágenes/pruebaFinal.jpg)

---

##  FIN PRÁCTICA 1 
