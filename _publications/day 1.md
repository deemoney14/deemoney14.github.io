---
title: " 30-DAY DEV PROJECT: DAY-1"
collection: Projects
category: conferences
permalink: /publication/2024-10-20-paper-title-number-4
excerpt: ' '
date: 2024-10-20
venue: 'Jan'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2024). &quot;Paper Title Number 3.&quot; <i>GitHub Journal of Bugs</i>. 1(3).'
---


                                 
Welcome to Day 1 of my 30-day development journey! In this project, I’ll demonstrate how to build an OpenWeather API integration with AWS S3. This project is a great opportunity to apply DevOps principles such as automation, error handling, and cloud infrastructure integration.
   
                           
                      The system:
                      
•	Fetch real-time weather data for multiple cities.

•	Display key metrics, including temperature (°F), humidity, and weather conditions.

•	Automatically store weather data in AWS S3.

•	Support tracking for multiple cities.

•	Timestamp all data for historical tracking purposes.


                        Step-by-Step Implementation

                        1.	Setting Up the Environment
Ensure all necessary dependencies are installed. For secure handling of sensitive credentials, create a .env file to store API keys and AWS credentials.

                          2.	Writing the Python Script

I created a WeatherDashboard class to handle the following tasks:
o	Fetching weather data from the OpenWeather API.
o	Uploading weather data to an AWS S3 bucket.
.
                     3.	Running the Script 

Run the Python script to fetch weather data for predefined cities and upload it to AWS S3.
![Profile Image](/images/hh2.png)
![Profile Image](/images/hh3.png)
![Profile Image](/images/hh4.png)

                4.	Checking the AWS S3 Bucket 

Verify the data stored in your AWS S3 bucket. The weather data will be organized in JSON format with timestamps.
![Profile Image](/images/hh5.png)

                       Tools and Technologies
•	Version Control: Git
•	Cloud Platform: AWS
•	API: OpenWeather

                             Challenges Faced 

During setup, I encountered a few challenges:

1.	The Python code defaulted to configuring the S3 bucket in the us-east-1 region, but I needed it in us-west-1. To resolve this, I added a region constraint in the configuration.

2.	Handling errors during the API calls and S3 uploads required adding robust error-handling logic to the script.

                                                     Final Thoughts
This sample project emphasized the need to refresh my Python skills. Starting a new project is always exciting, but it also comes with its challenges. I’m eager to see how much I can learn and accomplish over the next 30 days.
![Profile Image](/images/hh6.png)


                                       
                                       




