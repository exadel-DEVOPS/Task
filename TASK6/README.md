# JENKINS 

## Install Jenkins. It must be installed in a docker container

1. Created a bridge network

```
docker network create jenkins
```

In order to execute Docker commands inside jenkins node, the docker:dind image is used.

```
docker run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind --storage-driver overlay2
```

To customise official jenkins Docker image, i did the following steps:
####### a. Create Dockerfile with the following content

```

FROM jenkins/jenkins:2.346.1-jdk11
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.5 docker-workflow:1.28"

```

####### b. Build the new docker image from the dockerfile

```
docker build -t myjenkins-blueocean:2.346.1-1 .
```

####### c. Run a jenkins container from the jenkins image

```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.346.1-1
```


To acquire the password from the jenkins docker container, i used the following command:

```
docker exec <container_name> cat /var/jenkins_home/secrets/initialAdminPassword
```

<img width="944" alt="image" src="https://user-images.githubusercontent.com/107506005/177204622-01ec7f43-6d30-4df1-8d3c-ae8cd4f97d98.png">



##  2. Install necessary plugins

Installed suggested pluggins and created an administrative user

<img width="870" alt="image" src="https://user-images.githubusercontent.com/107506005/177513038-f180f84d-d94e-4c98-b874-0549f6c9a5a9.png">


## 3. Configure several (2-3) build agents. Agents must be run in docker.

<img width="924" alt="image" src="https://user-images.githubusercontent.com/107506005/177524257-510141ef-e330-474e-a3c6-b92ca176b200.png">
<img width="805" alt="image" src="https://user-images.githubusercontent.com/107506005/177525937-a191b23b-3bab-49c1-8de0-4a859d07932b.png">
<img width="950" alt="image" src="https://user-images.githubusercontent.com/107506005/177529730-12d40e53-087b-4269-9ceb-a9be9ffc8f15.png">
<img width="947" alt="image" src="https://user-images.githubusercontent.com/107506005/177531014-a08a138a-b279-413e-9777-c2e5bdf1b833.png">
<img width="845" alt="image" src="https://user-images.githubusercontent.com/107506005/177532045-22d8f880-1b3c-4189-9103-a128327a847e.png">




