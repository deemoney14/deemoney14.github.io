---
title: "Project 2: Manipulating S3 Buckets"
collection: publications
category: manuscripts
permalink: /publication/2015-10-01-paper-title-number-3
excerpt: 'two S3 buckets, uploaded files, and copied them between buckets using AWS CLI.'
date: 2024-10-01
venue: 'October'
slidesurl: 'http://academicpages.github.io/files/slides3.pdf'
paperurl: 'http://academicpages.github.io/files/paper3.pdf'
citation: 'Your Name, You. (2015). &quot;Paper Title Number 3.&quot; <i>Journal 1</i>. 1(3).'
---

In this project, I focused on using the AWS CLI to create two S3 buckets, upload files to one, and transfer those files to another bucket.
I created two S3 buckets: ```sam-sa-gh-test1``` and ```sam-sa-gh-test2```, using Terraform documentation to set them up.I uploaded files into ```sam-sa-gh-test``` using the CLI command ``` aws s3 cp /your saved file s3://sam-sa-gh-test1 --recursive```. This command uploads files from a directory. I also discovered the ```sync``` command for updating only new or modified files: ```aws s3 sync /your saved file s3://sam-sa-gh-test1 --recursive```. 
Next i copies the files from ```sam-sa-gh-test1``` to ```sam-sa-gh-test2``` using: ``` aws s3 cp s3://sam-sa-gh-test1/mypic s3://sam-sa-gh-test2/mypic --recursive``` Your can use the ```Datasync``` to manged updates between the two buckets. 


I realized I didn't have to apply policies to this S3 bucket since I have admin access and it was in the same account.

Closed out this project by applying the Terraform destroy.


