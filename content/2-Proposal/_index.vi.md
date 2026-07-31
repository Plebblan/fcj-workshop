---
title: "Bản đề xuất"
date: 2026-06-06
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Media Converter and Storage trên AWS
## Giải pháp serverless cho chuyển đổi và lưu trữ media trên AWS

### 1. Tóm tắt điều hành
Nền tảng Cloud Media Converter and Storage được thiết kế để cung cấp cho người dùng một giải pháp thuận tiện trên web nhằm tải lên, chuyển đổi và lưu trữ các tệp media bằng các dịch vụ AWS Cloud. Hệ thống ứng dụng kiến trúc serverless dựa trên Amazon CloudFront, Amazon API Gateway, AWS Lambda, Amazon S3 và Amazon DynamoDB để giảm yêu cầu quản lý hạ tầng, tăng khả năng mở rộng và tối ưu chi phí.

Người dùng có thể gửi yêu cầu lấy presigned URL qua API Gateway, tải tệp trực tiếp lên S3, sau đó Lambda xử lý media và lưu kết quả vào vùng S3 khác. DynamoDB quản lý trạng thái job và cung cấp phép theo dõi tiến trình. CloudFront phục vụ giao diện web tĩnh và nội dung tĩnh cho người dùng.

### 2. Giới thiệu vấn đề
#### 2.1 Vấn đề hiện tại
Các tệp media hiện nay tồn tại dưới nhiều định dạng khác nhau và người dùng thường cần phải chuyển đổi chúng trước khi chia sẻ, tải lên hệ thống khác hoặc sử dụng trong ứng dụng. Các phương pháp chuyển đổi truyền thống thường yêu cầu cài phần mềm chuyên dụng, gây phiền phức và tiêu tốn tài nguyên máy tính.

Khi số lượng và kích thước tệp tăng, quản lý chuyển đổi trên máy cá nhân trở nên không hiệu quả. Người dùng phải tự tải lên, xử lý và lưu trữ các tệp. Đối với đội phát triển, giải pháp server truyền thống cũng đồng nghĩa với việc duy trì máy chủ ngay cả khi lưu lượng thấp.

#### 2.2 Giải pháp đề xuất
Nền tảng này sử dụng presigned URL để khách hàng tải tệp trực tiếp tới S3 mà không cần truyền file qua backend. API Gateway xử lý yêu cầu từ giao diện web và gọi Lambda để tạo URL. Khi tệp được tải lên S3, sự kiện S3 kích hoạt Lambda xử lý media, lưu file đã chuyển đổi vào bucket khác và cập nhật trạng thái job trong DynamoDB.

Sơ đồ kiến trúc bao gồm:
- CloudFront phục vụ giao diện web tĩnh.
- API Gateway tiếp nhận yêu cầu từ trình duyệt.
- Lambda tạo presigned URL upload và presigned URL download.
- S3 lưu tệp gốc và tệp đã chuyển đổi.
- Lambda xử lý media khi S3 upload event xảy ra.
- DynamoDB lưu thông tin job và trạng thái xử lý.
- Thông báo có thể được gửi khi job hoàn tất nếu cần.

#### 2.3 Lợi ích và giá trị
Giải pháp giúp người dùng không phải cài đặt phần mềm chuyển đổi trên máy cá nhân và cho phép xử lý file trực tiếp trên cloud. Hệ thống serverless giảm công việc vận hành vì AWS Lambda chỉ chạy khi có yêu cầu, còn S3 và DynamoDB là dịch vụ được quản lý.

Nền tảng cung cấp giá trị:
- Tốc độ truy cập và xử lý linh hoạt.
- Khả năng mở rộng theo nhu cầu.
- Giảm chi phí quản lý hạ tầng.
- Nền tảng học tập thực tế cho team về AWS serverless và event-driven.
- Cơ sở để mở rộng thêm định dạng media, authentication, quản lý file và triển khai tự động.

### 3. Kiến trúc phần mềm
Kiến trúc đề xuất dựa trên AWS serverless và event-driven. Người dùng tương tác với giao diện web, giao tiếp qua API Gateway đến Lambda. Lambda tạo presigned URL cho phép tải file thẳng lên S3. Khi file xuất hiện trong bucket raw media, S3 gửi sự kiện đến Lambda processing. Lambda này xử lý chuyển đổi và lưu kết quả vào bucket processed media. DynamoDB lưu trạng thái job và metadata.

