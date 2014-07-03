ROS : Conceptos
=========

ROS tiene tres niveles de conceptos: el nivel del sistema de archivos ** **, el ** nivel de Computaci�n Gr�fica ** y ** el nivel de la comunidad . ** Estos niveles y conceptos se resumen a continuaci�n y las secciones posteriores entran en cada una de ellas con mayor detalle .

Adem�s de los tres niveles de conceptos , ROS tambi�n define dos tipos de nombres: ** Nombres de los recursos del paquete ** y ** Nombres Gr�fico de recursos **, tambi�n se analizan a continuaci�n .

nivel del sistema de archivos
-----------

Los conceptos de nivel de sistema de archivos se refieren principalmente a recursos de ROS que encuentre en el disco, como por ejemplo:

- **Paquetes** : Los paquetes son la unidad principal de la organizaci�n de software de ROS . Un paquete puede contener los procesos de ROS en tiempo de ejecuci�n (nodos) , una biblioteca ROS- dependiente , conjuntos de datos , archivos de configuraci�n , o cualquier otra cosa que se organiza eficazmente juntos. Los paquetes son el elemento de construcci�n m�s at�mica y el punto de liberaci�n de ROS . Lo que significa que lo m�s granular que pueda construir y la liberaci�n es un paquete .
- **Metapaquetes**: Metapaquetes son paquetes especializados que s�lo sirven para representar un grupo de otros paquetes relacionados. M�s com�nmente metapaquetes se utilizan como lugar reservado compatible para Stacks rosbuild convertidos.
- ** Manifiestos del paquete **: Manifiestos ( Paquete.xml ) proporcionan metadatos sobre un paquete, incluyendo su nombre, la versi�n , la descripci�n, informaci�n sobre la licencia , las dependencias , y otra informaci�n de meta como paquetes exportados . El manifiesto del paquete package.xml se define en el REP- 0127 .
- **Repositorios**: Una colecci�n de paquetes que comparten un sistema VCS com�n. Paquetes que comparten un VCS comparten la misma versi�n y puede ser liberado junto con la versi�n amento herramienta de automatizaci�n de la floraci�n. A menudo, estos dep�sitos se asignar�n a Stacks rosbuild convertidos. Repositorios tambi�n pueden contener s�lo un paquete.
- **(NVI) Tipos**: Descripciones de los mensajes almacenados en my_package / msg / MyMessageType.msg , definen las estructuras de datos para los mensajes enviados en ROS .
- **Servicio (SRV) tipos**: Descripciones del servicio , almacenados en my_package / srv / MyServiceType.srv , definen la solicitud y las estructuras de datos de respuesta para los servicios de ROS .

Nivel Gr�fico Computaci�n
-----------

La Computaci�n Gr�fica es la red de procesos de ROS que se est�n procesando los datos en conjunto de peer -to-peer . Los conceptos b�sicos de Computaci�n Gr�fica de ROS son * linf�ticos *, * maestro *, * Parameter Server * , * mensajes * , * Servicios *, * temas * , y * bolsas * , todos los cuales proporcionan datos a la gr�fica de diferentes maneras.

