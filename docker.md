## the nigelpoulton/gsd repo is from the Getting Started with Docker Pluralsight course

## multipass has the `multipass launch docker` command to provide a fresh VM running Docker Engine

multipass find

multipass launch docker --name node1

multipass list

multipass info node1

multipass shell node1

# images

docker pull redis

docker images --digests

docker info

docker manifest inspect redis

docker manifest inspect redis -v

docker inspect redis

docker rmi redis

docker images

sudo cat /var/lib/docker/image/overlay2/repositories.json

docker run -it --name alpine alpine

docker exec -it alpine /bin/sh

# building images

## https://github.com/nigelpoulton/ddd2023 -> node-app

docker build -t vegahen/ddd2023:nodeweb .

docker images

docker run -d --name web -p 8080:8080 vegahen/ddd2023:nodeweb

docker exec -it web /bin/sh

docker container stop web

docker container ls -a

docker rm web

docker rmi vegahen/ddd2023:nodeweb

docker build -t vegahen/ddd2023:nodeweb https://github.com/nigelpoulton/psweb.git#main

docker history vegahen/ddd2023:nodeweb

docker inspect vegahen/ddd2023:nodeweb

# working with containers

docker ps

docker run -it alpine /bin/sh

docker run -d alpine sleep 1d

docker rm $(docker ps -aq) -f

docker run -d --name web -p 5005:80 nginx

docker port web

# building a secure swarm

docker swarm init

docker swarm join-token worker

docker swarm join-token manager

docker node ls

sudo openssl x509 -in /var/lib/docker/swarm/certificates/swarm-node.crt -text

docker swarm join-token worker --quiet

docker swarm join-token manager --quiet

docker swarm update --autolock=true

sudo service docker restart

docker swarm unlock

# container networking

docker network ls

docker network inspect bridge

docker run -d --name web -p 8080:80 nginx

docker port web

docker network create -d bridge golden-gate

docker run --rm -d --network golden-gate alpine sleep 1d

docker network create -d overlay overnet

docker service create -d --name ping --network overnet --replicas 3 alpine sleep 1d

docker service create -d --name pong --network overnet --replicas 3 alpine sleep 1d

docker service ps ping

docker exec -it ad94dbd253e6 sh

ping pong

docker service inspect ping --pretty

# persistent data and volumes

docker volume ls

docker volume create --name myvol

docker volume inspect myvol

docker volume create ps-vol

sudo ls -l /var/lib/docker/volumes

docker volume rm myvol ps-vol

docker volume ls

docker run -dit --name voltest --mount source=ubervol,target=/vol alpine

docker exec -it voltest sh

echo "Let's be respectful to everyone" > /vol/newfile

sudo cat /var/lib/docker/volumes/ubervol/_data/newfile

docker rm voltest -f

docker run -dit --name volmore --mount source=ubervol,target=/vol alpine

docker exec -it volmore sh

echo "Let's do this" > /vol/newfile

echo "... and this and this and this" >> /vol/newfile

docker volume rm ubervol

docker rm volmore -f

docker volume rm ubervol

# docker compose

## https://github.com/nigelpoulton/ddd2023 -> compose

docker compose up

docker volume ls

docker network ls

docker images

docker ps -a

docker port compose-web-fe-1

docker compose down

docker compose up > /dev/null 2>&1

docker compose up > /dev/null 2>&1 &

docker compose up -d

docker compose up --detach

docker compose ls

docker compose ls -a

docker compose stop

docker compose start

docker compose down --volumes --rmi all

# production-grade multi-container apps

## https://github.com/nigelpoulton/ddd2023 -> stack

## stacks don't support builds

docker stack deploy -c compose.yaml psight

watch docker service ls

docker stack ls

docker stack ps psight

docker stack services psight

docker service scale psight_web-fe=10

docker stack rm psight
