---
title: "Week 9 Worklog"
date: 2026-11-16
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:
- Master the **Event-Driven Serverless** architecture mindset on AWS, clearly understanding the differences between traditional server models (EC2/ECS) and serverless models (AWS Lambda).
- Become proficient with **AWS SAM (Serverless Application Model)** to define Infrastructure as Code (IaC), run local emulations on **LocalStack**, and integrate the generative AI service **Amazon Bedrock**.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Deep-dived into **AWS Lambda** architecture (execution lifecycle, *Cold Start* behavior with Java 21, memory/timeout management, concurrency) and **Amazon API Gateway** (HTTP API vs. REST API, ingesting third-party Webhooks) <br> - Studied the **Amazon SQS** message queuing service (Standard vs. FIFO Queues, Visibility Timeout, Dead Letter Queue - DLQ) for asynchronous processing | 16/11/2026 | 16/11/2026 | AWS Serverless Docs |
| Tue | - Studied the NoSQL database **Amazon DynamoDB** (Partition Key, Sort Key, GSI, and On-Demand capacity mode for cost optimization on low-traffic applications) <br> - Explored **AWS SAM CLI**: `template.yaml` structure, defining Lambda, API Gateway, SQS, and DynamoDB resources, and configuring IAM Policies directly within the template | 17/11/2026 | 17/11/2026 | AWS SAM Documentation |
| Wed | - **LocalStack Hands-on Practice:** Installed and configured **LocalStack** alongside `sam local` to test Lambda functions, SQS queues, and DynamoDB tables locally without repeatedly deploying to live AWS | 18/11/2026 | 18/11/2026 | LocalStack Documentation |
| Thu | - Studied **Amazon Bedrock**: invoking Foundation Models (such as Claude/Nova) via the Bedrock Runtime API <br> - Explored **Multimodal** processing capabilities (analyzing text, reading image contents, and extracting file data) to detect scam indicators | 19/11/2026 | 19/11/2026 | Amazon Bedrock Docs |
| Fri | - Analyzed real-world requirements and finalized the architecture for the **Ask First (ScamProtection)** project: justifying the decoupling between the Telegram Webhook ingestion flow (returning `200 OK` immediately in under 3 seconds) and the heavy AI processing flow via an SQS queue | 20/11/2026 | 20/11/2026 | Project Design Docs |

### Week 9 Achievements:
- Mastered the modern Serverless application development workflow using **Java 21** and **AWS SAM**, confidently declaring entire infrastructures as code (`template.yaml`).
- Successfully set up a local development environment with **LocalStack**, shortening testing cycles and avoiding unnecessary costs during development.
- Understood how to integrate **Amazon Bedrock** to analyze conversational context and multimodal content for scam scenario detection.