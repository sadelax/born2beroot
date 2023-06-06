# Born to be root
script que provee info sobre tu ordenador llamado monitoring.sh. en el subject se pide que este script se ejecute cada 10 minutos, por lo que especificaremos con un administrador de tareas de Linux (`cron`) la ruta de monitoring.sh.
## explicación de los comandos
### architecture `uname -a`
para poder ver la arquitectura del SO y su versión de kernel. imprime la info excepto si el tipo de procesador ó el tipo de hardware son desconocidos.
### núcleos físicos `grep 'physical id' /proc/cpuinfo | wc -l`
para poder mostrar el número de núcleos físicos, los cuales se encuentran en /proc/cpuinfo. cada línea mostrada con `'physical id'` es un procesador, y así lo cuantificamos con `wc -l`. si hay 1 procesador marcará 0.
### núcleos virtuales `grep 'processor' /proc/cpuinfo | wc -l`
### memoria ram `free --mega`
para ver al momento info sobre la ram, la parte usada, libre, reservada para otros recursos, etc. `--mega` para verlo en megabytes.
### memoria del disco `df -BG`
para poder ver la memoria del disco ocupada y disponible.
### porcentaje uso de cpu `top -bn1 | grep '%Cpu' | awk '{printf("%.1f", $2+$4)}'`
para ver las tareas del sistema q se ejecutan en tiempo real
### último reinicio `who -b | cut -c23-`
para ver la fecha y hora del último reinicio. `who` da info a los usuarios q están conectados al sistema y también a otras infos como cuándo se arrancó al sistema y cuál es el nivel de ejecución del sistema. `-b` indica la hora.
### LVM activo `if [ $(lsblk | grep 'lvm' | wc -l) -gt 0 ]; then echo yes; else echo no; fi`
para checkear si LVM está activo o no haremos uso del comando `lsblk`, el cual muestra info de todos los dispositivos de bloque (discos duros, SSD, memorias, etc).
para este comando haremos un if *"si al contar el número de líneas q aparece lvm hay más de 0 imprime yes"*.
### conexiones tcp `grep 'TCP' /proc/net/sockstat | awk '{print($3)}'`
para mirar el número de conexiones tcp establecidas. en el archivo sockstat podemos encontrar dicha info.
### número de usuarios `users | wc -w`
### dirección ip `hostname -I`
### dirección mac `ip a | grep 'ether' | awk '{print $2}'`
para mostrar la info de la tabla de routing usamos el comando `ip a`
### número de comandos ejecutados con sudo `grep 'COMMAND' /var/log/sudo/sudo.log | wc -l`
el fichero sudo.log contiene registros sobre el uso del comando sudo.
### mostrar gráficamente el script `wall`
con `wall` se muestra un mensaje en los terminales de todos los usuarios registrados.





