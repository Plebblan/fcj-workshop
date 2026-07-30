---
title: "Worklog Tuần 4"
date: 2024-07-05
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Hoàn thiện kiến trúc tổng thể của hệ thống và xác định rõ nhiệm vụ, trách nhiệm của từng thành viên trong nhóm.
* Nghiên cứu AWS Key Management Service (KMS) và vai trò của dịch vụ trong việc bảo vệ dữ liệu.
* Thực hành tạo và quản lý khóa mã hóa, đồng thời triển khai mã hóa dữ liệu cho các tài nguyên AWS được sử dụng trong dự án.

### Các công việc cần triển khai trong tuần này:
| Thứ | Ngày | Công việc | Nguồn tài liệu |
| --- | ---- | --------- | -------------- |
| 2 | 29/06/2026 | **Hoàn thiện Kiến trúc Hệ thống:**<br>&emsp;+ Cập nhật và hoàn thiện sơ đồ kiến trúc hệ thống trên draw.io.<br>&emsp;+ Thảo luận, thống nhất và mô tả rõ luồng dữ liệu (Data Flow) giữa các thành phần trong hệ thống. |
| 3 | 30/06/2026 | **Phân chia Công việc trong Nhóm:**<br>&emsp;+ Tổ chức họp nhóm để phân chia các module và nhiệm vụ cụ thể cho từng thành viên, bao gồm Frontend, Backend và Infrastructure/AWS.<br>&emsp;+ Chuẩn bị môi trường phát triển chung thông qua Git repository và AWS IAM Accounts. |
| 4 | 01/07/2026 | **Nghiên cứu AWS KMS (Key Management Service):**<br>&emsp;+ Tìm hiểu khái niệm KMS, AWS Managed Keys và Customer Managed Keys (CMK).<br>&emsp;+ Nghiên cứu cơ chế bảo vệ dữ liệu khi lưu trữ (At-Rest) và khi truyền tải (In-Transit).<br>&emsp;+ Tìm hiểu cách xây dựng và quản lý Key Policies để kiểm soát quyền truy cập khóa. | <https://docs.aws.amazon.com/kms/latest/developerguide/> |
| 5 | 02/07/2026 | **Thực hành Mã hóa Dữ liệu với KMS:**<br>&emsp;+ Tạo và cấu hình Customer Managed Key (CMK) thông qua AWS KMS Console.<br>&emsp;+ **Thực hành:** Sử dụng khóa KMS để triển khai mã hóa cho dữ liệu được lưu trữ trên S3 Bucket, EBS Volume và DynamoDB Table. | <https://docs.aws.amazon.com/kms/latest/developerguide/> |
| 6 | 03/07/2026 | **Tổng kết và Đánh giá:**<br>&emsp;+ Kiểm tra khả năng truy cập và sử dụng dữ liệu đã được mã hóa từ ứng dụng.<br>&emsp;+ Rà soát lại kiến trúc hệ thống, nhiệm vụ của các thành viên và cập nhật nội dung báo cáo tuần 4. |

### Kết quả đạt được tuần 4:

* **Hoàn thiện Kiến trúc và Phân công Công việc:**
  * Hoàn thiện sơ đồ kiến trúc hệ thống bằng draw.io, thể hiện rõ mối quan hệ và luồng tương tác giữa EC2, S3, DynamoDB cùng các thành phần bảo mật.
  * Xác định và phân chia cụ thể nhiệm vụ cho từng thành viên, đồng thời thiết lập môi trường phát triển và làm việc chung thông qua Git và AWS IAM Roles/Users.

* **Bảo mật và Quản lý Khóa với AWS KMS:**
  * Hiểu được các khái niệm cơ bản về mã hóa dữ liệu trên môi trường Cloud, Customer Managed Key và Key Policy.
  * Tạo thành công Customer Managed Key (CMK) và cấu hình chính sách nhằm kiểm soát quyền truy cập vào khóa.
  * Triển khai mã hóa dựa trên KMS cho S3 Bucket, EBS Volume và DynamoDB Table, qua đó tăng cường bảo vệ dữ liệu trong trạng thái lưu trữ (At-Rest).