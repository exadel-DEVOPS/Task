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
 
 
