# exadel devops


# 1. Created two EC2 instances with Ubuntu and AWS linux OS
![image](https://user-images.githubusercontent.com/107506005/174427339-ddbf23b9-baa1-4c09-a80a-ab8dfa33dcb8.png)

# 2. I checked for ssh connection from my host to the client

1. Ubuntu host public-IP is:  54.144.189.20
2. AWS linux public-ip is  52.70.44.237 

# 3. I added a new inbound rule to the security group  in order to be able to ping both instances.

![image](https://user-images.githubusercontent.com/107506005/174427671-789d220d-6f43-40ba-9b62-0ddb5cc8423c.png)

# Checking up ping in both server 
<img width="506" alt="image" src="https://user-images.githubusercontent.com/107506005/174427804-c09e948e-e994-4ea1-b6f7-255fac27a87e.png">

<img width="523" alt="image" src="https://user-images.githubusercontent.com/107506005/174427872-04a77129-6023-473a-abcc-01acdd4cf1ee.png">

# Installed Apache web server to Linux

<img width="682" alt="image" src="https://user-images.githubusercontent.com/107506005/174429626-5fe560d1-7ed9-43f4-9d58-8b1359fe14c7.png">


# Created an hello-word page with information about OS version

![image](https://user-images.githubusercontent.com/107506005/174428552-dfc14f78-5630-4360-92c3-d411c9a46216.png)


# Added one more inbound rule to my security group to allow on http port 80

![image](https://user-images.githubusercontent.com/107506005/174428678-18ec08da-d5c9-4504-99f9-07b7c8313752.png)



