$ docker rm $(docker ps -a -q)  // remove all docker containers
$ docker stop $(docker ps -a -q) // stop all containers, use `docker ps -al` still can see
$ docker rmi $(docker images -q) //remove all docker images

$ docker commit -m='message' --author='author' <container_id> name/image_name:tag_name //save your work
$ docker save image_id > image_saved.tar                 # docker load < saved.tar
$ docker export container_id > container_exported.tar    # cat exported.tar | docker import - <image>:<tag>


http://www.daocloud.io // mirror for docker hub

$mkdir mydockerbuild
$cd mydockerbuild
$vi Dockerfile
$ cat Dockerfile
FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay

$ docker build -t docker-whale .
$ docker run docker-whale

$ docker login --username=maryatdocker --email=mary@docker.com
$ docker push maryatdocker/docker-whale
$ docker pull yourusername/docker-whale

------------
https://docs.docker.com/engine/userguide/basics/
$ docker run -i -t ubuntu /bin/bash # -i interactive -t terminal TTY
$ docker daemon -H 0.0.0.0:5555 &   # -H host for ip and port

$ docker ps # Lists only running containers
$ docker ps -a # Lists all containers
$ docker ps -l # return details of the last container started

$ PORT=$(docker port $JOB 4444 | awk -F: '{ print $2 }')
$ JOB=$(docker run -d -p 4444 ubuntu:12.10 /bin/nc -l 4444)
$ docker logs $JOB  #$JOB==<container_id>
$ docker kill $JOB  #stop, start, restart, rm, kill, ...

$ docker commit <container> <some_name>

$ docker run -d -P training/webapp python app.py
-d run the container in the background
-P map any required ports inside our container to our host
-training/webapp image name
-python app.py a command for our container to run

$ docker run -d -p 80:5000 training/webapp python app.py
-p 80:5000 map port 5000 inside container to port 80 on local host

curl http://localhost:80/  ==> container_5000
**If you have been using a VM, you'll need to get the IP of the virtual host instead of using localhost**
$ docker-machine ip <your-vm-name>
curl http://192.168.99.100:80/

**check container's ports***
-$docker ps -l 
-$docker port <container_id> 5000
-$docker logs -f <container_id>
-$docker inspect <container_id>

$ docker commit -m "Added json gem" -a "Kate Smith" <container_id> username/<image_name>:<tag>
-m message
-a author

------------
mkdir sinatra
cd sinatra
vi Dockerfile

#This is a comment
FROM ubuntu:14.04
MAINTAINER liu neo <liu.neo@qq.com>
RUN apt-get update && apt-get install -y ruby ruby-dev
RUN gem install sinatra

$docker build -t ouruser/sinatra:v2 .
$docker run -t -i ouruser/sinatra:v2 /bin/bash
$docker tag 5db5f8471261 ouruser/sinatra:devel
$docker push ouruser/sinatra

---------------

$docker run -d -P --name web training/webapp python app.py
--name web : name your container as web
$docker stop/rm/stop/restart web

$docker network ls
-docker provides 2 network drivers: bridge & overly
 -bridge network is limited to a single host running Docker Engine
 -overlay network can include multiple hosts 
-every docker engine includes 3 default networks: null, host, bridge

$docker network disconnect bridge <container_name>
-disconnect a container from a network

$ docker network create -d bridge my-bridge-network
-d bridge : create a network with bridge driver
$docker network ls
$docker network inspect my-bridge-network

$ docker run -d --net=my-bridge-network --name db training/postgresk
--net=my-bridge-network add container to the network 'my-bridge-network'
$ docker run -d --name web training/webapp python app.py
$ docker network connect my-bridge-network web
-connect allows you to attach a container to as many networks as you like
$ docker exec -it db bash
-ping web  : ping web from db container

-----------
$ docker run -d -P --name web -v /webapp training/webapp python app.py
-d in daemon mode
-P map all ports
--name set a name for container
-v create a new volume inside container
$ docker run -d -P --name web -v /opt/webapp:ro training/webapp python app.py
-volumes default to mount in RW mode, :ro means read-only
$ docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
-mount a host directory as a container volume  <host dir>:<container dir>
**hc rule => host (port/volume): container  (port/volume) **
** container-dir must always be an absolute path **

-------------
** How to set up a local docker repository **
http://www.centoscn.com/CentosServer/ftp/2015/0426/5280.html






