# Docker #
Docker notes. 

---
## Architecture:
### Docker Components:
- Images -> set of instructions to build the container configuration.
- Containers -> the running image.
- Registery -> like a repo.
- Client -> the CLI tool.
- Daemon -> takes the commands from the client and apply it on the runc.
- Namespaces -> isolate containers' resources from each other.
   
---
## Cheatsheet:
### Commands:
- `docker version`: shows the details of docker components.
- `docker images`: list all the local images.
- `docker pull imagename:version`: pulls image from dockerhub.
- `docker run imagename:version`: runs a specific image from the local images, and if the image doesn't exist locally, it pulls it first from the dockerhub.
- `docker ps -all` or `docker container ls -all`: list all the containers. 
- `docker container rm containerid`: removes the container, we can pass the first three letters of the container name. 
- `docker image rm imagename`: removes the image locally. 
- `docker container run -d`: runs the container in detached mode.
- `docker image inspect imagename`: shows the details of the image.
- `docker logs containerid`: gets the logs from the container.
- `docker stats containerid`: gets the resources consumption for a specific container.
- `docker info`: gets an overview of the docker client/server.
- `docker container inspect --format='{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}'`: gets the IP of the container.




---
## Popular Images:
- redis -> caching
- nginx -> webserver/proxy
- alpine -> lightweight linux image
- d


