---
title : "Detailed Guide"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Execution Flow

1. Prepare the local source code.
2. Install dependencies for backend, frontend, and iac.
3. Build the frontend locally to confirm there are no errors.
4. Synth the stack to check the CloudFormation template.
5. Deploy the entire system.
6. Run end-to-end using the UI.
7. Run end-to-end using the CLI.

---

## Step 0 - Clone the source and check the structure

```bash
git clone <repo-url>
cd Cloud-Media-Converter-and-Storage-on-AWS
```

Quick check:

```bash
dir
```

You should see at least the following directories:
- backend
- frontend
- iac
- docs

Check the 3 package.json files:

```bash
dir backend\package.json
dir frontend\package.json
dir iac\package.json
```

Expected:
- All package.json files exist.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image.png)

---

## Step 1 - Install backend dependencies

```bash
cd backend
npm install
```

Expected:
- backend/node_modules is created.
- No critical npm errors.

If you hit a Node version error:
- Check `node -v`.
- Install Node 18+ and run `npm install` again.

---

## Step 2 - Install frontend dependencies

```bash
cd ..\frontend
npm install
```

Expected:
- frontend/node_modules is created.

Verify the frontend build right after installing:

```bash
npm run build
```

Expected:
- Build succeeds.
- frontend/dist directory is created.

---

## Step 3 - Install iac dependencies

```bash
cd ..\iac
npm install
```

Expected:
- CDK dependencies installed successfully.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-1.png)

---

## Step 4 - Synth the stack (check before deploying)

```bash
npm run synth
```

Expected:
- Generates the CloudFormation template for 2 stacks:
  - CloudMediaConverterServerlessStack
  - CloudMediaConverterFrontend

If synth fails, resolve in this order:
1. Go back to frontend and rebuild:

```bash
cd ..\frontend
npm run build
```

2. Go back to iac and synth again:

```bash
cd ..\iac
npm run synth
```

3. If it still fails, delete node_modules for each part and reinstall.

The image below shows a successful execution of the npm run synth command
![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-2.png)

---

## Step 5 - Deploy the system

From the iac directory:

```bash
npm run deploy
```

During deployment, CDK will ask for confirmation of IAM/resource changes.
If a prompt appears, confirm to proceed.

After the deployment finishes, record the important outputs:
- ApiUrl
- RawBucketName
- ProcessedBucketName
- JobsTableName
- FrontendUrl

Expected:
- Both the backend stack and the frontend stack deploy successfully.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-3.png)

---

## Step 6 - Check the frontend after deployment

1. Open `FrontendUrl` in a browser.
2. Confirm the page loads.
3. Check that the UI has:
   - a file selection/drag-and-drop area
   - a target format selector
   - a Convert button

If the page loads but API calls don't work:
- Check the CloudFront behavior `/api/*` in [iac/lib/frontend-stack.js](iac/lib/frontend-stack.js).
- Check the API route in [iac/lib/serverless-backend-stack.js](iac/lib/serverless-backend-stack.js).

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-4.png)

---

## Step 7 - Quick check on the AWS Console (matching each step)

After completing the E2E flow, cross-check quickly:

1. API Gateway:
   - Has the route `POST /api/presigned-url`.
   - Has the route `GET /api/job-status/{jobId}`.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-9.png)

2. Lambda:
   - Has the 3 main functions (presigned, status, process-upload).

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-7.png)

3. S3:
   - The raw bucket has the object that was just uploaded.
   - The processed bucket has the output object.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-10.png)
<div align = "center">Object just uploaded to the raw bucket</div>

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-11.png)
<div align = "center">Object successfully converted</div>

4. DynamoDB:
   - The Jobs table has an item with a PK in the form `JOB#<jobId>`.
   - The item's final status is `COMPLETED` or `FAILED`.

![alt text](/fcj-workshop/images/5-Workshop/5.3-S3-vpc/image-12.png)
<div align = "center">Status of the convert job is completed</div>
