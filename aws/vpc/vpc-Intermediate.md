## VPC-Intermediate-UseCases

** What is AWS VPC in simple words? **
A virtual private cloud (VPC) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can launch your AWS resources, such as Amazon EC2 instances, into your VPC.


## Use Case 1 : VPC CReation along with restricted webserver environment

Create VPC and Should acheve the following

1. Public Subnet Should be there
2. Private subnet should be there
3. Deploy bastion host in public subnet
4. Deploy Webserver in private subnet
5. Deploy Nat gateway in VPC
6. From private server (web server)  need to access internet
7. Private webserver shouldnt be accessiable from direct internet

