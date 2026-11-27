---
title: "Week 10 Worklog"
date: 2026-11-23
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:
- Fully develop Backend services using **Java 21** and deploy the Serverless infrastructure on AWS for the **Ask First (ScamProtection)** project.
- Complete the multimodal message processing pipeline (text, images, files, audio) from the Telegram Bot, along with the family-linking and emergency alert features.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Initialized the **Ask First** project structure using Maven, Java 21, and AWS SAM (`template.yaml`) <br> - Designed the **Amazon DynamoDB** table schema to store elderly user profiles, Family Link pairing codes, risk check session history, and alert statuses | 23/11/2026 | 23/11/2026 | Project Practice |
| Tue | - Developed the **Webhook Receiver Lambda** integrated with **API Gateway**: ingested events from the **Telegram Bot API** (supporting local testing via ngrok and live AWS webhooks), validated secret tokens, pushed payloads into **Amazon SQS**, and returned an immediate `200 OK` status to prevent Telegram from retrying duplicate messages | 24/11/2026 | 24/11/2026 | Telegram Bot API Docs |
| Wed | - Developed the **Multimodal Worker Lambda** triggered by SQS events: <br>&emsp; + Downloaded media files (receipt/chat screenshots, attachments, audio files/voice notes) from Telegram servers and stored them securely in **Amazon S3** (configured with short-term Lifecycle auto-deletion to protect user privacy) <br>&emsp; + Transcribed audio to text (Speech-to-Text) and sent multimodal data to **Amazon Bedrock** with specialized prompts to assess scam risk levels | 25/11/2026 | 25/11/2026 | Amazon Bedrock & S3 Docs |
| Thu | - Developed the **Family Linking & Automated Alert** workflow: <br>&emsp; + Built pairing code generation to link an elderly user's Telegram account with a family guardian <br>&emsp; + Triggered automated responses when Bedrock detects high risk: formatting easy-to-understand guidance for the elderly user while simultaneously dispatching detailed alerts with evidence to the family member's Telegram | 26/11/2026 | 26/11/2026 | Project Practice |
| Fri | - Deployed the entire stack to AWS via `sam build` and `sam deploy` <br> - Configured **Environment Variables** / AWS Systems Manager Parameter Store to manage the Telegram Bot Token, assigned IAM Roles to each Lambda following the Least Privilege principle, and verified centralized logs on **CloudWatch** | 27/11/2026 | 27/11/2026 | AWS SAM Deployment |

### Week 10 Achievements:
- Completed the live **Ask First** Serverless Backend system on AWS, seamlessly integrated with the Telegram Bot.
- Enabled elderly users to directly forward text messages, screenshots, files, or voice recordings for scam risk analysis and receive clear, accessible guidance.
- Verified accurate operation of the multi-tiered alert mechanism: reassuring and advising elderly users while promptly notifying family members to intervene.