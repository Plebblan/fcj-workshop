---
title : "VPC Endpoint Policies"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Mục tiêu

* Tìm hiểu cách áp dụng VPC Endpoint Policy để giới hạn quyền truy cập dịch vụ.
* Viết chính sách VPC Endpoint cho phép chỉ các hành động S3 cần thiết.
* Kiểm thử policy bằng cách truy cập dịch vụ từ VPC với các tài khoản khác nhau.

#### Nội dung thực hành

1. Đọc về VPC Endpoint Policy và phạm vi áp dụng.
2. Viết policy để hạn chế truy cập chỉ tới bucket S3 được chỉ định.
3. Gán policy vào VPC Endpoint.
4. Kiểm thử truy cập S3 với policy và so sánh hành vi khi policy bị từ chối.
