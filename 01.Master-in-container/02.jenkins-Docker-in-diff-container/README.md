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
### 3. Create the Jenkins Master container in the Network "jenkins"

#### Build a new docker image from this Dockerfile
```
docker build -t myjenkins-blueocean:2.504.2-1 .
```
#### Create the Jenkins Master container along with Docker-cli install in the Network "jenkins"
```
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.504.2-1
```
## Test when Jenkins Job create Container that will launch in Docker server or Not

#### 1. Open Browser and Configure the Jenkins
#### 2. Create the Jenkins JOB under execute Shell run the Docker Command
```
docker run nginx
```
### Check UP
##### 1. Check wheather Job is Succeed or NOT
##### 2. Check Container Created or Not in the docker server container
```
Login to Jenkins Master container  and Docker server container using command "docker exec" and then hit the command "docker ps"
See in Both Jenkins master and Docker server are showing smae containers or Not
```

