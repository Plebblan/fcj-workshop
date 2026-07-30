---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Media Converter and Storage on AWS
## A Serverless Solution for Media Conversion and Cloud Storage

### 1. Executive Summary
The Cloud Media Converter and Storage platform is designed to provide users with a convenient way to upload, convert, and store media files using AWS Cloud services. The platform uses a serverless architecture based on Amazon S3, AWS Lambda, Amazon API Gateway, and Amazon DynamoDB to provide scalable media processing while minimizing infrastructure management. Users can upload media files through a web interface, monitor the conversion process, and access the converted files through cloud storage.

The system uses Amazon S3 for storing uploaded and converted media files, AWS Lambda for processing conversion tasks, API Gateway for communication between the web application and backend services, and DynamoDB for tracking conversion jobs and their statuses. AWS CDK is used to define and deploy the infrastructure, allowing the architecture to be managed through Infrastructure as Code.

### 2. Problem Statement
### What’s the Problem?
Media files are available in many different formats, and users often need to convert them before sharing, uploading, or using them with other applications. Traditional media conversion usually requires users to install specialized software locally, which can be inconvenient and consumes local storage and computing resources.

When the number and size of files increase, managing the conversion process locally can also become inefficient. Users need to manually upload, process, organize, and store their files. From a development perspective, building a conventional server-based media conversion application also requires maintaining servers even when there are few conversion requests.

### The Solution
The platform uses Amazon S3 to store uploaded and converted media files, AWS Lambda to handle media-processing tasks, Amazon API Gateway to provide communication between the frontend and backend, and Amazon DynamoDB to track conversion jobs and their processing status.

The system uses presigned URLs to allow users to upload files directly to Amazon S3 instead of transferring large files through the backend. After a file is uploaded, an S3 event automatically triggers the processing Lambda function. The function performs the required conversion and stores the resulting file in S3. DynamoDB records the job information and allows users to check the current status of their conversion.

The platform provides a simple workflow similar to other cloud-based file conversion services while focusing on a lightweight and serverless architecture. Key features include direct cloud uploads, automatic media processing, job status tracking, cloud storage, and scalable AWS infrastructure.

### Benefits and Return on Investment
The solution reduces the need for users to install and maintain local media conversion software while providing a centralized platform for managing media files. Users can access the application through a web interface and use cloud resources for file processing and storage.

The serverless architecture also reduces infrastructure management requirements because AWS Lambda runs processing functions only when required. Amazon S3 provides scalable storage, while DynamoDB provides a managed database for conversion jobs. This allows the system to handle increasing workloads without requiring the development team to maintain traditional servers.

The project also provides a practical learning resource for the development team. It allows team members to gain experience with AWS serverless architecture, event-driven systems, cloud storage, Infrastructure as Code, API development, and secure file uploads.

The platform can also serve as a foundation for future development, such as supporting additional media formats, authentication, file management, automated deployment, and more advanced media-processing features.

### 3. Solution Architecture
The platform employs a serverless AWS architecture to manage media uploads, conversion, and cloud storage. Users interact with the web application, which communicates with Amazon API Gateway. Lambda functions handle API requests and media processing, while Amazon S3 stores the original and converted files. DynamoDB stores information about conversion jobs and their current status.

The general workflow is:

**User → API Gateway → Lambda → Presigned S3 URL → S3 → Processing Lambda → Converted File → S3**

The conversion status is managed through:

**Processing Lambda → DynamoDB → API Gateway → User**

The architecture is detailed below:

![Cloud Media Converter Architecture]()

![Cloud Media Converter Workflow]()

### AWS Services Used
- **Amazon S3**: Stores uploaded source media files and converted output files.
- **AWS Lambda**: Generates presigned URLs, processes uploaded media, and handles conversion tasks.
- **Amazon API Gateway**: Facilitates communication between the web application and backend Lambda functions.
- **Amazon DynamoDB**: Stores conversion job information, metadata, and processing status.
- **AWS CDK**: Defines and deploys the AWS infrastructure using Infrastructure as Code.
- **AWS IAM**: Controls permissions and secures access between AWS services.
- **AWS CloudFormation**: Manages the infrastructure generated through AWS CDK.

### Component Design
- **Web Interface**: Provides users with an interface for selecting, uploading, and converting media files.
- **API Layer**: Amazon API Gateway receives requests from the web application and invokes the appropriate Lambda functions.
- **File Upload**: AWS Lambda generates a presigned URL that allows the user to upload the media file directly to Amazon S3.
- **Data Storage**: Amazon S3 stores the original uploaded media and converted output files.
- **Media Processing**: An S3 event triggers the processing Lambda when a new media file is uploaded.
- **Job Management**: Amazon DynamoDB stores job information and allows the system to track conversion progress.
- **Infrastructure Management**: AWS CDK defines the cloud resources and provides a consistent way to deploy the platform.

### 4. Technical Implementation
**Implementation Phases**

