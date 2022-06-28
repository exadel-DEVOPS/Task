# TASK4 DOCKER

## 1. Install docker. (Hint: please use VMs or Clouds  for this.)
## EXTRA 1.1. Write bash script for installing Docker

![image](https://user-images.githubusercontent.com/107506005/176232406-b2eca9af-7e3c-413b-8d60-b72e4e9a85c6.png)
### Note: script is located on TASK folder

### extra 1.1. Running hello-world docker container
<img width="636" alt="image" src="https://user-images.githubusercontent.com/107506005/176233124-89b30562-8ce5-42be-9eb0-9d0b7b7f81fc.png">

## 2.1 . Find, download and run any docker container "hello world". (Learn commands and parameters to create/run docker containers.
## EXTRA 2.1. Use image with html page, edit html page and paste text: <Userrname> 2022
 

![image](https://user-images.githubusercontent.com/107506005/176241245-2ff03dd0-a3f0-4d71-ad2f-6d36f6ae70fd.png)

```
echo "<html><body><h2>exadel-DEVOPS 2022 </h2></body></html>" > index.html
docker run --name web -dt nginx
docker exec web mkdir /var/www
 docker cp webfiles/default.conf web:/etc/nginx/conf.d/default.conf
docker cp webfiles/html/ web:/var/www/
 docker exec web chown -R nginx:nginx /var/www/
docker exec web nginx -s reload
curl <IP ADDRESS>
 docker commit web nginx-image
 docker run -dt --name web-nginx  -p 80:80  nginx-image 
 
  ```
  
  
  
     
<img width="680" alt="image" src="https://user-images.githubusercontent.com/107506005/176249838-12c5f81f-bcfd-472e-a38a-9ad0c26d9412.png">



#### 3.1. Create your Dockerfile for building a docker image. Your docker image should run any web application (nginx, apache, httpd). Web application should be #### located inside the docker image. 
#### EXTRA 3.1.1. For creating docker image use clear basic images (ubuntu, centos, alpine, etc.)
 
![image](https://user-images.githubusercontent.com/107506005/176254327-b6909b4f-c45b-41b3-84d4-b5f4500f8f0c.png)

 <img width="546" alt="image" src="https://user-images.githubusercontent.com/107506005/176255955-481793ab-6a12-4b0e-a700-3d53e198f4f5.png">

#### 3.2. Add an environment variable "DEVOPS=<username> to your docker image 
### EXTRA 3.2.1. Print environment variable with the value on a web page (if environment variable changed after container restart - the web page must be updated with a new value)
 
##### For this, i build another docker container based on the ubuntu image, supplied the env variable named ubuntu, but also added an entry point of bash script that will print out the env variable to the web page for each restart
 
 ![image](https://user-images.githubusercontent.com/107506005/176274946-a5165c58-4f62-44b8-aa2c-bde3f9e78088.png)

 ####- webpage script
 ![image](https://user-images.githubusercontent.com/107506005/176275308-e781e23d-c6e7-43f8-8193-9a5e19b8d981.png)

 <img width="381" alt="image" src="https://user-images.githubusercontent.com/107506005/176275515-6e314742-6782-456e-82ee-3e6ad98e9eb4.png">

 ##### to make sure the webpage is updated with a new value
 
 ```
 docker run -itd -e DEVOPS="Centos" --rm -p 80:80 --name web2 webserver
 ```
 
 <img width="453" alt="image" src="https://user-images.githubusercontent.com/107506005/176284870-41f6d4a7-3673-4edf-8457-d15d6f470e90.png">

 
 ###4. Push your docker image to docker hub (https://hub.docker.com/). Create any description for your Docker image. 
### EXTRA 4.1. Integrate your docker image and your github repository. Create an automatic deployment for each push. (The Deployment can be in the “Pending” status ### for 10-20 minutes. This is normal).

 ```
 docker login username=USERNAME
 docker tag <image> <repo>
 docker push <repo>
 ```
 
 <img width="644" alt="image" src="https://user-images.githubusercontent.com/107506005/176289321-8dc365a7-a2ec-457f-9791-5f7851894c77.png">

 
 
 

