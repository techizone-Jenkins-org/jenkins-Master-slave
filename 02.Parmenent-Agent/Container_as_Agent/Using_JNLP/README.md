# jenkins-Parmenet_Agent Container using SSH
## Build a new docker image from this Dockerfile
```
docker build -t myjenkins-agent:jnlp .
```
## Create a Container from our new docker image 

### 1. Create a Network for jenkins Master
```
docker network cerate jenkins
```
### 2. Create the Jenkins master with Docker container in that Network
```
docker run -d --rm --name=jenkins-JNLP \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  -e JENKINS_URL=http://<jenkins-host>:8080 \
  -e JENKINS_AGENT_NAME=agent1 \
  -e JENKINS_SECRET=<Jenkins-Node-secret-key-HERE> \
  --workdir /var/lib/jenkins \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume jenkins-workdir:/var/lib/jenkins \
  myjenkins-agent:jnlp

```


