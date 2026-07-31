---
title : "Tài liệu tham khảo"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

Các tài liệu tham khảo sau được sử dụng trong quá trình nghiên cứu, phát triển, triển khai và xây dựng tài liệu cho workshop.

## 1. Repository của dự án

- **FCAJ Workshop – Intern Report**  
  Repository GitHub chứa source code, tài liệu workshop, cấu hình và các tài nguyên được sử dụng trong dự án.  
  [https://github.com/Plebblan/fcj-workshop](https://github.com/Plebblan/fcj-workshop)

## 2. Tài liệu Amazon Web Services

### Amazon S3

- **Amazon S3 Documentation**  
  Tài liệu tham khảo về Amazon S3, bao gồm bucket, object, lưu trữ dữ liệu, quyền truy cập và các tính năng liên quan.  
  [https://docs.aws.amazon.com/s3/](https://docs.aws.amazon.com/s3/)

- **Download and Upload Objects with Presigned URLs**  
  Được sử dụng để tham khảo cách triển khai presigned URL nhằm cung cấp quyền upload và download tạm thời đối với các object trên Amazon S3.  
  [https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)

### AWS Lambda

- **AWS Lambda Developer Guide**  
  Tài liệu tham khảo về cách tạo, cấu hình, triển khai và thực thi các Lambda function.  
  [https://docs.aws.amazon.com/lambda/](https://docs.aws.amazon.com/lambda/)

- **Using Lambda with API Gateway**  
  Được sử dụng để tham khảo cách tích hợp AWS Lambda với API Gateway và xử lý các HTTP request.  
  [https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)

### Amazon API Gateway

- **Amazon API Gateway Developer Guide**  
  Tài liệu tham khảo về cách tạo API, cấu hình route, tích hợp Lambda, triển khai API và quản lý các API request.  
  [https://docs.aws.amazon.com/apigateway/](https://docs.aws.amazon.com/apigateway/)

- **Tutorial: Create a CRUD HTTP API with Lambda and DynamoDB**  
  Được sử dụng để tham khảo mô hình tích hợp giữa API Gateway, Lambda và DynamoDB trong kiến trúc serverless.  
  [https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html)

### Amazon DynamoDB

- **Amazon DynamoDB Developer Guide**  
  Tài liệu tham khảo về cách tạo bảng, lưu trữ thông tin job, truy vấn dữ liệu và quản lý tài nguyên DynamoDB.  
  [https://docs.aws.amazon.com/amazondynamodb/](https://docs.aws.amazon.com/amazondynamodb/)

### AWS Identity and Access Management (IAM)

- **AWS Identity and Access Management Documentation**  
  Tài liệu tham khảo về IAM user, role, policy, permission và cơ chế kiểm soát quyền truy cập được sử dụng trong workshop.  
  [https://docs.aws.amazon.com/iam/](https://docs.aws.amazon.com/iam/)

### Amazon VPC

- **Amazon VPC Documentation**  
  Tài liệu tham khảo về VPC, subnet, route table, Internet Gateway, security group và VPC endpoint.  
  [https://docs.aws.amazon.com/vpc/](https://docs.aws.amazon.com/vpc/)

- **Gateway Endpoints for Amazon S3 and DynamoDB**  
  Được sử dụng để tham khảo cách thiết lập VPC endpoint nhằm cho phép các tài nguyên trong VPC truy cập Amazon S3 và DynamoDB mà không cần Internet Gateway hoặc NAT device.  
  [https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html)

### Amazon CloudWatch

- **Amazon CloudWatch Documentation**  
  Tài liệu tham khảo về việc giám sát Lambda function, xem log, kiểm tra metric và theo dõi hiệu năng của ứng dụng.  
  [https://docs.aws.amazon.com/cloudwatch/](https://docs.aws.amazon.com/cloudwatch/)

## 3. AWS Architecture và Best Practices

- **AWS Well-Architected Framework**  
  Được sử dụng làm tài liệu tham khảo cho việc thiết kế kiến trúc cloud có tính bảo mật, tin cậy, hiệu quả, tối ưu chi phí và vận hành tốt.  
  [https://docs.aws.amazon.com/wellarchitected/](https://docs.aws.amazon.com/wellarchitected/)

- **AWS Serverless Applications Lens**  
  Tài liệu tham khảo về việc áp dụng các nguyên tắc AWS Well-Architected vào các ứng dụng serverless.  
  [https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/)

- **Establishing Guardrails and Monitoring for Presigned URLs**  
  Tài liệu tham khảo về các nguyên tắc bảo mật, kiểm soát và giám sát khi sử dụng presigned URL với Amazon S3.  
  [https://docs.aws.amazon.com/prescriptive-guidance/latest/presigned-url-best-practices/introduction.html](https://docs.aws.amazon.com/prescriptive-guidance/latest/presigned-url-best-practices/introduction.html)

## 4. Tài liệu phát triển bổ sung

- **AWS Command Line Interface Documentation**  
  Được sử dụng để tham khảo cách tương tác với các AWS service thông qua command line trong quá trình triển khai và kiểm thử.  
  [https://docs.aws.amazon.com/cli/](https://docs.aws.amazon.com/cli/)

- **AWS SDK for JavaScript Documentation**  
  Tài liệu tham khảo về cách tương tác với các AWS service thông qua code JavaScript.  
  [https://docs.aws.amazon.com/sdk-for-javascript/](https://docs.aws.amazon.com/sdk-for-javascript/)

- **FFmpeg Documentation**  
  Được sử dụng làm tài liệu kỹ thuật cho các thao tác xử lý và chuyển đổi media được thực hiện bởi ứng dụng.  
  [https://ffmpeg.org/documentation.html](https://ffmpeg.org/documentation.html)

## 5. Tổng kết

&emsp;Các tài liệu trên cung cấp nền tảng kiến thức kỹ thuật cho quá trình nghiên cứu, thiết kế và triển khai workshop. Tài liệu chính thức của AWS được sử dụng chủ yếu để tìm hiểu về các AWS service, kiến trúc serverless, phương pháp cấu hình, bảo mật và các phương thức tích hợp giữa các service.

&emsp;Repository GitHub của dự án chứa source code, tài liệu workshop và các thành phần triển khai được xây dựng trong quá trình thực hiện dự án.

&emsp;Các tài liệu tham khảo được sử dụng nhằm hỗ trợ quá trình học tập và phát triển. Kiến trúc, implementation, configuration, testing procedure và documentation cuối cùng được điều chỉnh dựa trên yêu cầu và mục tiêu cụ thể của workshop.