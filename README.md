# initServer

this init is for UBUNTU 22

## needed on you local machine
1. Filezilla https://filezilla-project.org/
2. Kitty http://www.9bis.net/kitty/index.html#!index.md 
3. Puttygen https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html 

## to do before you ssh
1. Genreate public and private key using puttygen
2. **BACKUP SSL PRIVATY KEY**, if you loose that you are out of the server - forever

## SSL Certificates
1. get private and public keys as SSL Certifacets from provider

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
4. Set up non root user webadmin [generade and store password]
```
groupadd sshlogin && adduser webadmin && echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config
```
5. Give webadmin sudo and ssh privilges, and switch user
```
usermod -aG sshlogin webadmin && usermod -aG sudo webadmin && su webadmin
```
5. Create ssh config directory in webadmin folder
```
mkdir -p ~/.ssh
```


6. **MODIDY** and copy local **public** ssh key content string via  ```echo "ssh-rsa XXX......YYY....ZZZ...keycode" >> ~/.ssh/authorized_keys```


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
echo "IPV6=no" >> /etc/ufw/ufw.conf && ufw allow OpenSSH && ufw allow https && ufw allow http && ufw --force enable && service ssh restart
```


PLease test if you can login via ssh:
Login via Root shoud not be possible anymore
Login via webadmin and password should not be possible
You need to add the local private key to Kitty to authenticae 

## Set up MySqlServer
1. ```sudo apt install mysql-server -y```
2. ```sudo systemctl start mysql.service```
3. ```sudo mysql```
4.(in sql) ```ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';```
5.(in sql) ```quit;```
6. ```sudo mysql_secure_installation``` (ENTER "password" as password not ROOT password ;)
8. change root passwort [generade and store password], and disable everthing
7. remove anynomas

## Connect with mysqlWorkbench over SSH
1. add openssh private key (you need to converse it from puttygen)
2. connect


## Install Node.Js
[https://github.com/nodesource/distributions/blob/master/README.md#debinstall](https://github.com/nodesource/distributions/blob/master/README.md#using-ubuntu-2)
Manual!


## Set up Apache 
1. ```sudo chown -R  webadmin:webadmin /var/www``` *(for wordpress installation it should be www-data)*
2. safe ssl certficate as key.pem in /etc/apache2/certs/
3. safe ssl certificate as cert.pem in /etc/apache2/certs/
4. ```chown -R root:root /etc/apache2/certs```
5. ```chmod -R 000 /etc/apache2/certs```
6. change default vhost to apache2 init file
7. ```sudo a2enmod ssl```
8. ```sudo a2enmod rewrite```
9. ```sudo service apache2 restart```



## Hndy Toolsi tool
1.screen
2.pm2








## ADVANCED SECURITY
1. Setup root login notifications 












