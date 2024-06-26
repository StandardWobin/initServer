# initServer
This is a small set up script for Ubuntu22 cloud / virtual server with root ssh access.
Ideal for basic web apps with DBMS on localhost for smaller projects. 


NO WARRANTY IF YOU USE THIS SCRIPT

## needed on you local machine
1. Filezilla https://filezilla-project.org/
2. Kitty http://www.9bis.net/kitty/index.html#!index.md 
3. Puttygen https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html 

## to do before you ssh
1. Generate public and private key using puttygen, you need putty and openssh private key
3. **BACKUP SSL PRIVATE KEYS**, if you loose that you are out of the server - forever and ever and ever

## SSL Certificates
1. get private and public keys as SSL certificates  from provider

## set up and secure basic server
1. ssh via Kitty as root
2. change root password *generate and store password*
```  
passwd root
``` 
3. Upgrade System
```
sudo apt update -y && sudo apt upgrade -y
```
4. Set up non root user webadmin [generate and store password]
```
groupadd sshlogin && adduser webadmin && echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config
```
5. Give webadmin sudo and ssh privileges, and switch user
```
usermod -aG sshlogin webadmin && usermod -aG sudo webadmin && su webadmin
```
5. Create ssh config directory in webadmin folder
```
mkdir -p ~/.ssh
```


6. **MODIFY** and copy local **public** ssh key content string via  ```echo "ssh-rsa XXX......YYY....ZZZ...keycode" >> ~/.ssh/authorized_keys```


7. set up permissions to ssh folder
```
chmod -R go= ~/.ssh && chown -R webadmin:webadmin ~/.ssh
```

7.switch to root
```
su root
```

8. EDIT sshd_config and set "PermitRootLogin **no**" and "PasswordAuthentication **no**"
```
nano /etc/ssh/sshd_config
``` 
 
9. Set up firewall  
```
echo "IPV6=no" >> /etc/ufw/ufw.conf && ufw allow OpenSSH && ufw allow https && ufw allow http && ufw allow ssh && ufw --force enable && service ssh restart
```


PLease test if you can login via ssh:
Login via Root should  not be possible anymore
Login via webadmin and password should not be possible
You need to add the local private key to Kitty to authenticate 

## Set up MySql
1. install my sql server
```
sudo apt install mysql-server -y
```

2. Start Sql Server service
```
sudo systemctl start mysql.service
```

3. Start Mysql Prompts
```
sudo mysql
```

4. (in sql) - remove root password temporary to enable secure installation
```
 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
 
5. (in sql) - quit mysql prompt
```
quit;
```

6. set up my sql enter *password* as password. **generate and store new root password** and deactivate everything  you will be asked and what sounds more secure
```
 sudo mysql_secure_installation
``` 


## Connect with mysqlWorkbench over SSH
1. add openssh private key (you need to converse it from puttygen)
2. connect


## Install Node.Js
[https://github.com/nodesource/distributions/blob/master/README.md#debinstall](https://github.com/nodesource/distributions/blob/master/README.md#using-ubuntu-2)
Manual!


## Set up Apache 
1. install apache2
```
 sudo apt-get install apache2 -y && sudo service apache2 stop
``` 

3. change ownership of web folder to webadmin (for wordpress installation it should be www-data)
```
 sudo chown -R  webadmin:webadmin /var/www
``` 
2. safe ssl certficate as key.pem in /etc/apache2/certs/
3. safe ssl certificate as cert.pem in /etc/apache2/certs/
5. Restrict acces to ssl files
```
chown -R root:root /etc/apache2/certs && chmod -R 000 /etc/apache2/certs
```
6. Edit default vhost (use template file in this repository), delete all other default vhost
7. change default vhost to apache2 init file
```
sudo a2enmod ssl && sudo a2enmod rewrite && sudo service apache2 restart
```















