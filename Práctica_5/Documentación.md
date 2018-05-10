# Práctica 5: Replicación de bases de datos MySQL
## Autor: Jonathan Martín Valera

Software utilizado:  

- Virtualización: VirtualBox -- Versión 5.2.8 r121009 (Qt5.6.2)
- Sistemas operativos: Ubuntu-16.04.4-server-amd64
- UbuntuServer1: 192.168.1.10
- UbuntuServer2: 192.168.1.20
- Cliente: 192.168.1.30
- Balanceador: 192.168.1.100
- ServidorBaseDatos1: 192.168.1.15
- ServidorBaseDatos2: 192.168.1.25
- Adaptador de red: Bridge


## Creación de una base de datos y tablas

En primer lugar, instalamos el sercivio mysql en el servidor de base de datos (en el caso de que no esté instalado). Para ello utilizamos


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/1.jpg)

---

Durante la instalación, se nos solicitará introducir los nuevos datos para el usuario root de la base de datos. Una vez introducidos, podemos acceder al sistema. Para ello utilizamos la orden: 


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/2.jpg)

---

A continuación creamos una base de datos de prueba, por ejemplo una llamada "información" y una tabla llamada "usuarios":


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/3.jpg)

---

Comprobamos que la tabla se ha creado correctamente con la orden **show tables**.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/4.jpg)

---

Insertamos tres registros de prueba en dicha tabla:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/5.jpg)

---

Comprobamos que los registros se han creado correctamente haciendo un "select" de toda la tabla.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/6.jpg)

---

También se puede comprobar la estructura de la tabla creada con la orden **describe nombreTabla**

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/7.jpg)

---

## Copia de seguridad de la BD completa usando mysqldump

A continuación vamos a realizar una copia de seguridad completa de una base de datos y exportarla a otro servidor de base de datos.

En primer lugar es necesario bloquear las tablas para evitar accesos a la base de datos mientras se está realizando la copia de seguridad.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/8.1.jpg)

---

Después usamos la siguiente orden con **mysqldump** para realizar la copia de seguridad de la base de datos "información". A continuación comprobamos que se ha creado el archivo .sql correspondiente.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/8.2.jpg)

---

Tras realizar eso, desbloqueamos las tablas que habíamos bloqueado:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/9.jpg)

---

Envíamos dicho archivo a través de **scp** hacia al servidor de base de datos 2

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/10.jpg)

---

Para poder restaurar dicha base de datos, es necesario crear una base de datos vacía con el mismo nombre que la que se quiere importar. Esto es así porque mysqldump no incluye  en  ese  archivo  la 
sentencia  para  crear  la  BD.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/11.jpg)

---

A continuación procedemos a volcar la información contenida en el archivo backup en la base de datos, con la orden:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/12.jpg)

---

Comprobamos que los datos se han importado correctamente: 

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/13.jpg)

---

## Replicación de BD mediante una configuración maestro-esclavo


Para realizar dicha configuración, Lo primero que debemos hacer es la configuración de mysql del  maestro (servidor 1) **/etc/mysql/mysql.conf.d/mysqld.cnf** 

En primer lugar, Comentamos el parámetro bind-address que sirve para que escuche a un servidor


![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/14.jpg)

---

Le indicamos el archivo donde almacenar el log de errores:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/15.jpg)

---

Asignamos un id para identificar al servidor:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/id.jpg)

---

El registro binario contiene toda la información que está disponible en el registro de actualizaciones, en un formato más eficiente y de una manera que es segura para las transacciones.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/16.jpg)

---

Reiniciamos el servicio mysql para que se apliquen dichos cambios.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/17.jpg)

---

A continuación nos vamos al servidor de base maestro (servidor 1) y creamos un usuario para que la máquina esclavo pueda acceder a la base de datos:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/18.jpg)

---

Otorgamos los permisos necesarios para que dicho usuario pueda realizar correctamente la copia de seguridad.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/19.jpg)

---

