**Resolución de la máquina TRUST de DockerLabs\
**\
Comenzamos haciendo un escaneo con nmap\
Podemos ver que tiene el puerto 80 abierto, en el cual está corriendo un
servidor apache

al igual que tiene abierto el servicio ssh

![](media/image5.png){width="6.267716535433071in"
height="1.9305555555555556in"}

Ingresamos la ip de la maquina victima y nos devuelve esto:

![](media/image8.png){width="6.267716535433071in"
height="3.8055555555555554in"}

Con la herramienta gobuster para encontrar directorios o archivos
ocultos en el servidor web que en este caso es el apache

![](media/image10.png){width="6.267716535433071in"
height="2.6527777777777777in"}

Como podemos ver gobuster devolvió un archivo html y un php asi como un
server status, por curiosidad revise el .html copiandolo junto con la
url en el navegador, el cual no tuvo respuesta y luego pase al .php el
cual sí me respondió con este mensaje

![](media/image2.png){width="6.125in" height="2.5833333333333335in"}

La web pertenece a alguien llamado Mario por lo que es una pista para el
siguiente paso

En el escaneo aparte del puerto 80 mostró el 22, un servicio ssh, como
también tenemos la pista que el usuario de la web es alguien llamado
Mario procedemos a hacer un ataque de fuerza bruta con Hydra, ya que al
estar un servicio ssh y al tener un nombre de usuario lo que buscaremos
sera la contraseña de dicho usuario para tener acceso

Recordemos que Hydra es una herramienta que automatiza ataques de fuerza
bruta contra servicios de autenticación como ssh, ftp, http, probando
miles de combinaciones de usuario o contraseña hasta encontrar las
credenciales correctas

![](media/image9.png){width="6.267716535433071in"
height="2.388888888888889in"}

le indicamos a hydra que queremos la contraseña del usuario mario y
efectivamente pudo encontrarla que en este caso es "chocolate"

![](media/image7.png){width="6.267716535433071in" height="5.25in"}

pudimos entrar

ahora verificamos si tenemos el permiso de superusuario utilizando sudo
-l

![](media/image6.png){width="6.267716535433071in"
height="1.7083333333333333in"}

nos devuelve que tenemos que usar vim como usuario root, así que ahora
pasamos a explotar esto

recurri a GFTOBins, esta plataforma nos muestra cómo explotar este tipo
de programa para obtener una shell root o realizar acciones
privilegiadas.

![](media/image4.png){width="6.270833333333333in"
height="2.2968755468066493in"}

obtenido esto ejecutamos el siguiente comando:

![](media/image1.png){width="3.7604166666666665in"
height="0.8541666666666666in"}

lo cual nos devolverá que somos usuario root

![](media/image3.png){width="6.267716535433071in"
height="2.1527777777777777in"}

Listo, máquina resuelta.