This project follows 4 main phases:
- **Build Theory and Draw Architecture**: Research cloud-based media conversion, study AWS services, and design the serverless architecture.
- **Calculate Price and Check Practicality**: Use AWS Pricing Calculator to estimate the expected operating cost and evaluate the practicality of the proposed architecture.
- **Fix Architecture for Cost or Solution Fit**: Optimize the AWS architecture based on performance, scalability, security, and cost requirements.
- **Develop, Test, and Deploy**: Implement the AWS infrastructure with CDK, develop the Lambda functions and web application, integrate all components, and test the system before deployment.

**Technical Requirements**
- **Media Converter Platform**: A web application for uploading and converting media files, with Amazon S3 used for cloud storage and AWS Lambda used for processing.
- **AWS Backend**: Practical knowledge of Amazon S3, Lambda, API Gateway, DynamoDB, IAM, and AWS CDK is required. S3 events are used to automatically trigger media-processing functions after files are uploaded.
- **File Upload System**: Presigned S3 URLs are used to allow users to upload files directly to S3, reducing the amount of data transferred through the backend.
- **Job Tracking**: DynamoDB stores conversion job information and status so that users can monitor whether a file is waiting, processing, completed, or failed.
- **Infrastructure**: AWS CDK is used to define and deploy the required cloud resources, making the architecture easier to maintain and reproduce.

### 5. Timeline & Milestones
**Project Timeline**
- **Pre-Internship (Month 0)**: 1 month for researching media conversion requirements, studying AWS services, and designing the initial architecture.
- **Internship (Months 1-3)**: 3 months.
    - **Month 1**: Study AWS serverless services and implement the initial cloud infrastructure.
    - **Month 2**: Develop the backend, media-processing workflow, file storage, and job tracking system.
    - **Month 3**: Complete the web application, integrate all components, test the system, optimize the architecture, and launch the application.
- **Post-Launch**: Continue improving the platform, monitoring AWS usage, fixing issues, and researching additional media conversion features.

### 6. Budget Estimation
You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/).

The final cost estimation will depend on the number of uploaded files, average file size, conversion frequency, storage duration, Lambda execution time, API requests, DynamoDB operations, and data transfer.

### Infrastructure Costs
- AWS Services:
    - **AWS Lambda**: Cost depends on the number of requests and execution time required for media conversion.
    - **S3 Standard**: Cost depends on the amount of source and converted media stored and the number of storage requests.
    - **Data Transfer**: Cost depends on the amount of media data transferred between AWS and users.
    - **Amazon API Gateway**: Cost depends on the number of API requests.
    - **Amazon DynamoDB**: Cost depends on the number of job records and read/write operations.
    - **AWS CDK / CloudFormation**: Used to manage infrastructure and does not require continuously running application resources.

Total: To be calculated using the AWS Pricing Calculator based on the expected workload.

- **Hardware:** $0 one-time additional hardware cost because the platform operates entirely on AWS Cloud infrastructure.

### 7. Risk Assessment
#### Risk Matrix
- Large Media Files: High impact, medium probability.
- Media Conversion Failures: High impact, medium probability.
- Storage Growth: Medium impact, medium probability.
- Unauthorized File Access: High impact, low probability.
- AWS Cost Overruns: Medium impact, low probability.
- Network or AWS Service Outages: Medium impact, low probability.

#### Mitigation Strategies
- **Large Files**: Use direct uploads to S3 through presigned URLs to avoid transferring large files through the backend.
- **Conversion Failures**: Store conversion status and error information in DynamoDB to allow failed jobs to be identified and handled.
- **Storage**: Regularly remove unnecessary source or converted files and consider lifecycle policies for long-term storage.
- **Security**: Use IAM least-privilege policies and presigned URLs to restrict access to stored media.
- **Cost**: Configure AWS budget alerts and regularly monitor and optimize AWS resource usage.
- **Availability**: Use AWS managed services and event-driven processing to reduce dependency on continuously running servers.

#### Contingency Plans
- Keep the original media file until the conversion has completed successfully.
- Store failed job information in DynamoDB for troubleshooting and retry operations.
- Use AWS CDK to redeploy the infrastructure if a major configuration problem occurs.
- Maintain a local development environment for testing and troubleshooting.
- Revert to a previous stable infrastructure configuration when necessary.

### 8. Expected Outcomes
#### Technical Improvements: 
Cloud-based media conversion replaces the need for users to perform all conversion tasks locally.  
The platform provides direct media uploads, automatic processing, job tracking, and cloud storage.  
The architecture can be extended to support more users, larger numbers of files, and additional media conversion formats.

#### Long-term Value
1. A reusable foundation for future cloud-based media processing applications.
2. Practical experience with AWS serverless and event-driven architecture.
3. A study resource for learning Amazon S3, Lambda, API Gateway, DynamoDB, IAM, and AWS CDK.
4. A foundation for adding more media formats and conversion functions.
5. Potential integration with authentication, monitoring, automated deployment, and advanced media-processing services.
6. A scalable architecture that can be reused for other cloud-based file processing projects.