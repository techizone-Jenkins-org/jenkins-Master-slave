# jenkins-Master Container
## Build a new docker image from this Dockerfile
```
docker build -t myjenkins-docker .
```
## Create a Container from our new docker image 

### 1. Create a Network for jenkins Master
```
docker network cerate jenkins
```
### 2. Create the Jenkins master with Docker container in that Network
```
docker run -dit -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --name jenkins-docker myjenkins-docker
```
