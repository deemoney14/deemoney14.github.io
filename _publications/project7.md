---
title: " Porject 7: CI/CD Pipeline"
collection: Projects
category: conferences
permalink: /publication/2024-02-17-paper-title-number-4
excerpt: 'This project is about understanding the foundation of CI/CD '
date: 2024-10-20
venue: 'December'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2024). &quot;Paper Title Number 3.&quot; <i>GitHub Journal of Bugs</i>. 1(3).'
---

This project focused on building and deploying a simple CI/CD pipeline using GitHub Actions. The goal was to learn the basics of Continuous Integration and Continuous Deployment by automating workflows triggered by code changes.

                                       Part 1: Basic GitHub Action Workflow
                                       
In the first phase, I created a simple workflow file in YAML. This workflow was designed to trigger whenever I pushed changes to my repository. The runner was configured to use the latest version of Ubuntu, and I included two basic steps in this workflow:

                                                Steps:
						
Print a Greeting:

This step outputs ```Hello, GitHub Action``` to the console.

Print the Repository Name:

This step uses the ```${{ github.repository }}``` variable to fetch and display the name of the repository where the workflow is running.

Although it was a simple concept, it demonstrated the foundational workings of GitHub Actions, and I gained hands-on experience with creating workflows triggered by repository events.
![Profile Image](/images/gh1.png)

                                Part 2: Deploying an AWS Lambda Function

Building on this, I decided to expand the workflow's complexity by incorporating a serverless architecture. While I plan to create a more comprehensive project on serverless in the future, this task introduced me to deploying an AWS Lambda function through a CI/CD pipeline.

                              Workflow Name: Deploy AWS Lambda

This workflow is designed to deploy an AWS Lambda function whenever changes are pushed to the main branch, specifically within the lambda/ directory.

                                    Trigger Configuration:

•	Branch: The workflow triggers only when changes are pushed to the main branch.

•	Path: It monitors changes within the lambda/ directory.

                                         Job Details
                                         
•	Runner: The job runs on the latest Ubuntu virtual environment (ubuntu-latest).

•	Steps: This workflow has five steps:

1.	Checkout Code:
	```actions/checkout@v2```: Clones the repository into the runner for access during the workflow.

2.	Set Up Python:
	```actions/setup-python@v2```: Installs Python 3.12 in the runner environment.

3.	Install Dependencies:
	Upgrades pip and installs Python dependencies from the ```requirements.txt``` file into the lambda/ directory.
(Note: For this project, the requirements.txt file was empty as no additional dependencies were required.)


4.	Configure AWS Credentials:
   
	aws-actions/configure-aws-credentials@v1:

	o Configures AWS access credentials using secrets stored in the repository (AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY).

	o Specifies the AWS region (us-west-1).

6.	Deploy Lambda Function:
   
o	Zips the contents of the lambda/ directory.

o	Uses the AWS CLI to update the Lambda function's code with the newly zipped file.

```lambda.yaml```
![Profile Image](/images/gh2.png)

```lambda_function```
![Profile Image](/images/gh3.png)


                                                           Reflection
							   
This project allowed me to explore the basics of CI/CD workflows and serverless deployment using GitHub Actions. While the initial example was simple, adding the Lambda deployment workflow helped me understand how CI/CD can facilitate automated updates in a serverless environment.

In the future, I plan to create more advanced projects involving serverless architectures, exploring topics like API Gateway integration and automated testing for Lambda functions.


