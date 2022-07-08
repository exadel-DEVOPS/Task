
 # TASK7---- LOGGING AND MONITORING

## 1. Zabbix:
    __Big brother is watching__
    
### 1.1 Install on server, configure web and base

I installed the server on ubuntu 18.04 VM

__Step1: Installed zappix repository___

```
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-3+debian10_all.deb
# dpkg -i zabbix-release_6.0-3+debian10_all.deb
# apt update
# apt-get install -y zabbix-apache-conf
```

__step2:  Install Zabbix server, frontend, agent___

```
# apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

___step3: Create initial database__
 I already had a running mysql server 
 
 ```
 # mysql -uroot -p
password
mysql> create database zabbix character set utf8mb4 collate utf8mb4_bin;
mysql> create user zabbix@localhost identified by '123';
mysql> grant all privileges on zabbix.* to zabbix@localhost;
mysql> quit;
 ```
 
 On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.

```
zcat /usr/share/doc/zabbix-sql-scripts/mysql/server.sql.gz | mysql -uzabbix -p zabbix

```
 
 __step4: Configure the database for Zabbix server___
 
 Edit file /etc/zabbix/zabbix_server.conf and uncomment DBPASSWORD AND add zabbix password
 
 __step4: Start Zabbix server and agent processes__
 
 ```
 # systemctl restart zabbix-server zabbix-agent apache2
# systemctl enable zabbix-server zabbix-agent apache2
 ```
 
 Zabbix server is ready at http://3.90.78.248/zabbix/setup.php
 
 ## 1.2 Prepare VM or instances
 
 #####  I prepared 2 VMS
 <img width="905" alt="image" src="https://user-images.githubusercontent.com/107506005/177949116-ea998510-145e-47cf-ba79-0729b6ae2dd4.png">

## 1.2.1 Install Zabbix agents on previously prepared servers or VM.

####### check the next for this answer

## Extra 1.2.2: Complete 1.2.1 using ansible
```
# ansible-playbook -i inventory agent.yaml -u centos --key-file=node.pem -b
---
- hosts: web01
  become: true
  gather_facts: true
  tasks:


    - name: install pcre2
      yum:
        name: "pcre2-devel.x86_64"

    - name: install zabbix centOS 7 rpm file
      yum:
        name: "https://repo.zabbix.com/zabbix/6.0/rhel/7/x86_64/zabbix-agent-6.0.0-1.el7.x86_64.rpm"
        validate_certs: no

    - name: upgrade all packages
      yum: name=* state=latest

    - name: install zabbix-agent 6.x for centOS 7
      yum:
        name: zabbix-agent
        state: latest



    - name: Start service Zabbix Agent, if not started
      ansible.builtin.service:
        name: zabbix-agent
        state: started

```

<img width="926" alt="image" src="https://user-images.githubusercontent.com/107506005/178020243-74369769-be26-443b-8bdb-13fbbbd91812.png">

## 1.3 Make several of your own dashboards, where to output data from your host/vm/container (one of them)

<img width="929" alt="image" src="https://user-images.githubusercontent.com/107506005/178024469-ef2dd801-a0c0-48c5-bcb3-a1299b0c18d0.png">

## 1.4 Active check vs passive check - use both types.

![image](https://user-images.githubusercontent.com/107506005/178026444-46cce9f4-f567-42b6-b456-2260b880507b.png)


If you use the Zabbix agent in the passive mode, it means that the poller (internal server process) connects to the agent on port 10050/TCP and polls for a certain value (e.g., host CPU load). The poller waits until the agent on the host responds with the value. Then the server gets the value back, and the connection closes.

In the active mode, all data processing is performed on the agent, without the interference of pollers. However, the agent must know what metrics should be monitored, and that is why the agent connects to the trapper port  10051/TCP of the server once every two minutes (by default). The agent requests the information about the items, and then performs the monitoring on the host and pushes the data to the server via the same TCP port.


### How steps i used in configuring both active and passive agent checks:

1. Opened the zabbix_agentd.conf configuration file
2. Specified my Zabbix Server address in the Server and ServerActive parameters
3. Defined the name of the host in the Hostname parameter
4. Restart the Zabbix Agent
5. Went to Configuration →  Hosts
6. Created two hosts in Zabbix frontend – one for passive and one for active checks
7. For passive Agent host – defined an Agent interface containing the address of my Zabbix Server
8. Applied the corresponding Linux by Zabbix Agent/Linux by Zabbix Agent active template

### passive  checks

<img width="947" alt="image" src="https://user-images.githubusercontent.com/107506005/178030972-1b308d06-39b6-41d0-b978-43eeb4cbefee.png">

##### active checks

<img width="946" alt="image" src="https://user-images.githubusercontent.com/107506005/178033897-bf1dc989-bf63-499f-94fc-ed945cd1ada4.png">

 
