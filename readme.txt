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

https://www.yalco.kr/36_docker/

https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html
https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html

http://pyrasis.com/private/2014/11/30/publish-docker-for-the-really-impatient-book

https://github.com/alicek106/start-docker-kubernetes

########################################################
# Docker Install

#  커널 버젼 확인 최소 3.10 버전 이상에서 도커 정상 구동됨
uname -r 

#  64bit 실행 권장 32bit 에서도 가능 하나 권장 하지 않음
getconf LONG_BIT

#  sudo 명령어를 통해 설치 하거나 root 권한을 소유한 계정으로 설치 진행

#  Linux 설치
https://www.docker.com/
docker 공식 문서 가이드 내용에 따라 설치 

docker는 리눅스에서 설치 운영 하는게 맞으나 Windows , Mac에서 사용 가능 (Docker Desktop)
Mac - xhyve - sierra 10.13 이상
Windows - Hyper-V  - wnidow 10 이상
Docker Desktop 네트워크 , 볼륨 기능 등이 일부 미지원 

#  관리자 계정(root) 가 아닌 일반 유저 계정으로 docker를 실행하는 법
1. 도커 그룹 생성 
    sudo groupadd docker
2. 현재 유저를 도커 그룹에 포함
    sudo usermod -aG docker $USER
3. 접근 에러가 발생하지 않도록 권한 부여
    sudo chmod 666 /var/run/docker.sock
4. docker 서비스 재시작 or reboot
    sudo service docker restart
5. 실행 확인
    docker run hello-world

########################################################
# Docker  Getting started

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

# 만들어진 컨테이너 시작하기
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
-v {호스트의 디렉토리}:{컨테이너의 디렉토리}	호스트와 컨테이너의 디렉토리를 연결합니다.
--rm	컨테이너가 종료되면{내부에서 돌아가는 작업이 끝나면} 컨테이너를 제거합니다. (필요시만 사용)

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

# 아래를 복붙하여 함께 실행하면 편리
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
# Docker CMD

docker 
Usage:  docker [OPTIONS] COMMAND
A self-sufficient runtime for containers
Options:
      --config string      Location of client config files (default "/home/ubuntu/snap/docker/2285/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with
                           "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/ubuntu/snap/docker/2285/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/ubuntu/snap/docker/2285/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/ubuntu/snap/docker/2285/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  builder     Manage builds
  buildx*     Docker Buildx (Docker Inc., v0.8.2)
  compose*    Docker Compose (Docker Inc., v2.5.0)
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.

To get more help with docker, check out our guides at https://docs.docker.com/go/guides/

########################################################
# Docker Guide

# 도커 정보 확인
docker info

# 도커 버젼 확인
docker -v
docker version

# 도커 컨테이너 다운로드 및 실행 
docker run ubuntu

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

root@96252752ab9d:/# ls    (96252752ab9d 호스트명은 16진수 해시 값으로 랜덤하게 생성됨)
bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  etc  lib   lib64  media   opt  root  sbin  sys  usr

# 컨테이너 종료 후 돌아오기     : exit , Ctrl-D

# 컨테이너 종료 없이 돌아오기  : Ctrl-P,Q

# 도커 이미지 검색
docker search image_name

image name : [저장소 이름]/[이미지 이름]:[태그]   
[저장소 이름] : 이미지가 저장된 장소 , 없으면 기본적으로 제공하는 이미지 저장소인 docker hub의 공식 이미지 , 생성할때 필수 항목이 아니므로 생략할수도 있음
[이미지 이름] : 생략 불가 
[태그] : 생략 가능 - 생략하면 도커 엔진은 이미지의 태그를 latest로 인식

# 도커 이미지 목록 출력
docker images [OPTIONS] [REPOSITORY[:TAG]]
docker images

# 도커 이미지 다운로드 
docker pull image_name:latest
ex) docker pull centos:latest

# 도커 이미지 삭제
docker rmi [OPTIONS] IMAGE [IMAGE...]

# 도커 컨테이너 생성 
docker create -i -t --name mycentos centos:latest
( create  명령어로 컨테이너 생성시 run 명령어와 다르게 실행되지 않고 내부로 진입 하지 도 않음)

# 컨테이너 시작
docker start mycentos 

# 내부로 진입 
docker attach mycentos 

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

