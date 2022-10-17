# Jenkins Installation 

# Steps

 -  step1: Check the basic and requirments
 -  step2: Check the java version 
 -  step3: Install the jenkins
 -  step4: Login to Jenkins and update password 


# step1: Check the basic and requirments


  Go to jenkins website  ``` https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos ```

#  step2: Check the java version

 Install java version
 
 ``` yum install java-1.8* ```

 Check the java version 
```
 java -version
 ```
 - To chcek the JDK path
 ```
 find / -name javac
 ``` 
# Update the Jave home path
 ```
 cd
 ```
``` vi .bash_profile ```
 
 ```
 JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64

PATH=$PATH:$JAVA_HOME:$HOME/bin
 
 ```

# step3: Install the jenkins

```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
```
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```
```
sudo yum upgrade
```
- Install JDK 
```
sudo yum install java-11-openjdk
```
```
sudo yum install jenkins
```
```
sudo systemctl daemon-reload
```
# Start the jenkins

You can enable the Jenkins service to start at boot with the command:
```
sudo systemctl enable jenkins
```

You can start the Jenkins service with the command:
```
sudo systemctl start jenkins
```
You can check the status of the Jenkins service using the command:
```
sudo systemctl status jenkins
```
# Step 4. Login to jenkins console using of basic password and update plugins

http://publicIP:8080

- Note : please make sure open the port on fireware level on respective cloud levels

- Change the password 

admin --> configure --> change the password --> then relogin

-  update the Java path 

click manage jenkins --> click Gobal tool configuration --> jdk 



Name: Jdk 

Path : /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.2.x86_64


