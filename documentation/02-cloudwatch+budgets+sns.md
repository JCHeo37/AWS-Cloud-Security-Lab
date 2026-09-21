# Setting Up Billing and Free Tier Usage Alerts via SNS and CloudWatch + AWS Budgets
-	Since my AWS account is on a limited Free Tier, this section is important to ensure that my billing doesn’t cross a certain threshold.

### 1.	Enable IAM user access to Billing and Cost management console pages.
a.	By default, only the root user can access the Billing and Cost Management Console. Since I plan on doing most of my AWS setup on a privileged IAM admin user rather than the root, this setting must be enabled.

b.	The LabAdmins group created above already allows full billing access, but for the sake of granularity, I also created a specific IAM role that requires associate users to have MFA enabled to access the billing console. <img width="573" height="441" alt="image" src="https://github.com/user-attachments/assets/276134ae-b765-4fa9-8579-a5479c2b0021" />
 
### 2.	Allow CloudWatch to send billing alerts and free tier usage alerts through the AWS Billing and Cost Management console.
a.	Billing alerts act as a safety net for when my free tier usage exceeds a spending threshold (in this case, $0).

b.	Free Tier alerts notifies my email when my resource usage gets close to its monthly cap for each service (in this case, 85%).
### 3.	Create an AWS Simple Notification Service (SNS) topic and subscription so my email gets notified when a billing alert is triggered.
### 4.	Create an AWS CloudWatch billing alarm, connecting my AWS SNS topic and subscription.
a.	CloudWatch metrics and alarms can also be viewed on the AWS mobile app.
### 5.	Configure a basic budget in the account settings to email me when spending exceeds $50.00 and $75.00.
a.	Using AWS Budgets, I set up recurring budget tracking to daily on all AWS services for the account. I also configured the alert threshold to 100% and 150%, which will notify my email if spending exceeds $50 and then $75.
