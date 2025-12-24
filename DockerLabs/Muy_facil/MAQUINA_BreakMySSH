## Resolución máquina BreakMySSH

Comenzamos haciendo un escaneo de puertos



vemos que tiene el puerto 22 abierto, un servicio ssh version openssh 7.7. Este servicio permite enumerar usuarios válidos sin necesidad de contraseña

—--------------------------------------------

haremos un ataque de fuerza bruta, no tenemos usuario ni password, en este tipo de CTFs el usuario a veces es root por lo que intentaremos con ese



el usuario coincidio y encontró un password que es “estrella”, asi que accedere por el puerto 22 

—---------------------------------------------





entre siendo usuario root por lo que está comprometida la máquina





---------------------------------------------

## Como corregir esta vulnerabilidad 
Estas son algunas de las soluciones para este tipo de vulnerabilides:

La versión OpenSSH 7.7 es vulnerable a CVE-2018-15473 (enumeración de usuarios) por lo que se debe actualizar SSH

El usuario root es el objetivo principal de los ataques por lo que debe deshabilitarse su acceso directo por SSH. Una alternativa más segura es crear un usuario no privilegiado y usar sudo para tareas administrativas

Las contraseñas son vulnerables a ataques de fuerza bruta. La autenticación por clave pública es mucho más segura

Mover SSH del puerto 22 reduce significativamente el tráfico de bots automatizados





