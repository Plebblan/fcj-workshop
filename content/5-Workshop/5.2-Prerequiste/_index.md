---
title : "Prerequisites"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---



Before joining the workshop, you need to prepare the following:

- **AWS Account**
  - Have access to the AWS Management Console and AWS CLI.
  - It is recommended to use a dedicated account or IAM user for the lab, **not the Root user**, to follow the *least privilege* principle and make it easier to revoke permissions when needed.
- **Region**
  - Use **ap-southeast-1 (Singapore)** to stay in sync with the workshop content.
- **Tools**
  - **Node.js 18+** and npm: used to build the frontend (Vite) and install the AWS CDK CLI. Version used in this project: Node.js `v24.18.1`, npm `v11.16.0`.
  - **AWS CLI**: configure a dedicated profile and run deployment commands.
  - **AWS CDK** / **CloudFormation** / **Terraform**: to define and provision infrastructure.
  - **AWS SAM** (optional): supports Lambda deployment and local testing.

```bash
node -v
npm -v
```

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image.png)

- **Required IAM Permissions**
  - Permissions to create, update, and delete the following AWS services:
    - S3
    - Lambda
    - API Gateway
    - DynamoDB
    - CloudFormation / CDK
    - IAM (role/policy)
    - CloudWatch Logs
    - CloudFront (if a static frontend is used)

```bash
aws configure --profile tama-deploy
aws sts get-caller-identity --profile tama-deploy
```

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-1.png)

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

> Note: the `AssumeCDKBootstrapRoles` and `SSMForCDKBootstrap` statements are required when deploying with AWS CDK — CDK does not deploy directly using the user's credentials, but instead through the **CDK execution roles** created during bootstrap (`deploy-role`, `file-publishing-role`, `image-publishing-role`, `lookup-role`, `cfn-exec-role`), and it also needs to read the bootstrap version from SSM Parameter Store. Missing either permission will result in an `AccessDeniedException` error when running `cdk deploy`.
>
> In a production environment, apply the least privilege principle and grant only the permissions required, scoping down `Resource` instead of using `*` where possible.

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-3.png)

Below is a screenshot of the IAM user (`tama-deploy`) granted permissions to create and manage AWS resources:

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-4.png)

### Provisioning Resources with AWS CDK

This workshop builds a serverless event-driven system using CloudFront, API Gateway, Lambda, S3, and DynamoDB.

Before deploying, make sure you have installed and configured:

- **AWS CLI**: `aws configure` with `region = ap-southeast-1`.
- **IAM user**: has sufficient permissions for CloudFormation, S3, Lambda, API Gateway, DynamoDB, CloudFront, IAM, and CloudWatch Logs (see the policy above).
- **AWS CDK**: Node.js and the CDK CLI installed (`npm install -g aws-cdk`).
- **Project structure**: 3 directories, each requiring its own packages:
  - `iac`: required CDK / IaC packages.
  - `frontend`: Vite project, using frontend libraries.
  - `backend`: Lambda / API backend using the AWS SDK.

#### Installing packages for each directory

- `frontend` (Vite):
  - `npm install --save vite`
  - `npm install --save-dev @vitejs/plugin-react` (if using React)
  - `npm install --save-dev typescript` (if using TypeScript)

- `backend`:
  - `npm install --save @aws-sdk/client-s3 @aws-sdk/s3-request-presigner @aws-sdk/client-dynamodb @aws-sdk/util-dynamodb`

- `iac`:
  - `npm install aws-cdk-lib constructs`
  - `npm install --save-dev typescript ts-node`
  - Add other IaC packages if the stack uses additional services.

#### Bootstrapping and Deploying with the AWS CDK CLI

1. Install the AWS CDK CLI (if not already installed):

```bash
npm install -g aws-cdk
cdk --version
```

2. Initialize the CDK environment for the current account/region:

```bash
cdk bootstrap aws://<AWS_ACCOUNT_ID>/ap-southeast-1 --profile tama-deploy
```

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-2.png)

3. Review the changes by synthesizing the template:

```bash
cdk synth --profile tama-deploy
```

4. Deploy the stack to AWS:

```bash
cdk deploy --all --profile tama-deploy --require-approval never
```

5. Clean up resources at the end of the workshop:

```bash
cdk destroy --all --profile tama-deploy --force
```

#### Verifying Resources After Deployment

- The raw/processed S3 buckets have been created.
- The AWS Lambda functions appear.
- The API Gateway has an endpoint.
- The DynamoDB table exists.
- The CloudFront distribution, if a static frontend is used.
- The Console displays the correct region: **Asia Pacific (Singapore)**.

![alt text](/fcj-workshop/images/5-Workshop/5.2-Prerequisite/image-5.png)

> Note: AWS CDK implicitly creates a CloudFormation stack to deploy resources, so the IAM user still needs CloudFormation permissions along with permissions to create the related AWS services.
