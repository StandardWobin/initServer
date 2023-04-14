# initServer


## needed on you local machine
1. Filezilla https://filezilla-project.org/
2. Kitty http://www.9bis.net/kitty/index.html#!index.md 
3. Puttygen https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
4. Save Place to store private key (if you loose that, ther server is not accessable anymore - THERE IST NO WAY AROUND)

## to do before you ssh
1. generate ssh files using ```ssh-keygen```
2. **BACKUP SSL PRIVATY KEY**, if you loose that you are out of the server - forever
3. convert ssh private key to ppk file using puttygen




## set up basics
1. ssh via Kitty
2. change root password ```passwd root``` [generate and store password]
3. ```sudo apt update -y```
4. ```sudo apt upgrade -y```
5. ```mkdir -p ~/.ssh ```
6. copy local private ssh key echo ```public_key_string >> ~/.ssh/authorized_keys```
7. ```chmod -R go= ~/.ssh```
8. ```groupadd sshlogin```
9. ```adduser webadmin``` [generade and store password]
10. ```usermod -aG sshlogin webadmin```
11. ```echo "AllowGroups sshlogin" >> /etc/ssh/sshd_config```
12. edit /etc/ssh/sshd_config and set "PermitRootLogin **no**" and "PasswordAuthentication **no**"
13. ```chown -R webadmin:webadmin ~/.ssh```
14. ```echo "IPV6=no" >> /etc/ufw/ufw.conf```
15. ```ufw allow OpenSSH
16. ```ufw allow https
17. ```ufw allow http
18. ```ufw --force enable```
19. ```service ssh restart```

PLease test if you can login via ssh:
Login via Root shoud not be possible anymore
Login via webadmin and password should not be possible
You need to add the local private key to Kitty to authenticae 








