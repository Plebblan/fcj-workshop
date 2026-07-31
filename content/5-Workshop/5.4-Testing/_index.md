---
title : "Testing and Validation"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

After successfully deploying the system, testing is performed according to the following steps to verify that the entire workflow operates correctly as designed.

## 1. Sending Requests

Send an actual request to the API to verify the end-to-end workflow.

### 1.1 Generate a Presigned URL

```bash
curl -X POST "<ApiUrl>api/presigned-url" ^
  -H "Content-Type: application/json" ^
  -d "{\"fileName\":\"sample.mp4\",\"targetFormat\":\"webm\"}"
```

Expected response contains `jobId`, `uploadUrl`, and `key`.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image.png)

### 1.2 Upload the File to S3 Using the Presigned URL

```bash
curl -X PUT "<uploadUrl>" ^
  -H "Content-Type: video/mp4" ^
  --data-binary "@sample.mp4"
```

Expected: HTTP `200` or `204`.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-1.png)

### 1.3 Check Job Status

```bash
curl "<ApiUrl>api/job-status/<jobId>"
```

Repeat the request until the `status` changes to `COMPLETED`.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-2.png)

## 2. Checking Logs

Check CloudWatch Logs to verify that each Lambda function is invoked correctly and that there are no runtime errors.

1. Go to **CloudWatch Console → Log groups**.
2. Select the corresponding log group for each function:
   - `/aws/lambda/CloudMediaConverterServer-GetPresignedUrlFunction...`
   - `/aws/lambda/CloudMediaConverterServer-GetJobStatusFunction...`
   - `/aws/lambda/CloudMediaConverterServer-ProcessUploadFunction...`
3. Open the latest **Log stream** and verify:
   - There is a `START RequestId...` and `END RequestId...` entry for each invocation.
   - There are no `ERROR` messages or exception traces in the `ProcessUploadFunction` logs, where the ffmpeg conversion is executed.
   - The Duration and Billed Duration are reasonable and there are no timeouts.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-3.png)

<div align = "center">Valid logs with no timeout or errors</div>

## 3. Checking Metrics

Check CloudWatch Metrics to evaluate system performance and error rates.

1. Go to **CloudWatch → Metrics → Lambda**.
2. For each function, check the following important metrics:
   - **Invocations**: Number of times the function was invoked, which should match the number of test requests sent.
   - **Errors**: Should be `0` after successful testing.
   - **Duration**: Processing time, especially for `ProcessUploadFunction` because the media conversion step is time-consuming.
   - **Throttles**: Should be `0`. A non-zero value indicates that the concurrency limit has been exceeded.
3. For API Gateway, also check:
   - **4XXError** / **5XXError**: Should be `0` for valid requests.
   - **Latency**: Average API response time.

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-4.png)

<div align = "center">The metrics indicate that the function is operating correctly</div>

## 4. Error Testing

Intentionally test error scenarios to verify that the system handles and reports errors correctly, rather than testing only the happy path.

| No. | Test Case | Test Method | Expected Result |
|---|---|---|---|
| 1 | File does not exist when polling status | Call `GET /api/job-status/<non-existent-jobId>` | API returns a `404` error or a clear response indicating that the job cannot be found |
| 2 | Input file is invalid or corrupted | Upload an empty file or a non-media file | `ProcessUploadFunction` sets the job status to `FAILED` and stores a specific `errorMessage` in DynamoDB |
| 3 | Incorrect API method | For example, call `GET /api/presigned-url` instead of `POST` | API Gateway returns `403`/`404` according to the configured route |

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-5.png)

<div align = "center">Result of test case 1</div>

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-6.png)

<div align = "center">Result of test case 2</div>

![alt text](/fcj-workshop/images/5-Workshop/5.4-S3-onprem/image-7.png)

<div align = "center">Result of test case 3</div>

## 5. Expected Results

After completing the testing and validation steps above, the system should meet the following criteria:

- The **happy path** (upload → convert → download) works successfully through both the UI and CLI.
- All Lambda function logs contain **no runtime errors** when processing valid requests.
- **Errors = 0** and **Throttles = 0** during the testing process.
- Error cases are handled correctly: appropriate status codes are returned, and the job is changed to `FAILED` with a clear `errorMessage` instead of causing the system to crash or hang.
- Data in S3 (raw/processed) and DynamoDB (Jobs table) matches the actual results of each test.