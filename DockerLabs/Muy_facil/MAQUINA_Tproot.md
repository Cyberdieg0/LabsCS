## Resolución máquina tproot

Comenzamos haciendo un escaneo de la ip victima 


podemos ver que tiene el puerto 21 y el 80 abiertos, por lo que verifico el puerto 80 y tiene un servidor apache




Realice una busqueda de vsftpd 2.3.4 y encuentro que la vulnerabilidad es un backdoor que se encuentra en el puerto 6200, en esta version esta el protocolo tcp










Ahora me conecto a FTP usando el usuario “user:)” y usando cualquier contraseña, esto para acticar el backdoor y abrir el puerto 6200



activado el backdoor, me conecto al puerto 6200 con netcat
podemos ver que somos root, pero en este  laboratorio debemos buscar una flag




Me moví entre directorios para buscar a flag y la encontramos en el  fichero root



Y como podemos ver la flag está hasheada:



Luego de intentar descifrarla y no tener resultados positivos damos por hecho que aqui terminamos la resolución de esta máquina.









## Como corregir esta vulnerabilidad

Este backdoor fue introducido por un atacante que comprometió el servidor de descarga de vsftpd en 2011. Solo las versiones descargadas de fuentes comprometidas contenían el backdoor.

El backdoor solo existe en vsftpd 2.3.4. Versiones posteriores corrigieron esta vulnerabilidad.

Lo mejor en estos casos sería tomar medidas de seguridad generales para servicios FTP, cómo deshabilitar y en vez de eso utilizar SFTP, ya que nos ofrece cifrado de extremo a extremo. Si en caso se debe usar FTP se podria implementar FTPS, restringir el acceso con firewall, etc




