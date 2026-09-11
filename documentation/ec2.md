# Configuring a Testing Environment with AWS EC2
-	AWS Elastic Compute Cloud is a primary service that allows the creation of VMs and instances using Amazon’s cloud resources. 
-	This is key for creating a cloud working environment which I can use to test security groups and web app testing through AWS.

  ### 1.	Launch an EC2 test instance.
o	OS: Amazon Linux

o	Amazon Machine Image (AMI): Amazon Linux 2023 kernel-6.18 AMI

o	Architecture: x86

o	Instance Type: t3.micro (2 vCPU, 1 GiB Memory)
### 2.	Create an RSA key pair to securely login to the EC2 test instance.
a.	A private key is securely stored on my device to login.
### 3.	Configure Networking + Security Groups for the VPC
a.	Created a secure public subnet for the instance to ensure that the testing environment is safe.

b.	Unlike NACLs, Security Groups (SGs) are stateful, meaning that they track traffic/connection context.

c.	Configured a Security Group (acts as a firewall for the instance level) to allow all outbound traffic and SSH inbound traffic from my IP. Also allowed inbound HTTPS from within the VPC to enable SSM Session Manager capabilities.

d.	Pairing SGs with NACLs is a strong security practice that employs layered defense.  <img width="922" height="672" alt="image" src="https://github.com/user-attachments/assets/30e7aa16-0a83-4e68-9382-d3a0defa21b5" />

### 4.	Configure Elastic Block Storage (EBS)
a.	An AWS EBS volume functions like a virtual hard drive. 

b.	This instance is running on a general-purpose SSD with 30GiB.

c.	Enabled EBS encryption by default using an AWS managed key as the master key.
### 5.	Configure Backups Using AWS Data Lifecycle Manager (AWS DLM)
a.	Created a policy that takes a snapshot of EBS volumes every 7 days that also expires in 7 days.

b.	Created a policy that takes a snapshot of AMIs and attached EC2/EBS resources every 7 days that also expires in 7 days.
### 6.	Attach an IAM Role to the Instance + Enable SSM Session Manager
a.	Created and attached a limited IAM role to the instance that enables features such as SSM access and security focused capabilities.

b.	The alternative to using an SSM-enabled IAM role is to enable the account level Dynamic Host Management Configuration, which automatically treats all EC2 instances on a given account as managed nodes. I opted for a least privilege style approach and created a limited role.
### 7.	Blocked Public Access and Sharing for AMIs and EBS Snapshots.
### 8.	Test SSM Access to EC2 Instance
a.	After some arduous troubleshooting, I was finally able to securely connect to my instance via SSM <img width="975" height="167" alt="image" src="https://github.com/user-attachments/assets/cafc1aa3-3e87-4f69-96ef-d9137bfed0c1" />

b.	Installed the AWS CLI v2 to laptop endpoint <img width="378" height="89" alt="image" src="https://github.com/user-attachments/assets/a1a35199-61a0-4697-af37-4fd6272e8830" />

9.	EVENTUALLY: Launch a replacement instance with autoassigned IP enabled

