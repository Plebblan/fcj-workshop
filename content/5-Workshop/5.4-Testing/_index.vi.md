---
title : "Kiểm thử và xác thực"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Sau khi deploy thành công, tiến hành kiểm thử hệ thống theo các bước sau để xác nhận toàn bộ luồng hoạt động đúng như thiết kế.

## 1. Gửi request

Gửi thử request thật đến API để kiểm tra luồng hoạt động end-to-end.

### 1.1 Tạo presigned URL

```bash
curl -X POST "<ApiUrl>api/presigned-url" ^
  -H "Content-Type: application/json" ^
  -d "{\"fileName\":\"sample.mp4\",\"targetFormat\":\"webm\"}"
```

Expected response chứa `jobId`, `uploadUrl`, `key`.
![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image.png)

### 1.2 Upload file lên S3 qua presigned URL

```bash
curl -X PUT "<uploadUrl>" ^
  -H "Content-Type: video/mp4" ^
  --data-binary "@sample.mp4"
```

Expected: HTTP `200` hoặc `204`.
![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-1.png)

### 1.3 Kiểm tra trạng thái job

```bash
curl "<ApiUrl>api/job-status/<jobId>"
```

Lặp lại request cho tới khi `status` chuyển thành `COMPLETED`.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-2.png)

## 2. Xem log

Kiểm tra CloudWatch Logs để xác nhận từng Lambda function đã được invoke đúng và không có lỗi runtime.

1. Vào **CloudWatch Console → Log groups**.
2. Chọn log group tương ứng từng function:
   - `/aws/lambda/CloudMediaConverterServer-GetPresignedUrlFunction...`
   - `/aws/lambda/CloudMediaConverterServer-GetJobStatusFunction...`
   - `/aws/lambda/CloudMediaConverterServer-ProcessUploadFunction...`
3. Mở **Log stream** mới nhất, xác nhận:
   - Có dòng `START RequestId...` và `END RequestId...` cho mỗi lần invoke.
   - Không có `ERROR` hoặc exception trace trong log của `ProcessUploadFunction` (nơi thực thi ffmpeg convert).
   - Duration và Billed Duration hợp lý, không bị timeout.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-3.png)

<div align = "center">Log hợp lệ, không có lỗi timeout hoặc error </div>

## 3. Check metric

Kiểm tra CloudWatch Metrics để đánh giá hiệu năng và tỷ lệ lỗi ở mức hệ thống.

1. Vào **CloudWatch → Metrics → Lambda**.
2. Với từng function, kiểm tra các metric quan trọng:
   - **Invocations**: số lần được gọi, khớp với số request test đã gửi.
   - **Errors**: phải bằng `0` sau khi test thành công.
   - **Duration**: thời gian xử lý, đặc biệt chú ý `ProcessUploadFunction` vì có bước convert media tốn thời gian.
   - **Throttles**: phải bằng `0`, nếu có nghĩa là vượt concurrency limit.
3. Với API Gateway, kiểm tra thêm:
   - **4XXError** / **5XXError**: phải bằng `0` cho các request hợp lệ.
   - **Latency**: thời gian phản hồi trung bình của API.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-4.png)
<div align = "center">Số liệu cho thấy rằng function là hợp lệ</div>

## 4. Kiểm thử lỗi

Chủ động thử các trường hợp lỗi để xác nhận hệ thống xử lý và báo lỗi đúng cách, không chỉ test happy path.

|STT| Trường hợp | Cách test | Kết quả mong đợi |
|---|---|---|---|
| 1 | File không tồn tại khi poll status | Gọi `GET /api/job-status/<jobId không tồn tại>` | API trả về lỗi `404` hoặc response rõ ràng báo không tìm thấy job |
| 2 | File input bị lỗi/hỏng | Upload file rỗng hoặc file không phải media | `ProcessUploadFunction` set job status thành `FAILED`, có `errorMessage` cụ thể trong DynamoDB |
| 3 | Gọi API không đúng method | VD: gọi `GET /api/presigned-url` thay vì `POST` | API Gateway trả về `403`/`404` theo đúng cấu hình route |

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-5.png)
<div align = "center">Kết quả của testcase 1</div>

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-6.png)
<div align = "center">Kết quả của testcase 2</div>

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-7.png)
<div align = "center">Kết quả của testcase 3</div>

## 5. Kết quả mong đợi

Sau khi hoàn tất các bước test và validation ở trên, hệ thống cần đạt các tiêu chí sau:

- Luồng **happy path** (upload → convert → download) chạy thành công qua cả UI và CLI.
- Toàn bộ Lambda function log **không có lỗi runtime** khi xử lý request hợp lệ.
- Metric **Errors = 0**, **Throttles = 0** trong quá trình test.
- Các trường hợp lỗi được xử lý đúng: trả về status code phù hợp, job chuyển `FAILED` kèm `errorMessage` rõ ràng thay vì hệ thống bị crash hoặc treo.
- Dữ liệu trong S3 (raw/processed) và DynamoDB (Jobs table) khớp với kết quả thực tế của từng lần test.

