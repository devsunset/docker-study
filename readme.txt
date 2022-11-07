-------------------------------------------------

			# DOCKER-WORK #

-------------------------------------------------
# Docker

https://www.docker.com/

https://docs.docker.com/

https://hub.docker.com/

https://kubernetes.io/


########################################################
# Reference

https://github.com/alicek106/start-docker-kubernetes

https://www.yalco.kr/36_docker/

https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html
https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html

http://pyrasis.com/private/2014/11/30/publish-docker-for-the-really-impatient-book

########################################################
# Docker Install

uname -r 
커널 버젼 확인 최소 3.10 버전 이상에서 도커 정상 구동됨

getconf LONG_BIT
64bit 실행 권장 32bit 에서도 가능 하나 권장 하지 않음

sudo 명령어를 통해 설치 하거나 root 권한을 소유한 계정으로 설치 진행

- Install
* ubuntu 18.04, 20.04
# curl -fsSL https://download.docker.com/linux/ubuntu/gpg  | sudo apt-key add -
# add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(slb_release -cs) stable"
# apt-get update
# apt-get install docker-create

* CentOS 7, RHEL 7
# yum install -y yum-utils
# yum-config -manager --add-repo https://dwonload.docker.com/linux/centos/docker-ce.repo
# yum install -y docker-ce
# systemctl start docker 

* docker 설치 제공 스크립트 (비추천)
# wget -q0- get.docker.com | sh 

docker는 리눅스에서 설치 운영 하는게 맞으나 Windows , Mac에서 사용 가능 (Docker Desktop)
Mac - xhyve - sierra 10.13 이상
https://docs.docker.com/desktop/install/mac-install/

Windows - Hyper-V  - wnidow 10 이상
https://docs.docker.com/desktop/install/windows-install/

Docker Desktop 네트워크 , 볼륨 기능 등이 일부 미지원 

관리자 계정(root) 가 아닌 일반 유저 계정으로 docker를 실행하는 법
1. 도커 그룹 생성 
    sudo groupadd docker
2. 현재 유저를 도커 그룹에 포함
    sudo usermod -aG docker $USER
3. 접근 에러가 발생하지 않도록 미리 권한 열기 
    sudo chmod 666 /var/run/docker.sock
4. docker 서비스 재시작 or reboot
    sudo service docker restart
5. 실행 확인
    docker run hello-world

########################################################
# Docker Simple Review
https://www.yalco.kr/36_docker/
git clone https://gitlab.com/yalco/practice-docker.git

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

########################################################
# Docker 

docker info
도커 정보 확인

docker version
docker -v
도커 버젼 확인

docker run ubuntu
도커 컨테이너 다운로드 및 실행 

docker run -it ubuntu bash
-i 상호 입출력 옵션
-t tty 활성화 
위 명령어 한 번으로 컨테이너 생성 (이미지 다운로드) 및 실행과 동시에 컨테이너 내부로 진입 
ex)
ubuntu@ubuntu2004:~$ docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
e96e057aae67: Pull complete 
Digest: sha256:4b1d0c4a2d2aaf63b37111f34eb9fa89fa1bf53dd6e4ca954d47caebca4005c2
Status: Downloaded newer image for ubuntu:latest

root@96252752ab9d:/# ls
bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  etc  lib   lib64  media   opt  root  sbin  sys  usr

호스트명은 16진수 해시 값으로 랜덤하게 생성됨

컨테이너 종료 후 돌아오기     : exit , Ctrl-D
컨테이너 종료 없이 돌아오기  : Ctrl-Q  or Ctrl-P

docker search image_name
도커 이미지 검색

image name : [저장소 이름]/[이미지 이름]:[태그]   
[저장소 이름] : 이미지가 저장된 장소 , 없으면 기본적으로 제공하는 이미지 저장소인 docker hub의 공식 이미지 , 생성할때 필수 항목이 아니므로 생략할수도 있음
[이미지 이름] : 생략 불가 
[태그] : 생략 가능 - 생략하면 도커 엔진은 이미지의 태그를 latest로 인식

docker images [OPTIONS] [REPOSITORY[:TAG]]

docker images [OPTIONS] [REPOSITORY[:TAG]]
docker images
도커 이미지 목록 출력

docker pull image_name:latest
ex) docker pull centos:latest
도커 이미지 다운로드 

docker create -i -t --name mycentos centos:latest
도커 컨테이너 생성 ( create  명령어로 컨테이너 생성시 run 명령어와 다르게 실행되지 않고 내부로 진입 하지 도 않음)

docker start mycentos 
컨테이너 시작

docker attach mycentos 
내부로 진입 

docker start [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker attach [OPTIONS] CONTAINER [CONTAINER...]

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
컨테이너 목록 확인 

docker rm [OPTIONS] CONTAINER [CONTAINER...]
docker rm -v $(docker ps -a -q -f status=exited)
컨테이너 삭제

docker rmi [OPTIONS] IMAGE [IMAGE...]
이미지 삭제 

docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
docker exec -it mysql /bin/bash
컨테이너 내부 콘솔 접속 

docker logs [OPTIONS] CONTAINER
docker logs --tail 10 ${WORDPRESS_CONTAINER_ID}
로그 확인



########################################################
# EXAMPLE

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

