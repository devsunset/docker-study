-------------------------------------------------

			# DOCKER-WORK #

-------------------------------------------------

########################################################
### Docker

https://www.docker.com/

https://docs.docker.com/

https://hub.docker.com/

https://kubernetes.io/

########################################################
### Reference

https://www.yalco.kr/36_docker/

https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html
https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html

http://pyrasis.com/private/2014/11/30/publish-docker-for-the-really-impatient-book

(시작하세요. 도커/쿠버네티스 book)
https://github.com/alicek106/start-docker-kubernetes

########################################################
### Docker Install

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
### Docker Command

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
### Docker Guide

https://github.com/alicek106/start-docker-kubernetes

# 도커 정보 확인
docker info

# 도커 버젼 확인
docker -v
docker version

# 도커 컨테이너 다운로드 및 실행 
docker run ubuntu

docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
-d      detached mode 흔히 말하는 백그라운드 모드
-p      호스트와 컨테이너의 포트를 연결 (포워딩)
-v      호스트와 컨테이너의 디렉토리를 연결 (마운트)
-e      컨테이너 내에서 사용할 환경변수 설정
–name   컨테이너 이름 설정
–rm     프로세스 종료시 컨테이너 자동 제거
-it     -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션
–link   컨테이너 연결 [컨테이너명:별칭]

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

# 도커 컨테이너 제어 
docker start [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker attach [OPTIONS] CONTAINER [CONTAINER...]

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

-p 컨테이너의 포트를 호스트의 포트와 바인딩해 연결하는 옵션 
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

# bridge 네트워크와 --net-alias
브리지 타입의 네트워크와 run 명령어의 --net-alias 옵션을 함께 쓰면 특정 호스트 이름으로 컨테이너 여러 개에 접근 가능
docker run -i -t -d --name network_alias_container1 --net mybridge --net-alias test ubuntu:14.04
docker run -i -t -d --name network_alias_container2 --net mybridge --net-alias test ubuntu:14.04
docker run -i -t -d --name network_alias_container3 --net mybridge --net-alias test ubuntu:14.04

docker inspect network_alias_container1 | grep IPAddress
docker inspect network_alias_container2 | grep IPAddress
docker inspect network_alias_container3 | grep IPAddress

docker run -i -t --name network_alias_ping --net mybridge ubuntu:14.04
root@e5c86f31ec1d:/# ping -c 1 test
PING test (172.18.0.4) 56(84) bytes of data.
64 bytes from network_alias_container3.mybridge (172.18.0.4): icmp_seq=1 ttl=64 time=0.088 ms

--- test ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.088/0.088/0.088/0.000 ms

매번 달라지는 IP를 결정하는 것은 라운드 로빈 방식 

root@e5c86f31ec1d:/#  apt-get update
root@e5c86f31ec1d:/#  apt-get install dnsutils
root@e5c86f31ec1d:/# dig test

; <<>> DiG 9.9.5-3ubuntu0.19-Ubuntu <<>> test
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39515
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;test.				IN	A

;; ANSWER SECTION:
test.			600	IN	A	172.18.0.4
test.			600	IN	A	172.18.0.2
test.			600	IN	A	172.18.0.3

;; Query time: 2 msec
;; SERVER: 127.0.0.11#53(127.0.0.11)
;; WHEN: Tue Nov 08 02:09:21 UTC 2022
;; MSG SIZE  rcvd: 82

# MacVLAN 네트워크 
MacVLAN은 호스트의 네트워크 인터페이스 카드를 가상화해 물리 네트워크 환경을 컨테이너에게 동일하게 제공 
MacVLAN을 사용하면 컨테이너는 물리 네트워크 상에서 가상의 Mac주소를 가지며 해당 넽워크에 연결된 다른 장치와의 통신이 가능
기본적으로 할당되는 IP대역대인 172.17.X.X 대신 네트워크 장비의 IP를 할당 
MacVLAN 네트워크를 사용하는 컨테이너는 기본적으로 호스트와 통신이 불가능
적어도 1개의 네트워크 장비와 서버가 필요 

공유기의 네트워크 정보 : 192.168.0.0/24
서버 1 : 192.168.0.50
서버 2 ; 192.168.0.51

 서버1 : docker network create -d macvlan --subnet=192.168.0.0/24 \
--ip-range=192.168.0.64/28 --gateway=192.168.0.1 \
-o macvlan_mode=bridge -o parent=eth0 my_macvlan

 서버2 : docker network create -d macvlan --subnet=192.168.0.0/24 \
--ip-range=192.168.0.128/28 --gateway=192.168.0.1 \
-o macvlan_mode=bridge -o parent=eth0 my_macvlan


# 도커 로그 확인
docker logs [OPTIONS] CONTAINER
docker logs --tail 10 ${WORDPRESS_CONTAINER_ID}  

docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=1234 mysql:5.7

--since 옵션에 유닉스 시간을 입력해 특정 시간 이후 로그 확인
 docker logs --since 1474765959 mysql

 -t 옵션 타임 스탬프 표시 
 -f 로그를 스트림으로 확인
 docker logs -f -t mysql

 로그파일은 json형태로 저장됨
 /var/lib/docker/containers/[container-id]/[container-id]-json.log

 --logs-opt  옵션으로   json로그 파일의 최대 크기(k,m,g) 를 지정 가능
  docker run -it --log-opt max-size=10k --log-opt max-file =3 --name log-test ubuntu:14.04
  default는 용량 무제한 파일 1개 

  기본은 json 로그로 처리 
  syslog, journald,fluentd,awslogs 등 애플리케이의 특징에 적합한 로깅 선택 가능
  도커 데몬 시작 옵션에서 --log-driver 옵션 사용 해서 설정 가능
  DOCKER_OPTS="--logs-driver=syslog"

  # syslog
docker run -d --name syslog_container --log-driver=syslog ubuntu:14.04 echo syslogtest
ubuntu -> /var/log/syslog
centos -> /var/log/messages

로그 확인
tail /var/logs/syslog 

syslog 원격에 저장하는 방법인 rsyslog 설정
서버 호스트 : 192.168.0.100
클라이언트  : 192.168.0.101

서버 호스트에서 rsyslog서비스가 시작하도록 설정된 컨테이너를 구동 
클라이언트에서 컨테이너 생성해 서버의 rsyslog 컨테이너에 로그를 저장 

[서버 설정]
docker run -i -t -h rsyslog --name rsyslog_server -p 514:514 -p 513:514/udp ubuntu:14.04
컨테이너 내부의 rsyslog.conf 파일 내용 중 syslog서버를 구동시키는 항목의 주석을 해제 
vi /etc/rsyslog/conf
    # provides UDP syslog reception
    $ModLoad imudp
    $UDPServerRun 514

    # provides TCP syslog reception
    $ModLoad imtcp
    $InputTCPServerRun 514

서비스 재시작 
service rsyslog restart

[클라이언트 설정]
docker run -i -t --log-driver=syslog --log-opt syslog-address=tcp://192.168.0.100:514 \
--log-opt tag="mytag" ubuntu:14.04

udp 활성화시 아래처럼 udp로도 설정 할 수 있음
docker run -i -t --log-driver=syslog --log-opt syslog-address=udp://192.168.0.100:514 \
--log-opt tag="mytag" ubuntu:14.04

syslog-facility 설정시 로그 생성하는 주체에 따라 로그를 다르게 저장 가능
기본은 daemon으로 설정되어 있지만 kern, user, mail 등 다른 facility를 사용 할 수 있음 
docker run -i -t --log-driver=syslog --log-opt syslog-address=tcp://192.168.0.100:514 \
--log-opt tag="maillog" --log-opt syslog-facility="mail"
ubuntu:14.04

rsyslog는 우분투에서 쓸 수 있는 기본적인 로깅 방법
logentries, LogAnalyzer 등관 같은 로그 분석기와 연동 하여 로그 쉽게 분석 가능

# fluented 로깅
fluentd 각종 로그를 수집하고 저장할수 있는 기능을 제공 하는 오픈소스

도커서버 1
                    flutend 서버 (로그 수집) -> mongodb (로그 저장)
도커서버 2 

도커서버 : 192.168.0.100
fluentd   : 192.168.0.101
몽고DB   : 192.168.0.102

docker run --name mongoDB -d -p 27017:27017 mongo

fluent.conf  파일 작성
    <source>
        @type forward
    </source>

    <match docker.**>
        @type mongo
        database nginx
        collection access
        host 192.168.0.102
        port 27017
        flush_interval 10s
        # mongodb 인증 설정시 아래 항목 정보 추가 
        # user userid
        # password passwd
    </match>

docker run -d --name fluented -p 24224:24224 \
-v $(pwd)/fluent.conf:/fluentd/etc/fluent.conf \
-e FLUENTD_CONF=fluent.conf alicek106/fluentd:mongo
(공식 fluented mogodb client 설치 안되어 있음 )

docker run -p 80:80 -d --log-driver=fluentd --log-opt fluentd-address=192.168.0.101:24224 \
--log-opt tag=docker.nginx.webserver nginx

# AWS CloudWatch 로그
 AWS 환경에서 도커 사용하고 있다면 컨테이너 로그 드라이버 옵션을 설정 하는 것만으로 
 CloudWatch 기능을 사용 가능

AWS에서 아래 단계 설정
 클라우드워치에 해당하는 IAM 권한 생성
 로그 그룹 생성 (mylogs)
 로그 그룹에 로그 스트림 생성 (mylogstream)
 클라우드워치의 IAM 권한을 사용할 수 있는 EC2 인스턴스 생성과 로그 전송 

docker run -i -t \
--log-driver=awslogs \
--log-opt awslogs-region=ap=northeast-2 \
--log-opt awslogs-group=mylogs \
--log-opt awslogs-stream=mylogstream ]
ubuntu:14.04

