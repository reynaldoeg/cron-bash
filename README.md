# Cron Bash

Ejemplo de programa en bash que se ejecuta cada x minutos y hace un push automático a GitHub.

----------

## Archivo bash

```
#!/bin/bash
echo `date +'%F %T'` >> /home/reynaldoeg/Documents/cron-bash/cron.log
cd /home/reynaldoeg/Documents/cron-bash/
git commit -am "`date +'%F %T'`"
git push
```

La primera línea indica al sistema que programa usar para ejecutar el archivo.

```
#!/bin/bash
```
La segunda  línea imprime la fecha (date) en formato aaaa-mm-ddd hh:mm:ss (2019-01-16 10:45:01) y la envía al archivo cron.log; el doble signo de mayor que ( >> ) imprime la línea al final del archivo conservando el contenido existente, a diferencia del signo mayor que sencillo ( > ) que borra todo el contenido del archivo.
```
echo `date +'%F %T'` >> /home/reynaldoeg/Documents/cron-bash/cron.log
```
La siguiente línea entra a la carpeta del proyecto que está en github.
```
cd /home/reynaldoeg/Documents/cron-bash/
``` 
La siguiente línea hace un commit 
```
git commit -am "`date +'%F %T'`"
``` 
La última hace el push a github
```
git push
``` 


----------


## Crontab

### Introducción
<img src="http://blog.paolorossi.net/content/images/2017/07/linux-daemon-600.png" width="300">
Cron es un proceso del sistema (daemon) que se utiliza para ejecutar las tareas deseadas (en segundo plano) en los momentos designados.

Un archivo crontab es un archivo de texto simple que contiene una lista de comandos destinados a ejecutarse en momentos específicos. Se edita utilizando el comando crontab. Los comandos en el archivo crontab (y sus tiempos de ejecución) son verificados por el proceso cron, que los ejecuta en el fondo del sistema.

Cada usuario (incluyendo root) tiene un archivo crontab. El proceso cron comprueba el archivo crontab de un usuario independientemente de si el usuario está realmente conectado al sistema o no.

Para visualizar la ayuda en línea para crontab ingrese:

```
$ man crontab
```

### Empezando a usar Cron

Para usar cron para tareas destinadas a ejecutarse solo para su perfil de usuario, agregue entradas al archivo crontab de su propio usuario. Para editar el archivo crontab ingrese:

```
$ crontab -e
```
Edite el crontab usando el formato descrito en las siguientes secciones.  Para mostrar la ayuda en línea que describe el formato del archivo crontab, ingrese:
```
$ man 5 crontab
```
Los comandos que normalmente se ejecutan con privilegios administrativos (es decir, generalmente se ejecutan utilizando sudo) deben agregarse a la raíz crontab. Para editar la raíz crontab ingrese:
```
$ sudo crontab -e
```
### Líneas de Crontab
Al ejecutar el comando anterior se abre el siguiente archivo para poder editar los trabajos:

``` 
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').\# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
# 
# m h  dom mon dow   command

*/15 * * * * /home/reynaldoeg/bin/githubreyes.sh 

```

Cada línea tiene cinco campos de fecha y hora, seguidos de un comando, seguido de un carácter de nueva línea ('\ n'). Los campos están separados por espacios. Los cinco campos de fecha y hora no pueden contener espacios. Los cinco campos de fecha y hora son los siguientes: minuto (0-59), hora (0-23, 0 = medianoche), día (1-31), mes (1-12), día de la semana (0-6, 0 = domingo).
```
01 04 1 1 1 /usr/bin/algundirectorio/alguncomando
```
El ejemplo anterior ejecutará /usr/bin/algundirectorio/alguncomando a las 4:01 am del 1 de enero, más todos los lunes de enero.

Se puede usar un asterisco (*) para cada instancia (cada hora, cada día laborable, cada mes, etc.) de un período de tiempo.
```
01 04 * * * /usr/bin/algundirectorio/alguncomando
```
El ejemplo anterior ejecutará  /usr/bin/algundirectorio/alguncomando a las 4:01 am todos los días de cada mes.

Los valores separados por comas se pueden usar para ejecutar más de una instancia de un comando en particular dentro de un período de tiempo. Los valores separados por guiones se pueden usar para ejecutar un comando continuamente.
```
01,31 04,05 1-15 1,6 * /usr/bin/algundirectorio/alguncomando
```
El ejemplo anterior ejecutará /usr/bin/algundirectorio/alguncomando a las 01 y 31 horas después de las 4:00 a.m. y a las 5:00 a.m. del 1 al 15 de enero y junio de cada año.

## Más información

[https://help.ubuntu.com](https://help.ubuntu.com/community/CronHowto)

[https://www.tldp.org](https://www.tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)