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
1. ssh via Kitty
2. change root password ```passwd root``` [generate and store password]
3. ```sudo apt update -y```
4. ```sudo apt upgrade -y```
9. ```groupadd sshlogin```
10. ```adduser webadmin``` [generade and store password]
11. ```usermod -aG sshlogin webadmin```
11. ```usermod -aG sudo webadmin```
13. ```su webadmin```
14. ```mkdir -p ~/.ssh ```
15. copy local **public** ssh key content string via  ```echo "ssh-rsa XXXXXXXXKEXYYYYYYYYYY" >> ~/.ssh/authorized_keys```
16. ```chmod -R go= ~/.ssh```
18. ```chown -R webadmin:webadmin ~/.ssh```
19. ```su root```
19. ```echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config```
20. ```nano /etc/ssh/sshd_config``` and set "PermitRootLogin **no**" and "PasswordAuthentication **no**"
21. ```echo "IPV6=no" >> /etc/ufw/ufw.conf```
22. ```ufw allow OpenSSH```
23. ```ufw allow https```
24. ```ufw allow http```
25. ```ufw --force enable```
26. ```service ssh restart```

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












