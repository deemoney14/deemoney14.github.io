---
title: "Project 3: Creating a Fault-Tolerant EC2 Server Across AWS Regions"
collection: publications
category: manuscripts
permalink: /publication/2010-10-01-paper-title-number-2
excerpt: 'This paper is about the number 2. The number 3 is left for future work.'
date: 2024-10-01
venue: 'October'
#slidesurl: 'http://academicpages.github.io/files/slides2.pdf'
#paperurl: 'http://academicpages.github.io/files/paper2.pdf'
#citation: 'Your Name, You. (2010). &quot;Paper Title Number 2.&quot; <i>Journal 1</i>. 1(2).'
---

The goal of this project was to create an EC2 server using a user data script and replicate its AMI in a different region for fault tolerance, ensuring that if one region experiences issues, the other remains unaffected.

I started by setting up a standard VPC template from scratch. I’m finding it easier to type configurations myself rather than relying on documentation, especially with steps like setting ```map_public_ip_on_launch``` for my public subnets—a step I sometimes overlook, leading to no public access.

For secure access to the instance, I decided to create my own key pair with the command: ```ssh-keygen -t rsa -b 2048 -f <key-name>```

This provided both my public and private keys, essential for SSH access to the instance. With the security group configured and Terraform initialized, planned, and applied, my first web server was up and running. However, I couldn’t access it over the web. I double-checked everything—route tables, internet gateway (IGW), and security group rules—but still no luck. I could SSH in and ping external sites, so internet connectivity was active.

After reaching out to “Toku” for advice, I decided to destroy the instance and start fresh. This time, I realized the issue was with the user data script, which hadn’t initialized on the previous instance. Once I restarted, everything worked as expected.

Next, I tackled the AMI replication. Copying the AMI to a different region in the console was straightforward, and deploying it in us-east-1a using Terraform became simpler once I learned to use an alias to distinguish between us-west and us-east. Using ```aws_ami_copy,`` I created a snapshot in us-east. To reference the default VPC and subnet, I used data ```aws_vpc```and data ```aws_subnet``` with filters for the specific AZ, which helped me refine the target setup.

Finally, I replaced the AMI in my EC2 configuration with the copy from us-west-1, verifying that the user data script ran and displayed the expected content in the new instance.

Once confirmed, I used ``` terraform destroy``` to clean up and save on costs.

