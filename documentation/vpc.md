# Create a Virtual Private Cloud Network with AWS VPC
-	AWS VPC is used to create a Virtual Private Cloud which is essentially an isolated slice of AWS’ own servers. This cloud is a network that can house AWS services/objects such as Elastic Compute Cloud (EC2) instances.
-	This is a key service that I will use to establish networking for my cloud environment.

### 1.	Assign the new VPC to an IPv4 CIDR block.
a.	x/16 size block allowing 65,536 IPs.
### 2.	Assign Availability Zones (AZs).
a.	Set up two AZs in us-east-1a and 1b for modest availability in case one zone goes down.
### 3.	Set up Custom Public and Private Subnets and CIDR Blocks
a.	Created two public and two private subnets with 256 IPs each at x/24 size blocks.<img width="975" height="189" alt="image" src="https://github.com/user-attachments/assets/2d59f8a2-ef44-417d-88c9-482e4579774f" />

### 4.	Enabled DNS hostnames and resolution to allow discovery via hostnames rather than strictly IP addresses.
### 5.	Enabled VPC endpoints via S3 Gateway.
a.	This allows my VPC to privately connect to services like S3 with no extra charge.
### 6.	Configured a network access control list (NACL)
a.	AWS NACLs are stateless, meaning that they do not retain connection details about traffic. Because of this, explicit inbound and outbound rules are needed.

b.	Explicitly allows inbound SSH (port 22), ephemeral return traffic (ports 1024 – 65535) from my home network, and HTTPS (port 443) from my VPC network. Explicitly allows all outbound traffic from the VPC. <img width="975" height="278" alt="image" src="https://github.com/user-attachments/assets/2c98ec20-3c44-4088-9064-8e3316d71994" /> <img width="975" height="167" alt="image" src="https://github.com/user-attachments/assets/7d0bf859-c4a1-4f3a-988b-f6aeeec5c43d" />

    

c.	Stateless NACLs need an inbound allow for ports 1024-65535 (known as ephemeral ports) because they allow response traffic from services such as HTTPS.
### 7.	Create Granular VPC Endpoints to Communicate with Core AWS Systems Manager (SSM) Services
a.	This allows my EC2 instance to communicate with services that are necessary for AWS SSM to function. AWS SSM is the most secure method to connect to an EC2 instance and also allows for a variety of other features.

b.	Enabled private DNS names for the endpoints so all traffic destined for SSM stay within the VPC.