# 컨테이너 자원 할당 제한
   기본은 호스트 자원 전부를 사용
   docker update (변경할 자원 제한) (컨테이너 이름)

   docker run -i -t --name ubuntu ubuntu:14.04

 #  메모리 제한 (m, g 최소는 6M)
   docker update --memory-swap="128MB" --memory="128MB" ubuntu

#   cpu 설정 변경
   --cpu-shares 컨테이너에 가중치를 설정해 해당 컨테이너가 CPU를 상대적으로 얼마나 사용할 수 있는지 설정 (갯수가 아닌 비중으로 할당)
   상대적인 값을 가짐 아무런 설정을 하지 않았을때 가지는 값 1024 이는 CPU 할당에서 1의 비중을 뜻함
   docker run -i -t --name cpu_share --cpu-shares 1024 ubuntu:14.04

   apt-get install stress
   설치 후 stress --cpu 1 명령어로 cpu 부하 확인 

--cpuset-cpus 호스트에 cpu가 여러개 있을 경우 특정 cpu만 사용 하도록 설정
   docker update --cpuset-cpus=1 ubuntu

   apt-get install htop 설치 후 확인 가능

--cpuset-cpus="0,3" 은 1, 4번째 cpu 사용 --cpuset-cpus="0-2"는 1,2,3번째 CPU를 사용하게 설정

--cpu-period, --cpu-quota 컨테이너 CFS(Completely Fail Scheduler) 주기는 기본으로 100ms로 설정 해당 옵션으로 변경 가능
docker run -d --name quota_1_4 \
--cpu-period=10000 \
--cpu-quota=2500 \
ubuntu:14.04