# 정지 되지 않은 컨테이너만 확인
docker ps [OPTIONS]
docker ps 

# 정지된 컨테이너 포함 전체 컨테이너 목록 확인 
docker ps -a
docker ps -a -q 
 (-a 컨테이너 상태와 관계없이 모든 컨터이너 , -q 컨테이너 ID만 출력)

# inspect 명령어로 컨테이너 전체 정보 확인 가능 위의 명령어는 Id 값 전체 값 확인 명령어 
docker inspect mycentos | grep Id

# 도커 name  변경 처리 
docker rename mycentos centos 

# 도커 ps 명령어 출력 항목 조정 처리 
docker ps --format "table {{.ID}}\t{{.Status}}\t{{.Image}}\t{{.Names}}

# 컨테이너 삭제
docker rm [OPTIONS] CONTAINER [CONTAINER...]
도커는 컨테이너가 실행중인 경우 삭제 안됨 stop 후 삭제 
docker stop 컨테이너명
docker rm 컨테이너명 
docker rm -r 도커컨테이너명  (실행 중인 컨테이너라도 강제 삭제)

# 모든 컨테이너 삭제 
docker container prune
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
모든 컨테이너 중지 후 삭제 처리 

# 컨테이너를 외부에 노출 
기본적으로 도커는 컨테이너에 172.17.0.x의 IP를 순차적으로 할당
기본적으로 컨테이너는 도커가 설치된 컨테이너에서만 접속 
외부에 컨테이너의 애플리케이션을 노출하기 위해서는 eth0의 IP와 포트를 호스트의 IP와 포트로 바인딩 처리 필요

docker run -i -t --name mywebserver -p 80:80 ubuntu:14.04
(생성 후 아래 명령어로 apache  설치 후 호스트 컴퓨터에서 localhost로 접속 )
apt-get upgrade
apt-get install apache2 -y
service  apache2 start

# -p 컨테이너의 포트를 호스트의 포트와 바인딩해 연결하는 옵션 
[호스트의 포트]:[컨테이너의 포트]
여러개의 포트를 개방하려면 -p 옵션을 여러번 사용해서 설정
docker run -i -t --name mywebserver -p 3306:3306 -p 80:80 ubuntu:14.04
호스트의 특정 ip를 사용하려면 -p 192.168.0.100:7777:80 같은 형식으로 설정

# 포트 확인 명령어 
docker port mywebserver

# wordpress 설치 예시 
docker run -d --name wordpressdb -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress mysql:5.7
docker run -d -e WORDPRESS_DB_HOST=mysql -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=password \
 --name wordpress  --link wordpressdb:mysql -p 80  wordpress

-d 옵션 컨테이너를 백그라운드에서 동작하는 애플리케이션으로써 실행
-e 옵션 컨테이너 내부의 환경 변수 echo ${ENVIROMENT_NAME} 으로 간단히 확인 가능
--link 내부 IP 알 필요 없이 컨테이너에 별명으로 접근 가능하게 설정 (deprecated 옵션 , 브리지 네트워크 사용하는 것 권장)

# 컨테이너 내부 콘솔 접속 
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
docker exec -it wordpressdb /bin/bash

# 단순히 결과만 반환
docker exec wordpressdb ls /

# 호스트 볼륨 처리 
docker run -d --name wordpressdb_hostvolume  -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress \
 -v /home/wordpress_db:/var/lib/mysql mysql:5.7
docker run -d -e WORDPRESS_DB_PASSWORD=password --name wordpress_hostvolume  --link wordpressdb_hostvolume:mysql -p 80  wordpress
호스트 볼륨 처리 
-v 옵션 호스트의 디렉토리와 컨테이너의 디렉토리 공유
[호스트의 공유디렉토리]:[컨테이너의 공유 디렉토리]
디렉토리 단위의 공유가 아닌 파일 단위도 가능
-v 옵션을 여러번 사용 가능
호스트에 이미 존재 하는 경우 컨테이너 파일 덮어 씌어짐 (호스트 파일이 컨테이너에 마운트 되는 형식임) 

--volumes-from : -v 옵션으로 볼륨을 사용하는 컨테이너를 다른 컨테이너와 공유하는 옵션

# 도커 볼륨
볼륨 생성
docker volume create myvolume
볼륨 리스트 확인
docker volume ls

