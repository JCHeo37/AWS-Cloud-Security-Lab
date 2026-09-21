# Configuring Security Controls, Policies, and Least Privilege with AWS Identity and Access Management (IAM)
## Password Policy and IAM Admin Account
-	An AWS best practice for root user accounts is to create an administrative user for everyday tasks. This is because the AWS root user account has unlimited permissions and access, so using a privileged Identity and Access Management (IAM) account limits the threat scope and introduces least privilege concepts.
-	(https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-best-practices.html)


### 1.	Enable Multi-Factor Authentication (MFA) on root account.

a.	Used Microsoft Mobile Authenticator which is locked with a PIN code.

b.	Root credentials are also locked behind a password vault.

### 2.	Ensure no root user access keys exist.
a.	The root user in AWS has built-in, full ownership of an AWS account. As a result, its permissions cannot be limited by design. Because of this, it is unwise to create programmatic root access keys that may be compromised.

b.	Safer alternatives include using temporary credentials or creating another IAM user with least privilege permissions.

c.	<img width="617" height="232" alt="image" src="https://github.com/user-attachments/assets/8ca26f3f-120d-4f09-b1bb-6e646e60729d" />
 
### 3.	Create an IAM policy to allow a given user to view and edit password policies.
a.	Custom password policies do not apply to the root user.

b.	Added a condition to this policy that requires associated users to be multi-factor authenticated. Here is the JSON for the full policy: <img width="629" height="486" alt="image" src="https://github.com/user-attachments/assets/63f76e83-63a3-4d00-9ddc-a0d21d421466" />

### 4.	Create an IAM group for admin users and attached the “AdministratorAccess” and “MFAFalseDenyAll” policies to the group.
a.	The “AdministratorAccess” policy is AWS-managed and created.

b.	Managing permissions at the group level rather than the user level is a best practice because this allows for scalable access control and auditing.

c.	Also created a policy “MFAFalseDenyAll” to force MFA for all admins. This policy uses an explicit deny for all services excluding those necessary for credential/MFA setup to avoid an account deadlock in the event of missing MFA: <img width="674" height="459" alt="image" src="https://github.com/user-attachments/assets/33489cdf-18c6-43a0-a62a-47819e6b156b" />

  
### 5.	Create a privileged IAM user for everyday admin tasks and setup.
a.	Added the “Flash-Admin” user to the “LabAdmins” group. Enabled console access for the user.

b.	Created a strong console password and enabled MFA.
### 6.	Updated the password policy with custom requirements through the IAM account settings.
a.	By default, AWS enforces min. 8 characters/max 128 characters, min. of three of the mix of character types (upper, lower, special, number), not identical to account name/email, and non-expiring passwords.

b.	My custom requirements now enforce the use of all four character types, expiration in 180 days, an administrator reset requirement, and prevention of password reuse from the last change.  <img width="773" height="347" alt="image" src="https://github.com/user-attachments/assets/48df5e7a-48bb-4e1d-b775-406457b41022" />


