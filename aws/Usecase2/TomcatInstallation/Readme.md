# Tomcat Installation 
# Steps
- step1: Check the Java version
- step2 : Download the tomcat software
- step3: update the correct permission to install
- step4: Create Softlinks 
- step5:  How to access the tomcat 
- Step6: Change the Port number
- step7: How to Access the webapp dirctory 
# step1: Check the Java version

```
java -version
```
- If its not installed 
```
yum install java-1.8*  or yum install java-11*
```
```
cd
```
- UPDATE BELOW LINES
```
vi .bash_profile
```
```
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64
```
```
PATH=$PATH:$JAVA_HOME:$HOME/bin
```
- Then test it 
```
echo $PATH
```
# step2 : Download the tomcat software

- Goto Tomcat main website 

```
https://tomcat.apache.org/download-90.cgi
```
```
mkdir /opt/
```
```
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
```
```
tar -xvzf /opt/apache-tomcat-<version>.tar.gz
```
# step3: Update correct permission to install

```
chmod +x /opt/apache-tomcat-<version>/bin/startup.sh 
chmod +x /opt/apache-tomcat-<version>/bin/shutdown.sh
```
# step4: Create softlinks

- create link files for tomcat startup.sh and shutdown.sh 
   ```
   ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
   ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown
   
   ```
- Run the tomcat ```tomcatup```

# Step5: Access the Tomcat 
- access tomcat application from browser on port 8080  
 ``` http://<Public_IP>:8080 ```
- Note : Please open the firewall rules before try it 
# step6: Change the Port Number

- Using unique ports for each application is a best practice in an environment. But tomcat and Jenkins runs on ports number 8080. Hence lets change tomcat port number to 8090. Change port number in conf/server.xml file under tomcat home
   
 - cd /opt/apache-tomcat-<version>/conf
-  update port number in the "connecter port" field in server.xml
-  restart tomcat after configuration update
```
tomcatdown
tomcatup
```
#### Check point :
Access tomcat application from browser on port 8090  
 - http://<Public_IP>:8090
  
 # step7: How to Access the webapp directory 
  
  now application is accessible on port 8090. but tomcat application doesnt allow to login from browser. changing a default parameter in context.xml does address this issue
   
   search for context.xml
  ```
   find / -name context.xml
   ```
above command gives 3 context.xml files. comment``` (<!-- & -->)```  `Value ClassName` field on files which are under webapp directory. 
After that restart tomcat services to effect these changes. 
At the time of writing this lecture below 2 files are updated. 
   ```sh 
   /opt/tomcat/webapps/host-manager/META-INF/context.xml
   /opt/tomcat/webapps/manager/META-INF/context.xml
  ```
  
  Update users information in the tomcat-users.xml file
goto tomcat home directory and Add below users to conf/tomcat-users.xml file
   ```sh
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="s3ven" roles="manager-gui"/>
  
  ```
  - Restart serivce and try to login to tomcat application from the browser. This time it should be Successful
  
