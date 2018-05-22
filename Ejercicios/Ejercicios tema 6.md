# Ejercicios tema 6(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T6.1: Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento. 
Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento**

Mediante las siguientes reglas denegamos todo el tráfico

![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/6.1.1.jpg)]


Comprobamos que no se nos permite hacer ping a otra máquina

![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/6.1.2.jpg)]


Ahora permitimos todo el tráfico mediante las siguientes reglas
![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/6.1.3.jpg)]


Podemos comprobar que ahora sí nos deja hacer ping a otra máquina
![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/6.1.4.jpg)]

---

**Ejercicio T6.2: Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.**

Podemos hacer la comprobación de estas propiedades mediante el comando: **netstat -tulpn**

![img](https://github.com/jmv74211/SWAP/blob/master/Ejercicios/Imágenes/6.2.1.jpg)]

--- 

**Ejercicio T6.3:Buscar información acerca de los tipos de ataques más comunes en servidores web (p.ej. secuestros de sesión). Detallar en qué consisten, y cómo se pueden evitar.** 

**Ataque Por Injection:** Los ataques de inyección, más específicamente sqli (Structured Query Language Injection) es una técnica para modificar una cadena de consulta de base de datos mediante la inyección de código en la consulta. El SQLI explota una posible vulnerabilidad donde las consultas se pueden ejecutar con los datos validados.

SQLI siguen siendo una de las técnicas de sitios web más usadas y se pueden utilizar para obtener acceso a las tablas de bases de datos, incluyendo información del usuario y la contraseña. Este tipo de ataques son particularmente comunes en los sitios de empresas y de comercio electrónico donde los hackers esperan grandes bases de datos para luego extraer la información sensible.Los ataques sqli también se encuentran entre los ataques más fáciles de ejecutar, que no requiere más que un solo PC y una pequeña cantidad de conocimientos de base de datos.

La forma de **prevenir** estos ataques es utilizar, como mínimo, las funciones de filtrado que nos proporcionan los distintos frameworks de desarrollo y, procurar siempre establecer la codificación de la página ya que si acepta varias codificaciones, pueden saltarse el filtro introduciendo caracteres en UTF7.

**DDoS:** La Denegación de Servicio (DoS) ó Denegación de Servicio Distribuida (DDoS) son las formas más comunes para congelar el funcionamiento de un sitio web. Estos son los intentos de inundar un sitio con solicitudes externas, por lo que ese sitio no podría estar disponible para los usuarios reales. Los ataques de denegación de servicio por lo general se dirigen a puertos específicos, rangos de IP o redes completas, pero se pueden dirigir a cualquier dispositivo o servicio conectado.

Evitar estos ataques no es tarea fácil, ya que al recibir solicitudes de multitud de redes diferentes es difícil saber cuáles son de clientes reales y cuáles son “bots”. A ello hay que sumarle que además hay una constante evolución para cambiar los patrones que los hacen detectables, lo que dificulta todavía más su ejecución.
**Algunos pasos para evitar este tipo de ataque son:**

- Mantén tus equipos con antivirus actualizados, ya que algunos monitorizan la actividad de la red y te avisarán de actividades anómalas, permitiéndote prepararte con antelación.
- Contrata servicios que se preocupen de tener actualizado el software de sus sistemas, ya que esto minimiza la posibilidad de explotar fallos de seguridad.
- Adecua los sistemas de tu empresa a la demanda de tráfico de tu web. En ocasiones tu web se satura porque tienes mucha visibilidad y estás escatimando en los servicios de         hosting que contratas.
- Contrata servicios especializados en protección DDoS, estos están pensados para redirigir el exceso de tráfico excedente y evitar que lleguen a afectar a nuestra web.
- Al mínimo síntoma (tiempos de carga excesivos en la web) chequea las IPs que están accediendo a tu servidor y busca aquellas que están constantemente enviando solicitudes para     poder bloquearlas. Normalmente, los proveedores de hosting web te proporcionan un panel de control muy intuitivo para realizar estas tareas.


Los ataques de denegación de servicio funcionan cuando una computadora con una conexión a Internet intenta inundar un servidor con paquetes. DDoS, por otro lado son cuando muchos dispositivos, a menudo ampliamente distribuidos, en un intento de botnet para inundar el objetivo con cientos, a menudo miles de peticiones.

**Fuerza Bruta:** Estos son básicamente intenta “romper” todas las combinaciones posibles de nombre de usuario + contraseña en una página web. Los ataques de fuerza bruta buscan contraseñas débiles para ser descifradas y tener acceso de forma facil. Los atacantes cuentan con buen tiempo, así que el truco es hacer que tus contraseñas sean lo bastante seguras y así el atacante se cansaría antes de descifrar tu contraseña. Mientras que las computadoras se vuelven más y más poderosa la necesidad de contraseñas más fuertes se vuelve cada vez más importante. El caso mas reciente de esta vulnerabilidad, se ha visto en cuanto a la vulneración de cuentas de algunos famosos alojadas en iCloud.

**Cross Site Scripting:** Los atacantes utilizan Cross-site Scripting (XSS) para inyectar scripts maliciosos en lo que serían sitios web inofensivos. Debido a que estos scripts parecen provenir de sitios web de confianza, el navegador de los usuarios finales casi siempre ejecuta la secuencia de comandos, la concesión de los piratas informáticos el acceso a la información contenida en las cookies o tokens de sesión utilizados con ese sitio. El XSS generalmente se utiliza para obtener acceso de un usuario de la cuenta.

De nuevo, la forma de **evitar** este tipo de ataques es filtrar todas las entradas con los frameworks disponibles, aunque a veces se encuentran vulnerabilidades que afectan a estos frameworks y todas las Webs que los usan quedan expuestas, como por ejemplo el ataque <%etiqueta> de algunas versiones del framework de .NET. Además, los data URIs dan una nueva forma de saltarse estos filtros. En estos casos no queda más remedio que actualizar los frameworks o el código de la Web.
Por otro lado, para aumentar la seguridad de las Cookies que contienen información de sesión, se recomienda activar el flag HttpOnly y, en caso de usar HTTPS, activar también el flag Secure.


**Referencias**

[http://blog.hostdime.com.co/tipos-de-ataques-mas-comunes-a-sitios-web-y-servidores/]

[https://www.humanlevel.com/articulos/desarrollo-web/como-evitar-ataques-de-hackers-en-una-pagina-web.html]

[https://www.econectia.com/blog/que-es-como-evitar-ataques-ddos-empresa]

---

[No hay más ejercicios propuestos para este tema]

--- 

##  FIN ejercicios tema 6
