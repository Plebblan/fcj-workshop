---
title : "Cleaning Up Resources"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.5. </b> "
---

#### Objectives

* Guide on how to clean up all resources created during the workshop.
* Minimize AWS costs by removing unnecessary resources.
* Ensure no leftover data or unnecessary endpoints remain.

---

#### Resources Deployed

Throughout the workshop, we used AWS CDK (in the `iac` folder) to deploy the following resources:

* **Amazon S3**: a bucket for storing raw files (`RAW_BUCKET_NAME`) and a bucket for storing processed files (`PROCESSED_BUCKET_NAME`).
* **Amazon DynamoDB**: a table for tracking job status (`JOBS_TABLE_NAME`).
* **AWS Lambda**: functions handling the backend logic.
* **Amazon API Gateway**: the endpoint used to communicate with the backend.
* **IAM**: roles and policies enabling Lambda and API Gateway to access the related services.

Since the entire infrastructure is managed as code (IaC) through CDK, cleanup can also be performed automatically with a single command, instead of manually deleting each service through the Console.

---

#### Steps

**Step 1**: Navigate to the infrastructure folder (`iac`):

```bash
cd iac
```

**Step 2**: Run the cleanup command to remove the entire CDK stack and its related resources:

```bash
npm run cleanup
```

This command will tear down the entire previously deployed stack (including the S3 buckets, the DynamoDB table, the Lambda function, the API Gateway, and the associated IAM roles).

**Step 3**: Check the AWS Console to confirm that all resources have been fully removed:

* In **CloudFormation**, confirm that the project's stack no longer appears in the list (or is in the `DELETE_COMPLETE` state).
* In **S3**, verify that both the `RAW_BUCKET_NAME` and `PROCESSED_BUCKET_NAME` buckets no longer exist.
* In **DynamoDB**, verify that the `JOBS_TABLE_NAME` table has been deleted.
* In **Lambda** and **API Gateway**, confirm that no function or endpoint from the project is still active.

{{% notice warning %}}
If an S3 bucket still contains data (raw or processed files) at the time of deletion, the cleanup process may fail because CloudFormation does not automatically delete a bucket that still contains objects. In that case, manually delete all objects inside the bucket first, then re-run `npm run cleanup`.
{{% /notice %}}

---

#### Notes

* It's recommended to perform the cleanup step right after finishing the workshop, or whenever the resources are no longer needed, to avoid unwanted costs.
* You can also check the **Billing & Cost Management** section of the AWS Console a few hours later to confirm that no further costs are being incurred from the deleted resources.
* If you plan to redeploy in the future, simply run `npm run deploy` again inside the `iac` folder; all resources will be recreated, and the bucket/table names will automatically be written into the backend's configuration file.
