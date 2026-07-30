---
title : "Access S3 from VPC"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Objectives

* Set up Gateway VPC Endpoint to access Amazon S3 from VPC.
* Configure route tables to direct S3 traffic through a private endpoint.
* Test S3 access from EC2 inside VPC without traversing public Internet.

#### Practical Exercises

1. Create VPC, subnets, and route tables.
2. Create S3 Bucket and configure basic access permissions.
3. Create Gateway VPC Endpoint for Amazon S3.
4. Update route table to direct S3 traffic to the endpoint.
5. Test object upload/download from EC2 inside VPC.
