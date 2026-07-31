---
title : "Hướng dẫn chi tiết"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Sơ đồ bước thực hiện

1. Chuẩn bị source code local.
2. Cài dependencies cho backend, frontend, iac.
3. Build frontend local để xác nhận không lỗi.
4. Synth stack để kiểm tra CloudFormation template.
5. Deploy toàn bộ hệ thống.
6. Chạy end-to-end bằng giao diện.
7. Chạy end-to-end bằng CLI.

---

## Step 0 - Clone source và kiểm tra cấu trúc

```bash
git clone <repo-url>
cd Cloud-Media-Converter-and-Storage-on-AWS
```

Kiểm tra nhanh:

```bash
dir
```

Cần thấy ít nhất các thư mục:
- backend
- frontend
- iac
- docs

Kiểm tra 3 package.json:

```bash
dir backend\package.json
dir frontend\package.json
dir iac\package.json
```

Expected:
- Các file package.json đều tồn tại.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image.png)

---

## Step 1 - Cài dependencies backend

```bash
cd backend
npm install
```

Expected:
- Tạo được backend/node_modules.
- Không có npm error nghiêm trọng.

Nếu lỗi phiên bản Node:
- Kiểm tra `node -v`.
- Đặt Node 18+ rồi chạy lại `npm install`.

---

## Step 2 - Cài dependencies frontend

```bash
cd ..\frontend
npm install
```

Expected:
- Tạo frontend/node_modules.

Kiểm tra build frontend ngay sau khi cài:

```bash
npm run build
```

Expected:
- Build thành công.
- Tạo thư mục frontend/dist.

---

## Step 3 - Cài dependencies iac

```bash
cd ..\iac
npm install
```

Expected:
- Cài đặt CDK dependencies thành công.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-1.png)

---

## Step 4 - Synth stack (kiểm tra trước deploy)

```bash
npm run synth
```

Expected:
- Sinh template CloudFormation cho 2 stack:
  - CloudMediaConverterServerlessStack
  - CloudMediaConverterFrontend

Nếu synth fail, xử lý theo thứ tự:
1. Quay lại frontend và build lại:

```bash
cd ..\frontend
npm run build
```

2. Quay lại iac và synth lại:

```bash
cd ..\iac
npm run synth
```

3. Nếu vẫn lỗi, xóa node_modules từng phần và cài lại.

Hình ảnh dưới đã thực thi thành công lệnh npm run synth 
![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-2.png)

---

## Step 5 - Deploy hệ thống

Tại thư mục iac:

```bash
npm run deploy
```

Trong quá trình deploy, CDK sẽ hỏi xác nhận thay đổi IAM/resource.
Nếu có prompt, chọn xác nhận để tiếp tục.

Sau khi deploy xong, ghi lại các output quan trọng:
- ApiUrl
- RawBucketName
- ProcessedBucketName
- JobsTableName
- FrontendUrl

Expected:
- Deploy thành công cả backend stack và frontend stack.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-3.png)

---

## Step 6 - Kiểm tra frontend sau deploy

1. Mở `FrontendUrl` trên browser.
2. Xác nhận trang load được.
3. Kiểm tra UI có:
   - khu vực chọn/kéo-thả file
   - chọn định dạng đích
   - nút Convert

Nếu vào được trang nhưng không gọi API:
- Kiểm tra CloudFront behavior `/api/*` trong [iac/lib/frontend-stack.js](iac/lib/frontend-stack.js).
- Kiểm tra API route trong [iac/lib/serverless-backend-stack.js](iac/lib/serverless-backend-stack.js).

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-4.png)

---

## Step 7 - Kiểm tra nhanh trên AWS Console (tương ứng từng bước)

Sau khi chạy xong luồng E2E, đối chiếu nhanh:

1. API Gateway:
   - Có route `POST /api/presigned-url`.
   - Có route `GET /api/job-status/{jobId}`.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-9.png)

2. Lambda:
   - Có 3 function chính (presigned, status, process-upload).

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-7.png)

3. S3:
   - Raw bucket có object vừa upload.
   - Processed bucket có object output.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-10.png)
<div align = "center">Object vừa upload trong raw bucket</div>

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-11.png)
<div align = "center">Object vừa convert thành công</div>

4. DynamoDB:
   - Jobs table có item với PK dạng `JOB#<jobId>`.
   - Item có status cuối là `COMPLETED` hoặc `FAILED`.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-12.png)
<div align = "center">Status của job convert là completed</div>

