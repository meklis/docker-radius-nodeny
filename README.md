# DHCP-радиус c Nodeny API в docker


### Установка и запуск 
1. Установить git, docker и docker-compose
2. Выполнить
```
cd /opt # Можно любой другой
git clone https://github.com/meklis/docker-radius-nodeny.git
cd docker-radius-nodeny
cp .env-example .env
```
3. В файле .env указать корректные данные для подключения к базе и секрет радиуса
4. Выполнить   
``` 
   docker-compose up -d 
```   
В результате по команде `docker ps` должно отображаться два контейнера: 
``` 
# docker ps
CONTAINER ID        IMAGE                         COMMAND                  CREATED             STATUS              PORTS               NAMES
acbb6109ce6a        nodeny-radius_radius-api      "/bin/sh -c 'envsubs…"   2 hours ago         Up 14 seconds                           radius-api
4cc4b949d43e        nodeny-radius_radius-server   "/opt/all-ok-radius …"   2 hours ago         Up 14 seconds                           radius-server
```
