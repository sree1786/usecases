#   USECASE-8(Deployment Types - Hot Deployment,Rolling Deployment, Blue-Green Deployment )
 
 Please watch Usecase-7  before come here
 
# What you will be learn this usecase :

Application Deployment, also known as Software Deployment, is the process of installing, configuring, updating, and enabling one application or suite of applications that make a software system available for use, like facilitating a certain URL on a server.

This usecase we are going to discuss different types of deployments , How its work and also Whats are difference for each deployment type.

# Architecture
![Watch the image](/aws/Usecase8/Deployment.png)

# Steps

 -  step1: Create the server
 -  step2: convert server to image
 -  step3: create load balancer
 -  step4: change target group settings
 -  step5: create auto scaling &  launch configuarion
 -  step6: create deployment group
 -  step7: Update the pipeline
 -  step8: Hot deployment 
 -  step9: Rolling deployment
 -  step10: Checking functionality of  rolling deployment.
 -  step11: Blue-Green Deployment 


# step1: Create the server

  Please chcek usecase-7 
 Just watch ealier use case ( https://github.com/cloudnloud/usecases/tree/main/aws/Usecase7 )
  
 

#  step2: convert server to image

  a. stop the server
  
  b. action --> image and template -->create image 
	 image name ( deployment-image ) --> no reboot enable --> create image (remaindefault)
	
  c. go to ami and chcek the image 

# step3: create load balancer

create loadbalncer -->application loadbalncer --> create --> name(deploy-loadbalncer) --> select minimum two regions --> select security group --> select target group ( if you not created please use default config and create)--> create loadbalncer

      
# step 4:change target group settings

loadbalncer --> target groups --> target group name --> attributes --> edit -->
	update 60 sec --> save changes

# step5: create auto scaling &  launch configuarion.

Launch configuarion:
	
Launch configuarion --> create launch configuration -->name --> select AMI --> choose basic instance type (t2 micro)--> select security group ( this security group we careated ealier you have select stick always one SG) 
		-->key pair -->create launch configuarion
		
Once launch configuration completed then we can create security group
	
Autoscaling group :
		
  Autoscaling group --> auto scaling group name --> select launch template -->next --> default vpc --> select AZ all three --> attached loadbalncer --> select loadbalncer -->select ELB --> 1500 sec --> select -->desired/min/max =2 --> remain default --> create autoscaling group 
		
Once auto scaling creation completed . its will automatclly create 2 ec2 instance

# step6: create deployment group

create code pipeline --> deploy --> application --> create deployment group -->  name --> role --> select in-place --> select EC2autoscaling -->  deployment setting select all at time --> select loadbalncer --> create deployment group

# step7: Update the pipeline ( if you are not create then create new pipleine already discussed ealier usecase)
  
  Edit pipeline --> update deploy area --> save
	then release the pipeline 
 # step8: Hot deployment
  
  modify the code and reploy using of code commit 
	git add .
	git commit -m "hot deploy"
	git push origin master
# step9: Rolling deployment
  
  a. edit the autoscale deployment capacity from 2 to 3.
	b. Go to deployment group --> deployment setting --> deplymentoneatatime -->  unchcek disable rollback --> save 
	c. change the code and repush 
	
you are oberved changed will happen one after another servers
# step10: update the code wrongly and check the functionality of rolling deployment.
  
  code pipeline --> deployment --> deployment history 
	once deployment failed automatically rollback old version but application level nothing impacted
  
# step11: Blue-Green Deployment 
  
  application --> deployment group --> edit --> deployment type --> blue/green --> deployment setting --> traffic rerouting (reroute traffic immeditally) & (terrimate the original instance in deployment group) --> deployment configuration (code deployment at a time) --> save

Update the code and redeploy 
	
Then automically number of double number of instance will created then slowly count will comeback normal.
