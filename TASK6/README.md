# JENKINS 

## Install Jenkins. It must be installed in a docker container

I deployed the jenkins LTS release on a single host machine using the jenkins official Docker image from docker hub. To install jenkins, the documenation
recommends the following command be used:

```
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
```
This docker command mounts a /var/jenkins_home_directory from the host machine, thus adding persistence to jenkins, meaning no data loss on container restart or update. And also exposes ports so that jenkins dashboard is available via web browser.

To acquire the password from the jenkins docker container, i used the following command:

```
docker exec ${CONTAINER_ID} cat /var/jenkins_home/secrets/initialAdminPassword
sudo apt install -y openjdk-8-jre
 wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
 wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
 sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
 sudo apt-get update
```

<img width="944" alt="image" src="https://user-images.githubusercontent.com/107506005/177204622-01ec7f43-6d30-4df1-8d3c-ae8cd4f97d98.png">

##  Install necessary plugins

