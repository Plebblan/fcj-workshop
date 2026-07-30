---
title: "Bản đề xuất"
date: 2026-06-06
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Media Converter and Storage trên AWS
## Giải pháp Serverless cho Chuyển đổi và Lưu trữ Media trên Cloud

### 1. Executive Summary
Nền tảng Cloud Media Converter and Storage được thiết kế nhằm cung cấp cho người dùng một phương thức thuận tiện để tải lên, chuyển đổi và lưu trữ các tệp media bằng các dịch vụ AWS Cloud. Nền tảng sử dụng kiến trúc serverless dựa trên Amazon S3, AWS Lambda, Amazon API Gateway và Amazon DynamoDB nhằm cung cấp khả năng xử lý media có thể mở rộng đồng thời giảm thiểu yêu cầu quản lý cơ sở hạ tầng. Người dùng có thể tải tệp media lên thông qua giao diện web, theo dõi quá trình chuyển đổi và truy cập các tệp đã được chuyển đổi thông qua cloud storage.

Hệ thống sử dụng Amazon S3 để lưu trữ các tệp media được tải lên và các tệp sau khi chuyển đổi, AWS Lambda để thực hiện các tác vụ xử lý và chuyển đổi, API Gateway để giao tiếp giữa ứng dụng web và các dịch vụ backend, và DynamoDB để theo dõi các conversion job cùng trạng thái của chúng. AWS CDK được sử dụng để định nghĩa và triển khai cơ sở hạ tầng, cho phép quản lý kiến trúc bằng Infrastructure as Code.

### 2. Problem Statement
### What’s the Problem?
Các tệp media tồn tại dưới nhiều định dạng khác nhau và người dùng thường cần chuyển đổi chúng trước khi chia sẻ, tải lên hoặc sử dụng với các ứng dụng khác. Phương pháp chuyển đổi media truyền thống thường yêu cầu người dùng cài đặt các phần mềm chuyên dụng trên máy tính, gây bất tiện và tiêu tốn tài nguyên lưu trữ cũng như khả năng xử lý của thiết bị.

Khi số lượng và kích thước tệp tăng lên, việc quản lý quá trình chuyển đổi trên máy tính cá nhân cũng trở nên kém hiệu quả. Người dùng phải tự thực hiện việc tải lên, xử lý, sắp xếp và lưu trữ các tệp. Về phía phát triển hệ thống, việc xây dựng một ứng dụng chuyển đổi media dựa trên server truyền thống cũng yêu cầu duy trì server ngay cả khi số lượng yêu cầu chuyển đổi thấp.

### The Solution
Nền tảng sử dụng Amazon S3 để lưu trữ các tệp media được tải lên và sau khi chuyển đổi, AWS Lambda để xử lý các tác vụ media, Amazon API Gateway để giao tiếp giữa frontend và backend, và Amazon DynamoDB để theo dõi các conversion job cùng trạng thái xử lý của chúng.

Hệ thống sử dụng presigned URL để cho phép người dùng tải tệp trực tiếp lên Amazon S3 thay vì truyền các tệp có kích thước lớn thông qua backend. Sau khi tệp được tải lên, một sự kiện từ S3 sẽ tự động kích hoạt processing Lambda function. Function này thực hiện quá trình chuyển đổi cần thiết và lưu tệp kết quả vào S3. DynamoDB lưu trữ thông tin của job và cho phép người dùng kiểm tra trạng thái chuyển đổi.

Nền tảng cung cấp một quy trình đơn giản tương tự các dịch vụ chuyển đổi tệp trên cloud, đồng thời tập trung vào kiến trúc serverless nhẹ và có khả năng mở rộng. Các tính năng chính bao gồm tải tệp trực tiếp lên cloud, tự động xử lý media, theo dõi trạng thái job, lưu trữ trên cloud và sử dụng cơ sở hạ tầng AWS có khả năng mở rộng.

