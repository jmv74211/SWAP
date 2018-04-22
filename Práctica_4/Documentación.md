# Práctica 4: Asegurar la granja web
## Autor: Jonathan Martín Valera

Software utilizado:  

- Virtualización: VirtualBox -- Versión 5.2.8 r121009 (Qt5.6.2)
- Sistemas operativos: Ubuntu-16.04.4-server-amd64
- UbuntuServer1: 192.168.1.10
- UbuntuServer2: 192.168.1.20
- Cliente: 192.168.1.30
- Balanceador: 192.168.1.100
- Adaptador de red: Bridge

## Función HTTPS

**Generar e instalar un certificado autofirmado**

Para  generar  un  certificado  SSL  autofirmado  en  Ubuntu  Server solo  debemos  activar el  módulo SSL de Apache,  generar  los  certificados  y  especificarle  la  ruta a los certificados en la configuración. Así pues, como root ejecutaremos:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/1.jpg)

---

Creamos el directorio donde vamos a almacenar los certificados:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/2.jpg)

---

A continuación usamos la siguiente orden para generar los archivos del certificado. Se nos pedirá una serie de datos:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/3.jpg)

---

Después, vamos a editar el siguiente archivo para activar el módulo SSL en el servidor web Apache.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/4.jpg)

---

En dicho archivo, añadimos las siguientes líneas:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/5.jpg)

(SSL ON: Activa el módulo SSL de apache, y a continuación indicamos las rutas de los archivos generados de nuestro certificado).

---

Por último, cargamos dicho archivo de configuración en el servidor apache, activando por completo el módulo SSL, y a continuación reiniciamos el servicio de apache.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/6.jpg)

---

Comprobamos que efectivamente, el servicio funciona mediante HTTPS

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/7.jpg)

---

Tras tener preparado el primer servidor, vamos a copiar el certificado generado para el servidor 2 y la máquina balanceadora.
Para poder copiar dicho archivo, es necesario que el usuario del servidor 2 sea propietario del directorio donde se va a copiar los archivos. 

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/8.jpg)

---

Copiamos los archivos del servidor 1 al servidor 2 mediante scp

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/9.jpg)

---

A continuación reiniciamos el servicio nginx mediante la siguiente orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/9.jpg)

---

Realizamos la misma acción para la máquina balanceadora de carga.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/10.jpg)

---

Finalmente comprobamos que el servicio web apache funciona tanto con HTTP como HTTPS en la máquina servidora 2.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/11.jpg)

---

Para realizar esta misma acción en la máquina balanceadora, tenemos que editar el archivo de configuración de NGINX: **/etc/nginx/conf.d/default.conf**, y añadir la línea para escuchar el puerto 443 (HTTPS), habilitar el módulo SSL e indicar donde estarán los archivos del certificado. El archivo de configuración resultante es el siguiente:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/12.jpg)

---

Finalmente, comprobamos que el servicio de balanceo funciona correctamente con HTTPS

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/19.jpg)

---
---

## Configuración del cortafuegos

**Configuración del cortafuegos iptables en Linux**

Para realizar dicha configuración, vamos a utilizar reglas de iptables. Dichas reglas se van a programar en un script. El contenido del script es el siguiente: 

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/13.jpg)

En dicho script se deniega todo el tráfico, y después se permite el tráfico desde localhost, el puerto 22(SSH), 80(HTTP) y 443(HTTPS).

---

Para ejecutarlo le damos permiso de ejecución, y lo lanzamos con la siguiente orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/14.jpg)

---

Comprobamos que la tarea se ha realizado correctamente con la siguiente orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/15.jpg)

---

Ahora vamos a realizar los mismos pasos para el servidor 2, y comprobamos que también funciona:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/16.jpg)

---

Finalmente, comprobamos que los servicios HTTP y HTTPS funcionan tanto en los servidores, como en la máquina balanceadora tras aplicar dichas reglas.

**Acceso al servidor 1**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/17.jpg)

**Acceso al servidor 2**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/18.jpg)

**Mediante balanceo de carga**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/19.jpg)

---

Para aplicar dicha configuración de forma automática, podemos hacer que se ejecute dicho script que contiene las reglas de iptables al inicio del servidor. Para realizar esto, basta con añadir dicho script en el fichero **/etc/rc.local**.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/20.jpg)


Quedaría de la siguiente forma:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/21.jpg)

---

Por último, comprobamos que funciona correctamente, y se aplica dicha configuración al inicio del servidor.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes/22.jpg)


##  FIN PRÁCTICA 4
