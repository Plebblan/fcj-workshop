---
title : "References"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

The following references were used during the research, development, implementation, and documentation of the workshop.

## 1. Project Repository

- **Cloud Media Converter on AWS**  
  GitHub repository containing the source code, infrastructure code, frontend, backend, and documentation related to the Cloud Media Converter on AWS project.  
  [https://github.com/danghuyenvu/Cloud-Media-Converter-and-Storage-on-AWS](https://github.com/danghuyenvu/Cloud-Media-Converter-and-Storage-on-AWS)

## 2. Amazon Web Services Documentation

### Amazon S3

- **Amazon S3 Documentation**  
  Reference for Amazon S3, including buckets, objects, data storage, access control, and related features.  
  [https://docs.aws.amazon.com/s3/](https://docs.aws.amazon.com/s3/)

- **Download and Upload Objects with Presigned URLs**  
  Used as a reference for implementing presigned URLs to provide temporary upload and download access to objects stored in Amazon S3.  
  [https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)

### AWS Lambda

- **AWS Lambda Developer Guide**  
  Reference for creating, configuring, deploying, and invoking Lambda functions.  
  [https://docs.aws.amazon.com/lambda/](https://docs.aws.amazon.com/lambda/)

- **Using Lambda with API Gateway**  
  Used as a reference for integrating AWS Lambda with API Gateway and handling HTTP requests.  
  [https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)

### Amazon API Gateway

- **Amazon API Gateway Developer Guide**  
  Reference for creating APIs, configuring routes, integrating Lambda functions, deploying APIs, and managing API requests.  
  [https://docs.aws.amazon.com/apigateway/](https://docs.aws.amazon.com/apigateway/)

- **Tutorial: Create a CRUD HTTP API with Lambda and DynamoDB**  
  Used as a reference for understanding the integration between API Gateway, Lambda, and DynamoDB in a serverless architecture.  
  [https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html)

### Amazon DynamoDB

- **Amazon DynamoDB Developer Guide**  
  Reference for creating tables, storing job information, querying data, and managing DynamoDB resources.  
  [https://docs.aws.amazon.com/amazondynamodb/](https://docs.aws.amazon.com/amazondynamodb/)

### AWS Identity and Access Management (IAM)

- **AWS Identity and Access Management Documentation**  
  Reference for IAM users, roles, policies, permissions, and access-control mechanisms used throughout the workshop.  
  [https://docs.aws.amazon.com/iam/](https://docs.aws.amazon.com/iam/)

### Amazon VPC

- **Amazon VPC Documentation**  
  Reference for VPCs, subnets, route tables, Internet Gateways, security groups, and VPC endpoints.  
  [https://docs.aws.amazon.com/vpc/](https://docs.aws.amazon.com/vpc/)

- **Gateway Endpoints for Amazon S3 and DynamoDB**  
  Used as a reference for configuring VPC gateway endpoints to allow resources within a VPC to access Amazon S3 and DynamoDB without requiring an Internet Gateway or NAT device.  
  [https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html)

### Amazon CloudWatch

- **Amazon CloudWatch Documentation**  
  Reference for monitoring Lambda functions, viewing logs, checking metrics, and monitoring application performance.  
  [https://docs.aws.amazon.com/cloudwatch/](https://docs.aws.amazon.com/cloudwatch/)

## 3. AWS Architecture and Best Practices

- **AWS Well-Architected Framework**  
  Used as a reference for designing secure, reliable, efficient, and cost-effective cloud architectures.  
  [https://docs.aws.amazon.com/wellarchitected/](https://docs.aws.amazon.com/wellarchitected/)

- **AWS Serverless Applications Lens**  
  Reference for applying AWS Well-Architected principles to serverless applications.  
  [https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/)

- **Establishing Guardrails and Monitoring for Presigned URLs**  
  Reference for security, control, and monitoring practices when using presigned URLs with Amazon S3.  
  [https://docs.aws.amazon.com/prescriptive-guidance/latest/presigned-url-best-practices/introduction.html](https://docs.aws.amazon.com/prescriptive-guidance/latest/presigned-url-best-practices/introduction.html)

## 4. Additional Development References

- **AWS Command Line Interface Documentation**  
  Used as a reference for interacting with AWS services through the command line during deployment and testing.  
  [https://docs.aws.amazon.com/cli/](https://docs.aws.amazon.com/cli/)

- **AWS SDK for JavaScript Documentation**  
  Reference for interacting with AWS services programmatically using JavaScript.  
  [https://docs.aws.amazon.com/sdk-for-javascript/](https://docs.aws.amazon.com/sdk-for-javascript/)

- **FFmpeg Documentation**  
  Used as a technical reference for media processing and conversion operations performed by the application.  
  [https://ffmpeg.org/documentation.html](https://ffmpeg.org/documentation.html)

## 5. Summary

&emsp;The references above provided the technical foundation for researching, designing, and implementing the workshop. Official AWS documentation was primarily used to understand AWS services, serverless architecture, configuration procedures, security practices, and integration methods.

&emsp;The project's GitHub repository contains the source code, infrastructure code, frontend, backend, and related documentation developed throughout the project.

&emsp;These references were used to support the learning and development process. The final architecture, implementation, configuration, testing procedures, and documentation were adapted according to the specific requirements and objectives of the workshop.