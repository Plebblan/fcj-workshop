---
title: "Week 6 Worklog"
date: 2026-07-19
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Connect the frontend application with the backend services deployed on AWS.
* Integrate the backend with AWS Lambda and other required AWS services.
* Configure AWS IAM permissions and roles to allow secure communication between application components.
* Test the complete application workflow from the frontend through the backend to AWS services.
* Identify and resolve integration, permission, and runtime issues to ensure the system operates correctly.

### Tasks to be implemented this week:
| Day | Date | Task | Reference Materials |
| --- | ---- | --------- | -------------- |
| 2 | 13/07/2026 | **Backend and AWS Integration:**<br>&emsp;+ Review the backend implementation and existing API endpoints.<br>&emsp;+ Connect backend APIs with the required AWS services.<br>&emsp;+ Configure AWS Lambda functions for backend processing.<br>&emsp;+ Verify communication between the backend and Lambda functions. | 
| 3 | 14/07/2026 | **AWS IAM Configuration:**<br>&emsp;+ Review the IAM Roles and Policies required by the backend services.<br>&emsp;+ Configure permissions for accessing AWS resources such as S3, DynamoDB, and Lambda.<br>&emsp;+ Test API requests with the configured IAM permissions.<br>&emsp;+ Identify and resolve permission-related errors. | 
| 4 | 15/07/2026 | **Frontend–Backend Integration:**<br>&emsp;+ Connect the frontend API calls with the deployed backend endpoints.<br>&emsp;+ Test file upload, media conversion requests, file information retrieval, and conversion status updates.<br>&emsp;+ Verify that data is correctly transferred between the frontend, backend, and AWS services. | 
| 5 | 16/07/2026 | **System Testing:**<br>&emsp;+ Test the complete application workflow from user interaction to AWS service processing.<br>&emsp;+ Test successful and failed requests.<br>&emsp;+ Check file upload and storage functionality using Amazon S3.<br>&emsp;+ Verify database operations using DynamoDB.<br>&emsp;+ Test Lambda execution and backend responses. | P
| 6 | 17/07/2026 | **Debugging and Final Integration:**<br>&emsp;+ Identify and fix integration issues found during testing.<br>&emsp;+ Review IAM permissions, API responses, and AWS service configurations.<br>&emsp;+ Perform end-to-end testing again after applying fixes.<br>&emsp;+ Confirm that the main application features are working correctly.<br>&emsp;+ Update project documentation and Week 6 worklog. | 

### Results Achieved in Week 6:

* **AWS Backend Integration:**
  * Connected the frontend application to the backend services through the defined API endpoints.
  * Integrated the backend with AWS Lambda for server-side processing.
  * Verified communication between the backend and the required AWS services.

* **IAM Configuration and Security:**
  * Reviewed and configured the IAM Roles and Policies required by the application.
  * Provided the necessary permissions for backend services to interact with resources such as S3, DynamoDB, and Lambda.
  * Tested access permissions and resolved authorization issues encountered during integration.

* **Frontend and Backend Connection:**
  * Successfully connected the frontend API calls with the backend endpoints.
  * Tested the main application workflows, including:
    * Uploading media files.
    * Sending conversion requests.
    * Retrieving file information.
    * Checking conversion status.
    * Accessing converted files.

* **AWS Service Testing:**
  * Tested Amazon S3 operations to ensure that uploaded and converted files were stored and retrieved correctly.
  * Verified DynamoDB operations for storing and retrieving application metadata.
  * Tested AWS Lambda functions and checked their responses through the backend.
  * Confirmed that the different AWS components could communicate correctly through the backend layer.

* **System Testing and Debugging:**
  * Performed end-to-end testing of the application from the frontend to the backend and AWS services.
  * Identified issues related to API communication, IAM permissions, AWS configuration, and application behavior.
  * Fixed integration issues and repeated testing to verify that the applied changes worked correctly.

* **Overall Project Progress:**
  * Established a functional connection between the frontend, backend, and AWS infrastructure.
  * Improved the stability and reliability of the application through integration and end-to-end testing.
  * Confirmed that the main components of the Cloud Media Converter and Storage system can operate together as an integrated application.
  * Prepared the project for further optimization, testing, and deployment activities.

* ...