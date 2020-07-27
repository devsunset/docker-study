-------------------------------------------------

			# DOCKER-WORK #

-------------------------------------------------


docker info

docker version

docker run hello-world

docker search image_name

docker images [OPTIONS] [REPOSITORY[:TAG]]
docker pull image_name:latest

docker images [OPTIONS] [REPOSITORY[:TAG]]
docker images

docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
-d      detached mode 흔히 말하는 백그라운드 모드
-p      호스트와 컨테이너의 포트를 연결 (포워딩)
-v      호스트와 컨테이너의 디렉토리를 연결 (마운트)
-e      컨테이너 내에서 사용할 환경변수 설정
–name   컨테이너 이름 설정
–rm     프로세스 종료시 컨테이너 자동 제거
-it     -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션
–link   컨테이너 연결 [컨테이너명:별칭]

docker ps [OPTIONS]
docker ps -a

docker start [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker attach [OPTIONS] CONTAINER [CONTAINER...]

docker rm [OPTIONS] CONTAINER [CONTAINER...]
docker rm -v $(docker ps -a -q -f status=exited)

docker rmi [OPTIONS] IMAGE [IMAGE...]

docker logs [OPTIONS] CONTAINER
docker logs --tail 10 ${WORDPRESS_CONTAINER_ID}

docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
docker exec -it mysql /bin/bash

########################################################

#ubuntu
docker run --rm -it ubuntu:16.04 /bin/bash

#redis
docker run -d -p 1234:6379 redis

# redis test
$ telnet localhost 1234
set mykey hello
+OK
get mykey
$5
hello

# mysql
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql

# MySQL test
$ mysql -h127.0.0.1 -uroot

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> quit

# before
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7

# after
docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  -v /my/own/datadir:/var/lib/mysql \ # <- volume mount
  mysql:5.7

#WordPress
# create mysql database
$ mysql -h127.0.0.1 -uroot
create database wp CHARACTER SET utf8;
grant all privileges on wp.* to wp@'%' identified by 'wp';
flush privileges;
quit

# run wordpress container
docker run -d -p 8080:80 \
  --link mysql:mysql \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_NAME=wp \
  -e WORDPRESS_DB_USER=wp \
  -e WORDPRESS_DB_PASSWORD=wp \
  wordpress

#tensorflow
docker run -d -p 8888:8888 -p 6006:6006 teamlab/pydata-tensorflow:0.1
