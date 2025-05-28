# jenkins-Master & docker server in differnt containers

### 1. Create a Network for jenkins Master
```
docker network cerate jenkins
```
### 2. Create the Docker server container in the Network "jenkins"
```
docker run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind --storage-driver overlay2
```


