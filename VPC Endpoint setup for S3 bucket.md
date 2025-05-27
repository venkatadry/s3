https://medium.com/@cse.20bcsd64/vpc-endpoint-setup-for-s3-bucket-b366a9ec0ec0

https://www.youtube.com/watch?v=i7aIsvch1y8&t=1s

![image](https://github.com/user-attachments/assets/100b2f30-034d-4585-8613-cef2be64f411)


In Case of private subnet it is not able to connect to s3 as it doesnt have internet access

![image](https://github.com/user-attachments/assets/706a2ce8-5f27-4238-aa56-e8ee6d25b780)


so we create VPC endpoint for private subnet to communicate to s3

![image](https://github.com/user-attachments/assets/8e887f1c-2103-47df-b602-9fb32ce32ade)

**S3 VPC endpoint**
A VPC endpoint for S3 will allow private IP addresses to access Amazon S3 with no exposure to the public internet.
By Default, VPC endpoint will allow access by any user or service within the VPC
Using route tables, we can enable access control for aws resources to access S3 via endpoints
S3 bucket and endpoint should be within the same regions.
There is limit to create endpoint gateway per vpc. (20 by default & 255 max)

**Accessing S3 bucket from public & Private subnet EC2**
Create VPC
Create Public & Private Subnet
VPC: 10.0.0.0/16
Public Subnet:
10.0.1.0/24
Private Subnet
10.0.0.0/24
Create IGW
Create Route table for private & Public
Create S3 Bucket policy and attach IAM role to EC2
Create EC2 End point for private subnet

IGW
![image](https://github.com/user-attachments/assets/5ce36e18-485e-4d38-b81d-01c76c25c07b)


public rt

![image](https://github.com/user-attachments/assets/3dbeded2-bde8-45a7-a17c-7e79eb06c011)

public-sg
![image](https://github.com/user-attachments/assets/7cfd263c-35ad-49ee-9108-45006db6212c)


private-rt
![image](https://github.com/user-attachments/assets/3088d354-d2db-4add-b175-e6e148ae9e09)

private-sg
![image](https://github.com/user-attachments/assets/4831be9d-7032-4698-bf07-320f30f997fe)

From public ec2 able to login ro private ec2

```[ec2-user@ip-10-0-1-67 ~]$ hostname
ip-10-0-1-67.ec2.internal
[ec2-user@ip-10-0-1-67 ~]$
[ec2-user@ip-10-0-1-67 ~]$
[ec2-user@ip-10-0-1-67 ~]$ ssh -i "ec2-pem.pem" ec2-user@10.0.0.33
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Tue May 27 04:07:39 2025 from 10.0.1.67
[ec2-user@ip-10-0-0-33 ~]$ ```



**we attach IGW to vpc .The route tables make it effect**

Connect to ec2 in provate subnet https://medium.com/@amitmavgupta/aws-accessing-an-ec2-instance-in-a-private-subnet-using-endpoints-787891e6e788

https://medium.com/@hobballah.yasser/secure-access-to-private-ec2-instance-in-private-subnet-methods-and-best-practices-d4ee75a506d3#7809



