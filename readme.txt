-------------------------------------------------

			# DOCKER-WORK #

-------------------------------------------------


https://www.docker.com/
https://hub.docker.com/

https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html
https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html

http://pyrasis.com/private/2014/11/30/publish-docker-for-the-really-impatient-book

https://kubernetes.io/


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



#  도커 버전 확인
docker -v

#  도커 이미지 다운만 받기
docker pull {이미지명}:{태그}
# 예: docker pull python:3

#  컴퓨터 내 도커 이미지들 보기
docker images

# 이미지로 컨테이너 생성하기
docker create {옵션} {이미지명}:{태그}
# 예: docker create -it python

# 만들어진 컨테이너 시작하기 (이미지에 CMD로 지정해놓은 작업 시키기)
docker start {컨테이너 id 또는 이름}

# 컨테이너로 들어가기 (컨테이너 내 CLI 이용하기)
docker attach {컨테이너 id 또는 이름}

# 이미지를 다운받아(없을 시에만) 바로 컨테이너 실행하여 진입하기
docker run {이미지명}:{태그}
# 예: docker -it run python:3
* pull, create, start, attach 를 한꺼번에 실행하는 것과 같습니다.
옵션	설명
-d	데몬으로 실행(뒤에서 - 안 보이는 곳(백그라운드)에서 알아서 돌라고 하기)
-it	컨테이너로 들어갔을 때 bash로 CLI 입출력을 사용할 수 있도록 해 줍니다.
--name {이름}	컨테이너 이름 지정
-p {호스트의 포트 번호}:{컨테이너의 포트 번호}	호스트와 컨테이너의 포트를 연결합니다.
--rm	컨테이너가 종료되면{내부에서 돌아가는 작업이 끝나면} 컨테이너를 제거합니다.
-v {호스트의 디렉토리}:{컨테이너의 디렉토리}	호스트와 컨테이너의 디렉토리를 연결합니다.

# 동작중인 컨테이너 재시작
docker restart {컨테이너 id 또는 이름}

# 도커 컨테이너의 내부 쉘에서 빠져나오기 (컨테이너를 종료)
exit
* 또는 Ctrl + D

# 도커 컨테이너의 내부 쉘에서 빠져나오기 (컨테이너를 종료하지 않음)
* Ctrl + P, Q

# (동작중인) 컨테이너들 보기
docker ps
* 동작중이 아닌 것을 포함한 모든 컨테이너를 보려면 -a 옵션을 뒤에 붙입니다.

# 컨테이너 삭제
docker rm {컨테이너 id 또는 이름}

# 모든 컨테이너 삭제
docker rm `docker ps -a -q`

# 이미지 삭제
docker rmi {옵션} {이미지 id}
* 컨테이너가 있을 시 강제삭제: -f 옵션 사용

# 모든 컨테이너 중지
docker stop $(docker ps -aq)

# 사용되지 않는 모든 도커 요소(컨테이너, 이미지, 네트워크, 볼륨 등) 삭제
docker system prune -a

# 아래를 복붙하여 함께 실행하면 편리합니다.
docker stop $(docker ps -aq)
docker system prune -a
* 확인 질문에 y로 답하고 마무리합니다.

도커파일로 이미지 생성
# Dockerfile 파일이 있는 디렉토리 기준.  마지막의 . 이 상대주소
docker build -t {이미지명} .

도커 컴포즈 실행
# docker-compose 파일이 있는 디렉토리 기준
docker-compose up
* 백그라운드에서 데몬으로 돌도록 하려면 -d 옵션