아래 처럼 생성한 볼륨을 -v 옵션에 사용 가능
-v [볼륨 이름]:[컨테이너 공유 디렉토리]
(도커 볼륨도 호스트 볼륨 공유와 마찬가지로 호스트에 저장 함으로써 데이터가 보존 실제로 파일이 어디에 저장되는지는 사용자는 알필요 없음)

inspect 명령어로 도커 볼륨 실제 경로 확인
ubuntu@ubuntu2004:~$ docker inspect --type volume myvolume
[
    {
        "CreatedAt": "2022-11-07T18:51:41-05:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/snap/docker/common/var-lib-docker/volumes/myvolume/_data",
        "Name": "myvolume",
        "Options": {},
        "Scope": "local"
    }
]

도커 volume create 생성 하지 않아도 -v 옵션 시 자동으로 생성 됨 
docker run -i -t --name volume_autho -v /root ubuntu:14.04

사용하지 않는 volume 한꺼번에 삭제 처리
docker volume prune

컨테이너가 아닌 외부에 데이터를 저장 하고 컨테이너는 그 데이터로 동작하게 설계 하는 것을 stateless라고 함
위와 반대로 컨테이너가 데이터를 저장 하는 경우 stateful

-v 옵션 대신 --mount 옵션 사용 가능
docker run -i -t --name mount_option --mount type=volume, source=myvolume, target=/root ubuntu:14.04
docker run -i -t --name mount_option --mount type=bind, source=/home/wordpress_db,target=/home/testdir ubuntu:14.04

# 도커 네트워크   (veth - virtual eth)
도커컨테이너1(eth0 lo)  , 도커컨테이너2(eth0 lo) ,  도커컨테이너3(eth0 lo)
            veth..                           veth..                           veth..    
                                             docker0
                                                 eth0

도커는 내부 IP를 순차적으로 할당 IP는 컨테이너가 재시작할 때마다 변경될 수도 있음
veth라는 네트워크 인터페이스를 생성 

아래 명령어로 docker0 브릿지에 veth이 실제로 바인딩 되었는지 확인 
brctl show docker0 

도커가 자체적으로 제공하는 네트워크 드라이버
bridge, host, none, container, overlay 

기본적으로 사용할 수 있는 네트워크 드라이버 확인
 docker network ls
 
 docker network inspect bridge
 아무런 설정 없이 컨테이너 생성하면 자동으로 docker0브릿지 사용 

# bridge 네트워크
docker network create --driver bridge mybridge
docker run -i -t --name mynetwork_container --net mybridge ubuntu:14.04
docker network disconnect , connect (bridge, overlay 네트워크만 사용 가능 host, none 은 사용 불가 )
docker network disconnect mybridge mynetwork_container
docker network connect bridge mynetwork_container

docker network create --driver=bridge \
--subnet=172.72.0.0/16 \
--ip-range=172.72.0.0/24 \
--gateway=172.72.0.1 \
my_custom_network

# host 네트워크
네트워크를 호스트로 설정하면 호스트의 네트워크 환경 그대로 사용
docker run -i -t --name network_host --net host ubuntu:14.04
호스트 머신에서 설정한 호스트 이름도 컨테이너가 물려받기 때문에 무작위 16진수가 아닌 도커엔진이 설치된 호스트 머신의 호스트 이름으로 설정됨
host 네트워크로 설정하면 별도의 포트포워딩 없이 바로 서비스 가능

# none 네트워크
docker run -i -t --name network_none --net none ubuntu:14.04
아무런 네트워크도 사용 하지 않음 외부와 연결이 단절
네트워크 인터페이스 확인하면 로컬 호스트를 나타내는  lo 외에는 존재하지 않음

# Container 네트워크 
docker run -i -t -d --name network_container1 ubuntu:14.04
docker run -i -t -d --name network_container2 --net container:network_container1 ubuntu:14.04
다른 컨테이너의 네트워크 네임스페이스 환경을 공유(공유되는 속성은 내부 IP, 네트워크 인터페이스의 MAC주소)
내부 IP를 새로 할당 받지 않으며 호스트에 veth로 시작하는 가상 네트워크 인터페이스도 생성되지 않음
network_container2는 network_container1과 동일 



# 도커 로그 확인
docker logs [OPTIONS] CONTAINER
docker logs --tail 10 ${WORDPRESS_CONTAINER_ID}  




