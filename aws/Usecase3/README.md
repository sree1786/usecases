#   USECASE-3 (Integration GIT,Maven,Jenkins , Docker, Tomcat)
 
 Please watch usecase-2 before come here
 
# What you will be learn this usecase :

As IT employees we work on many areas ( coding,support,infrastructure ) but while onboarding any new service we really are not aware how exactly code will deploy to production . There  are many possibilities  we can onboard our requirements to production .This use case will explain one of the ways to deploy our code to prod. 

This video  I have explained  how to troubleshoot the issues  also . After this recording was completed I had recorded another video without troubleshooting . But I feel People need to learn how to correct the mistakes also . So I preferred to upload this video . Keep Fail and learn more 

# Architecture
![Watch the image](/DockerJenkins.png)

# Steps

 -  step1: Install Jenkins,Maven,GIT and Tomcat ( please watch usecase-2)
 -  step2: Install Docker
 -  step3: Add Docker info in jenkins 
 -  step4: Exchange ssh keys betwen jenkins server and Docker server
 -  step5: Create the jenkins job
 -  step6: Access web application


# step1: Install Jenkins,Maven,GIT and Tomcat

  Please watch ealier video's ( How to install Jenkins, Maven and Tomact) and follow the document attached  files in same repository
  
  Once Jenkins, maven and tomcat ready

#  step2: Install Docker

# Install docker on EC2 instance and start services
```yum install docker```

```service docker start```

# create a new user for Docker management and add him to Docker (default) group
```useradd dockeradmin```

```passwd dockeradmin```

```usermod -aG docker dockeradmin```

```visudo```

```dockeradmin ALL=(ALL)       NOPASSWD: ALL``` (add dockeradmin user after root)

```vi /etc/ssh/sshd_config```  ( disable --> PasswordAuthentication no  & enable PasswordAuthentication yes )

```service sshd restart```

# Write a Docker file under /opt/docker

```mkdir /opt/docker```

```chown -R dockeradmin:dockeradmin /opt/docker/ ```
# Create Docker image
 ```
 vi Dockerfile
 ```


```
From tomcat:9-jre9 

# Maintainer
MAINTAINER "cloudnloud" 

# copy war file on to container 
COPY ./webapp.war /usr/local/tomcat/webapps 
```
# step3: Add Docker info in jenkins

Login to Jenkins console and add Docker server to execute commands from Jenkins

Manage Jenkins --> Configure system --> Publish over SSH --> add Docker server and credentials
      Click add 
           SSH server : dockerhost
           Hostname: server ip (public ip)
      Username: dockeradmin
      Click advange  enable password password : give dockeradminpassword
      
# step 4: Exchange keys between jenkins server and Docker server


login to jenkins as dockeradmin user

```
ssh-keygen
```
Presee enter and main default everything

 ls -a
 cd .ssh/
 ssh-copy-id IPADDREE(second server ip address)
 
 ( to link between docker server and jenkins server ( in jeninkins servers you install both junekins,tomcat,git )
 
# step 5: create the jenkins job

Create Jenkins job

create job --> maven project --> 

A) Source Code Management
Repository : https://github.com/veejee2331/webapplication 
Branches to build : */main

B) Build Root POM: pom.xml
Goals and options : clean install package

C)  Post steps  --> Add Post buid step -- > select 

send files or execute commands over SSH 

Name: docker_host
Source files : ```webapp/target/*.war ``` Remove prefix : ```webapp/target``` Remote directory : ```//opt//docker```

Exec command[s] :

```
docker stop cloundnloud_demo;
docker rm -f cloundnloud_demo;
docker image rm -f cloundnloud_demo;
cd /opt/docker;
docker build -t cloundnloud_demo .
```

D) Select again --> 

send files or execute commands over SSH

Name: docker_host
Exec command : 

```
docker run -d --name cloundnloud_demo -p 8090:8080 cloundnloud_demo
```

E) Login to Docker host( through ssh) and check images and containers. (no images and containers)

F) Execute Jenkins job

G )check images and containers again on Docker host. This time an image and container get creates through Jenkins job

# step6: Access web application

Access web application from browser which is running on container
```
http://<docker_host_Public_IP>:8090/uri
```
Note : Please make sure you have to open 8090 port in firewall/outbound rules 

