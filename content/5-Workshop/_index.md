---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Overview

## Introduction

Cloud Media Converting is the process of converting, encoding, and optimizing multimedia content (video, audio, images) using cloud services. In this workshop, we will explore how to build a secure, automated, and scalable media conversion pipeline using storage, compute, event triggers, and content delivery.

## Workshop Objectives

* Understand media conversion architecture on cloud platforms.
* Deploy workflows for upload, conversion, and output storage.
* Optimize media quality and formats for various platforms.
* Protect content using IAM, VPC Endpoints, and access policies.

## Key Benefits

* **Flexible Scalability:** Process multiple media files concurrently without investing in on-premises infrastructure.
* **Automation:** Trigger media conversion via upload events or schedules.
* **Fast Delivery:** Use CDN to serve converted content with low latency.
* **Cost Efficiency:** Pay only for actual resource usage and delete temporary files when no longer needed.

## Basic Architecture

A Cloud Media Converting system typically includes the following components:

1. **Media source:** Media files uploaded to storage such as Amazon S3.
2. **Event trigger:** Upload events or API calls triggering the workflow.
3. **Media conversion:** Transcoding services or compute instances performing encoding and generating output formats.
4. **Output storage:** Storing converted files in various formats and resolutions.
5. **Distribution:** CDN or private endpoints to distribute content.
6. **Monitoring:** Monitoring progress, processing duration, and errors.

## Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Access S3 from VPC](5.3-S3-vpc/)
4. [Access S3 from On-premises Data Center](5.4-S3-onprem/)
5. [VPC Endpoint Policies (Bonus)](5.5-Policy/)
6. [Resource Cleanup](5.6-Cleanup/)