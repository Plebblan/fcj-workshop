---
title: "Week 3 Worklog"
date: 2026-06-28
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Research AWS EC2 Auto Scaling and understand how it can be applied to the group's project.
* Study Amazon S3 and its role in storing media files and other project-related data.
* Research Amazon DynamoDB and evaluate its suitability for storing application metadata.
* Analyze how EC2 Auto Scaling, Amazon S3, and DynamoDB can work together in the Cloud Media Converter and Storage project.
* Continue researching and documenting the project's AWS architecture.

### Tasks to be implemented this week:
| Day | Date | Task | Reference Materials |
| --- | ---- | --------- | ------------------- |
| 2 | 22/06/2026 | Research **EC2 Auto Scaling**, including Auto Scaling Groups, launch templates, scaling policies, and how instances can automatically scale based on workload. Analyze how Auto Scaling could support the media conversion workload of the project. |
| 3 | 23/06/2026 | Research **Amazon S3** and its storage model. Study buckets, objects, storage classes, access control, and how S3 can be used to store uploaded media files and converted output files. |
| 4 | 24/06/2026 | Research **Amazon DynamoDB** and its NoSQL database model. Learn about tables, items, attributes, primary keys, and how DynamoDB can be used to store media conversion metadata and processing status. |
| 5 | 25/06/2026 | Analyze the relationship between **EC2 Auto Scaling, Amazon S3, and DynamoDB** in the project architecture.<br><strong>Practice:</strong><br>&emsp;+ Design a basic workflow for uploading media files to S3.<br>&emsp;+ Define the metadata that should be stored in DynamoDB.<br>&emsp;+ Research how EC2 instances can process conversion tasks.<br>&emsp;+ Consider how Auto Scaling can increase or decrease the number of EC2 instances according to workload. |
| 6 | 26/06/2026 | Review the proposed AWS architecture for the **Cloud Media Converter and Storage** project.<br><strong>Practice:</strong><br>&emsp;+ Identify the role of each AWS service.<br>&emsp;+ Review the data flow between the web application, S3, DynamoDB, and EC2.<br>&emsp;+ Document the architecture and research findings for the project report. |

### Results Achieved in Week 3:

* Gained a better understanding of **Amazon EC2 Auto Scaling** and its role in automatically adjusting computing resources based on application workload.

* Learned about the main components of EC2 Auto Scaling, including:
  * Auto Scaling Groups
  * Launch Templates
  * Minimum and maximum instance capacity
  * Desired capacity
  * Scaling policies
  * Health checks

* Understood how EC2 Auto Scaling can be applied to the project's **media conversion workload**:
  * Increase the number of EC2 instances when the conversion workload increases.
  * Reduce the number of instances when demand decreases.
  * Improve availability by replacing unhealthy instances.
  * Avoid relying on a single EC2 instance for media processing.

* Researched **Amazon S3** and understood its role as object storage for the project.

* Learned the basic concepts of Amazon S3, including:
  * Buckets
  * Objects
  * Object keys
  * Storage classes
  * Access permissions
  * Upload and download operations

* Identified potential S3 storage locations for the project:
  * Uploaded/original media files
  * Converted media files
  * Temporary or intermediate files when required

* Researched **Amazon DynamoDB** and its NoSQL data model.

* Learned the basic components of DynamoDB, including:
  * Tables
  * Items
  * Attributes
  * Partition keys
  * Sort keys
  * Query operations

* Identified DynamoDB as a suitable location for storing **media conversion metadata**, such as:
  * File ID
  * Original file name
  * Input file type
  * Output file type
  * File location
  * Conversion status
  * Upload time
  * Conversion completion time

* Analyzed the relationship between the main AWS services used in the project:
  * **Amazon S3** → Stores uploaded and converted media files.
  * **Amazon DynamoDB** → Stores file metadata and conversion status.
  * **Amazon EC2** → Provides computing resources for media conversion.
  * **EC2 Auto Scaling** → Adjusts the number of EC2 instances according to the workload.

* Developed a better understanding of how storage, database, and compute services can be combined to build a scalable media conversion platform.

* Documented the research findings and used them to further refine the AWS architecture of the **Cloud Media Converter and Storage** project.

* Improved understanding of the importance of selecting AWS services based on:
  * Workload requirements
  * Scalability
  * Reliability
  * Performance
  * Cost
  * Ease of management

* ...