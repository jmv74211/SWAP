# Práctica 2: Clonar la información de un sitio web
## Autor: Jonathan Martín Valera

Software utilizado:  

- Virtualización: VirtualBox -- Versión 5.2.8 r121009 (Qt5.6.2)
- Sistemas operativos: Ubuntu-16.04.4-server-amd64
- UbuntuServer1: 192.168.56.10
- UbuntuServer2: 192.168.56.20
- Adaptador de red: Bridge

En primer lugar, vamos a hacer que los directorios /var/www pertenezcan a los usuarios ubuntuServer en lugar de a root:

**Cambio de propietario en la máquina principal (ubuntuServer1)**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/chown1.jpg)


**Cambio de propietario en la máquina secundaria (ubuntuServer2)**

---

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/chown2.jpg)

---

A continuación, vamos a realizar una prueba para comprobar el funcionamiento de la herramienta **rsync**. Lo que se pretende 
a continuación es realizar mediante ssh una copia del directorio /var/www/ de la máquina principal a la máquina secundaria.
Como se puede observar, nos solicita la contraseña de sesión de la máquina principal.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/rsync_1.jpg)

---

Luego comprobamos en la máquina secundaria que se haya copiado correctamente los archivos. Como se puede apreciar, también se ha 
generado un archivo .save en el directorio de la copia.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/rsync_2.jpg)

---

Para automatizar el proceso, se va a configurar el servicio ssh para que no nos solicite la contraseña cada vez que ejecutemos ssh hacia la máquina principal.
Para ello vamos a generar una clave pública mediante **ssh-keygen**. A continuación se nos solicitará introducir la clave privada, en cuyo caso la introduciremos 
en blanco para que no nos solicite ninguna contraseña, y de este modo hacer que el proceso de backup sea automático.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/ssh_1.jpg)

---

Posteriormente, hacemos una copia de esa clave hacia la máquina principal a través del comando **ssh-copy-id**.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/ssh_2.jpg)

---

Para comprobar que el proceso se ha realizado correctamente, volvemos a iniciar sesión en la máquina principal mediante ssh, y comprobamos que esta vez no nos
solicita introducir la contraseña de inicio de sesión.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/ssh_3.jpg)

---

Finalmente, para automatizar el proceso y ejecutarlo cada cierto tiempo sin la necesidad de introducir el comando necesario, vamos a programar la tarea con **crontab**.
Inicialmente se va a programar para que se ejecute cada minuto de cada hora de cada día de la semana, poniendo los 5 primeros campos con asteriscos, estableciendo que el usuario
que ejecuta la orden es ubuntuServer1 y añadiendo el comando para ejecutar el proceso de backup con la herramienta rsync. El fichero a editar es **/etc/crontab**, y debería quedar
de la siguiente forma:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/crontab_1.jpg)

---

Para comprobar su funcionamiento, vemos que el directorio /var/www/ de la máquina secundaria está vacío.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/crontab_2.jpg)

---

Tras esperar un minuto, volvemos a comprobar el directorio /var/www y esta vez podemos ver que si tiene contenido, y dicho contenido es la copia de backup realizada de la máquina principal.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/crontab_3.jpg)

---

Por último, configuramos crontab para que la tarea se ejecute cada hora. El fichero /etc/crontab quedaría de la siguiente forma

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_2/Imágenes/crontab_4.jpg)

---

##  FIN PRÁCTICA 2 
