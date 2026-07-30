---
title : "Truy cập S3 từ TTDL On-premises"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Mục tiêu

* Thiết lập kết nối VPN giả lập giữa VPC On-Prem và AWS Cloud.
* Dùng Interface VPC Endpoint và VPC Endpoint DNS để truy cập S3 từ môi trường On-Prem.
* Kiểm thử truy cập S3 từ EC2 trên VPC On-Prem qua kết nối riêng tư.

#### Nội dung thực hành

1. Đảm bảo VPN Site-to-Site hoạt động giữa VPC Cloud và VPC On-Prem.
2. Tạo Interface VPC Endpoint phù hợp cho S3 hoặc dịch vụ cần thiết.
3. Cấu hình DNS và route để truy cập dịch vụ qua endpoint.
4. Kiểm thử truy cập S3 từ EC2 trong VPC On-Prem.
