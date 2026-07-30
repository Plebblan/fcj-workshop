---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Tổng quan về kiến trúc workshop

Workshop này trình bày cách xây dựng một hệ thống chuyển đổi media trên AWS theo mô hình serverless và event-driven. Kiến trúc được mô tả trong diagram gồm các thành phần chính:

- **Amazon CloudFront**: phục vụ giao diện web tĩnh và nội dung front-end cho người dùng.
- **Amazon API Gateway**: tiếp nhận yêu cầu từ trình duyệt để tạo presigned URL và truy vấn trạng thái job.
- **AWS Lambda**: tạo presigned URL, xử lý sự kiện khi tệp được tải lên, cập nhật trạng thái công việc và trả về đường dẫn download.
- **Amazon S3**: lưu trữ hai loại file: raw media khi người dùng upload và processed media sau khi chuyển đổi.
- **Amazon DynamoDB**: lưu trữ thông tin job, trạng thái xử lý và metadata.
- **AWS CloudFormation / AWS CDK**: định nghĩa và triển khai toàn bộ hạ tầng dưới dạng mã.

### Luồng xử lý chính

1. Người dùng yêu cầu presigned URL upload qua API Gateway.
2. Lambda tạo presigned URL và trả về cho trình duyệt.
3. Trình duyệt tải file media trực tiếp lên bucket raw media trên S3.
4. S3 kích hoạt một Lambda khác để xử lý file khi có upload mới.
5. Lambda processing chuyển đổi media và lưu kết quả vào bucket processed media.
6. Lambda cập nhật trạng thái job trong DynamoDB: `PENDING`, `PROCESSING`, `COMPLETED` hoặc `FAILED`.
7. Người dùng có thể yêu cầu presigned URL download để tải file đã chuyển đổi từ S3.

### Các dịch vụ AWS trong workshop

#### AWS CloudFront

CloudFront phân phối các trang web tĩnh và nội dung front-end tới người dùng với độ trễ thấp. Đây là điểm truy cập đầu tiên trên sơ đồ cho ứng dụng web.

#### AWS API Gateway

API Gateway cung cấp điểm kết nối REST API cho frontend. Trong workshop, API Gateway nhận yêu cầu lấy presigned URL upload/download và yêu cầu kiểm tra trạng thái job.

#### AWS Lambda

AWS Lambda thực hiện hai chức năng chính:
- Tạo presigned URL upload/download cho S3.
- Xử lý sự kiện upload từ S3 để chuyển đổi media và cập nhật trạng thái trong DynamoDB.

#### Amazon S3

S3 dùng để lưu trữ:
- **Raw Media Bucket**: file gốc được người dùng upload.
- **Processed Media Bucket**: file đã chuyển đổi sau khi Lambda xử lý.

#### Amazon DynamoDB

DynamoDB lưu trữ trạng thái công việc và metadata, giúp theo dõi tiến trình chuyển đổi media và trả về thông tin cho frontend.

#### AWS CloudFormation / AWS CDK

CloudFormation và CDK là công cụ để định nghĩa, quản lý và triển khai hạ tầng AWS. Workshop sẽ sử dụng IaC để tạo các resource như S3 bucket, Lambda function, API Gateway và DynamoDB.

### Mục tiêu workshop

Trong workshop này, bạn sẽ học được:

* Thiết kế kiến trúc AWS serverless theo sơ đồ workflow.
* Triển khai API Gateway, Lambda và S3 để xử lý upload media.
* Dùng presigned URL để tải file trực tiếp lên S3.
* Xây dựng event-driven processing với S3 event và Lambda.
* Lưu trữ trạng thái job trong DynamoDB để theo dõi quá trình xử lý.
* Triển khai hạ tầng bằng AWS CDK / CloudFormation.

### Kết quả mong đợi

Sau workshop, bạn sẽ có khả năng xây dựng một pipeline chuyển đổi media an toàn, linh hoạt và mở rộng trên AWS. Bạn cũng hiểu rõ cách các dịch vụ AWS phối hợp với nhau qua diagram để đảm bảo dòng dữ liệu từ upload tới download được xử lý tự động.

