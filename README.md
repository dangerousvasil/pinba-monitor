# How to
```
mysql ----------------------\/
php -> pinba(mysql) -> collectd -> ingluxDB -> grafana
```

# Set up php
Install on php-application server php-pinba extension and setup it send statistic to host and 30002 port machine with running service.

## Build collectd dbi mysql driver 
```
cd collectd
docker build -t collectd_dbi_mysql .
```
## Setup pinba mysql  
```
cd pinba
docker-composer up
```
Open pinba server from you mysql client and __add user__ or change permissions for current user
```
UPDATE mysql.user SET `host`='%' WHERE `host`='localhost';
```
Save state of container and tag it, else all changes will be dropped
```
docker ps

# CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS               NAMES
# 7f752cf2af4c        tony2001/pinba      "/local/mysql/bin/..."   About a minute ago   Up About a minute                       pinba_pinba_1

docker commit 7f752cf2af4c  pinba_users
```


## Run service
```
$ docker-compose up -d
```

Then you can open:
- <http://localhost:8083>  influxdb admin page
- <http://localhost:3000>  grafana web page (login with admin/admin)
- <http://localhost:3306>  mysql server


## Configure collectd.conf

Read instruction and you can collect you stats 
by setup collectd/collectd.conf

