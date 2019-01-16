# Cron Bash

Ejemplo de programa en bash que se ejecuta cada x minutos y hace un push automático a GitHub.

----------

## Archivo bash


```
#!/bin/bash
echo `date +'%F %T'` msg >> /home/reynaldoeg/Documents/cron-bash/cron.log
cd /home/reynaldoeg/Documents/cron-bash/
git commit -am "`date +'%F %T'` reyes"
git push
```


----------


## Crontab

Comando para editar los crones
```
$ crontab -e
```
Se abre el siguiente archivo para poder editar los trabajos:

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
