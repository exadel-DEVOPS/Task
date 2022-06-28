# TASK4 DOCKER

## 1. Install docker. (Hint: please use VMs or Clouds  for this.)
## EXTRA 1.1. Write bash script for installing Docker

![image](https://user-images.githubusercontent.com/107506005/176232406-b2eca9af-7e3c-413b-8d60-b72e4e9a85c6.png)
### Note: script is located on TASK folder

### extra 1.1. Running hello-world docker container
<img width="636" alt="image" src="https://user-images.githubusercontent.com/107506005/176233124-89b30562-8ce5-42be-9eb0-9d0b7b7f81fc.png">

## 2.1 . Find, download and run any docker container "hello world". (Learn commands and parameters to create/run docker containers.
## EXTRA 2.1. Use image with html page, edit html page and paste text: <Username> 2022

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
 
  ```
  
  
  
  





