---
title: "Project 1: Deploying WordPress on EC2 Using Terraform"
collection: Projects
category: conferences
permalink: /publication/2024-02-17-paper-title-number-4
excerpt: 'This project is about Deploying Wordpress server on EC2 '
#date: 2024-10-20
venue: 'October'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2024). &quot;Paper Title Number 3.&quot; <i>GitHub Journal of Bugs</i>. 1(3).'
---

This is my first official project outside of class, inspired by online research. I decided to start with something that seemed simple—deploying WordPress on an EC2 instance. Sure, I could have done it easily via the AWS console, but where's the fun in that? Instead, I chose to use a cloud-agnostic tool called Terraform (oooo, scaryyyyy!).


My plan was to create an EC2 instance with an attached security group, use a user-data script to install WordPress, and deploy everything within the default VPC in the US-West-1 region. it sounded simple enough in my head.

The first hurdle came when I discovered I had accidentally deleted my default VPC.  I could have switched to another region, but where’s the fun in that? Instead, I decided to create a new VPC from scratch. I set up the VPC with one subnet, one  (AZ), an (IGW), and the necessary route tables and associations. The Terraform documentation was key to getting this done.
![Profile Image](/images/Picture1.png)
 
With the VPC set up, it was time to provision my EC2 instance. This part was trickier than expected because I couldn’t find the user-data script to install WordPress. Thank you, ChatGPT! I finally got the script and also learned a neat trick: outputting the instance IP address directly in Terraform using:``` output "instance_ip" {
  value = aws_instance.web.public_ip
}```

This little trick saved me from hunting through the console for the IP address. My naming conventions still need some work, but I’m sure that will improve over time.
 ![Profile Image](/images/Picture2.png)

Last part was supposed to be the easiest, but I struggled only because I had too many documentation options. I think was overwhelmed and didn’t know which one to use. I used aws_security_group and also used ```aws_security_group_ingress_rules``` not knowing all I did was duplicate it. LOL. I remember in class we used ```security_group_rule with aws_security_group```, I didn’t go that route. Watched some YouTube videos and realized that I can use include ingress  in ```aws_security_group```. Now, terraform init, plan and apply. Everything is but I cant get access to my WordPress. I go over to the console and everything seems correct on my end. I remember from class if you have  issues with the internet, it's most likely resulting from the security group. 

The last part was supposed to be the easiest—setting up the security group—but I ran into issues because I was overwhelmed with too many documentation options. At first, I used both ```aws_security_group``` and ```aws_security_group_ingress_rule```, not realizing I had essentially duplicated the same rules. LOL.

In class, we had used ```security_group_rule``` with ```aws_security_group```, but I decided to do it my own way. After watching some YouTube tutorials, I realized I could include the ingress rules directly in the ```aws_security_group resource```.

With everything in place, I ran terraform init, plan, and apply. Everything deployed successfully, but I couldn’t access my WordPress site. After some head-scratching and double-checking in the AWS console, I remembered from class: if there are internet issues, it’s likely related to the security group.
![Profile Image](/images/Picture3.png)



 
Sure enough, my security group had no outbound rules. I quickly added an egress rule, and... 
![Profile Image](/images/Picture4.png)

Look at this now—WordPress is up and running! 🚀  
![Profile Image](./images/Picture5.png)
This is my command to clean resources: ```terraform destroy``` . This way I save on cost.

