# Домашнее задание к занятию "`backupHW/backup`" - `Османов Ренат`


### Задание 1


![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/backupHW/backup1.1.png)


![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/backupHW/backup1.1.png)


### Задание 2


````
#!/bin/bash

src_dir="/home/vagrant/"
dest_dir="/tmp/backup/"
log_file="/var/log/syslog"


rsync -a --progress --delete --exclude='.*' $src_dir $dest_dir

if [ $? -ne 0 ]
        then
                echo "$(date) $(hostname) rsync : backupHW/backup creation failed!!!" >> $log_file
        else
                echo "$(date) $(hostname) rsync : backupHW/backup creation successfully" >> $log_file
fi
````




crontab task

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/backupHW/backup2.1.png)


Logs

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/backupHW/backup2.2.png)