Ejecutamos las siguientes órdenes para actualizar los cambios:

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/20.jpg)

---

Para finalizar con la configuración en el maestro, obtenemos los datos de la BD que vamos a replicar para posteriormente usarlos en la configuración del esclavo.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/21.jpg)

---

Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/23.jpg)

---

Arrancamos el esclavo y ya está todo listo para que los demonios de MySQL de las dos máquinas repliquen automáticamente los datos que se introduzcan/modifiquen/borren en el servidor maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/24.jpg)

---

Por  último, volvemos al maestro y volvemos a activar las tablas para que puedan meterse nuevos datos en el maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/25.jpg)

---

Ahora, si queremos asegurarnos de que todo funciona perfectamente y que el esclavo no tiene ningún problema para replicar la información, nos vamos al esclavo y con la siguiente orden: **SHOW SLAVE STATUS\G**. Podemos comprobar que el parámetro Seconds_Behind_Master es distinto de null, luego es correcto.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/26.jpg)

---

Para realizar la prueba, vamos a insertar un registro en la base de datos del servidor maestro (servidor  1) y a comprobar si automáticamente el servidor esclavo posee dicho registro, lo que querrá decir que se han actualizado correctamente.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/27.jpg)

---

Comprobamos en el servidor esclavo si la base de datos se ha actualizado, y comprobamos que sí, el registro insertado en el servidor maestro está en el esclavo.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/28.jpg)

---

## PARTE OPTATIVA: Replicación de BD mediante una configuración maestro-maestro

Para realizar dicha configuración, es necesario establecer el servidor de base de datos 1 sea esclavo del segundo y viceversa. Dado que anteriormente hemos establecido que el servidor 2 es esclavo del 1, ahora vamos a hacer que el servidor 1 sea esclavo del 2. Para ello vamos a modificar el archivo de configuración para el servidor maestro (servidor 2 en este caso) como lo hemos hecho anteriomente: **/etc/mysql/mysql.conf.d/mysqld.cnf**.

Tras haber añadido la configuración necesaria y haber establecido a este servidor con id=2, vamos a crear en el servidor maestro (servidor 2) el usuario esclavo, otorgándole los permisos de replicación. 

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/29.jpg)

---

Para finalizar con la configuración en el maestro, obtenemos los datos de la BD que vamos a replicar para posteriormente usarlos en la configuración del esclavo.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/30.jpg)

---

Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/31.jpg)

---

Por  último, volvemos al maestro y volvemos a activar las tablas para que puedan meterse nuevos datos en el maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/32.jpg)

---

Arrancamos el esclavo y ya está todo listo para que los demonios de MySQL de las dos máquinas repliquen automáticamente los datos que se introduzcan/modifiquen/borren en el servidor maestro.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/33.jpg)

---

Ahora, si queremos asegurarnos de que todo funciona perfectamente y que el esclavo no tiene ningún problema para replicar la información, nos vamos al esclavo y con la siguiente orden: **SHOW SLAVE STATUS\G**. Podemos comprobar que el parámetro Seconds_Behind_Master es distinto de null, luego es correcto.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/34.jpg)

---

Finalmente hacemos la prueba de fuego, es decir, vamos a insertar datos en ambos servidores, y cada uno de ellos tiene que ser capaz de actualizarse automáticamente tras cada uno de éstos. Empezamos insertando un registro en el servidor de base de datos 1.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/35.jpg)

---

Comprobamos el servidor 2 y observamos que los datos se han actualizado correctamente. 

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/36.jpg)

---

A continuación vamos a realizar el mismo proceso a la inversa, es decir, vamos a insertar datos en el servidor 2 y observar si automáticamente se actualizan los datos del servidor 1.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/37.jpg)

---


Comprobamos que también se ha actualizado, luego podemos concluir que el sistema se actualiza correctamente y, ¡funciona todo a la perfección!.

![img](https://github.com/jmv74211/SWAP/blob/master/Práctica_5/Imágenes/38.jpg)

---
---


##  FIN PRÁCTICA 5
