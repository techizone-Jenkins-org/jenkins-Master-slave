# jenkins-Parmenet_Agent Container using SSH
## Build a new docker image from this Dockerfile
```
docker build -t myjenkins-agent:ssh .
```
## Create a Container from our new docker image 

### 1. Create a Network for jenkins Master
```
docker network cerate jenkins
```
### 2. Create the Jenkins master with Docker container in that Network
```
docker run -d --rm --name=jenkins-agent1 \
  --publish 2200:22 \
  --network agent-network \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume jenkins-workdir:/var/lib/jenkins \
  -e "JENKINS_AGENT_SSH_PUBKEY=<Your-SSH-KEY-HERE>" \
  myjenkins-agent:ssh

```


