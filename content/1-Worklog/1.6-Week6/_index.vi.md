---
title: "Worklog Tuần 6"
date: 2026-07-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Kết nối ứng dụng frontend với các dịch vụ backend được triển khai trên AWS.
* Tích hợp backend với AWS Lambda và các AWS service cần thiết cho dự án.
* Cấu hình AWS IAM Roles và Permissions để đảm bảo các thành phần trong hệ thống có thể giao tiếp một cách an toàn.
* Kiểm thử toàn bộ quy trình của ứng dụng, từ frontend thông qua backend đến các AWS service.
* Xác định và khắc phục các lỗi liên quan đến tích hợp, quyền truy cập và quá trình thực thi để đảm bảo hệ thống hoạt động ổn định.

### Các công việc cần triển khai trong tuần này:
| Thứ | Ngày | Công việc | Nguồn tài liệu |
| --- | ---- | --------- | -------------- |
| 2 | 13/07/2026 | **Tích hợp Backend với AWS:**<br>&emsp;+ Kiểm tra phần backend và các API endpoint đã xây dựng.<br>&emsp;+ Kết nối các API của backend với những AWS service cần thiết.<br>&emsp;+ Cấu hình các AWS Lambda function phục vụ quá trình xử lý backend.<br>&emsp;+ Kiểm tra khả năng giao tiếp giữa backend và Lambda. | 
| 3 | 14/07/2026 | **Cấu hình AWS IAM:**<br>&emsp;+ Kiểm tra các IAM Role và Policy cần thiết cho backend service.<br>&emsp;+ Cấu hình quyền truy cập đến các tài nguyên như S3, DynamoDB và Lambda.<br>&emsp;+ Kiểm tra các API request với IAM permission đã cấu hình.<br>&emsp;+ Xác định và khắc phục các lỗi liên quan đến quyền truy cập. | 
| 4 | 15/07/2026 | **Tích hợp Frontend và Backend:**<br>&emsp;+ Kết nối các API call từ frontend với các backend endpoint đã triển khai.<br>&emsp;+ Kiểm thử chức năng upload file, gửi yêu cầu chuyển đổi media, lấy thông tin file và cập nhật trạng thái chuyển đổi.<br>&emsp;+ Kiểm tra dữ liệu được truyền chính xác giữa frontend, backend và các AWS service. |
| 5 | 16/07/2026 | **Kiểm thử Hệ thống:**<br>&emsp;+ Kiểm tra toàn bộ quy trình từ thao tác của người dùng đến quá trình xử lý trên AWS service.<br>&emsp;+ Kiểm thử các request thành công và thất bại.<br>&emsp;+ Kiểm tra chức năng upload và lưu trữ file thông qua Amazon S3.<br>&emsp;+ Kiểm tra các thao tác với DynamoDB.<br>&emsp;+ Kiểm tra quá trình thực thi của Lambda và response từ backend. |
| 6 | 17/07/2026 | **Debug và Hoàn thiện Tích hợp:**<br>&emsp;+ Xác định và sửa các lỗi phát hiện trong quá trình kiểm thử.<br>&emsp;+ Rà soát IAM permission, API response và cấu hình các AWS service.<br>&emsp;+ Thực hiện lại kiểm thử end-to-end sau khi hoàn thành các thay đổi.<br>&emsp;+ Xác nhận các chức năng chính của ứng dụng hoạt động chính xác.<br>&emsp;+ Cập nhật tài liệu dự án và worklog tuần 6. |

### Kết quả đạt được tuần 6:

* **Tích hợp Backend với AWS:**
  * Kết nối ứng dụng frontend với các backend service thông qua các API endpoint đã được xây dựng.
  * Tích hợp backend với AWS Lambda để thực hiện các tác vụ xử lý phía server.
  * Kiểm tra khả năng giao tiếp giữa backend và các AWS service cần thiết.

* **Cấu hình IAM và Bảo mật:**
  * Kiểm tra và cấu hình các IAM Role và Policy cần thiết cho ứng dụng.
  * Cấp các quyền cần thiết để backend có thể tương tác với các tài nguyên như S3, DynamoDB và Lambda.
  * Kiểm tra quyền truy cập và xử lý các lỗi authorization phát sinh trong quá trình tích hợp.

* **Kết nối Frontend và Backend:**
  * Kết nối thành công các API call từ frontend với các backend endpoint.
  * Kiểm thử các luồng chức năng chính của ứng dụng, bao gồm:
    * Upload file media.
    * Gửi yêu cầu chuyển đổi.
    * Lấy thông tin file.
    * Kiểm tra trạng thái chuyển đổi.
    * Truy cập các file đã được chuyển đổi.

* **Kiểm thử AWS Service:**
  * Kiểm tra các thao tác với Amazon S3 để đảm bảo file được upload và file sau khi chuyển đổi được lưu trữ và truy xuất chính xác.
  * Kiểm tra các thao tác với DynamoDB để đảm bảo metadata của ứng dụng được lưu trữ và lấy ra đúng cách.
  * Kiểm thử AWS Lambda và kiểm tra response được trả về thông qua backend.
  * Xác nhận các thành phần AWS khác nhau có thể giao tiếp chính xác thông qua backend layer.

* **Kiểm thử và Debug Hệ thống:**
  * Thực hiện kiểm thử end-to-end từ frontend đến backend và các AWS service.
  * Xác định các vấn đề liên quan đến API communication, IAM permission, cấu hình AWS và hoạt động của ứng dụng.
  * Khắc phục các lỗi tích hợp và thực hiện kiểm thử lại để đảm bảo các thay đổi hoạt động chính xác.

* **Tiến độ Dự án:**
  * Thiết lập thành công kết nối giữa frontend, backend và hạ tầng AWS.
  * Cải thiện tính ổn định và độ tin cậy của ứng dụng thông qua quá trình tích hợp và kiểm thử end-to-end.
  * Xác nhận các thành phần chính của hệ thống Cloud Media Converter and Storage có thể hoạt động cùng nhau như một ứng dụng hoàn chỉnh.
  * Chuẩn bị dự án cho các công việc tiếp theo như tối ưu hóa, kiểm thử bổ sung và triển khai.

* ...