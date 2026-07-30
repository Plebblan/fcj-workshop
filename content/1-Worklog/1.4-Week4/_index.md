---
title: "Week 4 Worklog"
date: 2026-07-05
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Finalize the overall system architecture and clearly define the responsibilities and tasks of each team member.
* Research AWS Key Management Service (KMS) and understand its role in protecting data.
* Practice creating and managing encryption keys and applying data encryption to the AWS resources used in the project.

### Tasks to be implemented this week:
| Day | Date | Task | Reference Materials |
| --- | ---- | --------- | -------------- |
| 2 | 29/06/2026 | **Finalize System Architecture:**<br>&emsp;+ Update and complete the overall system architecture diagram using draw.io.<br>&emsp;+ Discuss and finalize the Data Flow between the different components of the system. |
| 3 | 30/06/2026 | **Team Task Assignment:**<br>&emsp;+ Conduct a team meeting to divide specific modules and responsibilities among members, including Frontend, Backend, and Infrastructure/AWS.<br>&emsp;+ Set up a shared development environment using a Git repository and AWS IAM Accounts. |
| 4 | 01/07/2026 | **Research AWS KMS (Key Management Service):**<br>&emsp;+ Study the concepts of KMS, AWS Managed Keys, and Customer Managed Keys (CMK).<br>&emsp;+ Learn about data protection mechanisms for data at rest and data in transit.<br>&emsp;+ Research how to create and manage Key Policies to control access to encryption keys. | <https://docs.aws.amazon.com/kms/latest/developerguide/> |
| 5 | 02/07/2026 | **Practice Data Encryption with KMS:**<br>&emsp;+ Create and configure a Customer Managed Key (CMK) through the AWS KMS Console.<br>&emsp;+ **Practice:** Use the KMS key to implement encryption for data stored in an S3 Bucket, EBS Volume, and DynamoDB Table. | <https://docs.aws.amazon.com/kms/latest/developerguide/> |
| 6 | 03/07/2026 | **Weekly Review and Evaluation:**<br>&emsp;+ Test the application's ability to access and use encrypted data.<br>&emsp;+ Review the system architecture and team responsibilities, then update the Week 4 report. |

### Results Achieved in Week 4:

* **System Architecture and Task Assignment:**
  * Completed the system architecture diagram using draw.io, clearly illustrating the relationships and interactions between EC2, S3, DynamoDB, and the security components.
  * Defined and assigned specific responsibilities to each team member while establishing a shared development environment using Git and AWS IAM Roles/Users.

* **Data Security and Key Management with AWS KMS:**
  * Gained a better understanding of data encryption in the Cloud environment, Customer Managed Keys, and Key Policies.
  * Successfully created a Customer Managed Key (CMK) and configured policies to control access to the encryption key.
  * Implemented KMS-based encryption for the S3 Bucket, EBS Volume, and DynamoDB Table, improving the protection of data at rest.