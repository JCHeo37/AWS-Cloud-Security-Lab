# AWS Cloud Lab Documentation

The cloud half of my overall 2 endpoint SOC homelab. The infrastructure consists of services such as EC2, VPC, S3, CloudTrail, CloudWatch, and IAM that will be connected to the VMWare portion of my homelab. 


## Overview
A security-focused AWS homelab built to practice cloud identity security,
network segmentation, EC2 hardening, audit logging, alerting, and cost governance.
The environment supports cloud-security and incident-response exercises using
AWS CloudTrail, S3, CloudWatch, SNS, and local SIEM monitoring. 

As mentioned, this lab is a part of a greater whole that will combine 2 endpoints (a powerful desktop running VMWare Workstation Pro and a laptop serving as a cloud agent and attacker) and a carefully thoughtout tech stack.


## Objectives
- Apply least-privilege IAM and MFA protections
- Build a segmented VPC and securely administer an EC2 workload
- Centralize AWS API audit logs with CloudTrail and S3
- Configure monitoring and notifications with CloudWatch and SNS
- Control laboratory spending with AWS Budgets
- Investigate simulated cloud security events
## Architecture
[IN PROGRESS]
## AWS Services Used
| Service | Purpose |
|---|---|
| IAM | Administrative access, least-privilege policies, roles, MFA |
| VPC | Isolated cloud network, routing, security groups |
| EC2 | Linux cloud test workload |
| S3 | Private CloudTrail log storage |
| CloudTrail | AWS API activity logging and investigation evidence |
| CloudWatch | Metrics, logs, and alarms |
| SNS | Security and budget notifications |
| AWS Budgets | Cost threshold alerts |
## Security Controls Implemented
- MFA enabled for privileged account access
- Root account not used for daily administration
- Separate identities/roles for administration, workloads, and log collection
- SSM Session Manager preferred over publicly exposed SSH
- SSH restricted to an approved source IP when used as a fallback
- Private, encrypted S3 log storage with Block Public Access enabled
- CloudTrail enabled to preserve API audit evidence
- Budget and alert thresholds configured to reduce unexpected charges
## Detection Scenario
### IAM privilege-change investigation
1. Generate an authorized test IAM policy attachment or removal event.
2. Confirm the event is recorded in CloudTrail.
3. Review the event principal, source IP, API name, affected resource, and timestamp.
4. Determine whether the activity was expected.
5. Document containment and remediation actions.

### Evidence
[IN PROGRESS]
## Lessons Learned
- Why SSM reduces remote-access exposure compared with open SSH
- How CloudTrail supports attribution and incident timelines
- Why separate IAM identities improve accountability
- How budget alerts support secure, sustainable cloud-lab operations
- What services are necessary for restricted accounts limited by an MFAFalseDenyAll policy
- How Security Groups and Network Access Control Lists (NACLs) inbound/outbound rules impact services such as AWS Sessions Manager (SSM). 
## Future Improvements
- Forward CloudTrail events to Wazuh for centralized investigation
- Add a private subnet and restricted workload
- Add VPC Flow Logs after reviewing cost implications
- Build the environment with Terraform
- Add GuardDuty/Security Hub detection exercises with budget controls
## Resources Used

 - [AWS Documentation](https://docs.aws.amazon.com/)
 - Amazon Q AI for service knowledge and troubleshooting
 - Perplexity AI for implementation guidance and context
