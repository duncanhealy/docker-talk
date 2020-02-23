# First steps

use docker hub 

- [https://hub.docker.com/](https://hub.docker.com/)

use github

- [GCR Package Registry](https://github.com/features/packages) https://github.com/features/packages

others private cloud acr, gcr, aws...

docker.pkg.github.com/{OWNER}/{REPOSITORY}/{IMAGE_NAME}:{TAG}


## Github setup

https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

```bash
OWNER=duncanhealy
REPOSITORY=docker-talk
IMAGE_NAME=helloworld
TAG=latest
IMAGE_TAG=docker.pkg.github.com/${OWNER}/${REPOSITORY}/${IMAGE_NAME}:${TAG}

```


## Dockerhub

docker login

cat ~/.docker/config.json

docker ps

docker run ${IMAGE_NAME}box

docker pull ubuntu:xenial

docker images

![not the kind of images that cause this](i/soreeyes.png)

docker pull alpine

cat > Dockerfile <<EOF
FROM busybox
CMD echo "Hello world! This is my first Docker image."
EOF

docker build . -t ${OWNER}/${IMAGE_NAME}:1.0.0

:latest

sha1sum


![Docker hub](i/dockerhubs.png)


Hmm containers 

interactively build and snapshot

- most people ignore this and prefer to build from base image or long complicated Dockerfile

docker commit -m="wut" ${IMAGE_NAME} ${OWNER}/${IMAGE_NAME}

docker images

docker push ${OWNER}/${IMAGE_NAME}

docker pull ${OWNER}/${IMAGE_NAME}

docker run ${OWNER}/${IMAGE_NAME} -p 8080:8080

docker run -p 8080:8080 ${OWNER}/${IMAGE_NAME}

docker ps -a 


docker exec -it ${OWNER}/${IMAGE_NAME} bash

docker exec -it `docker ps -q` bash

docker stop `docker ps -q`

docker volume ls

docker volume prune

docker run -v /dbdata --name dbstore ubuntu /bin/bash

docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata

docker run -v /dbdata --name dbstore2 ubuntu /bin/bash

docker run --rm --volumes-from dbstore2 -v $(pwd):/backup ubuntu bash -c "cd /dbdata && tar xvf /backup/backup.tar --strip 1"

- [A container tool repo](https://github.com/containers)
Let us install 

Podman 

```bash
. /etc/os-release
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"
wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/xUbuntu_${VERSION_ID}/Release.key -O- | sudo apt-key add -
sudo apt-get update -qq
sudo apt-get -qq -y install podman
```

nope - I'm not sure 

lets run it in a container

docker 

docker-compose

```
pip3 install podman-compose
pip3 install https://github.com/containers/podman-compose/archive/devel.tar.gz

```