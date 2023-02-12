# Docker #
Docker notes. 

---
## Architecture
### Docker Components:
- Images -> set of instructions to build the container configuration.
- Containers -> the running image.
- Registery -> like a repo.
- Client -> the CLI tool.
- Daemon -> takes the commands from the client and apply it on the runc.
- Namespaces -> isolate containers' resources from each other.
   
---
## Docker CLI
### Commands:
- `docker version`: shows the details of docker components.
- `docker info`: gets an overview of the docker client/server.
- `docker login`: sets the dockerhub credentials to be able to pull/push from and to private repos.
- `docker logout`: logs out. 

---
## Images

### Commands:
- `docker build --tag imagename:version dockerfiledirectory`: build a new image.
- `docker images` or `docker image ls`: list all the local images.
- `docker pull imagename:version`: pulls image from dockerhub.
 - `docker image inspect imagename`: shows the details of the image.
- `docker image rm imagename`: removes the image locally. 
- `docker history imagename`: gets the history/details of the image layers. 
- `docker tag sourceimage:!tag targetimage:!tag`: create a tag target_image that refers to source_image.
- `docker push imagename`: push the image to the dockerhub.

### Examples:
Saving an image as tar file.
```
docker save my-app:1.0 > my-app.tar
```

Loading an image from tar file.
```
docker load -i /home/ubuntu/my-app.tar
```
---
## Containers

### Commands:
- `docker run [OPTIONS] imagename:version`: runs a specific image from the local images, and if the image doesn't exist locally, it pulls it first from the dockerhub.
  - `-d`: runs the container in detached mode. -d equals --detach
  - `-p port:port`: defines the container with a specific port mapping. -p equals --publish
  - `--name`: defines the container name.
  - `-v volumename/bindpath:destination`: defines a friendly name for the volume.
  - `-e`: passing environment variables.
  - `--network`: defines the network of the container.
  - `--link containername`: links the container with another
- `docker ps -all` or `docker container ls -all`: list all the containers. 
- `docker stats containerid`: gets the resources consumption for a specific container.
- `docker container stop containerid`: stops a container.
- `docker container stop containerid`: starts a container.
- `docker container inspect --format='{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}'`: gets the IP of the container.
- `docker logs containerid`: gets the logs from the container.
- `docker exec -it containerid command`: runs interactive shell for a specific container. like docker exec -it containerid bash, opens a bash session.
- `docker container rm containerid`: removes the container, we can pass the first three letters of the container name. 
---

## Storage
there are different types of storage: 
- Volumes 
- Mount points 
- tmpfs

### Commands:
- `docker volume ls`: list all volumes.

### Examples:
Attaching a volume while running a container
```
docker run -it -d -v myvolume:/mounted_folder alpine
```
---

## Networking
types of networks:
- Bridge network: the default internal network for docker. Only containers inside the same network can see each other.
- Host: The host machine network, this is allowing containers to see each other.
- None: Isolation of the container, will not be published or even accessible by the other containers. 
- Overlay
- Macvlan

### Commands:
- `docker network ls`: list all networks.
- `docker network inspect networkname`: gets the details of the network and its attached containers.
- `docker network create --driver drivername networkname`: creates a network.
  - `--subnet 172.120.0.0/16`: defines the subnet of the network.
- `docker network disconnect [OPTIONS] networkname containername`: disconnects a container from the network.
- `docker network connect [OPTIONS] networkname containername`: connects a container from the network.
---
## Docker Compose

### Commands:
- `docker compose build`: rebuild the image/s if there's a change done on it.
---
## Tips and Tricks

To stop all the running containers, use the below: (the same goes for the remove)
```
docker container stop $(docker container ps)
```


---

## Popular Images:
- alpine -> lightweight linux image
- nginx -> webserver/proxy
- redis -> caching/in-memory database
- mariadb -> database
- timer -> prints timestamp every second