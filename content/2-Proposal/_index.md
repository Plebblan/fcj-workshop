---
title: "Proposal"
date: 2026-06-06
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Media Converter and Storage on AWS
## Serverless solution for media conversion and storage on AWS

### 1. Executive Summary
The Cloud Media Converter and Storage platform is designed to provide users with a convenient web-based solution for uploading, converting, and storing media files using AWS Cloud services. The system adopts a serverless architecture based on Amazon CloudFront, Amazon API Gateway, AWS Lambda, Amazon S3, and Amazon DynamoDB to reduce infrastructure management requirements, increase scalability, and optimize costs.

Users can submit presigned URL requests via API Gateway, upload files directly to S3, after which Lambda processes the media and saves the output to another S3 bucket. DynamoDB manages job status and provides progress tracking. CloudFront serves the static web interface and static content to users.

### 2. Problem Statement
#### 2.1 Current Problem
Media files nowadays exist in many different formats, and users often need to convert them before sharing, uploading to other systems, or using them within applications. Traditional conversion methods usually require installing specialized software, causing inconvenience and consuming local computer resources.

As file volume and size grow, managing conversion on personal machines becomes inefficient. Users must manually upload, process, and store files. For development teams, traditional server solutions also mean maintaining servers even during low traffic periods.

#### 2.2 Proposed Solution
This platform uses presigned URLs to allow clients to upload files directly to S3 without passing files through the backend. API Gateway handles requests from the web interface and invokes Lambda to generate URLs. When a file is uploaded to S3, an S3 event triggers a media processing Lambda function, saving the converted file into another bucket and updating the job status in DynamoDB.

The architecture diagram includes:
- CloudFront serving static web interface.
- API Gateway receiving requests from browsers.
- Lambda generating upload and download presigned URLs.
- S3 storing raw and converted files.
- Lambda processing media when S3 upload events occur.
- DynamoDB storing job information and processing status.
- Notifications can be sent when jobs complete if needed.

#### 2.3 Benefits and Value
The solution frees users from installing conversion software on personal machines and allows direct media processing in the cloud. The serverless system reduces operational workload because AWS Lambda runs only on demand, while S3 and DynamoDB are fully managed services.

The platform provides value:
- Fast access speed and flexible processing.
- Scalability on demand.
- Reduced infrastructure management costs.
- Practical learning platform for the team on AWS serverless and event-driven architectures.
- Foundation for expanding supported media formats, authentication, file management, and automated deployment.

### 3. Software Architecture
The proposed architecture is based on AWS serverless and event-driven design. Users interact with the web interface, communicating via API Gateway to Lambda. Lambda creates a presigned URL allowing direct file upload to S3. When a file arrives in the raw media bucket, S3 sends an event to the processing Lambda. This Lambda handles conversion and saves results into the processed media bucket. DynamoDB stores job status and metadata.

Main workflow in the diagram:

1. User requests upload presigned URL via API Gateway.
2. Lambda generates upload presigned URL and returns it to the browser.
3. Browser uploads media file to Raw Media bucket on S3.
4. S3 event triggers Processing Lambda.
5. Lambda converts media and saves output to Processed Media bucket.
6. Lambda updates job status in DynamoDB (PENDING → PROCESSING → COMPLETED/FAILED).
7. User can request download presigned URL via API Gateway to download converted file.

**Job State Flow**
- PENDING: Job created.
- PROCESSING: File being processed.
- COMPLETED/FAILED: Processing completed successfully or failed.

The architecture is illustrated in the following diagram:

![Cloud Media Converter Architecture](/fcj-workshop/images/2-Proposal/diagram.png)

#### AWS Services Used
- **Amazon CloudFront**: Distributes static content and web interface.
- **Amazon API Gateway**: Receives requests from frontend and routes to Lambda.
- **AWS Lambda**: Generates presigned URLs, processes upload/download, and performs media conversion.
- **Amazon S3**: Stores original files and converted files.
- **Amazon DynamoDB**: Stores job details, metadata, and processing state.
- **AWS IAM**: Manages access permissions across services.
- **AWS CDK / CloudFormation**: Defines and deploys AWS infrastructure as code.