stress --cpu 1 로 확인

--cpus 옵션은 --cpu-period, --cpu-quota와 동일한 기능을 하지만 직관적으로 CPU 개수를 직접 지정 한다는게 차이 
--cpus=0.5  설정 값과 --cpu-period=100000 --cpu-quota=50000 설정 값은 동일

# Block I/O 제한 
--device-write-bps, --device-read-bps, --device-write-iops, --device-read-iops옵션으로 블록 입출력 제한 할 수 있음
Direct I/O의 경우에만 블록 입출력이 제한 되며  Buffered I/O는 제한되지 않음

읽고 쓰기 초당 1mb로 제한 ( kb, mb, gb 단위로 설정 가능)
docker run -it --device-write-bps /dev/xvda:1mb ubuntu:14.04
[디바이스 이름] : [값] 형태로 설정  aws ec2에서 /dev/xvda 사용하고 있기 때문에 위의 예시 값에 쓰임

아래 명령어는 10MB의 파일을 Direct I/O를 통해 쓰기 작업 수행
dd if=/dev/zero of=test.out bs=1M count=10 oflag=direct

설정 값을 상대 값으로 설정 가능 (2배 가량 차이나게 설정 예시)
docker run -it --device-write-iops /dev/xvda:5 ubuntu:14.04
docker run -it --device-write-iops /dev/xvda:10 ubuntu:14.04

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

# 도커 이미지 생성
docker run -i -t --name commit_test ubuntu:14.04
docker commit [OPTIONS] CANTAINER [REPOSITORY[:TAG]]
docker commit -a "devsunset" -m "my first commit" commit_test commit_test:first
-a : author 
-m : commit messages
docker run -i -t --name commit_test2 commit_test:first
docker commit -a "devsunset" -m "my second commit" commit_test2 commit_test:second

docker inspect ubuntu:14.04
docker inspect commit_test:first
docker inspect commit_test:second
Layers 부분 확인하면 기존 바탕이 되는 Container에 commit 된 부분이 새로운 Layers로 추가 됨

hisotry 내용 확인
docker history commit_test:second

# 도커 이미지 삭제 
docker rmi 이미지 
이미지를 사용한 컨테이너가 동작 중인 경우 삭제 가 안됨 컨테이너 중지 및 삭제 후 이미지 삭제 처리 
컨테이너가 사용중인 이미지를 docker rmi -f 로 강제로 삭제하면 이미지의 이름이 <none>으로 변경되며 이러한 이미지를 댕글링(dangling) 이미지라 함
댕글링 이미지는 docker images -f dangling=true 명령어로 확인 가능
docker image prune 명령어로 사용 중이지 않는 댕글링 이미지를 한번에 삭제 가능 

 docker stop commit_test2 && docker rm commit_test2
 docker rmi commit_test:first
 Untagged: commit_test:first <- Untagged 의미는 commit_test:second에 사용되므로 실제 이미지를 삭제 하지 안혹 레이어에 부여된 이름만 삭제 함 

# 도커 이미지 추출
docker save -o ubuntu_14_04.tar ubuntu:14.04
open .docker_temp_678847958: permission denied ( permission 에러 발생하면 아래 와 같이 실행)

mkdir ~/docker-images
cd ~/docker-images
chmod 777 ./
sudo docker save <img_id> -o ./<filename>

추출한 이미지 로드 
sudo docker load -i ubuntu_14_04.tar

컨테이너 export 후 이미지로 import
docker export -o rootFS.tar my_container
docker import rootFS.tar myimage:0.0

# 도커 이미지 배포 

# Docker Hub
도커 허브에 회원 가입 후 Create Repository 생성 

docker run -i -t --name commit_container1 ubuntu:14.04

docker commit commit_container1 my-image-name:0.0

특정 이름의 저장소에 이미지를 올리려면 저장소 이름을 이미지 앞에 접두어로 추가 해야 함
docker tag [기존의 이미지 이름] [새롭게 생성될 이미지 이름]
docker tag my-image-name:0.0 devsunset/my-image-name:0.0

docker hub에 로그인 
docker login
(로그인 한 정보는 /[게정명]/.docker/config.json 파일에 저장됨 삭제 하려면 docker logout 명령어 실행 - 경로는 설치 버젼 따라 상이한듯 함)
docker push devsunset/my-image-name:0.0
docker pull devsunset/my-image-name:0.0

docker hub  조직/팀 생성하여 공유할 수 있음 (유료)

Webhook 기능
이미지  push 된 경우 특정 url 호출 기능 제공 

# Docker 사설 레지스트리

도커 공식 사설 레지스트리 이미지 제공
 docker run -d --name myregistry -p 5000:5000 --restart=always registry:2.6
 --restart 옵션은 호스트나 도커 엔진을 재시작시 컨테이너도 항상 재시작 
 on-failure  -> on-failure:5 컨테이너 종료코드가 0이 아닐때 컨테이너 재시작을 5번까지 시도 
 unless-stopped  -> 컨테이너를 stop으로 종료 했으면 호스트나 도커엔진이 재시작해도 컨테이너 재시작 안함

curl localhost:5000/v2/  실행해서 설치 여부 확인

docker tag my-image-name:0.0 ${DOCKER_HOST_IP}:5000/my-image-name:0.0

docker tag my-image-name:0.0 192.168.0.100:5000/my-image-name:0.0

ex)
 ubuntu@ubuntu2004:~$ docker push 192.168.0.100:5000/my-image-name:0.0
The push refers to repository [192.168.0.100::5000/my-image-name]
Get "https://192,168.0.100::5000/v2/": http: server gave HTTP response to HTTPS client

