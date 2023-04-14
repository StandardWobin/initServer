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
5. ```mkdir -p ~/.ssh ```
6. copy local **public** ssh key content string via  ```echo **public_key_string** >> ~/.ssh/authorized_keys```
7. ```chmod -R go= ~/.ssh```
8. ```groupadd sshlogin```
9. ```adduser webadmin``` [generade and store password]
10. ```usermod -aG sshlogin webadmin```
11. ```echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config```
12. ```nano /etc/ssh/sshd_config``` and set "PermitRootLogin **no**" and "PasswordAuthentication **no**"
13. ```chown -R webadmin:webadmin ~/.ssh```
14. ```echo "IPV6=no" >> /etc/ufw/ufw.conf```
15. ```ufw allow OpenSSH```
16. ```ufw allow https```
17. ```ufw allow http```
18. ```ufw --force enable```
19. ```service ssh restart```

PLease test if you can login via ssh:
Login via Root shoud not be possible anymore
Login via webadmin and password should not be possible
You need to add the local private key to Kitty to authenticae 

## Set up MySqlServer and phpmyadmin with ssl
1.