#### System Components
- **Web Interface**: Allows users to select files, send requests, and track status.
- **API Layer**: API Gateway receives requests and calls Lambda.
- **File Upload**: Lambda creates upload presigned URL so browsers send files directly to S3.
- **Data Storage**: S3 stores raw and converted files.
- **Media Processing**: S3 event triggers processing Lambda for new files.
- **Job Management**: DynamoDB stores job status and metadata.
- **Infrastructure Management**: AWS CDK defines resources and deploys architecture.

### 4. Technical Implementation
#### Implementation Phases
The project is implemented across four phases:
- **Research & Architectural Design**: Study media conversion, AWS services, and draft architecture diagrams.
- **Cost & Feasibility Evaluation**: Use AWS Pricing Calculator to estimate costs and verify practical viability.
- **Architecture Optimization**: Adjust for performance, security, and cost efficiency.
- **Development, Testing & Deployment**: Build Lambda, APIs, web interface, and deploy via CDK.

#### Technical Requirements
- **Media Conversion Platform**: Web app enabling upload and conversion of media files, stored in S3, processed by Lambda.
- **AWS Backend**: Utilizing S3, Lambda, API Gateway, DynamoDB, IAM, and CDK.
- **File Upload**: S3 Presigned URL for uploading files directly to raw media bucket.
- **Job Tracking**: DynamoDB storing status (PENDING, PROCESSING, COMPLETED, FAILED).
- **Infrastructure**: AWS CDK defining resources, allowing easy deployment and reusability.

### 5. Roadmap and Milestones
#### Project Roadmap
- **Internship (Months 1-2)**:
    - **Month 1**: Research requirements, explore AWS services, and design architecture.
    - **Month 2**: Deploy infrastructure, develop backend, media processing workflow, and file management.
- **Post-Deployment**: Monitoring, optimization, bug fixes, and feature expansions.

### 6. Budget Estimation
Estimated costs reference at [AWS Pricing Calculator](https://calculator.aws/).

Actual costs depend on file count, size, conversion frequency, storage capacity, Lambda execution duration, API request volume, and DynamoDB operations.

#### Infrastructure Costs
- **AWS Lambda**: Pay per request count and execution duration.
- **Amazon S3**: Storage fees and request fees for raw/processed buckets.
- **Data Transfer**: Fees based on inbound/outbound data volume.
- **Amazon API Gateway**: Request-based pricing.
- **Amazon DynamoDB**: Pricing based on record count and read/write operations.
- **AWS CDK / CloudFormation**: Infrastructure deployment cost is minimal, with no continuous execution fees.

Total cost will be calculated based on expected workload and actual configuration.

### 7. Risk Assessment
#### Risk Matrix
- **Large media files**: High impact, medium probability.
- **Conversion failure**: High impact, medium probability.
- **Storage growth**: Medium impact, medium probability.
- **Unauthorized access**: High impact, low probability.
- **AWS costs exceeding budget**: Medium impact, low probability.
- **AWS service / network outage**: Medium impact, low probability.

#### Mitigation Strategies
- **Large files**: Use upload presigned URLs to avoid routing files through backend.
- **Conversion failure**: Store state and error info in DynamoDB for monitoring and retries.
- **Storage**: Delete unnecessary files and apply lifecycle policies.
- **Security**: Apply IAM least-privilege and presigned URLs for file access.
- **Costs**: Set up budget alerts and monitor resource usage.
- **Availability**: Utilize managed AWS services and event-driven processing.

#### Contingency Plan
- Retain original files until conversion succeeds.
- Record failed jobs in DynamoDB for investigation and retry.
- Redeploy infrastructure using AWS CDK if necessary.
- Maintain local environment for testing and troubleshooting.
- Restore stable configuration in case of failure.

### 8. Expected Outcomes
#### Technical Improvements
The cloud media conversion platform reduces the need for local desktop processing. The system enables S3 uploads, automated processing, job status tracking, and cloud storage. The architecture easily scales to support multiple users and various media formats.

#### Long-term Value
1. Provides a foundation for future cloud media processing applications.
2. Enhances practical hands-on experience with AWS serverless and event-driven architecture.
3. Provides learning material covering S3, Lambda, API Gateway, DynamoDB, IAM, and CDK.
4. Paves the way for supporting additional media formats and advanced functions.
5. Can integrate authentication, monitoring, and automated deployment.
6. Builds a scalable and reusable architecture for other cloud file processing projects.