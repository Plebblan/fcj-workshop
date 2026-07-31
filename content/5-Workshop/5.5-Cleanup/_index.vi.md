---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.5. </b> "
---

#### Mục tiêu

* Hướng dẫn cách dọn dẹp toàn bộ tài nguyên đã tạo trong workshop.
* Giảm thiểu chi phí AWS bằng cách xóa các tài nguyên thừa.
* Đảm bảo không để lại dữ liệu hoặc endpoint không cần thiết.

---

#### Các tài nguyên đã được triển khai

Trong suốt workshop, chúng ta đã sử dụng AWS CDK (thư mục `iac`) để triển khai các tài nguyên sau:

* **Amazon S3**: bucket lưu trữ file gốc (`RAW_BUCKET_NAME`) và bucket lưu trữ file đã xử lý (`PROCESSED_BUCKET_NAME`).
* **Amazon DynamoDB**: bảng lưu trạng thái xử lý (`JOBS_TABLE_NAME`).
* **AWS Lambda**: các hàm xử lý logic backend.
* **Amazon API Gateway**: endpoint để giao tiếp với backend.
* **IAM**: các role và policy phục vụ cho Lambda, API Gateway truy cập các dịch vụ liên quan.

Do toàn bộ hạ tầng được quản lý dưới dạng mã (IaC) thông qua CDK, việc dọn dẹp cũng sẽ được thực hiện tự động thông qua một lệnh duy nhất, thay vì phải xóa thủ công từng dịch vụ trên Console.

---

#### Các bước thực hiện

**Bước 1**: Di chuyển vào thư mục hạ tầng (`iac`):

```bash
cd iac
```

**Bước 2**: Chạy lệnh dọn dẹp để xóa toàn bộ stack CDK và các tài nguyên liên quan:

```bash
npm run cleanup
```

Lệnh này sẽ gỡ bỏ toàn bộ stack đã được triển khai trước đó (bao gồm S3 bucket, bảng DynamoDB, Lambda function, API Gateway và các IAM role đi kèm).

**Bước 3**: Kiểm tra lại trên AWS Console để đảm bảo các tài nguyên đã được xóa hoàn toàn:

* Vào **CloudFormation**, xác nhận stack của dự án không còn xuất hiện trong danh sách (hoặc đã ở trạng thái `DELETE_COMPLETE`).
* Vào **S3**, kiểm tra hai bucket `RAW_BUCKET_NAME` và `PROCESSED_BUCKET_NAME` đã không còn tồn tại.
* Vào **DynamoDB**, kiểm tra bảng `JOBS_TABLE_NAME` đã bị xóa.
* Vào **Lambda** và **API Gateway**, xác nhận không còn function hay endpoint nào của dự án còn hoạt động.

{{% notice warning %}}
Nếu S3 bucket chứa dữ liệu (file gốc hoặc file đã xử lý) tại thời điểm xóa, quá trình cleanup có thể thất bại do CloudFormation không tự động xóa bucket còn chứa object. Trong trường hợp đó, cần xóa thủ công toàn bộ object bên trong bucket trước, sau đó chạy lại lệnh `npm run cleanup`.
{{% /notice %}}

---

#### Lưu ý

* Nên thực hiện bước dọn dẹp ngay sau khi hoàn tất workshop hoặc khi không còn nhu cầu sử dụng, tránh phát sinh chi phí ngoài ý muốn.
* Có thể kiểm tra thêm mục **Billing & Cost Management** trên AWS Console sau vài giờ để xác nhận không còn chi phí phát sinh từ các tài nguyên đã xóa.
* Nếu dự định triển khai lại trong tương lai, chỉ cần chạy lại `npm run deploy` trong thư mục `iac`; toàn bộ tài nguyên sẽ được tạo mới và tên bucket/bảng sẽ tự động được ghi vào file cấu hình của backend.
