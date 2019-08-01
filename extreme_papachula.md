---
layout: post
title:  "Papachula Cookbook"
date:   2019-06-06 00:01:00 -0500
categories: [computer-config]
published: true
---

# Docker Images

## Oracle

### Pulling image

```
docker pull oracleinanutshell/oracle-xe-11g

```

### Installing container

```
docker run -d -p 49161:1521 oracleinanutshell/oracle-xe-11g

```

## MS SQL

### Pulling image

```
docker pull mcr.microsoft.com/mssql/server:2019-CTP2.5-ubuntu
```

### Installing container

```

docker run --name mssql -e ACCEPT_EULA=Y -e SA_PASSWORD=M@c@ren@347! -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-CTP2.5-ubuntu
```

### Running into bash

```
docker run -it --entrypoint /bin/bash mcr.microsoft.com/mssql/server:2019-CTP2.5-ubuntu -s

```

## MariaDB

#### Pulling image

```
docker pull mariadb
```

#### Installing container

```
docker run --name mariadb -e MYSQL_ROOT_PASSWORD=password -d mariadb:latest

```

# Docker commands

Stop/Start/		Restart all containers
```
docker [stop|start|restart] $(docker ps -a -q)
```
```
docker ps
docker images ls -al
docker rm _container_id_
docker inspect _container_id_
docker logs _container_id_

# Find container's ip
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' _container_
```

### Reference

* [Removing Docker Images](https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/)

* [Debug Container](https://vsupalov.com/debug-docker-container/)

* [Microsoft SQL Server Container](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-linux-ver15&pivots=cs1-bash#pullandrun2019)

* [MS SQL Server Container Troubleshooting](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-configure-docker?view=sql-server-linux-ver15#troubleshooting)

* [Logs](https://docs.docker.com/engine/reference/commandline/logs/)

* [Post Install Steps](https://docs.docker.com/install/linux/linux-postinstall/)






