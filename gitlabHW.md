# Домашнее задание к занятию "`Zabbix_vol1`" - `Османов Ренат`


### Задание 1

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/zabbix_vol1/zabbzabbix1.1.png)


````
apt update && apt upgrade -y
apt install postgresql -y
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'zabbix\'';"'
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
systemctl restart zabbix-server zabbix-agent nginx php7.4-fpm
systemctl enable zabbix-server zabbix-agent nginx php7.4-fpm

````

### Задание 2
![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/zabbix_vol1/zabbzabbix2.1.png)
![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/zabbix_vol1/zabbzabbix2.2.png)
![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/zabbix_vol1/zabbzabbix2.3.png)



````
wget --no-check-certificate https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
sed 's/https/http/g' /etc/apt/sources.list.d/zabbix.list -i
sed 's/https/http/g' /etc/apt/sources.list.d/zabbix-agent2-plugins.list -i
apt install zabbix-agent net-tools
sed 's/Server=127.0.0.1/Server=192.168.56.10/g' /etc/zabbix/zabbix_agentd.conf -i
systemctl restart zabbix-agent
systemctl enable zabbix-agent
ifconfig
````


