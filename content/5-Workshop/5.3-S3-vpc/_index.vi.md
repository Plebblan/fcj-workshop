---
title : "Truy cập S3 từ VPC"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Mục tiêu

* Thiết lập Gateway VPC Endpoint để truy cập Amazon S3 từ VPC.
* Cấu hình route table để gửi lưu lượng S3 qua điểm cuối riêng tư.
* Kiểm thử truy cập S3 từ EC2 trong VPC mà không đi qua Internet công cộng.

#### Nội dung thực hành

1. Tạo VPC, subnet và bảng định tuyến.
2. Tạo S3 Bucket và cấu hình quyền truy cập cơ bản.
3. Tạo Gateway VPC Endpoint cho Amazon S3.
4. Cập nhật route table để hướng lưu lượng S3 tới endpoint.
5. Kiểm thử upload/download đối tượng từ EC2 trong VPC.
