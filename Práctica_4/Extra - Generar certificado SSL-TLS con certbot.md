# Generar certificado SSL - TLS con certbot
## Autor: Jonathan Martín Valera

## Cómo generar un certificado SSL/TLS gratis con certbot


**Certbot** es un cliente ACME automático y fácil de utilizar, que obtiene certificados SSL/TLS gratis para sitios Web, provistos por Let's Encrypt. 

Certbot (anteriormente el cliente Let's Encrypt letsencrypt-auto) es el cliente recomendado por Let's Encrypt para emitir sus certificados, y opcionalmente auto-configurar HTTPS en tu servidor Web.

Certbot soporta un número de diferentes plugins que pueden ser utilizados para obtener y/o instalar certificados. Para aquellos usuarios poco experimentados, certbot tiene la capacidad de auto-configurar a la mayoría de los servidores HTTP, a fin de instalar el certificado generado y poner en funcionamiento HTTPS. Sin embargo, si se utiliza una configuración de HTTP/HTTPS personalizada y se cuenta con acceso a la configuración del servidor Web, resultará conveniente realizar la autenticación del dominio (ACME challenge) utilizando el servidor Web actual. Esto tiene la ventaja de no tener que detener el servicio Web durante la generación del certificado.

Antes de comenzar, configurar el servidor Web en cuestión para que el acceso a los archivos en el directorio **.well-known/acme-challenge/** sea de tipo MIME "text/plain". Para el caso de servidores Nginx, configurar el directorio, dentro de la configuración del sitio, de la siguiente forma:


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/1.jpg)

Para el caso de Apache:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/2.jpg)

Al finalizar es necesario recargar la configuración (**service nginx reload** o **service apache2/httpd reload**). De esta forma no es necesario detener el servicio Web en ningún momento.

---

## Instalación de cerbot

Para los sistemas que no dispongan certbot desde paquete, la instalación es trivial. Simplemente descargar el cliente **certbot-auto** y otorgarle permisos de ejecución:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/3.jpg)

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/4.jpg)

---

## Generación de un certificado SSL/TLS utilizando el plugin webroot

La creación del certificado es extremadamente simple, porque el cliente se encarga de crear los archivos con el contenido correcto (antes tenía que realizarlo uno manualmente). Sólo basta con ejecutar **./certbot-auto certonly**

Por ejemplo, generar un certificado TLS para los dominios "linuxito.com" y "www.linuxito.com":

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/5.jpg)

En el primer paso, seleccionar "webroot":

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/6.jpg)

Luego, especificar una dirección de correo electrónica válida:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/7.jpg)

Esta dirección será utilizada para notificar al antes de que expire el certificado generado y así poder renovarlo. Recordar que los certificados emitidos por Let's Encrypt tienen una validez de 3 meses.

A continuación, aceptar los términos del servicio:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/8.jpg)


Si se desea, es posible recibir por correo las novedades de la EFF:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/9.jpg)

Luego viene la parte importante, indicar claramente los dominios para los cuales el certificado será válido:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/10.jpg)

Es posible separar los dominios con coma o espacio en blanco.

Siguiente, especificar la raíz del sitio web ("webroot") relacionado a los dominios a certificar. La primera vez es necesario agregar un webroot:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/11.jpg)

En este caso, la raíz del sitio Web es **/var/www/linuxito.com**. Una vez agregada, seleccionarla:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/12.jpg)

Finalmente, se genera el nuevo certificado:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/13.jpg)

El certificado (**cert.pem**) y su clave privada (**privkey.pem**) quedan almacenados en el directorio **/etc/letsencrypt/live/linuxito.com/**:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/14.jpg)

Sólo resta configurar HTTPS en Nginx o Apache, según corresponda. Recuerden que, para asegurarse que el sitio sea confiable en todos los navegadores, es necesario utilizar la cadena completa (**fullchain.pem**) en lugar de sólo el certificado (**cert.pem**), junto con la clave privada del certificado (**privkey.pem**).

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/15.jpg)

---

## Renovar automáticamente todos los certificados

Certbot tiene la opción de renovar automáticamente (y de forma desatendida) todos los certificados emitidos según la configuración utilizada previamente. Para ello, simplemente se debe ejecutar **./certbot-auto renew**.

Es posible hacer una corrida a modo de prueba utilizando la opción --dry-run:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_4/Imágenes_certbot/16.jpg)

Si funciona correctamente, es posible definir un cronjob que corra de forma periódica y se encargue de las renovaciones:

**./path/to/certbot-auto renew --quiet --no-self-upgrade**

Esto no requiere reiniciar o recargar la configuración de los servidores Web que utilizan los certificados, pues los archivos dentro de **/etc/letsencrypt/live/linuxito.com/** son enlaces simbólicos a los certificados y claves.

Let's Encrypt recomienda correr esta tarea dos veces al día (eligiendo un minuto aleatorio, para aliviar la carga en sus servidores). Tal vez parezca exagerado (siendo que los certificados son válidos por tres meses) pero evitará interrupciones en el servicio en caso de que Let's Encrypt revoque certificados por alguna razón (brecha de seguridad, cambio en algoritmos de hashing, etc.) Tener en cuenta que este trabajo no realiza ninguna tarea si los certificados no están por expirar o revocados.

##  FIN PRÁCTICA 4
