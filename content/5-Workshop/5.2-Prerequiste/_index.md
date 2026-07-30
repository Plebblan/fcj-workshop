---
title : "Prerequisites"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### IAM permissions
Attach the following IAM permission policy to your AWS user account to deploy and clean up resources in this workshop.
```


```

#### Resource Initialization via CloudFormation

In this lab, we will use the Singapore region (ap-southeast-1).

To prepare the workshop environment, deploy the following CloudFormation template (click link): [PrivateLinkWorkshop ](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://s3.us-east-1.amazonaws.com/reinvent-endpoints-builders-session/Nested.yaml&stackName=PLCloudSetup). Keep all default options.

![create stack](/images/5-Workshop/5.2-Prerequisite/create-stack1.png)

+ Select the 2 acknowledgment checkboxes
+ Click Create stack

![create stack](/images/5-Workshop/5.2-Prerequisite/create-stack2.png)

The CloudFormation deployment process takes approximately 15 minutes to complete.

![complete](/images/5-Workshop/5.2-Prerequisite/complete.png)

+ 2 VPCs have been created

![vpcs](/images/5-Workshop/5.2-Prerequisite/vpcs.png)

+ 3 EC2s have been created

![EC2](/images/5-Workshop/5.2-Prerequisite/ec2.png)