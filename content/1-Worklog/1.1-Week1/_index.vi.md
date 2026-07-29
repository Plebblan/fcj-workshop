---
title: "Worklog Tuần 1"
date: 2026-06-14
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Tìm hiểu các dịch vụ AWS sẽ được sử dụng trong đề tài của nhóm.
* Hiểu vai trò của từng dịch vụ AWS trong kiến trúc hệ thống và cách chúng phối hợp với nhau.

### Các công việc cần triển khai trong tuần này:

| Thứ | Ngày | Công việc | Nguồn tài liệu |
| --- | ---- | --------- | -------------- |
| 2 | 08/06/2026 | Tìm hiểu kiến trúc tổng quan của đề tài.<br>Xác định các dịch vụ AWS sẽ sử dụng trong hệ thống. | <https://docs.aws.amazon.com/> |
| 3 | 09/06/2026 | Tìm hiểu Amazon S3 để lưu trữ dữ liệu và triển khai website tĩnh.<br>Tìm hiểu Amazon CloudFront để phân phối nội dung và tăng hiệu năng truy cập. | <https://docs.aws.amazon.com/> |
| 4 | 10/06/2026 | Tìm hiểu AWS Lambda và Amazon API Gateway.<br>Nghiên cứu luồng xử lý yêu cầu từ frontend đến backend trong mô hình serverless. | <https://docs.aws.amazon.com/> |
| 5 | 11/06/2026 | Tìm hiểu Amazon DynamoDB để lưu trữ dữ liệu.<br>Tìm hiểu AWS IAM để quản lý quyền truy cập và bảo mật tài nguyên AWS. | <https://docs.aws.amazon.com/> |
| 6 | 12/06/2026 | Tìm hiểu AWS Elemental MediaConvert để xử lý và chuyển đổi video.<br>Tổng hợp kiến thức và xây dựng sơ đồ kiến trúc thể hiện sự tương tác giữa các dịch vụ AWS trong hệ thống. | <https://docs.aws.amazon.com/> |

### Kết quả đạt được tuần 1:

* Xác định được các dịch vụ AWS cần sử dụng để triển khai hệ thống của đề tài.

* Hiểu được vai trò của từng dịch vụ trong kiến trúc tổng thể:
  * Amazon S3 dùng để lưu trữ tệp và triển khai giao diện web tĩnh.
  * Amazon CloudFront dùng để tăng tốc phân phối nội dung đến người dùng.
  * Amazon API Gateway dùng để cung cấp các API cho ứng dụng.
  * AWS Lambda dùng để xử lý logic nghiệp vụ theo mô hình serverless.
  * Amazon DynamoDB dùng để lưu trữ dữ liệu NoSQL.
  * AWS IAM dùng để quản lý người dùng, quyền truy cập và bảo mật tài nguyên.
  * AWS Elemental MediaConvert dùng để xử lý và chuyển đổi định dạng video.

* Hiểu được luồng hoạt động của hệ thống, từ giao diện người dùng, API, xử lý nghiệp vụ đến lưu trữ dữ liệu và xử lý video.

* Có cái nhìn tổng quan về cách các dịch vụ AWS phối hợp với nhau để xây dựng một hệ thống điện toán đám mây hiện đại.

* Hoàn thành tài liệu tổng hợp về vai trò của từng dịch vụ và sơ đồ kiến trúc ban đầu của hệ thống, làm nền tảng cho việc triển khai ở các tuần tiếp theo.