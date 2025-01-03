 Домашнее задание к занятию «Redis/Memcached»-Османов Ренат


### Задание 1. Кеширование 

Приведите примеры проблем, которые может решить кеширование. 

ОТВЕТ: 

Кэширование позволяет увеличить скорость обработки запросов, снизить нагрузку на БД, увеличить стабильность при высоких нагрузках, а так же позволяет ускорить работу с медленными источниками данных. 

### Задание 2. Memcached

Установите и запустите memcached.

*Приведите скриншот systemctl status memcached, где будет видно, что memcached запущен.*

---
Решение:
Запушен в Docker 
'''
docker run --name test-cache -p 11211:11211 -d memcached
'''
![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/ssdb_vol2/ssdb_2.png)

### Задание 3. Удаление по TTL в Memcached

Запишите в memcached несколько ключей с любыми именами и значениями, для которых выставлен TTL 5. 

*Приведите скриншот, на котором видно, что спустя 5 секунд ключи удалились из базы.*

---

Решение:

![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/ssdb_vol2/ssdb_3.png)



### Задание 4. Запись данных в Redis

Запишите в Redis несколько ключей с любыми именами и значениями. 

*Через redis-cli достаньте все записанные ключи и значения из базы, приведите скриншот этой операции.*



---

Решение 
Запущен в Docker 

'''

docker run --name test-redis -d redis
# Так же зашел в redis-cli при помощи данной команды
docker exec -it test-redis redis-cli

'''


![img](https://github.com/racnuzg9u/netologyHW/blob/main/img/ssdb_vol2/ssdb_4.png)