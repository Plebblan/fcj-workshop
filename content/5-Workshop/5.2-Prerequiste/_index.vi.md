---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### IAM permissions
Gắn IAM permission policy sau vào tài khoản aws user của bạn để triển khai và dọn dẹp tài nguyên trong workshop này.
```


```

#### Khởi tạo tài nguyên bằng CloudFormation

Trong lab này, chúng ta sẽ dùng Singapore region (ap-southeast-1).

Để chuẩn bị cho môi trường làm workshop, chúng ta deploy CloudFormation template sau (click link): [PrivateLinkWorkshop ](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://s3.us-east-1.amazonaws.com/reinvent-endpoints-builders-session/Nested.yaml&stackName=PLCloudSetup). Để nguyên các lựa chọn mặc định.

![create stack](/images/5-Workshop/5.2-Prerequisite/create-stack1.png)

+ Lựa chọn 2 mục acknowledgement 
+ Chọn Create stack

![create stack](/images/5-Workshop/5.2-Prerequisite/create-stack2.png)

Quá trình triển khai CloudFormation cần khoảng 15 phút để hoàn thành.

![complete](/images/5-Workshop/5.2-Prerequisite/complete.png)

+ 2 VPCs đã được tạo

![vpcs](/images/5-Workshop/5.2-Prerequisite/vpcs.png)

+ 3 EC2s đã được tạo

![EC2](/images/5-Workshop/5.2-Prerequisite/ec2.png)