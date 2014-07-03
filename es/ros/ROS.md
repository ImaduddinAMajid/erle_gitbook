El Sistema Operativo de Robot ( ROS ): Encender robots del mundo
=========

![ros](img/rosorg-nb.png)

�Qu� es ROS ?
-----
El [Sistema Operativo de Robot] (http://www.ros.org/) (ROS) es un **sistema operativo de c�digo abierto** para su robot mantenida por el [Open Source Rob�tica Fundaci�n] (http://www.osrfoundation.org/) (OSRF). Proporciona los servicios que cabe esperar de un sistema operativo, incluyendo abstracci�n de hardware , control de dispositivos de bajo nivel , la implementaci�n de la funcionalidad de uso com�n , entre los procesos de paso de mensajes y gesti�n de paquetes. Tambi�n proporciona herramientas y bibliotecas para la obtenci�n , la construcci�n , la escritura y la ejecuci�n de c�digo en varios equipos. ROS es similar en algunos aspectos a los "marcos de robots, 'como jugador , YARP , Orocos , CARMEN , Orca, MOOS , y Microsoft Robotics Studio.

El tiempo de ejecuci�n "graph" ROS es una * red de procesos de peer -to-peer * que est�n d�bilmente acoplados utilizando la infraestructura de comunicaci�n ROS . ROS implementa varios estilos diferentes de comunicaci�n , incluida la comunicaci�n sincr�nica de estilo RPC a trav�s de los servicios , la transmisi�n as�ncrona de datos a trav�s de los temas , y el almacenamiento de datos en un servidor * Par�metro * .

** ROS no es un marco de tiempo real ** , aunque es posible integrar de ROS con el c�digo de tiempo real . ROS tambi�n tiene una perfecta integraci�n con el Orocos Toolkit en tiempo real .

Objetivos
-----
El objetivo principal de ROS es ** c�digo de soporte reutilizaci�n en la investigaci�n y el desarrollo de la rob�tica . ** ROS es un marco distribuido de procesos (tambi�n conocido como nodos ) que permite a los ejecutables que ser dise�ado de forma individual y de acoplamiento flexible en tiempo de ejecuci�n . Estos procesos se pueden agrupar en paquetes y pilas , que puede ser f�cilmente compartida y distribuida . ROS tambi�n es compatible con un sistema federado de repositorios de c�digo que permite la colaboraci�n a distribuir tambi�n. Este dise�o , desde el nivel del sistema de archivos a nivel de la comunidad , permite tomar decisiones independientes sobre el desarrollo y puesta en pr�ctica, pero todo puede ser llevado junto con herramientas de infraestructura ROS .

En apoyo de este objetivo primordial de compartir y colaborar , hay varios otros objetivos del marco de ROS:

- ** Thin **: ROS est� dise�ado para ser lo m�s fina posible - no vamos a envolver su main () - para que el c�digo escrito para ROS se puede utilizar con otros marcos de software robot. Un corolario de esto es que los ROS es f�cil de integrar con otros marcos de software robot : ROS ya ha sido integrada con OpenRAVE , Orocos y jugador.
- ** Bibliotecas ** ROS- agn�sticos : el modelo de desarrollo preferido es escribir bibliotecas ROS- agn�stico con interfaces funcionales limpias .
- ** Independencia Idioma **: el marco ROS es f�cil de implementar en cualquier lenguaje de programaci�n moderno . Ya hemos implementado en Python * *, * C + + * , y * Lisp * , y tenemos bibliotecas experimentales en Java * y * Lua .
- ** Pruebas ** F�cil : ROS tiene un marco de prueba de unidad / integraci�n incorporado llamado ROSTEST que hace que sea f�cil de llevar y derribar accesorios de la prueba .
- ** ** Escala : ROS es apropiado para sistemas de tiempo de ejecuci�n de grandes y para grandes procesos de desarrollo.

Sistemas Operativos
-------
ROS en la actualidad s�lo se ejecuta en las plataformas basadas en Unix ** . ** Software de ROS se prueba principalmente en * Ubuntu * y * sistemas * X Mac OS.

Distribuciones
----------
Los siguientes distribuciones han sido probados en el robot [ Erle ] ( http://erlerobot.com ) .

----

** Por defecto las im�genes proporcionadas por Erle vienen con ROS preinstalado y completamente funcional. **

----

| Distro | Fecha de salida | Foros | INSTRUCTIONS |
| -------- | -------------- | -------- | ------------- |
| [ ROS Hydro Medusa ] ( http://wiki.ros.org/hydro ) | 04 de septiembre 2013 | ! [ Medusa ] ( http://i.imgur.com/xvfZPAo.png ) | [ Instalaci�n] (http :/ / wiki.ros.org / hidro / Instalaci�n / UbuntuARM ) |
| [ ROS Groovy Gal�pagos ] ( http://wiki.ros.org/groovy ) | 31 de diciembre 2012 | ! [ Medusa ] ( http://www.ros.org/images/groovygalapagos-320w.jpg ) | [ Instalaci�n] ( http://wiki.ros.org/groovy/Installation/UbuntuARM ) |


licencia
-------
Parte de este material ha sido tomado de la [ ROS wiki] ( http://wiki.ros.org/ ) . Excepto donde se indique lo contrario, el wiki de ROS est� licenciado bajo Creative Commons Attribution 3.0.









