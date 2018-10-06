# Docker
Personal Docker Note

## Delete Docker Image
docker rmi $(docker images -a -q)
conflict: unable to delete ec496b4bc6e3 (cannot be forced) - image has dependent child images
sudo docker rmi $(sudo docker images -aq) --force

## Stop/Remove Docker Container
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)

## Remove Docker Volume
docker volume rm $(docker volume ls)

## Build Docker Image (Golang)

(Size - 94.4MB)
FROM google/debian:wheezy
EXPOSE 6767
ADD accountservice-linux-amd64 accountservice-linux-amd64 
ENTRYPOINT ["./accountservice-linux-amd64"]

(Size - 545MB) ( Do not work ) 
FROM iron/go:dev
WORKDIR /app
ADD accountservice-linux-amd64 /app/
ENTRYPOINT ["./app/accountservice-linux-amd64"]

## Docker Swarm

[Link back to H2](#id-goes-here)
https://github.com/callistaenterprise/goblog/blob/master/extras/docker-setup.md