Quy trình chính trong sơ đồ:

1. Người dùng yêu cầu presigned URL tải lên qua API Gateway.
2. Lambda tạo presigned URL upload và trả về cho trình duyệt.
3. Trình duyệt tải tệp lên bucket Raw Media trên S3.
4. Sự kiện S3 kích hoạt Lambda Processing.
5. Lambda chuyển đổi media và lưu kết quả vào bucket Processed Media.
6. Lambda cập nhật trạng thái job trong DynamoDB (PENDING → PROCESSING → COMPLETED/FAILED).
7. Người dùng có thể yêu cầu presigned URL download qua API Gateway để tải tệp đã chuyển đổi.

**Luồng trạng thái job**
- PENDING: Job đã được tạo.
- PROCESSING: File đang được xử lý.
- COMPLETED/FAILED: Kết quả xử lý đã xong hoặc thất bại.

Kiến trúc được mô tả trong sơ đồ sau:

![Cloud Media Converter Architecture](/fcj-workshop/images/2-Proposal/diagram.png)

#### Dịch vụ AWS được sử dụng
- **Amazon CloudFront**: Phân phối nội dung tĩnh và giao diện web.
- **Amazon API Gateway**: Nhận yêu cầu từ frontend và điều phối tới Lambda.
- **AWS Lambda**: Tạo presigned URL, xử lý upload/download và chuyển đổi media.
- **Amazon S3**: Lưu trữ file gốc và file sau khi chuyển đổi.
- **Amazon DynamoDB**: Lưu trữ thông tin job, metadata và trạng thái xử lý.
- **AWS IAM**: Quản lý quyền truy cập cho các dịch vụ.
- **AWS CDK / CloudFormation**: Định nghĩa và triển khai hạ tầng AWS.

#### Thành phần hệ thống
- **Giao diện Web**: Cho phép người dùng chọn file, gửi yêu cầu và theo dõi trạng thái.
- **Lớp API**: API Gateway nhận request và gọi Lambda.
- **Tải file lên**: Lambda tạo presigned URL upload để trình duyệt gửi file thẳng vào S3.
- **Lưu trữ dữ liệu**: S3 lưu file gốc và file đã chuyển đổi.
- **Xử lý media**: S3 event kích hoạt Lambda processing cho file mới.
- **Quản lý job**: DynamoDB lưu trạng thái và metadata của job.
- **Quản lý hạ tầng**: AWS CDK định nghĩa resource và triển khai kiến trúc.

### 4. Triển khai kỹ thuật
#### Các giai đoạn thực hiện
Dự án được triển khai theo bốn giai đoạn:
- **Nghiên cứu và thiết kế kiến trúc**: Tìm hiểu chuyển đổi media, dịch vụ AWS và vẽ sơ đồ kiến trúc.
- **Đánh giá chi phí và tính khả thi**: Dùng AWS Pricing Calculator để ước tính chi phí và kiểm tra khả năng thực tế.
- **Tối ưu kiến trúc**: Điều chỉnh để phù hợp về hiệu năng, bảo mật và chi phí.
- **Phát triển, kiểm thử và triển khai**: Xây dựng Lambda, API, giao diện web và triển khai bằng CDK.

#### Yêu cầu kỹ thuật
- **Nền tảng chuyển đổi media**: Web app cho phép tải lên và chuyển đổi file media, lưu trữ S3, xử lý bằng Lambda.
- **Backend AWS**: Sử dụng S3, Lambda, API Gateway, DynamoDB, IAM và CDK.
- **Tải file**: Presigned URL S3 để tải file trực tiếp lên bucket raw media.
- **Theo dõi job**: DynamoDB lưu trạng thái (PENDING, PROCESSING, COMPLETED, FAILED).
- **Hạ tầng**: AWS CDK định nghĩa resource, triển khai và tái sử dụng dễ dàng.