### Benefits and Return on Investment
Giải pháp giúp giảm nhu cầu người dùng phải cài đặt và duy trì các phần mềm chuyển đổi media trên máy tính cá nhân, đồng thời cung cấp một nền tảng tập trung để quản lý các tệp media. Người dùng có thể truy cập ứng dụng thông qua giao diện web và sử dụng tài nguyên cloud để thực hiện việc xử lý và lưu trữ tệp.

Kiến trúc serverless cũng giúp giảm yêu cầu quản lý cơ sở hạ tầng vì AWS Lambda chỉ thực thi các function xử lý khi có yêu cầu. Amazon S3 cung cấp khả năng lưu trữ có thể mở rộng, trong khi DynamoDB cung cấp cơ sở dữ liệu được quản lý để lưu trữ thông tin các conversion job. Điều này cho phép hệ thống xử lý khối lượng công việc tăng lên mà không yêu cầu nhóm phát triển phải duy trì các server truyền thống.

Dự án cũng cung cấp một môi trường học tập thực tế cho nhóm phát triển. Các thành viên có cơ hội làm việc với kiến trúc AWS serverless, hệ thống event-driven, cloud storage, Infrastructure as Code, phát triển API và cơ chế tải tệp an toàn.

Nền tảng cũng có thể được sử dụng làm cơ sở cho các phát triển trong tương lai như hỗ trợ thêm nhiều định dạng media, authentication, quản lý tệp, automated deployment và các tính năng xử lý media nâng cao.

### 3. Solution Architecture
Nền tảng sử dụng kiến trúc AWS serverless để quản lý quá trình tải lên, chuyển đổi và lưu trữ media. Người dùng tương tác với ứng dụng web, ứng dụng này giao tiếp với Amazon API Gateway. Các Lambda function xử lý các API request và quá trình xử lý media, trong khi Amazon S3 lưu trữ các tệp gốc và tệp sau khi chuyển đổi. DynamoDB lưu trữ thông tin về các conversion job và trạng thái hiện tại của chúng.

Quy trình tổng quát:

**User → API Gateway → Lambda → Presigned S3 URL → S3 → Processing Lambda → Converted File → S3**

Trạng thái chuyển đổi được quản lý thông qua:

**Processing Lambda → DynamoDB → API Gateway → User**

Kiến trúc được mô tả chi tiết bên dưới:

![Cloud Media Converter Architecture](/images/2-Proposal/cloud_media_converter_architecture.jpeg)

![Cloud Media Converter Workflow](/images/2-Proposal/cloud_media_converter_workflow.jpeg)

### AWS Services Used
- **Amazon S3**: Lưu trữ các tệp media gốc được tải lên và các tệp đầu ra sau khi chuyển đổi.
- **AWS Lambda**: Tạo presigned URL, xử lý các tệp media được tải lên và thực hiện các tác vụ chuyển đổi.
- **Amazon API Gateway**: Cung cấp khả năng giao tiếp giữa ứng dụng web và các Lambda function phía backend.
- **Amazon DynamoDB**: Lưu trữ thông tin, metadata và trạng thái xử lý của các conversion job.
- **AWS CDK**: Định nghĩa và triển khai cơ sở hạ tầng AWS bằng Infrastructure as Code.
- **AWS IAM**: Quản lý quyền truy cập và bảo mật giữa các AWS service.
- **AWS CloudFormation**: Quản lý cơ sở hạ tầng được tạo thông qua AWS CDK.

### Component Design
- **Web Interface**: Cung cấp giao diện để người dùng lựa chọn, tải lên và chuyển đổi các tệp media.
- **API Layer**: Amazon API Gateway nhận request từ web application và gọi Lambda function tương ứng.
- **File Upload**: AWS Lambda tạo presigned URL cho phép người dùng tải tệp media trực tiếp lên Amazon S3.
- **Data Storage**: Amazon S3 lưu trữ tệp media gốc và các tệp đã được chuyển đổi.
- **Media Processing**: Sự kiện từ S3 kích hoạt processing Lambda khi một tệp media mới được tải lên.
- **Job Management**: Amazon DynamoDB lưu trữ thông tin job và cho phép hệ thống theo dõi quá trình chuyển đổi.
- **Infrastructure Management**: AWS CDK định nghĩa các cloud resource và cung cấp phương thức nhất quán để triển khai nền tảng.

