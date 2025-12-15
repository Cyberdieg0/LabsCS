Resolución máquina FirstHacking

primero hacemos un escaneo argumentando el servicio y la versión del
servicio que en este caso es un ftp, protocolo de transferencia de
archivos corriendo en el puerto 21 con un SO unix

![image alt](https://github.com/Cyberdieg0/LabsCS/blob/main/images/ss11.png?raw=true)

-------------------------------------------------------------------------------------------------

revisaremos si el servicio nos permite un login anónimo

![image alt](https://github.com/Cyberdieg0/LabsCS/blob/main/images/ss12.png?raw=true)

lo que hice fue hacer una busqueda en google \"CVE vsftpd 2.3.4\" que
es el servicio que aparece en esta maquina y el resultado de la búsqueda
nos indica que tiene un backdoor

esta vulnerabilidad consiste en que si en ftp al ingresar de usuario un
\": )\" esto abrira una bind shell en el puerto 6200

--------------------------------------------------------------------------------------------------

un Bind Shell es un programa ejecutado en la máquina de la víctima que
abre un puerto de red y se queda escuchando ese puerto, el atacante se
conecta directamente a este puerto para obtener una terminal de comandos
y así controlar la máquina remotamente

![image alt](https://github.com/Cyberdieg0/LabsCS/blob/main/images/ss13.png?raw=true)

es un comando que imprime texto en la terminal tal cual se lo escribamos

\"USER backdoor:)\\r\\n\"

es el texto que enviará

ESto es un comando ftp que esta enviando el usuario llamado backdoor:)

\\r\\n significa carriage return + newline, lo cual lo busque y es
\"salto de línea estilo Windows.\"

FTP obliga a usar este tipo de salto de línea para que el servidor
entienda el comando.

El comando crea el texto USER backdoor:) con el salto de línea correcto
para FTP y lo envía directamente como entrada a netcat, que lo conectará
al servidor FTP en 172.17.0.2 por el puerto 21, simulando que estás
enviando un usuario.

la respuesta depende de lo que envio el servidor, en este caso 220 nos
dice que el servicio esta listo, 331 dice que este acepto el usuario y
ahora pide el password

Entonces cuando cuando recibe \"331 Please specify the password\" es la
señal de que el backdoor ya esta activo y que ya puede conectarse al
puerto 6200 y obtener una bind shell

-------------------------------------------------------------------------------------

en otra terminal usamos nc 172.17-0-2 6200, aqui el comanto netcat (nc)
se usa para que establezcamos una conexion directa con un puerto
especifico, en este caso el puerto 6200

![image alt](https://github.com/Cyberdieg0/LabsCS/blob/main/images/ss14.png?raw=true)

En esta maquina había un backdoor oculto creado dentro del código de
vsftpd

Ese backdoor abre una shell interactiva pero no por el puerto 21 sino
por un puerto alternativo, generalmente el 6200

al ejecutarlo netcat intentara conectarse al puerto 6200 de la maquina
victima

el backdoor funciono correctamente por lo que netcat mostrara una shell
que nos confirma que tuvimos acceso

------------------------------------------------------------------------------------

![image alt](https://github.com/Cyberdieg0/LabsCS/blob/main/images/ss15.png?raw=true)

luego de que en la bind shell escribieramos el comando whoami y nos devolviera que somos usuario root podemos darnos cuenta que en esta maquina ya nos dieron todos los privilegios, por lo que aqui terminariamos de resolver esta maquina
