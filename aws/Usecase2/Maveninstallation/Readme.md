# Maven Installation 

# Steps
- step1 : Create directory 
- step2: download the software
- step3 : Unzip the software
- step4: update require configuration

# step1 : Create directory 
```
mkdir -p /opt/maven
```
```
cd /opt/maven/
```
- Please chcek the latest software 
```
https://maven.apache.org/download.cgi
```
# step2: download the software

```
wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
```
```
ls
```

# step3 : Unzip the software
```
tar -xvzf apache-maven-3.8.6-bin.tar.gz
```
```
cd apache-maven-3.8.6/
```
# step4: update require configuration

```
cd
```
```
vi .bash_profile
```
- UPDATE highlated lines in .bash_profile


if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi



JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.161-0.b14.el7_4.x86_64

𝐌𝟐_𝐇𝐎𝐌𝐄=/𝐨𝐩𝐭/𝐦𝐚𝐯𝐞𝐧/𝐚𝐩𝐚𝐜𝐡𝐞-𝐦𝐚𝐯𝐞𝐧-𝟑.𝟖.𝟔   
𝐌𝟐=$𝐌𝟐_𝐇𝐎𝐌𝐄/𝐛𝐢𝐧

PATH=$PATH:$JAVA_HOME:$𝐌𝟐_𝐇𝐎𝐌𝐄:$𝐌𝟐:$HOME/bin


export PATH

- test the configuation 

```
echo $PATH
```

- you can able to maven and jenkins paths

- Update maven details  in Jenkins 

manage jenkins --> global tool configuration --> maven 
  given name : maven and path : /opt/maven/apache-maven-3.8.6
 
 - If git not install please install git also
 
 ```
 yum install git -y
 ```
  


