---
title: " Porject 6: Auto Scaling for High Availability and Scalability"
collection: Projects
category: conferences
permalink: /publication/2024-02-17-paper-title-number-4
excerpt: 'This project is about Deploying Wordpress server on EC2 '
#date: 2024-10-20
venue: 'November'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2024). &quot;Paper Title Number 3.&quot; <i>GitHub Journal of Bugs</i>. 1(3).'
---

In this project, I dive into the world of Auto Scaling and Load Balancing, critical components for creating a high-performing, fault-tolerant cloud architecture. The goal was to deploy a dynamic and scalable infrastructure capable of handling varying traffic loads efficiently while ensuring high availability and cost optimization

Project Objectives
1.	Deploy an Auto Scaling Group (ASG) integrated with an Application Load Balancer (ALB).
   
3.	Install and configure the NGINX web server as the primary application server.
   
5.	Set up dynamic scaling using AWS CloudWatch alarms:
o	Scale up when CPU utilization exceeds 70%.
o	Scale down when CPU utilization falls below 30%.

7.	Design a ```fault-tolerant and scalable architecture``` using two Availability Zones (AZ) and three subnets.
   ![Profile Image](/images/t1.png)

                                 	Implementation Steps
  	
1. VPC and Networking Setup
    
The foundation of this project began with creating the Virtual Private Cloud (VPC) to establish a scalable and secure networking environment:

•	Subnets: Deployed across two Availability Zones (AZs) with three subnets (two public and one private).

•	Internet Gateway (IGW): Enabled internet access for resources in the public subnets.

•	NAT Gateway: Configured to allow instances in private subnets to access the internet securely, such as for updates and software installation.

3. Application Load Balancer (ALB)
   
To manage incoming traffic, I set up an Application Load Balancer:

•	Placement: Configured in the public subnet to route traffic to backend servers.

•	Integration: Linked with the Auto Scaling Group (ASG) to dynamically distribute traffic to healthy instances.

4.	Launch Template
   
   This project marked my first experience working with AWS Launch Templates, which streamline instance configuration:
   
5.	Defined key parameters, such as the Amazon Machine Image (AMI), instance type, and user data.
   
7.	Automated the NGINX web server installation and setup using base64-encoded user data. Here’s the script used: 
#!/bin/bash 
yum update -y 
yum install -y nginx 
systemctl start nginx 
systemctl enable nginx

Lesson Learned: Without base64 encoding, the user data script failed to execute correctly, highlighting the importance of proper formatting. 
 ![Profile Image](/images/t2.png)

4. Auto Scaling Group (ASG)
   
The ASG was configured to maintain high availability for the application:

•	Placement: Initially deployed in the public subnet (with the ALB), which caused misconfiguration issues. I later corrected it to reside in the private subnets, as the ASG manages the backend servers hosting NGINX.

•	Integration: Designed to work seamlessly with the ALB, enabling dynamic scaling based on traffic. 
 ![Profile Image](/images/t3.png)

5. CloudWatch Alarms
   
To enable dynamic scaling, I set up two CloudWatch alarms:

•	Scale Up: Triggers when CPU utilization exceeds 70%, adding one instance to the ASG
 ![Profile Image](/images/t4.png)

•	Scale Down: Triggers when CPU utilization drops below 30%, removing one instance from the ASG.
 ![Profile Image](/images/t5.png)

•	Policies: Both alarms were configured with simple scaling policies to adjust the ASG instance count dynamically.
 ![Profile Image](/images/t6.png)
  ![Profile Image](/images/t7.png)

                                          Challenges and Lessons Learned
                                          
1.	VPC Zone Identifier:
Initially, I misunderstood the vpc_zone_identifier parameter, assuming it should match the ALB in the public subnet. I later realized it is meant for the subnet, where the servers (NGINX) reside.

3.	Base64 Encoding for User Data:
The NGINX setup script wouldn’t execute without being properly base64-encoded, emphasizing the importance of formatting for instance initialization scripts.

5.	Documentation is Key:
AWS documentation proved invaluable for configuring CloudWatch alarms, scaling policies, and troubleshooting misconfigurations.

