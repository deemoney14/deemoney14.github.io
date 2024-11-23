---
title: "Project 5:  Identity Management at StartupCo"
collection: publications
category: manuscripts
#permalink: /publication/2009-10-01-paper-title-number-1
excerpt: 'Objective: Deploy a WordPress website in a secure and scalable manner using a three-tier architecture. This setup includes a Load Balancer, Target Groups, EC2 Instances, RDS Database, VPC, and a Bastion Host, all provisioned using Terraform.'
date: 2024-10-01
venue: 'November'
#slidesurl: 'http://academicpages.github.io/files/slides1.pdf'
#paperurl: 'http://academicpages.github.io/files/paper1.pdf'
#citation: 'Your Name, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
---

Scenario:

StartupCo, a fast-growing tech startup, recently launched a fitness tracking app and has been using AWS for three months. To meet their launch deadlines, all 10 employees have been sharing the AWS root account credentials to manage cloud resources. Now that the product is live, their CTO realizes the security risks of this practice and wants to address cloud security fundamentals.

                                    Current Setup

                                  Current Infrastructure
                              
                        •	Everyone uses the root account.                          •	No separate permissions for different teams.
                        •	No MFA or password policies.                             •	AWS credentials are shared via team chat.
                        •	Infrastructure includes:                                 o	EC2 instances running the application.
                        o	S3 buckets storing user data and application assets.     o	RDS database for user information.
                         o	CloudWatch for monitoring several development and production environments.
________________________________________


Step 1: Drawing the Current Infrastructure
![Profile Image](/images/ch1.png)

Step 2: Proposed Improvements
![Profile Image](/images/ch2.png)


To address the issues and improve the current infrastructure, I implemented the following:
1. Secure Infrastructure Setup with a 3-Tier Architecture

I restructured the infrastructure into a 3-tier architecture distributed across two Availability Zones (AZs) for improved scalability, resiliency, and high availability.

•	Public Subnet: Contains an Application Load Balancer (ALB) to route traffic securely.

•	Private Subnet 1: Hosts the web server and fitness application.

•	Private Subnet 2: Hosts the RDS database.

The fitness app is now accessed exclusively through the ALB, which routes traffic to the target groups in the private subnet.

![Profile Image](/images/ch3.png)
![Profile Image](/images/ch4.png)
![Profile Image](/images/ch5.png)
![Profile Image](/images/ch6.png)
3. Secure Secrets Management
Previously, I included database credentials directly in the application code. To improve security, I implemented AWS Secrets Manager to store sensitive information securely. Credentials are decoded dynamically using:
```jsondecode(aws_secretsmanager_Secret_version.<name_your_cred>.secret_string)```
![Profile Image](/images/ch7.png)
![Profile Image](/images/ch8.png)
4. Configuring S3 and CloudWatch in the VPC
To enhance security and monitoring, I configured:
•	S3: Created an S3 bucket and an Endpoint Gateway, then connected it to the private route table via route_table_ids.
•	IAM Role for EC2: Created a policy to allow S3 and CloudWatch access. I also added an Instance Profile to EC2 with full permissions for S3.
•	CloudWatch Agent: Installed the CloudWatch agent on the EC2 instance for enhanced monitoring.
![Profile Image](/images/ch9.png)
![Profile Image](/images/ch10.png)
Step 3: Identity and Access Management (IAM)
To establish least privilege access, I created specific IAM groups and policies for each team:
Developers (4 Users)
•	Access: EC2, S3, and CloudWatch Logs (viewing only).
•	Setup: Created an aws_iam_group and used locals to streamline usernames. Attached the policy to the group based on AWS documentation.
![Profile Image](/images/ch11.png)
![Profile Image](/images/ch12.png)
![Profile Image](/images/ch13.png)
Data Analysts (3 Users)
•	Access: S3 (read-only) and database (read-only).
•	Setup: Similar process as developers, with customized policies for the analysts' needs.
![Profile Image](/images/ch14.png)
![Profile Image](/images/ch15.png)
Finance Team (1 User)
•	Access: Cost Explorer, AWS Budget, and read-only resource access.
•	Setup: Configured policies for cost management. Finding the correct read-only policies required additional research due to limited documentation.
![Profile Image](/images/ch16.png)
![Profile Image](/images/ch17.png)
Operations Team (2 Users)
•	Access: Full permissions for EC2, CloudWatch, Systems Manager, and RDS.
•	Setup: Attached full permissions directly to the iam_group_policy_attachment for simplicity.
![Profile Image](/images/ch18.png)
![Profile Image](/images/ch19.png)
MFA and Strong Password Policies
Finally, I enforced MFA for all users and implemented a strong password policy:
•	Passwords must be renewed every 90 days.
•	Strict password requirements ensure enhanced account security.
![Profile Image](/images/ch20.png)
![Profile Image](/images/ch21.png)
Reflection and Learning Outcomes
This project allowed me to explore key AWS identity management and security practices:
1.	IAM Best Practices: Implementing least privilege access and group policies based on team roles.
2.	Secrets Management: Securely managing credentials with AWS Secrets Manager.
3.	Infrastructure Design: Configuring a gateway for S3 access and integrating CloudWatch for enhanced monitoring.
4.	Password and MFA Policies: Strengthening account security with robust policies.
This hands-on experience reinforced the importance of secure identity management and highlighted the need to familiarize myself with IAM tools and configurations for future projects.