기본적으로 도커 데몬은 HTTPS를 사용하지 않은 레지스트리 컨테이너에 접근 하지 못하도록 설정됨
임시로 http를 사용하려면 아래 옵션을 사용하여 도커를 재시작
DOCKER_OPTS="--insecure-registry=${DOCKER_HOST_IP}:5000"

insecure-registry 설정 (IP 값을 127.0.0.1 or localhost 를 사용 하면 기본적으로 insecure-registry 예외 적용됨)
/etc/docker/daemon.json 파일을 열어 예시처럼 작성합니다. 없을 경우 생성하면 됩니다.
{
    "insecure-registries" : ["${DOCKER_HOST_IP}:5000"]
}

docker 재시작
# flush changes
sudo systemctl daemon-reload
# restart docker
sudo systemctl restart docker

docker pull 127.0.0.1:5000/my-image-name:0.0

컨테이너 삭제 할때 볼륨에 이미지가 남기 때문에 --volumes 옵션 사용해 삭제 한다.
docker rm --volumes myregistry

# Nginx 서버로 접근 권한 설정
인증서 생성
mkdir certs
openssl genrsa -out ./certs/ca.key 2048
openssl req -x509 -new -key ./certs/ca.key -days 10000 -out ./certs/ca.crt
openssl genrsa -out ./certs/domain.key 2048
openssl req -new -key ./certs/domain.key -subj /CN=127.0.0.1 -out ./certs/domain.csr
echo subjectAltName = IP:127.0.0.1 > extfile.cnf
openssl x509 -req -in ./certs/domain.csr -CA ./certs/ca.crt -CAkey ./certs/ca.key -CAcreateserial -out ./certs/domain.crt -days 10000 -extfile extfile.cnf

계정 패스워드 생성 ( htpasswd 설치 되어 있지 않으면 sudo apt-get install apache2-utils로 설치)
htpasswd -c htpasswd devsunset
mv htpasswd certs/

vi certs/nginx.conf
        upstream docker-registry {
        server registry:5000;
        }
        server {
        listen 443;
        server_name ${DOCKER_HOST_IP};
        ssl on;
        ssl_certificate /etc/nginx/conf.d/domain.crt;
        ssl_certificate_key /etc/nginx/conf.d/domain.key;
        client_max_body_size 0;
        chunked_transfer_encoding on;

        location /v2/ {
            if ($http_user_agent ~ "^(docker\/1\.(3|4|5(?!\.[0-9]-dev))|Go ).*$" ) {
            return 404;
            }
            auth_basic "registry.localhost";
            auth_basic_user_file /etc/nginx/conf.d/htpasswd;
            add_header 'Docker-Distribution-Api-Version' 'registry/2.0' always;

            proxy_pass http://docker-registry;
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_read_timeout 900;
        }
        }

docker stop myregistry; docker rm myregistry
docker run -d --name myregistry --restart=always registry:2.6

설정시 옵션 설정 가능
docker run -d -p 5001:5000 --name registry_delete_enabled --restart=alwasy \
-e REGISTRY_STORAGE_DELETE_ENABLED=true \
-e REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY=/var/lib/mydocker \
registry: 2.6

-e 옵션을 주고 설정 하는 방식이 있고 설정 내용인 config.xml 파일 내용에 적용해도 됨
docker exec -it myregistry cat /etc/docker/registry/config.yml

docker run -d --name nginx_frontend -p 443:443 --link myregistry:registry -v $(pwd)/certs/:/etc/nginx/conf.d nginx:1.9

docker login https://127.0.0.1

인증서 문제 발생하는 경우 자체 생성한 인증서 임으로 신뢰할수 있는 인증서에 추가
sudo cp certs/ca.crt /usr/local/share/ca-certificates/
sudo update-ca-certificates

 sudo service docker restart
docker start nginx_frontend

docker push 127.0.0.1/my-image-name:0.0

# 도커 레지스트리 RESTful API (공식 문서 참조)
 https://docs.docker.com/registry/spec/api/


# Dockerfile
이미지 생성하는 방법
1. empty(ubuntu, CentOS) image로 컨테이너 생성
2.애플리케이션 환경 설치 구동
3.컨테이너를 이미지로 커밋 
위의 방법은 수작업으로 진행 필요

Dockerfile 위와 같은 일련의 작업을 하나의 파일에 기술 하고 build 하여 한번에 수행되게 처리 
Dockerfile을 Docker Hub에 배포 할수도 있음

# Dockerfile EXAMPLE
mkdir dockerfile && cd dockerfile
echo test >> test.html

vi Dockerfile
###
    FROM ubuntu:14.04
    MAINTAINER devsunset
    LABEL "purpose"="practice"
    RUN apt-get update
    RUN apt-get install apache2 -y
    ADD test.html /var/www/html
    WORKDIR /var/www/html
    RUN ["/bin/bash", "-c", "echo hello >> test2.html"]
    EXPOSE 80
    CMD apachectl -DFOREGROUND
###

# Dockerfile 명령어 
FROM : 생성할 이미지의 베이스가 될 이미지 ( 반드시 한번 이상 입력해야 함)
MAINTAINER : 이미지를 생성한 개발자의 정보 (일반적으로 이메일등 입력 도커 1.13.0 버젼 이후로 사용 하지 않음 대신 LABEL로 대체 )
                        LABEL maintainer "devsunset <devsunset@gmail.com>"
LABEL : 이미지에 메타 데이타 추가 메타 데이터는 키:값 형태로 저장 여려개의 메타데이타가 저장 될수 있음
RUN : 이미지를 만들기 위해 컨테이너 내부에서 명령어를 실행 (명령어 실행시 입력을 받아야 하는경우 미리 설정 안그러면 오류로 간주 됨)
          RUN ["/bin/bash", "-c", "echo hello >> test2.html"] 일부 명령어는 배열 형태로 사용 할수 있음 
