
#   USECASE-6 (Integration AWS codecommit, AWS Pipeline and S3 )
 
  
# What you will be learn this usecase :

As part of automation , our day to day  work we will follow many methods . In AWS they provided some list of options to make our work become easy . This is a use case where we will discuss how developers will push the code to AWS and how deployment to destination  with minimal action  as part of CI/CD. 

# Architecture
![Watch the image](/aws/Usecase6/AWS-Pipeline.png)


# Steps


- Step1. Developer --> Source S3 --> codepipeline --> Destinations  s3

- Step2. Developer  --> Code commit --> code pipeline --> S3 bucket

- Step3. Developer --> code commit --> different env --> final deployment





# Step 1)  How we create pipeline s3 to  s3 ( Developer --> Source S3 --> codepipeline --> Destinations  s3 )
        
   a. Create two buckets with different names , One should be source and another one destination bucket.
        
   b. For source bucket  just enable the bucket version and the remaining will be the default setting .
        
   c. Uploaded error.html and index.html pages in source bucket as zip format.

   d. Create a destination bucket and enable public level access and version then remain as default
        
   e. Once created destination then  enable static website hosting on destination bucket and update index document --> index.html and Error document error.html

   f. Create code pipeline --> pipeline name --> remain default --> source provider  ( Amazon s3 ) --> bucket name ( source backet name ) --> S3 object key ( zip            file fullname like mywebsite.zip what we uploaded in s3) --> build stage(skip) --> 
      add deploy stage (amazon s3 & bucket name & enable extract before        deploy)--> create pipeline

   g. Go to the destination bucket and check the files and http://S3 static name/Bucket foldername

   h. If you change the code and reupload automatically rerun
   

#  step 2 )How to upload & deploy  the code use of codecommit and S3 bucket ( Developer  --> Code commit --> code pipeline --> S3 bucket )

  a. Create IAM user --> create user --> then security credential --> HTTPS Git credential for AWS code commit --> generate git credential --> download

  b. Create Ec2 instance --> create two files index.html and error.html

  c. Go to code commit in AWS gui --> create repository -> copy clone https url

  d. Back to Ec2 instance files area --> git add . --> git commit -m " " --> git remote add origin clone url --> git push origin master ( enter downloade credential )

  e. create pipeline --> default config -->source ( aws commit  , repository, branch ), Skip the build stage --> deploy (s3 bucket and name and region(ireland ),             extract before deploy , canned ACl (public-read)) --> next --> create pipeline


# step 3) Deploy the code in different environment using of code commit and code deploy (Developer --> code commit --> different env --> final deployment)

  a. Copy the project in linux server and push to aws code repository using code commit
 
  b. Cross on build.yaml file on our project

  c. Push the code to repository

  e. Code pipeline --> default configuration --> source code ( aws code commit , repo: mywebsite ,branch : master ) remain default--> build ( select code build ,            create project --> projectname: --> OS : ubuntu -->runtime stand --> img version -->env --> remain default --> continue pipeline -->next --> deploy provide: s3        and bucket name , exact before deploy -->Connect ACl(public read)--> create pipeline

  f. Add one more environment --> edit the action --> fill required details
