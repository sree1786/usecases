#   USECASE-4 (Integration GIT,Maven,Jenkins , Docker, Tomcat and  Ansible )
 
 Please watch Usecase-2,Usecase-3  before come here
 
# What you will be learn this usecase :

As IT employees we work on many areas ( coding,support,infrastructure ) but while onboarding any new service we really are not aware how exactly code will deploy to production . There  are many possibilities  we can onboard our requirements to production .This use case will explain one of the ways to deploy our code to prod. 

This video  I have explained  how to troubleshoot the issues  also . After this recording was completed I had recorded another video without troubleshooting . But I feel People need to learn how to correct the mistakes also . So I preferred to upload this video . Keep Fail and learn more 

# Architecture
![Watch the image](/GIT-Ansible-Tomcat.png)

# Steps

 -  step1: Please setup Ansible envionment  ( please chcek ealier video and follow document )
 -  step2: Please setup Jenkins,Tomcat envionment (Usecase-2)
 -  step3: Update Ansible server in jenkins
 -  step4: Create new mavin job 
 -  step5: Check the process of excution 
 -  step6: Test


# sstep1: Please setup Ansible envionment  ( please chcek ealier video and follow document )

  Please watch ealier video's ( How to install Ansible ) and follow the document attached  files in same repository
  
 

#  step2: Please setup Jenkins,Tomcat envionment (Usecase-2)

Install jenkins plugin  --> publish over ssh

# step3: Update Ansible server in jenkins

manage jenkis --> configure systems --> publish over to ssh --> ssh servers --> add 

   name : ansiblemaster
  
  hostname: ipaddress (private bez of same vpc)
 
 username : ansadmin

 click advances session 
 
 password: asnadmin password 
 
 clieck test connection ( its show success or fail for our confirmation )

 
 Note: you have exchange the keys between jenkis and master server then only test connection will success


      
# step 4:Create new maven job

create job --> maven project -->

A) Source Code Management Repository : https://github.com/veejee2331/webapplication Branches to build : */main

B) Build Root POM: pom.xml Goals and options : clean install package

C) Post steps --> Add Post buid step -- > select

select post steps --> select Send files or execute commands over SSH ( this is avaible once you insaltted publish over ssh plugin)
            update below info
	 
ssh server : name --> ansiablemaster ( automactally come bez we updated in congifg area on ealier steps)
transfer : source file--> webapp/target/*.war
Remote directory : //home//ansadmin//playbook
	
	
once again 
	
select post steps --> select Send files or execute commands over SSH ( this is avaible once you insaltted publish over ssh plugin)
update below info

ssh server : name --> ansiablemaster ( automactally come bez we updated in congifg area on ealier steps)
exec command : ansible-playbook /home/ansadmin/playbook/copyfile.yml ( just only this line) --> apply

##################################################################################  
    
 /home/ansadmin/playbook/copyfile.yml ( below you need to update on copyfile.yml)   
 
 ```
---
- hosts: all_hosts  ( what you updated on /etc/ansible/hosts file ex: [webserver] 54.167.179.56 )
  become: true
  tasks:
      - name: copy war onto tomcat
        copy:
          src: /home/ansadmin/playbook/webops/target/webapp.war
          dest: /opt/apache-tomcat-8.5.81/webapps/
  
  ```
  
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

# step5: Check the process of excution

click the build  ---> and chcek .war file created under /home/ansadmin/playbook/webapp/target location 
              and also chcek copied to /opt/apache-tomcat-####/URI/

# Step6: Test the Result

test --> http://IPADRSSS:8090/URI/