ADD : 파일을 이미지에 추가 , 추가 하는 파일은 Dockfiler이 위치한 디렉토리인 Context 에서 가져옴
          ADD 명령어는 JSON 형태로 ["추가할 파일1", "추가할 파일2","컨텐이너에 추가될 위치"] 형식으로 여러개 파일 처리 가능 
WORKDIR  : 명령어를 실행할 디렉토리 ( cd 와 비슷함 )
EXPOSE : Dockfile 빌드로 생성된 이미지에서 노출할 포트 설정 (호스트 포트와 바인딩 되는건 아님)
CMD : 컨테이너가 시작될 때마다 실행할 명령어 설정 Dockerfile에서 한번만 사용 가능 CMD로 설정한 값이 run의 커맨드를 덮어씀 
            JSON 배열 형태로 설정 가능

# Dockerfile 빌드 
docker build -t mybuild:0.0 ./
-t 옵션 생성될 이미지 이름 설정 설정 안하면 16진수 형태의 이름으로 지정됨
이미지 이름 다음에는 Dockerfile 저장된 위치 지정 
-f 옵션으로 직접 Dockerfile을 지정 가능  

docker run -d -P --name myserver mybuild:0.0
  -P 옵션은 Dockerfile에서 EXPOSE로 설정된 포트를 호스트의 포트와 연결되게 처리 해 줌 (동작이 잘 안되는지 연결이 안됨 -p 80:80으로 처리)
  docker port myserver 로 확인

아래와 같이 filter 옵션을 사용하여 이미지 찾을 수 있음
  docker images --filter "label=purpose=practice"