Estos conceptos son implementados en el repositorio [ ros_comm ] ( http://wiki.ros.org/ros_comm ) .

- [ ** Nodos ** ] ( http://wiki.ros.org/Nodes ) : Los nodos son procesos que realizan el c�lculo . ROS est� dise�ado para ser modular en una escala de grano fino ; un sistema de control del robot comprende por lo general muchos nodos . Por ejemplo , un nodo controla un tel�metro de l�ser , un nodo controla los motores de las ruedas , un nodo lleva a cabo la localizaci�n , un nodo realiza planificaci�n de trayectoria , un Nodo proporciona una vista gr�fica del sistema , y as� sucesivamente . Un nodo de ROS se escribe con el uso de un [ biblioteca de cliente ] ROS ( http://wiki.ros.org/Client % 20Libraries ) , como [ roscpp ] ( http://wiki.ros.org/roscpp ) o [ Rospy ] ( http://wiki.ros.org/rospy ) .
- [** Maestro **] ( http://wiki.ros.org/Master ) : El ROS Master proporciona el registro de nombres y b�squeda para el resto de la Computaci�n Gr�fica . Sin el Maestro , los nodos no ser�an capaces de encontrar unos a otros mensajes de cambio, o invocar servicios .
- [** Par�metro Servidor **] ( http://wiki.ros.org/Parameter % 20Server ) : El servidor de par�metros permite que los datos sean almacenados por la clave en una ubicaci�n central . Actualmente forma parte del M�ster .
- [Mensajes ** **] ( http://wiki.ros.org/Messages ) : Los nodos se comunican entre s� mediante el paso [ mensajes ] ( http://wiki.ros.org/Messages ) . Un mensaje es simplemente una estructura de datos , que comprende los campos con tipo. Se admiten los tipos primitivos est�ndar (entero , coma flotante , booleanos , etc ) , as� como los arreglos de tipos primitivos. Los mensajes pueden incluir estructuras y arrays anidados arbitrariamente (parecido C estructuras) .
- [** Temas **] ( http://wiki.ros.org/Topics ) : Los mensajes se enrutan a trav�s de un sistema de transporte con la publicaci�n / suscripci�n sem�ntica. Un nodo env�a un mensaje mediante su publicaci�n en un determinado [ tema ] ( http://wiki.ros.org/Topics ) . El tema es un [ nombre ] ( http://wiki.ros.org/Names ) que se utiliza para identificar el contenido del mensaje . Un nodo que est� interesado en un determinado tipo de datos suscribir� el tema correspondiente. Puede haber m�ltiples editores y suscriptores concurrentes para un solo tema , y un �nico nodo puede publicar y / o suscribirse a m�ltiples temas. En general , los editores y suscriptores no son conscientes de la existencia de los dem�s. La idea es disociar la producci�n de informaci�n de su consumo . L�gicamente , se puede pensar en un tema como un bus de mensajes inflexible de tipos. Cada autob�s tiene un nombre, y cualquier persona puede conectarse al bus para enviar o recibir mensajes mientras son del tipo correcto .
[] ( http://ros.org/images/wiki/ROS_basic_concepts.png )

- [** Servicios **] ( http://wiki.ros.org/Services ) : El modelo de publicaci�n / suscripci�n es un paradigma de comunicaci�n muy flexible , pero su - muchos-a- muchos, el transporte de ida no es apropiado para petici�n / respuesta interacciones , que a menudo se requieren en un sistema distribuido. Petici�n / respuesta se realiza a trav�s de servicios , que se definen por un par de estructuras de mensajes : uno para la solicitud y uno por la respuesta. Un nodo que proporciona ofrece un servicio con un nombre y un cliente utiliza el servicio mediante el env�o del mensaje de solicitud y en espera de la respuesta. Bibliotecas de cliente ROS generalmente presentan esta interacci�n para el programador como si fuera una llamada a procedimiento remoto.
- [** Bolsas **] ( http://wiki.ros.org/Bags ) : Las bolsas son un formato para guardar y reproducir datos de mensajes de ROS . Las bolsas son un mecanismo importante para el almacenamiento de datos, como los datos de los sensores , que pueden ser dif�ciles de recoger , pero es necesario para desarrollar y probar algoritmos.

El ROS maestro act�a como un servicio de nombres en el ROS Computaci�n Gr�fica . Almacena temas y servicios de informaci�n de registro para los nodos ROS . Los nodos se comunican con el Maestro de reportar su informaci�n de registro. A medida que estos nodos se comunican con el Maestro , pueden recibir informaci�n sobre otros nodos inscritos y hacer las conexiones , seg�n corresponda. El Maestro tambi�n har� devoluciones de llamada a estos nodos cuando se ejecutan estos cambios en la informaci�n de registro , lo que permite que los nodos para crear din�micamente las conexiones como nuevos nodos.

Los nodos se conectan a otros nodos directamente ; el Maestro s�lo proporciona informaci�n de b�squeda , al igual que un servidor DNS. Los nodos que se suscriben a un tema solicitar�n las conexiones desde los nodos que publican ese tema , y se establecer� que la conexi�n a trav�s de un acuerdo sobre la protocolo de conexi�n . El protocolo m�s com�n que se utiliza en un ROS se llama [ TCPROS ] ( http://wiki.ros.org/ROS/TCPROS ), que utiliza sockets TCP / IP est�ndar .


Esta arquitectura permite una operaci�n desconectada , donde los nombres son el medio principal por el que los sistemas m�s grandes y complejos se pueden construir . Los nombres tienen un papel muy importante en ROS: nodos , los temas , los servicios y todos los par�metros tienen nombre. Cada ROS soportes biblioteca cliente [ Reasignaci�n de l�nea de comandos de nombres ] ( http://wiki.ros.org/Remapping % 20Arguments ) , lo que significa un programa compilado se pueden reconfigurar en tiempo de ejecuci�n para operar en una topolog�a de Computaci�n Gr�fica diferente.

----

Por ejemplo, para controlar un tel�metro l�ser Hokuyo , podemos iniciar el controlador hokuyo_node , que habla con el l�ser y publica sensor_msgs / messages LaserScan sobre el tema de an�lisis. Para procesar los datos , podr�amos escribir un nodo utilizando laser_filters que se suscribe a los mensajes sobre el tema de an�lisis. Tras la suscripci�n , nuestro filtro comenzar� autom�ticamente a recibir mensajes desde el l�ser.

Observe c�mo se desacoplan los dos lados. Todo el nodo hokuyo_node hace es publicar exploraciones , sin el conocimiento de si alguien est� suscrito . Todo el filtro no se suscriben a las exploraciones , sin el conocimiento de si alguien los est� publicando . Los dos nodos se pueden iniciar, asesinados, y arrancar� de nuevo en cualquier orden, sin inducir las condiciones de error .

M�s tarde podr�amos a�adir otro l�ser a nuestro robot, as� que tenemos que volver a configurar nuestro sistema. Todo lo que necesitamos hacer es volver a asignar los nombres que se utilizan . Cuando comenzamos nuestra primera hokuyo_node , podr�amos decir que en lugar de reasignar exploraci�n para base_scan , y hacer lo mismo con nuestro nodo de filtro. Ahora , tanto de estos nodos se comunican mediante el tema base_scan lugar y no escuchar los mensajes sobre el tema de exploraci�n . Entonces s�lo podemos comenzar otra hokuyo_node para el nuevo tel�metro l�ser.



nivel comunitario
-----------

Los conceptos ROS Comunidad de nivel son ROS recursos que permitan a las comunidades separadas para intercambiar software y conocimiento. Estos recursos incluyen :

- [**Distribuciones**] ( http://wiki.ros.org/Distributions ) : ROS Distribuciones son colecciones de pilas versionados que se pueden instalar . Las distribuciones juegan un papel similar al de las distribuciones de Linux : hacen m�s f�cil la instalaci�n de una colecci�n de software, y tambi�n mantienen versiones consistentes en un conjunto de software.
- [** Repositorios **] ( http://wiki.ros.org/Repositories ) : ROS basa en una red federada de repositorios de c�digo , en los que diferentes instituciones puedan desarrollar y lanzar sus propios componentes de software del robot.
- [** El ROS Wiki **] ( http://wiki.ros.org/Documentation ) : La comunidad ROS Wiki es el principal foro para la documentaci�n de informaci�n sobre ROS . Cualquier persona puede inscribirse para una cuenta y contribuir con su propia documentaci�n , proporcionar correcciones o actualizaciones , escribir tutoriales y m�s.
- ** Sistema de Tickets Bug **: Por favor, vea [ Entradas ] ( http://wiki.ros.org/Tickets ) para obtener informaci�n sobre las entradas de archivo.
- [** Listas de Correo **] ( http://wiki.ros.org/Mailing % 20Lists ) : Los ros- lista de distribuci�n es el principal canal de comunicaci�n sobre los nuevos cambios a ROS , as� como un foro para hacer preguntas sobre el software ROS .
- [** ROS Respuestas **] ( http://answers.ros.org/ ) : Un Q & A sitio para responder a sus preguntas relacionadas con Ros- .
- [** Blog **] ( http://www.willowgarage.com/blog ) : El [ Blog Willow Garage ] ( http://www.willowgarage.com/blog ) proporciona actualizaciones regulares, incluyendo fotos y videos.

Nombrando
------

# # # Nombres Gr�fico de recursos

Nombres de recursos Gr�fica proporcionan una estructura de nombres jer�rquico que se utiliza para todos los recursos en un ROS Computaci�n Gr�fica , como nodos , Par�metros , Temas, y Servicios. Estos nombres son muy poderosos en ROS y central a c�mo los sistemas m�s grandes y complejas se componen de ROS, por lo que es fundamental para entender c�mo estos nombres funcionan y c�mo se pueden manipular .

Antes de describir los nombres m�s , he aqu� algunos ejemplos de nombres :

- / ( El espacio de nombres global)
- / Foo
- / Stanford / robot / Nombre
- / Wg/node1

Nombres de recursos gr�fica son un mecanismo importante en ROS para proporcionar encapsulaci�n. Cada recurso se define dentro de un espacio de nombres , que se puede compartir con muchos otros recursos. En general , los recursos pueden crear recursos dentro de su espacio de nombres y que puedan acceder a los recursos dentro o por encima de su propio espacio de nombres. Se pueden hacer conexiones entre los recursos de los espacios de nombres distintos, pero eso se hace generalmente por c�digo de integraci�n por encima de los dos espacios de nombres. Esta encapsulaci�n a�sla diferentes partes del sistema de agarrar accidentalmente el recurso incorrecto nombrado o globalmente secuestrar nombres.

Los nombres se resuelven relativamente , por lo que los recursos no tienen que ser conscientes de que el espacio de nombres que est�n adentro Esto simplifica la programaci�n como nodos que trabajan en conjunto se pueden escribir como si todos ellos est�n en el espacio de nombres de nivel superior. Cuando estos nodos est�n integrados en un sistema m�s grande , que pueden ser empujados hacia abajo en un espacio de nombres que define su colecci�n de c�digo . Por ejemplo , se podr�a tomar una demo de Stanford y una versi�n parcial de Willow Garage y fusionarlas en una nueva demo con stanford y subgrafos wg . Si las dos demos tuvieron un nodo llamado "c�mara" , que no entren en conflicto . Herramientas de visualizaci�n gr�fica (por ejemplo ), as� como los par�metros ( por ejemplo demo_name ) que deben ser visibles para todo el gr�fico se pueden crear nodos de nivel superior .

# # # # Nombres v�lidos

Un nombre v�lido tiene las siguientes caracter�sticas :

. 1 El primer car�cter es un car�cter alfab�tico ( [az | AZ] ) , tilde ( ~ ) o barra diagonal (/ )
. 2 caracteres siguientes pueden ser alfanum�rica ( [ 0-9 | az | AZ] ) , guiones bajos ( _), o barras diagonales ( / )

------

** ** Excepci�n : los nombres de bases ( descritos a continuaci�n) no puede tener barras diagonales (/) o tildes ( ~) en ellos.

------
# # # # Resolver

Hay cuatro tipos de recursos Nombres Gr�fico en ROS : base , en relaci�n , a nivel mundial , y privadas , que tienen la siguiente sintaxis :

- Base
- Relativa / Nombre
- / Global / Nombre
- ~ Privado / Nombre


Por defecto , la resoluci�n se realiza en relaci�n con el espacio de nombres del nodo. Por ejemplo , el nodo `/ wg/node1 ` tiene el espacio de nombres `/ wg ` , por lo que el nombre de nodo 2 se resolver� en `/ wg/node2 ` .

Nombres sin calificadores de espacio de nombres en absoluto son nombres de base . Nombres base son en realidad una subclase de nombres relativos y tienen las mismas reglas de resoluci�n . Nombres de base se utilizan con mayor frecuencia para inicializar el nombre de nodo.

Los nombres que comienzan con un "/" son globales - que se consideran totalmente resueltos. * Los nombres globales deben evitarse tanto como sea posible , ya que limitan la portabilidad del c�digo * .

Los nombres que comienzan con un "~" son privadas. Convierten el nombre del nodo en un espacio de nombres . Por ejemplo , el nodo 1 en espacio de nombres `/ wg /` tiene el espacio de nombres privado `/ wg/node1 ` . Nombres privados son �tiles para pasar par�metros a un nodo espec�fico a trav�s del servidor de par�metros.

Estos son algunos ejemplos de resoluci�n de nombres :

| Node | relativa ( por defecto) | Global | Privado |
| - | - | - | - |
| ` / Node1 ` | ` bar -> / bar ` | `/ bar -> / bar ` | `~ bar -> / node1/bar ` |
| ` / wg/node2 ` | ` bar -> / wg / bar ` | `/ bar -> / bar ` | `~ bar -> / wg/node2/bar ` |
| ` / Wg/node3 ` | ` foo / bar -> / wg / foo / bar ` | `/ foo / bar -> / foo / bar ` | `~ foo / bar -> / wg/node3/foo/bar `|

# # # # Reasignaci�n

Cualquier nombre dentro de un nodo ROS se puede reasignar al iniciar el nodo en la l�nea de comandos. Para obtener m�s informaci�n sobre esta funci�n, consulte [ Reasignaci�n Argumentos ] ( http://wiki.ros.org/Remapping % 20Arguments ) .

# # # Nombres de los recursos del paquete

Paquete Nombres de los recursos se utilizan en ROS con los conceptos del sistema de archivos de nivel para simplificar el proceso de hacer referencia a archivos y tipos de datos en el disco . Paquete Nombres de los recursos son muy simples : no son m�s que el nombre del paquete que el recurso est� en m�s el nombre del recurso. Por ejemplo , el nombre ` std_msgs / Cadena ` se refiere a la "Cadena" tipo de mensaje en el " std_msgs " Package.

Algunos de los archivos relacionados con los ROS que se puede hacer referencia a la utilizaci�n del paquete Nombres de recursos incluyen:

- [ Mensaje ( msg) tipos ] ( http://wiki.ros.org/msg )
- [ Servicio (SRV) tipos ] ( http://wiki.ros.org/srv )
- [ Tipos de nodo ] ( http://wiki.ros.org/Nodes )

Paquete Nombres de los recursos son muy similares a presentar sendas , excepto que son mucho m�s cortos . Esto es debido a la capacidad de ROS para localizar paquetes en el disco y hacer suposiciones adicionales acerca de su contenido . Por ejemplo , las descripciones de mensajes siempre se almacenan en el subdirectorio ` msg ` y tienen la extensi�n ` . ` Msg, por lo que ` std_msgs / Cadena ` es la abreviatura de ` ruta / al / std_msgs / msg / String.msg ` . Del mismo modo , el tipo de nodo ` foo / bar ` es equivalente a la b�squeda de un archivo llamado ` bar ' en el paquete ` foo ` con permisos de ejecuci�n .

# # # # Nombres v�lidos

Nombres de los recursos del paquete tienen estrictas reglas de nomenclatura , ya que a menudo se utilizan en el c�digo generado autom�ticamente. Por esta raz�n, un paquete de ROS no puede tener caracteres especiales que no sean un gui�n bajo , y deben comenzar con un car�cter alfab�tico . Un nombre v�lido tiene las siguientes caracter�sticas :

1. El primer car�cter es un car�cter alfab�tico ( [az | AZ] )
2. caracteres siguientes pueden ser alfanum�rica ( [ 0-9 | az | AZ] ) , guiones bajos ( _ ) o una barra diagonal (/ )
3. Hay a lo sumo una barra ( '/') .

