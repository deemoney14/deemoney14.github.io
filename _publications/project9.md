---
title: "Project 9: Fixing Tech Health Inc. Infrastructure"
collection: publications
category: manuscripts
permalink: /publication/2015-08-01-paper-title-number-3
excerpt: ''
date: 2025-10-01
venue: 'January'
#slidesurl: 'http://academicpages.github.io/files/slides3.pdf'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2015). &quot;Paper Title Number 3.&quot; <i>Journal 1</i>. 1(3).'
---

Tech Health Inc. has been managing its infrastructure manually through the AWS Console for over five years. The goal of this project is to modernize their infrastructure by migrating it to Infrastructure as Code (IaC), allowing for better scalability, automation, and consistency. ![Profile Image](/images/oo1.png)

                                       Key Tasks and Solutions:

•	VPC Setup: I created a Virtual Private Cloud (VPC) with two Availability Zones (AZs) and four subnets – two public and two private. The EC2 instances were placed in the public subnets, and the RDS instances were placed in the private subnets.  ![Profile Image](/images/oo2.png)


•	Security Groups & Network Isolation: I ensured that the EC2 instances and RDS databases are isolated in different subnets, with security groups configured to allow only necessary access. This setup follows best practices of least privilege.

•	Cost Considerations: I chose t2.micro for the EC2 instance (eligible for the AWS free tier) and db.t3.micro for RDS (to keep costs low). 
 ![Profile Image](/images/oo3.png)
  ![Profile Image](/images/oo4.png)

o	Avoided using NAT Gateways as a cost-saving measure.
o	Made sure to destroy resources after testing to avoid unnecessary charges.

                                          AWS Best Practices Implemented:
                                          
```•	Network Design:``` I ensured proper segregation of public and private subnets, with sensitive resources like RDS placed in the private subnet.

•	Security:
o	No direct public access to the RDS database.
o	Restricted EC2 SSH access to my IP for secure access.
o	Stored database credentials securely using AWS Secrets Manager.
o	Used security groups instead of NACLs for more granular control over network traffic. 
 ![Profile Image](/images/oo5.png)
  ![Profile Image](/images/oo6.png)

IAM Roles & Policies: I set up IAM roles for the EC2 instances to interact with RDS and Secrets Manager. I also created policies to allow the EC2 instances to retrieve database credentials from Secrets Manager, and ensured that the IAM instance profile was correctly attached to the EC2 instance for permission management. 
 ![Profile Image](/images/oo7.png)

                                                            Lessons Learned:
                                                            
```•	Modularization:``` Setting up infrastructure with modules greatly simplified the process. By reusing modules for components like VPC, EC2, and RDS, I can easily manage and scale the infrastructure as needed.
```•	Security Focus:``` It’s crucial to limit access and follow the principle of least privilege when configuring security groups and IAM roles.
```•	Cost Management:``` Opting for the smallest EC2 and RDS instances (t2.micro and db.t3.micro) helped keep costs low while still providing the necessary resources for the patient portal.
```•	Automation:``` IaC allows for more consistent and repeatable deployments. The infrastructure can be destroyed and recreated easily, ensuring a clean environment for testing and deployment.
 ![Profile Image](/images/oo8.png)
  ![Profile Image](/images/oo9.png)