### 4. Technical Implementation
**Implementation Phases**

Dự án được thực hiện theo 4 giai đoạn chính:
- **Build Theory and Draw Architecture**: Nghiên cứu về chuyển đổi media trên cloud, tìm hiểu các AWS service và thiết kế kiến trúc serverless.
- **Calculate Price and Check Practicality**: Sử dụng AWS Pricing Calculator để ước tính chi phí vận hành và đánh giá tính khả thi của kiến trúc được đề xuất.
- **Fix Architecture for Cost or Solution Fit**: Tối ưu kiến trúc AWS dựa trên các yêu cầu về hiệu năng, khả năng mở rộng, bảo mật và chi phí.
- **Develop, Test, and Deploy**: Triển khai cơ sở hạ tầng AWS bằng CDK, phát triển Lambda function và web application, tích hợp các thành phần và kiểm thử hệ thống trước khi triển khai.

**Technical Requirements**
- **Media Converter Platform**: Một web application cho phép người dùng tải lên và chuyển đổi các tệp media, sử dụng Amazon S3 cho cloud storage và AWS Lambda cho quá trình xử lý.
- **AWS Backend**: Yêu cầu kiến thức thực tế về Amazon S3, Lambda, API Gateway, DynamoDB, IAM và AWS CDK. S3 event được sử dụng để tự động kích hoạt các function xử lý media sau khi tệp được tải lên.
- **File Upload System**: Presigned S3 URL được sử dụng để cho phép người dùng tải tệp trực tiếp lên S3, giúp giảm lượng dữ liệu phải truyền qua backend.
- **Job Tracking**: DynamoDB lưu trữ thông tin và trạng thái của conversion job để người dùng có thể theo dõi tệp đang chờ xử lý, đang xử lý, đã hoàn thành hoặc thất bại.
- **Infrastructure**: AWS CDK được sử dụng để định nghĩa và triển khai các cloud resource cần thiết, giúp kiến trúc dễ bảo trì và tái triển khai.

### 5. Timeline & Milestones
**Project Timeline**
- **Pre-Internship (Month 0)**: 1 tháng nghiên cứu yêu cầu chuyển đổi media, tìm hiểu AWS service và thiết kế kiến trúc ban đầu.
- **Internship (Months 1-3)**: 3 tháng.
    - **Month 1**: Tìm hiểu AWS serverless service và triển khai cơ sở hạ tầng cloud ban đầu.
    - **Month 2**: Phát triển backend, media-processing workflow, hệ thống lưu trữ tệp và job tracking.
    - **Month 3**: Hoàn thiện web application, tích hợp các thành phần, kiểm thử hệ thống, tối ưu kiến trúc và triển khai ứng dụng.
- **Post-Launch**: Tiếp tục cải thiện nền tảng, theo dõi việc sử dụng AWS, sửa lỗi và nghiên cứu thêm các tính năng chuyển đổi media.

