---
title: "Worklog Tuần 3"
date: 2026-06-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Tìm hiểu về EC2 Auto Scaling và cách áp dụng vào dự án của nhóm.
* Tìm hiểu Amazon S3 và vai trò của dịch vụ này trong việc lưu trữ các file media và dữ liệu liên quan đến dự án.
* Tìm hiểu Amazon DynamoDB và đánh giá khả năng sử dụng dịch vụ để lưu trữ metadata của ứng dụng.
* Phân tích cách EC2 Auto Scaling, Amazon S3 và DynamoDB có thể kết hợp với nhau trong dự án Cloud Media Converter and Storage.
* Tiếp tục nghiên cứu và hoàn thiện kiến trúc AWS của dự án.

### Các công việc cần triển khai trong tuần này:
| Thứ | Ngày | Công việc | Nguồn tài liệu |
| --- | ---- | --------- | -------------- |
| 2 | 22/06/2026 | Tìm hiểu về **EC2 Auto Scaling**, bao gồm Auto Scaling Groups, Launch Templates, Scaling Policies và cách các EC2 instance có thể tự động tăng hoặc giảm dựa trên workload. Phân tích cách Auto Scaling có thể hỗ trợ workload chuyển đổi media của dự án. |
| 3 | 23/06/2026 | Tìm hiểu về **Amazon S3** và mô hình lưu trữ của dịch vụ. Tìm hiểu về bucket, object, storage class, quyền truy cập và cách S3 có thể được sử dụng để lưu trữ các file media được upload và các file sau khi chuyển đổi. |
| 4 | 24/06/2026 | Tìm hiểu về **Amazon DynamoDB** và mô hình cơ sở dữ liệu NoSQL. Tìm hiểu về table, item, attribute, primary key và cách DynamoDB có thể được sử dụng để lưu trữ metadata và trạng thái của quá trình chuyển đổi media. |
| 5 | 25/06/2026 | Phân tích mối quan hệ giữa **EC2 Auto Scaling, Amazon S3 và DynamoDB** trong kiến trúc dự án.<br><strong>Thực hành:</strong><br>&emsp;+ Thiết kế quy trình cơ bản để upload file media lên S3.<br>&emsp;+ Xác định các metadata cần lưu trữ trong DynamoDB.<br>&emsp;+ Tìm hiểu cách EC2 instance có thể xử lý các tác vụ chuyển đổi file.<br>&emsp;+ Xem xét cách Auto Scaling có thể tăng hoặc giảm số lượng EC2 instance dựa trên workload. |
| 6 | 26/06/2026 | Kiểm tra lại kiến trúc AWS được đề xuất cho dự án **Cloud Media Converter and Storage**.<br><strong>Thực hành:</strong><br>&emsp;+ Xác định vai trò của từng AWS service.<br>&emsp;+ Kiểm tra luồng dữ liệu giữa web application, S3, DynamoDB và EC2.<br>&emsp;+ Ghi lại kết quả nghiên cứu và hoàn thiện tài liệu cho báo cáo dự án. |

### Kết quả đạt được tuần 3:

* Hiểu rõ hơn về **Amazon EC2 Auto Scaling** và vai trò của dịch vụ trong việc tự động điều chỉnh tài nguyên compute dựa trên workload của ứng dụng.

* Tìm hiểu các thành phần chính của EC2 Auto Scaling, bao gồm:
  * Auto Scaling Groups
  * Launch Templates
  * Minimum và maximum instance capacity
  * Desired capacity
  * Scaling Policies
  * Health Checks

* Hiểu cách EC2 Auto Scaling có thể được áp dụng cho **workload chuyển đổi media** của dự án:
  * Tăng số lượng EC2 instance khi workload chuyển đổi tăng.
  * Giảm số lượng instance khi nhu cầu xử lý giảm.
  * Cải thiện khả năng sẵn sàng bằng cách thay thế các instance gặp lỗi.
  * Tránh phụ thuộc vào một EC2 instance duy nhất cho việc xử lý media.

* Tìm hiểu về **Amazon S3** và hiểu được vai trò của dịch vụ này trong việc lưu trữ object cho dự án.

* Nắm được các khái niệm cơ bản của Amazon S3, bao gồm:
  * Bucket
  * Object
  * Object Key
  * Storage Classes
  * Access Permissions
  * Upload và Download Operations

* Xác định các loại dữ liệu có thể được lưu trữ trên S3 trong dự án:
  * File media gốc được upload.
  * File media sau khi chuyển đổi.
  * Các file tạm thời hoặc file trung gian nếu cần thiết.

* Tìm hiểu về **Amazon DynamoDB** và mô hình dữ liệu NoSQL của dịch vụ.

* Nắm được các thành phần cơ bản của DynamoDB, bao gồm:
  * Table
  * Item
  * Attribute
  * Partition Key
  * Sort Key
  * Query Operations

* Xác định DynamoDB là một lựa chọn phù hợp để lưu trữ **metadata của quá trình chuyển đổi media**, chẳng hạn như:
  * File ID
  * Tên file gốc
  * Loại file đầu vào
  * Loại file đầu ra
  * Vị trí lưu trữ file
  * Trạng thái chuyển đổi
  * Thời gian upload
  * Thời gian hoàn thành chuyển đổi

* Phân tích mối quan hệ giữa các AWS service chính được sử dụng trong dự án:
  * **Amazon S3** → Lưu trữ các file media được upload và các file sau khi chuyển đổi.
  * **Amazon DynamoDB** → Lưu trữ metadata của file và trạng thái chuyển đổi.
  * **Amazon EC2** → Cung cấp tài nguyên compute để thực hiện quá trình chuyển đổi media.
  * **EC2 Auto Scaling** → Tự động điều chỉnh số lượng EC2 instance dựa trên workload.

* Hiểu rõ hơn cách kết hợp các dịch vụ storage, database và compute để xây dựng một nền tảng chuyển đổi media có khả năng mở rộng.

* Ghi chép và tổng hợp các kết quả nghiên cứu để tiếp tục hoàn thiện kiến trúc AWS của dự án **Cloud Media Converter and Storage**.

* Cải thiện hiểu biết về tầm quan trọng của việc lựa chọn AWS service dựa trên:
  * Yêu cầu workload
  * Khả năng mở rộng
  * Độ tin cậy
  * Hiệu năng
  * Chi phí
  * Khả năng quản lý

* ...