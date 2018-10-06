# Docker
Personal Docker Note

## Delete Docker Image
- docker rmi $(docker images -a -q)
- conflict: unable to delete ec496b4bc6e3 (cannot be forced) - image has dependent child images
- sudo docker rmi $(sudo docker images -aq) --force

## Stop/Remove Docker Container
- docker stop $(docker ps -a -q)
- docker rm $(docker ps -a -q)

## Remove Docker Volume
- docker volume rm $(docker volume ls)

## Build Docker Image (Golang)

(Size - 94.4MB)
~~~
FROM google/debian:wheezy
EXPOSE 6767
ADD accountservice-linux-amd64 accountservice-linux-amd64 
ENTRYPOINT ["./accountservice-linux-amd64"]
~~~

(Size - 545MB) ( Do not work ) 
~~~
FROM iron/go:dev
WORKDIR /app
ADD accountservice-linux-amd64 /app/
ENTRYPOINT ["./accountservice-linux-amd64"]
~~~
(Size - 10MB) 
~~~
FROM iron/base
ADD stock  / 
ENTRYPOINT ["/stock"]
~~~

### Error - standard_init_linux.go:190: exec user process caused "no such file or directory"
~~~
You most likely either:
    use the binary for the wrong platform
    the binary is not statically linked (has not all the necessary libraries)
You can use CGO_ENABLED=0 to build your binary statically.
~~~

## Docker Swarm

- [Docker Machine](https://docs.docker.com/machine/install-machine/#install-machine-directly)
- [Deriklupander's Swarm Manager Configuration](https://github.com/callistaenterprise/goblog/blob/master/extras/docker-setup.md)
- [Swarm Visualizer](https://github.com/ManoMarks/docker-swarm-visualizer)

~~~
docker service create \
  --name=viz \
  --publish=8000:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  manomarks/visualizer    
~~~

## Docker Network

- docker network create --driver overlay my_network_name

