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
13. ```mkdir -p ~/.ssh ```
14. copy local **public** ssh key content string via  ```echo "ssh-rsa XXXXXXXXKEXYYYYYYYYYY" >> ~/.ssh/authorized_keys```
15. ```chmod -R go= ~/.ssh```
18. ```chown -R webadmin:webadmin ~/.ssh```
19. ```su root```
16. ```echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config```
17. ```nano /etc/ssh/sshd_config``` and set "PermitRootLogin **no**" and "PasswordAuthentication **no**"
20. ```echo "IPV6=no" >> /etc/ufw/ufw.conf```
21. ```ufw allow OpenSSH```
22. ```ufw allow https```
23. ```ufw allow http```
24. ```ufw --force enable```
25. ```service ssh restart```

PLease test if you can login via ssh:
Login via Root shoud not be possible anymore
Login via webadmin and password should not be possible
You need to add the local private key to Kitty to authenticae 

## Set up MySqlServer and phpmyadmin with ssl
1.









