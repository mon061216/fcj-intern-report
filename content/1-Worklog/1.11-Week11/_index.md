---
title: "Week 11 Worklog"
date: 2026-11-30
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:
- Conduct end-to-end testing of the **Ask First** system's accuracy and stability across multiple input formats and real-world scam scenarios.
- Optimize Java Lambda latency (Cold Start), handle SQS queue failure edge cases, and review Serverless cost efficiency.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Executed End-to-End Testing on Telegram with common scam scenarios: messages impersonating police/banks, forged bank transfer receipts, suspicious files, and voice messages demanding money transfers | 30/11/2026 | 30/11/2026 | Project Practice |
| Tue | - **Performance Optimization & Troubleshooting:** <br>&emsp; + Reduced **Java 21 Lambda** Cold Start duration by optimizing JAR/dependency package sizes and configuring tiered compilation (`JAVA_TOOL_OPTIONS`) <br>&emsp; + Tested the SQS **Dead Letter Queue (DLQ)** mechanism when Bedrock API errors occur or oversized audio/image files are submitted, tracing errors via **CloudWatch Logs** | 01/12/2026 | 01/12/2026 | AWS Lambda Java Best Practices |
| Wed | - Reviewed security and user data privacy: verified automatic media deletion policies on the **S3 Bucket** (S3 Lifecycle Expiration), ensured DynamoDB data encryption at rest, and confirmed Lambda Functions hold only minimum required permissions to designated resources | 02/12/2026 | 02/12/2026 | AWS Well-Architected Framework |
| Thu | - Analyzed operational costs of the Serverless architecture via **AWS Cost Explorer** (comparing pay-per-request pricing across API Gateway, Lambda, SQS, DynamoDB On-Demand, and Amazon Bedrock tokens against running 24/7 EC2/RDS instances) | 03/12/2026 | 03/12/2026 | AWS Pricing & Cost Explorer |
| Fri | - Configured **CloudWatch Alarms** for system health monitoring: triggering immediate alerts whenever messages enter the Dead Letter Queue (DLQ), Lambda error rates exceed thresholds, or Bedrock invocation costs spike unexpectedly | 04/12/2026 | 04/12/2026 | Project Practice |

### Week 11 Achievements:
- Improved bot reliability and response latency on Telegram; thoroughly handled edge cases such as malformed file uploads and queue backlogs.
- Demonstrated the superior cost efficiency of the Serverless architecture for real-world workloads: incurring near-zero cost during idle periods while scaling instantaneously under concurrent message spikes.