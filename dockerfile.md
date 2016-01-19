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


