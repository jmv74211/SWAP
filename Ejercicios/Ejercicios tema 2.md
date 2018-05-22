# Ejercicios tema 2(SWAP)
## Autor: Jonathan Martín Valera
## Fecha: Mayo 2018

**Ejercicio T2.1. - Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).**

•	Web: 85%

•	Applications: 90%

•	Database: 99.9%

•	DNS: 98%

•	Firewall: 85%

•	Switch: 99%

•	Data Center: 99.99%

•	ISP: 95%

Aplicando la fórmula **As = Ac1 + (1-Ac1) * Ac2** para la disponibilidad al replicar y **As = Ac1 * Ac2 * Ac3 * ... * Acn"** para la total, tenemos los siguiente:

•	Web: 0.85 + (1-0.85) * 0.85 = 0.9775

•	Applications: 0.9 + (1-0.9) * 0.9 = 0.99

•	Database: 0.999 + (1-0.999) * 0.999 = 0.999999

•	DNS: 0.98 + (1-0.98) * 0.98 = 0.9996

•	Firewall: 0.9775 (La misma que el componente Web).

•	Switch: 0.99 + (1-0.99) * 0.99 = 0.9999

•	Data Center: 0.9999 + (1-0.9999) * 0.9999 = 0.99999999

•	ISP: 0.95 + (1-0.95) * 0.95 = 0.9975

 **Total =** 0.9775*0.99*0.999999*0.9996*0.9775*0.9999*0.99999999*0.9975)*100 =**94.3%**

---

**Ejercicio T2.2 - Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.**

**Spring Framework** es un proyecto de código abierto que proporciona una infraestructura para objetos **Java™** simples que les permite utilizar el contenedor Java EE a través de clases de derivador y una configuración XML. Además, se asegura de que la aplicación pueda utilizar las calidades de servicio que el servidor de aplicaciones proporciona, por ejemplo seguridad, gestión de carga de trabajo y alta disponibilidad.

**Kumbia Enterprise Framework** versión modificada del Kumbia PHP Framework comunitario que ha sido probado e implementado en entornos de alta disponibilidad donde corren aplicaciones críticas.

---

**Ejercicio T2.3 - ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas.**

Para realizar esta tarea, podemos utilizar algunas de las siguientes aplicaciones (Existen muchas más):

**-Google Page Speed** mide de 0 a 100 la velocidad de carga del sitio e indica, por orden de prioridad, qué mejorar, aportando información al respecto.

**-Pingdom:** Pingdom es una de las mejores y más fiables de su tipo. Mediante el test que realiza, puntúa (de 0 a 100) la velocidad, monitoriza el número de solicitudes ejecutadas, el tiempo de carga y el tamaño total de la página web.

**-Load Impact** ejecuta una prueba de resistencia y estrés a la página web que le indiques. Cuenta con dos versiones: una gratuita y otra de pago. La gratuita realiza una simulación de carga con 50 usuarios. La información obtenida es 
representada en forma de gráficos y mediante un mapa.

**-Loads.in** permite establecer la carga desde diferentes localizaciones mundiales y escoger el navegador. El resultado del análisis que efectúa se muestra mediante varias capturas de pantalla, junto al tiempo (en segundos) de carga en las que se han obtenido. Permite realizar varios tests y compararlos visualmente entre sí.

---

**Ejercicio T2.4 - Buscar ejemplos de balanceadores software y hardware (productos comerciales).**

**Balanceadores software**

**-NGINX** es un servidor web HTTP de código abierto que incluye servicios de correo electrónico con acceso al Internet Message Protocol (IMAP) y al servidor Post Office Protocol (POP). Además, NGINX está listo para ser utilizado como un proxy inverso. En este modo, se utiliza para equilibrar la carga entre los servidores back-end, como también para ser utilizado como caché en un servidor back-end lento.
Empresas como **Facebook y WordPress.com**, lo utilizan porque la arquitectura asíncrona del servidor web deja una pequeña huella de memoria y bajo consumo de recursos, haciéndolo ideal para el manejo de múltiples y cambiantes activas páginas Web.
Esa es una tarea difícil. Es así como NGINX puede soportar cientos de millones de usuarios de Facebook.

**-Apache HTTP Server:** Es el servidor web más usado en el mundo, pero como pasa en muchos casos, lo más usado no es siempre lo mejor, solo lo que se conoce más. Apache tiene muchas características positivas, pero su gran deficiencia es el rendimiento, cosa que es sumamente importante en las aplicaciones de hoy en día.

**Balanceadores hardware**

**-LoadMaster R320 de KEMP:** permite a los clusters de centros de datos distribuir de forma eficiente e inteligente el tráfico de la red entre los servidores de aplicaciones y la web. Una capa de optimización de recurso delante de los servidores de aplicaciones y de la infraestructura otorga a los administradores de TI mayor control para adaptarse a los cambios de la red y conseguir el mejor rendimiento de la infraestructura y de la web.

**- Load-balancing Cisco ACE:** distribuye el tráfico entrante entre varios servidores o máquinas virtuales en el interior de su Rack virtual. Es una solución de hardware que garantiza la accesibilidad y simplifica el aumento de carga de sus sitios web o aplicaciones.El load-balancer Cisco ACE detecta los servidores o máquinas defectuosos y los excluye automáticamente de su "pool", redirigiendo el tráfico a los otros servidores o MV.

**-Buscar productos comerciales para servidores de aplicaciones.**
-	WidFly – JBoss Application Server
	•	Undertow (servidor web)
	•	Apache CXF (web services basado en SOAP)
	•	RestEasy ( web services basado en REST)
	•	Infinispan (plataforma de Data Grid y Cluster )
	•	HornetQ (proveedor de JMS)
	•	JGroups (framework de comunicación Multicast)
-	GlassFish
-	Apache Geronimo
	•	Apache Tomcat (Servidor HTTP y contenedor de servlet)
	•	Jetty (Servidor HTTP y contenedor de servlet, alternativo a Tomcat)
	•	Apache ActiveMQ (proveedor de JMS 1.1)
	•	Apache OpenEJB (contenedor EJB)
	•	Apache OpenJPA (Implementación de Java Persistence API – JPA 1.0)
	•	Apache ServiceMix (Enterprise Services Bus)
	•	Apache CXF (framework de web services con una variedad de protocolos)
	•	Apache Derby (administrador de base de datos relacional con un soporte nativo para JDBC)
	•	Apache WADI (solución cluster y de balanceo de carga)
-	JOnAS
-	Apache TomEE


**-Buscar productos comerciales para servidores de almacenamiento.**
-	Apollo
-	HPE Synergy
-	HPE Nimble Storage

--- 

[No hay más ejercicios propuestos para este tema]

--- 

##  FIN ejercicios tema 2
