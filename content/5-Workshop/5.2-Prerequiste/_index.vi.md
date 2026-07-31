---
title : "Prerequisite"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---




Trước khi tham gia workshop, bạn cần chuẩn bị các phần sau:

- **Tài khoản AWS**
  - Có quyền truy cập vào AWS Management Console và AWS CLI.
  - Nên dùng tài khoản hoặc IAM user riêng cho bài lab, **không sử dụng Root user** để đảm bảo nguyên tắc *least privilege* và dễ dàng thu hồi quyền khi cần.
- **Region**
  - Sử dụng **ap-southeast-1 (Singapore)** để đồng bộ với nội dung workshop.
- **Công cụ**
  - **Node.js 18+** và npm: dùng để build frontend (Vite) và cài đặt AWS CDK CLI. Phiên bản sử dụng trong dự án: Node.js `v24.18.1`, npm `v11.16.0`.
  - **AWS CLI**: cấu hình profile riêng và chạy lệnh deploy.
  - **AWS CDK** / **CloudFormation** / **Terraform**: để định nghĩa và triển khai hạ tầng.
  - **AWS SAM** (nếu có): hỗ trợ triển khai Lambda và local testing.

```bash
node -v
npm -v
```

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image.png)

- **Quyền IAM cần thiết**
  - Quyền để tạo, cập nhật và xóa các dịch vụ AWS sau:
    - S3
    - Lambda
    - API Gateway
    - DynamoDB
    - CloudFormation / CDK
    - IAM (role/policy)
    - CloudWatch Logs
    - CloudFront (nếu dùng giao diện tĩnh)

```bash
aws configure --profile tama-deploy
aws sts get-caller-identity --profile tama-deploy
```

![image 1](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-1.png)

#### IAM permissions

Add the following IAM permission policy to your user account to deploy and run the Cloud Media Converter and Storage workshop.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CloudMediaConverterStoragePermissions",
            "Effect": "Allow",
            "Action": [
                "cloudformation:*",
                "s3:*",
                "lambda:*",
                "apigateway:*",
                "dynamodb:*",
                "iam:PassRole",
                "iam:CreateRole",
                "iam:AttachRolePolicy",
                "iam:PutRolePolicy",
                "iam:CreatePolicy",
                "iam:DeleteRole",
                "iam:DeletePolicy",
                "logs:*",
                "cloudfront:*"
            ],
            "Resource": "*"
        },
        {
            "Sid": "AssumeCDKBootstrapRoles",
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::<AWS_ACCOUNT_ID>:role/cdk-*"
        },
        {
            "Sid": "SSMForCDKBootstrap",
            "Effect": "Allow",
            "Action": "ssm:GetParameter",
            "Resource": "arn:aws:ssm:ap-southeast-1:<AWS_ACCOUNT_ID>:parameter/cdk-bootstrap/*"
        }
    ]
}
```

> Lưu ý: hai statement `AssumeCDKBootstrapRoles` và `SSMForCDKBootstrap` là bắt buộc khi deploy bằng AWS CDK — CDK không deploy trực tiếp bằng credentials của user mà thông qua các **CDK execution role** được tạo lúc bootstrap (`deploy-role`, `file-publishing-role`, `image-publishing-role`, `lookup-role`, `cfn-exec-role`), đồng thời cần đọc version bootstrap qua SSM Parameter Store. Thiếu 1 trong 2 quyền này sẽ gặp lỗi `AccessDeniedException` khi chạy `cdk deploy`.
>
> Với môi trường thực tế, nên áp dụng nguyên tắc least privilege và chỉ cấp quyền cần thiết, giới hạn `Resource` thay vì dùng `*` khi có thể.

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-3.png)

Dưới đây là hình ảnh IAM user (`tama-deploy`) được cấp quyền tạo và quản lý các tài nguyên AWS:

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-4.png)

### Khởi tạo tài nguyên bằng AWS CDK

Workshop này xây dựng hệ thống serverless event-driven dùng CloudFront, API Gateway, Lambda, S3 và DynamoDB.

Trước khi triển khai, đảm bảo bạn đã cài đặt và cấu hình:

- **AWS CLI**: `aws configure` với `region = ap-southeast-1`.
- **IAM user**: có đủ quyền CloudFormation, S3, Lambda, API Gateway, DynamoDB, CloudFront, IAM và CloudWatch Logs (xem policy ở trên).
- **AWS CDK**: đã cài đặt Node.js và CDK CLI (`npm install -g aws-cdk`).
- **Project structure**: có 3 thư mục cần cài package riêng:
  - `iac`: các package CDK / IaC cần thiết.
  - `frontend`: dự án Vite, dùng thư viện frontend.
  - `backend`: Lambda / API backend dùng AWS SDK.

#### Cài package cho từng thư mục

- `frontend` (Vite):
  - `npm install --save vite`
  - `npm install --save-dev @vitejs/plugin-react` (nếu dùng React)
  - `npm install --save-dev typescript` (nếu dùng TypeScript)

- `backend`:
  - `npm install --save @aws-sdk/client-s3 @aws-sdk/s3-request-presigner @aws-sdk/client-dynamodb @aws-sdk/util-dynamodb`

- `iac`:
  - `npm install aws-cdk-lib constructs`
  - `npm install --save-dev typescript ts-node`
  - Thêm các package IaC khác nếu stack dùng thêm dịch vụ cụ thể.

#### Bootstrap và triển khai bằng AWS CDK CLI

1. Cài đặt AWS CDK CLI (nếu chưa có):

```bash
npm install -g aws-cdk
cdk --version
```

2. Khởi tạo môi trường CDK cho account/region hiện tại:

```bash
cdk bootstrap aws://<AWS_ACCOUNT_ID>/ap-southeast-1 --profile tama-deploy
```

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-2.png)

3. Kiểm tra thay đổi synthesize template:

```bash
cdk synth --profile tama-deploy
```

4. Triển khai stack lên AWS:

```bash
cdk deploy --all --profile tama-deploy --require-approval never
```

5. Dọn dẹp resource khi kết thúc workshop:

```bash
cdk destroy --all --profile tama-deploy --force
```

#### Kiểm tra resource sau khi deploy

- S3 bucket raw/processed đã được tạo.
- AWS Lambda function xuất hiện.
- API Gateway có endpoint.
- DynamoDB table tồn tại.
- CloudFront distribution nếu dùng giao diện tĩnh.
- Region hiển thị đúng **Asia Pacific (Singapore)** trên Console.

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-5.png)

> Lưu ý: AWS CDK tạo CloudFormation stack ngầm định để triển khai resource, nên IAM user vẫn cần quyền CloudFormation và quyền tạo các dịch vụ AWS liên quan.
