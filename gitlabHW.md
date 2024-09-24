# Домашнее задание к занятию "`Zabbix_vol1`" - `Османов Ренат`
![img](/img/zabbix/zabbix1.1.png)

### Задание 1

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


````
stages:
  - test
  - build

test:
  stage: test
  image: golang:1.17
  script:
   - go test .

build:
    stage: test
    image: docker:latest
    script:
        docker build .
````

![img](/img/gitlab2.3.pnf)