### 6. Budget Estimation
Có thể tìm thấy ước tính chi phí trên [AWS Pricing Calculator](https://calculator.aws/).

Chi phí cuối cùng sẽ phụ thuộc vào số lượng tệp được tải lên, kích thước tệp trung bình, tần suất chuyển đổi, thời gian lưu trữ, thời gian thực thi Lambda, số lượng API request, các thao tác DynamoDB và lượng dữ liệu được truyền tải.

### Infrastructure Costs
- AWS Services:
    - **AWS Lambda**: Chi phí phụ thuộc vào số lượng request và thời gian thực thi cần thiết cho quá trình chuyển đổi media.
    - **S3 Standard**: Chi phí phụ thuộc vào lượng media gốc và media sau chuyển đổi được lưu trữ cũng như số lượng storage request.
    - **Data Transfer**: Chi phí phụ thuộc vào lượng dữ liệu media được truyền giữa AWS và người dùng.
    - **Amazon API Gateway**: Chi phí phụ thuộc vào số lượng API request.
    - **Amazon DynamoDB**: Chi phí phụ thuộc vào số lượng job record và các thao tác đọc/ghi.
    - **AWS CDK / CloudFormation**: Được sử dụng để quản lý cơ sở hạ tầng và không yêu cầu tài nguyên ứng dụng phải chạy liên tục.

Total: Sẽ được tính toán bằng AWS Pricing Calculator dựa trên workload dự kiến.

- **Hardware:** $0 chi phí phần cứng bổ sung một lần vì nền tảng hoạt động hoàn toàn trên AWS Cloud.

### 7. Risk Assessment
#### Risk Matrix
- **Large Media Files**: Mức độ ảnh hưởng cao, xác suất trung bình.
- **Media Conversion Failures**: Mức độ ảnh hưởng cao, xác suất trung bình.
- **Storage Growth**: Mức độ ảnh hưởng trung bình, xác suất trung bình.
- **Unauthorized File Access**: Mức độ ảnh hưởng cao, xác suất thấp.
- **AWS Cost Overruns**: Mức độ ảnh hưởng trung bình, xác suất thấp.
- **Network or AWS Service Outages**: Mức độ ảnh hưởng trung bình, xác suất thấp.

#### Mitigation Strategies
- **Large Files**: Sử dụng phương thức tải trực tiếp lên S3 thông qua presigned URL để tránh truyền các tệp lớn qua backend.
- **Conversion Failures**: Lưu trạng thái chuyển đổi và thông tin lỗi trong DynamoDB để xác định và xử lý các job thất bại.
- **Storage**: Thường xuyên xóa các tệp nguồn hoặc tệp đã chuyển đổi không còn cần thiết và cân nhắc sử dụng lifecycle policy cho việc lưu trữ lâu dài.
- **Security**: Sử dụng IAM least-privilege policy và presigned URL để giới hạn quyền truy cập vào các tệp media được lưu trữ.
- **Cost**: Thiết lập AWS budget alert và thường xuyên theo dõi, tối ưu việc sử dụng AWS resource.
- **Availability**: Sử dụng các AWS managed service và event-driven processing để giảm sự phụ thuộc vào các server chạy liên tục.

#### Contingency Plans
- Giữ lại tệp media gốc cho đến khi quá trình chuyển đổi hoàn tất thành công.
- Lưu thông tin các job thất bại trong DynamoDB để phục vụ việc kiểm tra và retry.
- Sử dụng AWS CDK để triển khai lại cơ sở hạ tầng nếu xảy ra vấn đề nghiêm trọng về cấu hình.
- Duy trì môi trường phát triển local để kiểm thử và xử lý sự cố.
- Khôi phục về cấu hình infrastructure ổn định trước đó khi cần thiết.

### 8. Expected Outcomes
#### Technical Improvements: 
Chuyển đổi media trên cloud giúp giảm nhu cầu người dùng phải thực hiện toàn bộ quá trình chuyển đổi trực tiếp trên máy tính cá nhân.  
Nền tảng cung cấp khả năng tải media trực tiếp lên S3, tự động xử lý, theo dõi conversion job và lưu trữ tệp trên cloud.  
Kiến trúc có thể được mở rộng để hỗ trợ nhiều người dùng hơn, số lượng tệp lớn hơn và nhiều định dạng media khác nhau.

#### Long-term Value
1. Cung cấp nền tảng có thể tái sử dụng cho các ứng dụng xử lý media trên cloud trong tương lai.
2. Cung cấp kinh nghiệm thực tế về kiến trúc AWS serverless và event-driven.
3. Làm tài liệu học tập thực tế về Amazon S3, Lambda, API Gateway, DynamoDB, IAM và AWS CDK.
4. Tạo nền tảng để bổ sung thêm nhiều định dạng media và các chức năng chuyển đổi.
5. Có khả năng tích hợp authentication, monitoring, automated deployment và các dịch vụ xử lý media nâng cao.
6. Cung cấp một kiến trúc có khả năng mở rộng và có thể tái sử dụng cho các dự án xử lý tệp trên cloud khác.