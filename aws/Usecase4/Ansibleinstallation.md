![Watch the image](/Ansibleinstallation.png)
# Steps

 -  step1: Create three Ec2 instance (one master and two child)
 -  step2: Install ansible rpm in master server
 -  step3: Create ansadmin user both master and child servers and provide root privileges access 
 -  step4: Check the connectivity between master and child servers 
 -  step5: Add child server ip address in master server host area
 -  step6: Testing 


# step1: Create three Ec2 instance (one master and two child

  Please create three instance with minimum configuration of linux
   

#  step2: Install ansible rpm in master server 

```
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```
```
yum install ansible
```
```
ansible --version
 ```
      
# step3: Create ansadmin user both master and child servers and provide root privileges access 

```
 useradd ansadmin
 
 passwd ansadmin
 
 visudo   ( add this line after root --> ansadmin ALL=(ALL)       NOPASSWD: ALL ) 
 
 cd /etc/ssh
 
 ls
 
 vi sshd_config  ( disable --> PasswordAuthentication no  & enable PasswordAuthentication yes )
 
 service sshd restart
 
 ```

# step4: Check the connectivity between master and child servers

First login to master servers as ansadmin user
Then exchange keys between master and child 

```
ssh-keygen
ls -a
cd .ssh/
ssh-copy-id IPADDREE(second server ip address)
```

login to jenkins as dockeradmin user

```
ssh-keygen
```
Presee enter and main default everything

 ls -a
 cd .ssh/
 ssh-copy-id IPADDREE(second server ip address)
 
 
# step5: Add child server ip address in master server host area

Please add child servers information 

sudo vi /etc/ansible/hosts
(add below info)
[all_hosts]
IPADDRESS (both servers) --> save

# Step6: Testing 
```
ansible all -m ping
```

Some more Basic commands 

```
ansible all -m copy -a "src=/home/ansadmin/hello.html dest=/home/ansadmin"
rebooting --> ansible all -a "/sbin/reboot"
copy file --> ansible all -m copy -a "src=/home/dan dest=/tmp/home"
create user --> ansible all -m user -a "name=testuser password=<encryptedpassword>"
remove user --> ansible all -m user -a "name=testuser state=absent"
change file permission --> ansible all -m file -a "dest=/home/dan/file.txt mode=777"
install package --> ansible all -m yum -a "name=httpd state=latest"
start service ---> ansible all -m service -a "name=httpd state=started"
start service --> ansible all +m service -a "name=httpd state=stopped"

```
