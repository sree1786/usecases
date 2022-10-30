
#   USECASE-7 (Integration AWS codecommit, AWS codedeploy and Ec2 )
 
  
# What you will be learn this usecase :

we will discuss what is code deploy and how its work . Use of code deployment how to deploy angular project to EC2 instance . How access that application externely .

# Architecture
![Watch the image](/aws/Usecase6/AWS-Pipeline.png)

# What is code deploy
 CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS  services.

# Steps


- Step1. Create IAM Role

- Step2. Create Ec2 instance using of IAM Role

- Step3. insatlled codedeploy agent

- step4. Installation Nginx in EC2 server

- Step5. Deploy code using of codedeploy to EC2 

- step6: Create the repository in codecommit and push the content

- step 7: create application in codedeploy area

- Step 8: Create Pipeline for EC2 instance 


# Step 1 :  Create IAM Role
        
   Search IAM --> Roles --> Create Role --> click AWS service & Use case Ec2 --> permission policies (code deploy) --> select AmazonEC2RoleforAWSCodeDeploy  --> Next -->Role Details ( Rolename) --> Create Role 
        

#  step 2 : Create Ec2 instance using of IAM Role

 Serach Ec2 --> Launch instance --> instance name  --> OS --> default remaining --> select create IAM --> create instance  

# step 3. insatlled codedeploy agent

  ```
sudo yum update -y

sudo yum install -y ruby wget

wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install

chmod +x ./install

sudo ./install auto

```

# Checking CodeDeploy Agent status
```
sudo service codedeploy-agent status
```
#step4. Installation Nginx in EC2 server

Installing Nginx
```
sudo amazon-linux-extras install -y nginx1
```
Checking Nginx status
```
sudo service nginx status
```
Starting Nginx
```
sudo service nginx start
```
Enabling Nginx to restart on system reboot
```
sudo chkconfig nginx on
```
Creating folders for deployments
```
sudo mkdir -p /var/www/my-angular-project
```
Changing Nginx configuration
```
sudo nano /etc/nginx/nginx.conf
```

Only change root to /var/www/my-angular-project
 
Press `Ctrl + X` to exit, press `Y` to save and press `Enter` to approve.


Restart Nginx
```
sudo service nginx restart
```

#step5: Deploy code using of codedeploy to EC2 

copy the code ec2 instance and untar the files .

Please find attachment of code my-angular-project-final2.zip

# step6: Create the repository in codecommit and push the content

Updater the conetnet and push to code commit respoitory ( i have already expalin on my ealier video how to do it )

# step 7: create application in codedeploy area

Search code deploy --> select application --> create application --> Give application name & select Ec2/on-premises --> create application 
create deployment group --> select name --> create IAM role like below and select --> env configuration (EC2 instance) --> unchcek load balance --> Create deployment Group

Create IAM for deployment group --> serach IAM --> role --> code deploy --> select just code deploy --> permission policy (AWSCODEDEPLOYROLE)--> next --> role name -->create role 


# Step 8: Create Pipeline for EC2 instance 

Search Pipeline --> pipelinename -->default -->Source ( code commit ) --> repository name --> branch name (master) --> next --> build (code build)--> create project --> projectname --> Os(ubuntu)--> runtime(std) --> latest image --> remain default -->next  --> deploy -->aws code deploy--> select application name --> deployment group -->create  

# step 9 : testing 
