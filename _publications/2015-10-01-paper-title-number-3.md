---
title: "Project 2: Manipulating S3 Buckets"
collection: publications
category: manuscripts
permalink: /publication/2015-10-01-paper-title-number-3
excerpt: 'two S3 buckets, uploaded files, and copied them between buckets using AWS CLI.'
date: 2024-10-01
venue: 'October'
#slidesurl: 'http://academicpages.github.io/files/slides3.pdf'
#paperurl: 'http://academicpages.github.io/files/paper3.pdf'
#citation: 'Your Name, You. (2015). &quot;Paper Title Number 3.&quot; <i>Journal 1</i>. 1(3).'
---

In this project, I focused on using the AWS CLI to create two S3 buckets, upload files to one, and transfer those files to another bucket.

Step 1: Creating the S3 Buckets
I created two S3 buckets: ```sam-sa-gh-test1``` and ```sam-sa-gh-test2```, using Terraform documentation to set them up.

Step 2: Uploading Files to the First Bucket
To upload files into ```sam-sa-gh-test1```, I used the CLI command:
