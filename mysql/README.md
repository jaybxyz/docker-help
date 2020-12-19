# Running MySQL with Docker

## [1] Docker 

### [Official MySQL Docker Image](https://hub.docker.com/_/mysql)

```shell
# Search mysql in docker hub
docker search mysql

# Prevent from data will be reset after some test
mkdir data

# Run 
# -d: detach mode (run in background)
# -e: configure envrinment variables (https://hub.docker.com/_/mysql)
# -v 볼륨
# -p 포트 포워딩
# --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci (한글이 깨지지 않도록 설정)
docker run -d \
--name dev-mysql \
-e MYSQL_ROOT_PASSWORD=admin123 \
-p 3306:3306 \
-v $PWD/data/:/var/lib/mysql \
mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

# Check that the container is running
docker ps

# Stop and start
docker stop dev-mysql
docker start dev-mysql

# Enter the container with bash (MySQL 컨테이너 bash 쉘 접속)
docker exec -it dev-mysql bash
>>
> mysql -u root -p
> show databases;
> create database test; 
> use test;
> create table user (
    id int NOT NULL auto_increment primary key,
    name VARCHAR(15) NOT NULL,
    phone VARCHAR(15) NOT NULL
  );
> show tables;
> describe user;

# Check logs
docker logs dev-mysql
```

## [2] Docker Compose

`docker-compose.yml` 파일을 통한 컨테이너 생성 및 실행

```shell
# Docker Compose 설치
https://github.com/docker/compose/releases/

# Run docker-compose.yml that initializes postgresql database
docker-compose up
docker-compose up -d 
```