### 5. Lộ trình và mốc thời gian
#### Lộ trình dự án
- **Thực tập (Tháng 1-2)**:
    - **Tháng 1**: Nghiên cứu yêu cầu, tìm hiểu dịch vụ AWS và thiết kế kiến trúc.
    - **Tháng 2**: Triển khai hạ tầng, phát triển backend, quy trình xử lý media và quản lý file.
- **Sau khi triển khai**: Theo dõi, tối ưu, sửa lỗi và mở rộng tính năng.

### 6. Ước tính ngân sách
Ước tính chi phí tham khảo tại [AWS Pricing Calculator](https://calculator.aws/).

Chi phí thực tế phụ thuộc vào số file, kích thước, tần suất chuyển đổi, dung lượng lưu trữ, thời gian thực thi Lambda, số request API và thao tác DynamoDB.

#### Chi phí hạ tầng
- **AWS Lambda**: Phí theo số request và thời gian thực thi.
- **Amazon S3**: Phí lưu trữ và request cho bucket raw/processed.
- **Data Transfer**: Phí theo lượng dữ liệu vào/ra.
- **Amazon API Gateway**: Phí theo số request.
- **Amazon DynamoDB**: Phí theo số record và thao tác đọc/ghi.
- **AWS CDK / CloudFormation**: Chi phí triển khai hạ tầng rất thấp, không phát sinh chi phí chạy liên tục.

Tổng chi phí sẽ được tính toán dựa trên workload dự kiến và cấu hình thực tế.

### 7. Đánh giá rủi ro
#### Ma trận rủi ro
- **Tệp media lớn**: Ảnh hưởng cao, xác suất trung bình.
- **Chuyển đổi thất bại**: Ảnh hưởng cao, xác suất trung bình.
- **Tăng trưởng lưu trữ**: Ảnh hưởng trung bình, xác suất trung bình.
- **Truy cập trái phép**: Ảnh hưởng cao, xác suất thấp.
- **Chi phí AWS vượt dự toán**: Ảnh hưởng trung bình, xác suất thấp.
- **Ngắt quãng dịch vụ AWS / mạng**: Ảnh hưởng trung bình, xác suất thấp.

#### Giải pháp giảm thiểu
- **Tệp lớn**: Dùng presigned URL upload để tránh truyền qua backend.
- **Thất bại chuyển đổi**: Lưu trạng thái và thông tin lỗi trong DynamoDB để theo dõi và retry.
- **Lưu trữ**: Xóa file không cần thiết và áp dụng lifecycle policy.
- **Bảo mật**: Dùng IAM least-privilege và presigned URL cho truy cập file.
- **Chi phí**: Thiết lập cảnh báo ngân sách và theo dõi sử dụng.
- **Sẵn sàng**: Dùng dịch vụ AWS được quản lý và event-driven processing.

#### Kế hoạch dự phòng
- Giữ file gốc cho đến khi chuyển đổi thành công.
- Lưu job thất bại trong DynamoDB để điều tra và thử lại.
- Triển khai lại hạ tầng bằng AWS CDK nếu cần.
- Duy trì môi trường local để kiểm thử và xử lý sự cố.
- Khôi phục cấu hình ổn định khi xảy ra sự cố.

### 8. Kết quả kỳ vọng
#### Cải tiến kỹ thuật
Nền tảng chuyển đổi media trên cloud giúp giảm nhu cầu xử lý trực tiếp trên máy tính cá nhân. Hệ thống cho phép tải file lên S3, xử lý tự động, theo dõi trạng thái job và lưu trữ kết quả trên cloud. Kiến trúc dễ mở rộng để hỗ trợ nhiều người dùng và nhiều định dạng media.

#### Giá trị lâu dài
1. Cung cấp cơ sở cho các ứng dụng xử lý media trên cloud trong tương lai.
2. Tăng kinh nghiệm thực tế về kiến trúc AWS serverless và event-driven.
3. Cung cấp tài liệu học tập về S3, Lambda, API Gateway, DynamoDB, IAM và CDK.
4. Mở đường cho hỗ trợ thêm định dạng media và chức năng cao cấp.
5. Có thể tích hợp authentication, monitoring và automated deployment.
6. Xây dựng kiến trúc mở rộng và tái sử dụng cho các dự án xử lý file cloud khác.