Dockerfile 파일 위치하는 곳이 build context 해당 경로에 있는 파일 및 디렉토리도 포함 됨으로 필요한 파일만 위치 시킴
.dockerignore  (무시 하는 내용 작성 파일 경로는 Dockerfile이 위치하는 경로가 기준이 됨) 
vi .dockerignore
test2.html
*.html
*/*.html (디렉토리 하위의 파일 대상)
test.htm? (html , htma  등 ? 값은 모든 값을 뜻함)
!test*.html (! 값은 특정 파일을 제외하지 않음을 뜻함)

Dockerfile파일이 한줄 실행 시마다 이전 Step에서 생성된 이미지에 의해 새로운 컨테이너가 생성 다 수행  된 후 새로운 이미지 레이어로 저장됨
한번 이미지 빌드 후 재 실행하게 되면 이전 캐시 사용
이미지 빌드 실패시 -t옵션의 값으로 지정한 이미지 이름이 아닌 <none>:<none>으로 이미지가 생성
git clone 등으로 소스를 받아와서 빌드 하는 경우 git 내용이 변경이 되더라도 캐시를 사용하여 소스가 변경이 안됨
--no-cache 옵션을 사용하여 캐시 사용안하게 지정
docker build --no-cache -t mybuild:0.0
특정 캐시를 사용해서 빌드 할 수도 있음
docker build --cache-from nginx -t my_extend_nginx:0.0

# 멀티 스테이지 빌드 
하나의  Dockerfile 안에 여러 개의 FROM 이미지를 정의 함으로써 빌드 완료 시 최종적으로 생성될 이미지의 크기를 줄이는 역활

아래 처럼 처리하면 간단한 프로그램 인데 go build시 필요한 라이브러리 참조로 생성되는 이미지 용량이 큼
mkdir gobuid && cd gobuild

vi main.go
    package main
    import "fmt"
    func main(){
        fmt.Println("hello world")
    } 

vi Dockerfile
    FROM golang
    ADD main.go /root
    WORKDIR /root
    RUN go build -o /root/mainApp /root/main.go
    CMD ["./mainApp"]

docker build . -t go_helloworld

위와 동일한 처리나 멀티 스테이지 빌드로 경량화 처리 
vi DockerfileLite
    FROM golang
    ADD main.go /root
    WORKDIR /root
    RUN go build -o /root/mainApp /root/main.go

    FROM alpine:latest
    WORKDIR /root
    COPY --from=0 /root/mainApp .
    CMD ["./mainApp"]

COPY --from=0  첫번째  FROM 절에서 빌드된 이미지의 최종 상태를 의미
alpine:latest는 실행에 필수적인 런타임 요소만 갖추고 있는 리눅스 배포판 

아래 처럼 이미지 SIZE 값을 경량화 할수 있음
ubuntu@ubuntu-2204:~/gobuild$ docker images
REPOSITORY      TAG           IMAGE ID       CREATED         SIZE
go_helloworld   multi-stage   8ef3b3ad3042   6 seconds ago   7.36MB
go_helloworld   latest        f1a4fde6af8a   4 minutes ago   994MB

FROM golang as builder  처럼  Alias 를 주면 
여러개의 FROM 절 사용시 COPY --from=0 처럼 인덱스 값이 아닌 
COPY --from=builder 형식으로 사용 할 수 도 있음

# 기타 Dockerfile 명령어
https://docs.docker.com/engine/reference/builder/

ENV : Dockerfile에서 사용될 환경 변수를 지정 ${ENV_NAME} 또는 $ENV_NAME 형태로 사용
ex) 
ENV test /home
WORKDIR $test
run 명령어 에서 -e 변수로 환경변수 설정시 기존의 값을 덮어 씀 (run 명령어 -e 옵션이 우선 순위)
${env_name:-value} env_name라는 환경변수가 설정되어 있지 않으면 이 환경 변수의 값을 value로 대체
$(env_name:-value) env_name라는 환경변수가 설정되어 있으면 이 환경 변수의 값을 value로 대체 없으면 공백으로 대체

VOLUME : 빌드된 이미지로 컨테이너를 생성했을 때 호스트와 공유할 컨테이너 내부의 디렉토리를 설정
JSON배열 형식으로 여러개 사용 가능 VOLUME /home/dir /home/dir2 형태로도 사용 가능
ex)
VOLUME /home/volume

ARG : build 명령어를 실행할때 추가로 입력을 받아  Dockerfile 내에서 사용할 변수 값을 설정
ex)
ARG my_arg
RUN touch ${my_arg}/mytouch

dockr build --build-arg myarg=/home-t myarg:0.0 ./
--build-arg 옵션에 키=값 형태로 설정
값 설정 형태가 ENV 와 동일함으로  ARG에서 설정한 변수를 ENV에서 같은 이름으로 다시 설정하면 ENV값으로 덮어 쓰임

USER : 컨테이너 내에서 사용될 사용자 계정이나 UID를 설정 그 아래 명령어는 해당 계정으로 진행됨
일반적으로 RUN으로 사용자 그룹과 계정을 생성한뒤 사용 
ex)
RUN groupadd -r author && useradd -r -g author devsunset
USER devsunset

ONBUILD : 빌드된 이미지를 기반으로 하는 다른 이미지가 Dockfile로 생성될 때 실행할 명령어를 추가 
ex)
ONBUILD RUN echo "onbuild" >> /onbuild_file
Dockerfile 빌드 할때 실행 되지 않으며 , 별도의 정보로 이미지에 저장될 뿐 
나중에 빌드될 이미지를 위해 미리 저장해 놓는 기능

STOPSIGNAL : 컨테이너가 정지될 때 사용될 시스템 콜의 종류를 지정 아무것도 설정 하지 않으면 기본적으로 SIGTERM으로 설정
ex)
STOPSIGNAL SIGKILL
Dockerfile의 STOPSIGNAL은 docker run 명령어에요 --stop-signal 옵션으로 컨테이너에 개별적으로 설정 가능 
docker stop , docker kill 에도 적용 

HEALTHCHECK : 이미지로 부터 생성된 컨테이너에서 동작하는 애플리케이션의 상태를 체크 
ex)
vi Dockerfile
FROM nginx
RUN apt-get update && apt-get install curl -y
HEALTHCHECK --interval=1m --timout=3s --retries=3 CMD curl -f http://localhost || exit 1
curl 명령어로 nginx 1분마다 호출 하여 3초 이상 소요되면 이를 한번의 실패로 간주 3번 이상 타임아웃 발생 하면 해당 컨테이너는  unhealthy상태
docker ps 항목중 STATUS 값과 docker inspect의 출력중 State - Health - Log 항목을 확인

SHELL :  Dockerfile에서 기본적으로 사용 하는 Shell은 "/bin/bash -c" 윈도우에서는 "cmd /S /C"
사용하려는 Shell을 따로 지정 CMD의 JSON배열을 통해 shell을 따로 지정 하는 것도 가능 하지만 SHELL을 사용하면 편리
ex)
SHELL ["/usr/local/bin/node"]

COPY : 파일 복사 (ADD 명령어와 도일) - COPY는 로컬의 파일만 이미지에 추가 ADD는 외부 URL 및 tar파일에서도 파일을 추출하여 추가 할수 있다는 점이 차이
ex)
COPY test.html /home/
COPY ["test.html", "/home"]
ADD https://..../test.html /home
ADD test.tar /home ( tar 파일을 그대로 추가 하는게 아니라 /home 디렉토리에 압축 해제 함)

ENTRYPOINT : CMD 와 동일하게 컨테이너가 시작될 때 수행할 명령어 지정 
커맨드를 인자로 받아 사용할 수 있는 스크립트의 역할을 할 수 있다는 점이 CMD와 차이점 

# entrypoint : 없음 , cmd: /bin/bash
docker run -i -t --name no_entrypoint ubuntu:14.04 /bin/bash
root@host: /#   <- /bin/bash 쉘이 실행이 됨

# entrypoint : echo , cmd : /bin/bash
docker run -i -t --entrypoint="echo" --name yes_entrypoint ubuntu:14.04 /bin/bash
/bin/bash <- 맨 마지막 값을 인자로 사용하여 /bin/bash 라는 값이 출력됨

 entrypoint , cmd 둘중 하나라도 설정되어 있지 않으면 컨테이너 생성되지 않고 에러 발생 반드시 둘중 하나는 설정 해야 함

entrypoint를 이용한 스크립트 실행 (실행할 스크립트는 컨테이너 내부에 존재해야 함)
docker run -i -t --name entrypoint_sh --entrypoint="/test.sh" ubuntu:14.04 /bin/bash

vi Dockerfile
    FROM ubuntu:14.04
    RUN apt-get update
    RUN apt-get install apache2 -y
    ADD entrypoint.sh /entrypoint.sh
    RUN chmod +x /entrypoint.sh
    ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]

# JSON 배열 형태와 일반 형식의 차이점
JSON 배열 형태로 입력하지 않으면 CMD와 ENTRYPOINT에 명시된 명령어의 앞에 /bin/bash -c가 추가
CMD echo test
# -> /bin/bash -c echo test
JSON 배열 형태로 입력 하면 명령어가 그대로 사용
CMD ["echo", "test"]
# -> echo test

# Dockerfile로 빌드할 때 주의할 점
긴 구문 사용시  \ 를 사용 하여 가독성 높임
.dockerignore 파일을 작성해 불피요한 파일 컨텍스트에 포함 배제 
빌드 캐시 사용
한줄 실행시 마다 이미지가 생성됨으로 RUN  명령어 실행시 && 조합으로 한번에 실행  

# 도커 데몬

# 도커의 구조
docker server , docker client
which docker
ps aux | grep docker
/var/run/docker.sock

1.사용자가 docker version 실행
2./usr/bin/docker는 /var/run/docker.sock 유닉스 소켓을 사용해 도커 데몬에게 명령어 전달
3.도커 데몬은 명령어 파싱하고 명령어에 해당 하는 작업 수행
4.수행 결과를 도커 클라이언트에 반환 하고 사용자에게 결과 출력

# 도커 데몬 실행
service docker start
service docker stop
레드햇 개열은 systemctl enable docker 로 서비스 활성화 
dockerd ( 직접 실행 )

# 도커 데몬 설정
ubuntu@ubuntu-2204:~$ dockerd --help

Usage:	dockerd [OPTIONS]

A self-sufficient runtime for containers.

Options:
      --add-runtime runtime                     Register an additional OCI compatible runtime (default [])
      --allow-nondistributable-artifacts list   Allow push of nondistributable artifacts to registry
      --api-cors-header string                  Set CORS headers in the Engine API
      --authorization-plugin list               Authorization plugins to load
      --bip string                              Specify network bridge IP
  -b, --bridge string                           Attach containers to a network bridge
      --cgroup-parent string                    Set parent cgroup for all containers
      --config-file string                      Daemon configuration file (default "/etc/docker/daemon.json")
      --containerd string                       containerd grpc address
      --containerd-namespace string             Containerd namespace to use (default "moby")
      --containerd-plugins-namespace string     Containerd namespace to use for plugins (default "plugins.moby")
      --cpu-rt-period int                       Limit the CPU real-time period in microseconds for the parent cgroup for all
                                                containers
      --cpu-rt-runtime int                      Limit the CPU real-time runtime in microseconds for the parent cgroup for all
                                                containers
      --cri-containerd                          start containerd with cri
      --data-root string                        Root directory of persistent Docker state (default "/var/lib/docker")
  -D, --debug                                   Enable debug mode
      --default-address-pool pool-options       Default address pools for node specific local networks
      --default-cgroupns-mode string            Default mode for containers cgroup namespace ("host" | "private") (default "private")
      --default-gateway ip                      Container default gateway IPv4 address
      --default-gateway-v6 ip                   Container default gateway IPv6 address
      --default-ipc-mode string                 Default mode for containers ipc ("shareable" | "private") (default "private")
      --default-runtime string                  Default OCI runtime for containers (default "runc")
      --default-shm-size bytes                  Default shm size for containers (default 64MiB)
      --default-ulimit ulimit                   Default ulimits for containers (default [])
      --dns list                                DNS server to use
      --dns-opt list                            DNS options to use
      --dns-search list                         DNS search domains to use
      --exec-opt list                           Runtime execution options
      --exec-root string                        Root directory for execution state files (default "/var/run/docker")
      --experimental                            Enable experimental features
      --fixed-cidr string                       IPv4 subnet for fixed IPs
      --fixed-cidr-v6 string                    IPv6 subnet for fixed IPs
  -G, --group string                            Group for the unix socket (default "docker")
      --help                                    Print usage
  -H, --host list                               Daemon socket(s) to connect to
      --host-gateway-ip ip                      IP address that the special 'host-gateway' string in --add-host resolves to.
                                                Defaults to the IP address of the default bridge
      --icc                                     Enable inter-container communication (default true)
      --init                                    Run an init in the container to forward signals and reap processes
      --init-path string                        Path to the docker-init binary
      --insecure-registry list                  Enable insecure registry communication
      --ip ip                                   Default IP when binding container ports (default 0.0.0.0)
      --ip-forward                              Enable net.ipv4.ip_forward (default true)
      --ip-masq                                 Enable IP masquerading (default true)
      --ip6tables                               Enable addition of ip6tables rules
      --iptables                                Enable addition of iptables rules (default true)
      --ipv6                                    Enable IPv6 networking
      --label list                              Set key=value labels to the daemon
      --live-restore                            Enable live restore of docker when containers are still running
      --log-driver string                       Default driver for container logs (default "json-file")
  -l, --log-level string                        Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --log-opt map                             Default log driver options for containers (default map[])
      --max-concurrent-downloads int            Set the max concurrent downloads for each pull (default 3)
      --max-concurrent-uploads int              Set the max concurrent uploads for each push (default 5)
      --max-download-attempts int               Set the max download attempts for each pull (default 5)
      --metrics-addr string                     Set default address and port to serve the metrics api on
      --mtu int                                 Set the containers network MTU
      --network-control-plane-mtu int           Network Control plane MTU (default 1500)
      --no-new-privileges                       Set no-new-privileges by default for new containers
      --node-generic-resource list              Advertise user-defined resource
      --oom-score-adjust int                    Set the oom_score_adj for the daemon
  -p, --pidfile string                          Path to use for daemon PID file (default "/var/run/docker.pid")
      --raw-logs                                Full timestamps without ANSI coloring
      --registry-mirror list                    Preferred Docker registry mirror
      --rootless                                Enable rootless mode; typically used with RootlessKit
      --seccomp-profile string                  Path to seccomp profile
      --selinux-enabled                         Enable selinux support
      --shutdown-timeout int                    Set the default shutdown timeout (default 15)
  -s, --storage-driver string                   Storage driver to use
      --storage-opt list                        Storage driver options
      --swarm-default-advertise-addr string     Set default address or interface for swarm advertised address
      --tls                                     Use TLS; implied by --tlsverify
      --tlscacert string                        Trust certs signed only by this CA (default "/home/ubuntu/.docker/ca.pem")
      --tlscert string                          Path to TLS certificate file (default "/home/ubuntu/.docker/cert.pem")
      --tlskey string                           Path to TLS key file (default "/home/ubuntu/.docker/key.pem")
      --tlsverify                               Use TLS and verify the remote
      --userland-proxy                          Use userland proxy for loopback traffic (default true)
      --userland-proxy-path string              Path to the userland proxy binary
      --userns-remap string                     User/Group setting for user namespaces
  -v, --version                                 Print version information and quit

아래 처럼 dockerd 실행시 직접 옵션을 설정 할 수 도 있음  service로 데몬 구동시 해당 옵션은 적용 안됨
dockerd -H tcp://0.0.0.0:2375 --insecure-registry=DOCKER_HOST_IP:5000 --tls=false

 service로 데몬 구동시는 /etc/default/docker라는 파일을 읽어 옵션이 적용됨
vi /etc/default/docker
DOCKER_OPTS="dockerd -H tcp://0.0.0.0:2375 --insecure-registry=DOCKER_HOST_IP:5000 --tls=false"

# 도커 데몬 제어
-H : IP 주소와 포트번호를 입력하면 원격 API인 Docker Remote API로 도커를 제어

호스트의 모든 네트워크 인터페이스 카드에 할당된 IP 주소와 2375번 포트로 도커 데몬을 제어 함과 동시에 클라이언트도 사용할 수 있는 예시 
dockerd -H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375

dockerd -H tcp://192.168.99.100:2375
curl 192.168.99.100:2375/version --silent | python -m json.tool

# 도커 데몬에 보안 적용 --tlsverify

docker daemon
ca.pem , server-cert.pem , server-key.pem

docker client
ca.pem , cert.pem , key.pem

# server
mkdir keys && cd keys
1. 인증서에 사용될  key 생성
openssl genrsa -aes256 -out ca-key.pem 4096
2. 공용 키 생성
openssl req -new -x509 -days 10000 -key ca-key.pem -sha256 -out ca.pem
3. 서버 측에서 사용할 key 생성
openssl genrsa -out server-key.pem 4096
4. 서버측에서 사용될 인증서를 위한 인증 요청서 파일 생성
openssl req -subj "/CN=$HOST" -sha256 -new -key server-key.pem -out server.csr
5.접속에 사용될 IP 주소를 extfile.cnf 파일로 저장
echo subjectAltName = IP:$HOST, IP:127.0.0.1 > extfile.cnf
6. 서버측의 인증서 파일 생성
openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out server-cert.pem -extfile extfile.cnf

# client
1. 클라이언트 측의 키파일과 인증요청 파일을 생성하고 extfile.conf 파일에 extendedKeyUsage 항목 추가
openssl genrsa -out key.pem 4096
openssl req -subj 'CN=client' -new -key key.pem -out client.csr
echo extendedKeyUsage = clientAuth > extfile.cnf
2. 클라이언트 측의 인증서를 생성
openssl x509 -req -days 30000 -sha256 -in client.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out cert.pem -extfile extfile.cnf
3. ls (아래 파일 생성 확인)
ca-key.pem  , ca.pem , ca.srl , cert.pem , client.csr , extfile.cnf , key.pem , server-cert.pem , server.csr , server-key.pem 
4. 파일의 쓰기 권한을 삭제 해 읽기 전용 파일로 처리 
chmod -v 0400 ca-key.pem key.pem server-key.pem ca.pem server-cert.pem cert.pem
5. 도커 데몬의 설정파일이 존재하는 디렉토리인 ~/.docker로 도커 데몬 측에서 필요한 파일을 이동 
cp {ca,server-cert,server-key,cert,key}.pem ~/.docker

# 보안 적용 
dockerd --tlsverify \
--tlscacert=/root/.docker/ca.pem \
--tlscert=/root/.docker/server-cert.pem \
--tlskey=/root/.docker/server-key.pem \
-H=0.0.0.0:2376 \
-H unix:///var/run/docker.sock

관례적으로 Remote API 포트는 보안이 적용 안되어 있으면 2375 적용되어 있다면 2376을 사용 

docker -H 192.168.99.100:2376/version 
명령어 실행시 TLS 보안이 설정 되지 않았다는 에러가 출력됨

아래 처럼 보안 연결 원격 제어
docker -H 192.168.99.100:2376 \
--tlscacert=/root/.docker/ca.pem \
--tlscert=/root/.docker/cert.pem \
--tlskey=/root/.docker/key.pem \
--tlsverify version 

매번 옵션 입력 하기 불편 (아래 처럼 환경 변수로 설정) ~./bashrc 등에 설정
export DOCKER_CERT_PATH="/root/.docker"
export DOCKER_TLS_VERIFY=1

docker -H 192.168.99.100:2376 version

curl로 보안이 적용된 도커 데몬의 Remote API 사용 하려면 아래와 같이 플래그를 추가 
curl https://192.168.99.100:2376/version \
--cert ~/.docker/cert.pem \
--key ~/.docker/key.pem \
--cacert ~/.docker/ca.pem

# 도커 스토리지 드라이버 변경 --storage-driver (실행 환경에 따라 자동으로 설정 되지만 해당 옵션으로 변경 할 수 있음)
docker info | grep "Storage Driver"
Storage Driver: overlay2

지원하는 드라이버 : OverlayFS, AUFS , Btrfs, Devicemapper, VFS, ZFS
dockerd --storage-driver=devicemapper 

/var/lib/docker/devicemapper 에 저장됨  aufs로 설정시는 /var/lib/docker/aufs에 저장
서로 다른 저장소에 저장된 이미지는 서로 호환 사용이 안됨

Redhat 계열은 OVerlayFS  안정성을 우선시 한다면 Btrfs
https://docs.docker.com/engine/userguide/storagedriver/selectadriver/#/which-storage-drive=should-you-choose






