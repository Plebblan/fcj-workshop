---
title : "Introduction"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Workshop Architecture Overview

This workshop demonstrates how to build a media conversion system on AWS using a serverless and event-driven model. The architecture described in the diagram consists of key components:

- **Amazon CloudFront**: serves static web interfaces and front-end content to users.
- **Amazon API Gateway**: receives browser requests to generate presigned URLs and query job statuses.
- **AWS Lambda**: generates presigned URLs, processes file upload events, updates task statuses, and returns download paths.
- **Amazon S3**: stores two types of files: raw media uploaded by users and processed media after conversion.
- **Amazon DynamoDB**: stores job details, processing status, and metadata.
- **AWS CloudFormation / AWS CDK**: defines and deploys the entire infrastructure as code.

### Main Processing Workflow

1. User requests an upload presigned URL via API Gateway.
2. Lambda generates the presigned URL and returns it to the browser.
3. Browser uploads the media file directly to the raw media bucket on S3.
4. S3 triggers another Lambda function to process the file upon new upload.
5. Processing Lambda converts media and saves output to the processed media bucket.
6. Lambda updates job status in DynamoDB: `PENDING`, `PROCESSING`, `COMPLETED`, or `FAILED`.
7. User can request a download presigned URL to retrieve the converted file from S3.

### AWS Services in the Workshop

#### AWS CloudFront

CloudFront distributes static web pages and front-end content to users with low latency. This is the first entry point on the diagram for the web application.

#### AWS API Gateway

API Gateway provides REST API endpoints for the frontend. In the workshop, API Gateway receives requests to obtain upload/download presigned URLs and check job status.

#### AWS Lambda

AWS Lambda performs two main functions:
- Generating upload/download presigned URLs for S3.
- Processing S3 upload events to convert media and update status in DynamoDB.

#### Amazon S3

S3 is used to store:
- **Raw Media Bucket**: original files uploaded by users.
- **Processed Media Bucket**: converted files after Lambda processing.

#### Amazon DynamoDB

DynamoDB stores task statuses and metadata, helping track media conversion progress and returning information to the frontend.

#### AWS CloudFormation / AWS CDK

CloudFormation and CDK are tools to define, manage, and deploy AWS infrastructure. The workshop will use IaC to create resources such as S3 buckets, Lambda functions, API Gateway, and DynamoDB.

### Workshop Objectives

In this workshop, you will learn to:

* Design AWS serverless architecture based on workflow diagrams.
* Deploy API Gateway, Lambda, and S3 to process media uploads.
* Use presigned URLs to upload files directly to S3.
* Build event-driven processing with S3 events and Lambda.
* Store job statuses in DynamoDB to track processing progress.
* Deploy infrastructure using AWS CDK / CloudFormation.

### Expected Outcomes

After the workshop, you will be able to build a secure, flexible, and scalable media conversion pipeline on AWS. You will also clearly understand how AWS services collaborate via diagrams to ensure automated data flow from upload to download.