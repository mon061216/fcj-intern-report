---
title: "Week 7 Worklog"
date: 2026-11-02
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
- Upgrade application architecture from local storage to a decoupled cloud model: offloading relational data to **Amazon RDS** and static files to **Amazon S3**.
- Apply cloud security best practices: attaching an **IAM Role** to EC2 instead of hardcoding access keys, injecting credentials via environment variables, and centralizing logs via **Amazon CloudWatch**.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Provisioned a **PostgreSQL** instance on **Amazon RDS** (selected *No* for Public Access to prevent internet exposure) <br> - Configured **Security Group chaining**: allowed inbound TCP traffic on **Port 5432** originating strictly from the **EC2 Security Group ID** | 02/11/2026 | 02/11/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - Injected database connection strings (RDS Endpoint, DB Name, Username, Password) via **Environment Variables** in the EC2 `systemd` service configuration <br> - Updated ASP.NET Core code using Entity Framework Core / Npgsql, executed database migrations, and verified persistent storage on RDS PostgreSQL | 03/11/2026 | 03/11/2026 | Microsoft EF Core Docs |
| Wed | - Authored a least-privilege **IAM Policy** granting `s3:PutObject` and `s3:GetObject` on the project bucket, plus CloudWatch logging permissions (`logs:CreateLogStream`, `logs:PutLogEvents`) <br> - Created an **IAM Role**, attached the policy, and assigned it to the EC2 instance via *Modify IAM Role* (avoiding storing `AWS_ACCESS_KEY_ID` in code or configs) | 04/11/2026 | 04/11/2026 | AWS IAM Best Practices |
| Thu | - Integrated `AWSSDK.S3` into the Web API, implementing endpoints allowing users to upload file attachments directly to **Amazon S3** while persisting object keys in RDS | 05/11/2026 | 05/11/2026 | AWS SDK for .NET Docs |
| Fri | - Configured logging libraries (`AWS.Logger.AspNetCore` or CloudWatch Agent) to stream application logs from EC2 to **Amazon CloudWatch Logs** <br> - Verified the end-to-end flow: Client calls EC2 API -> writes metadata to RDS -> saves file to S3 -> streams structured logs instantaneously to CloudWatch | 06/11/2026 | 06/11/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 7 Key Outcomes:
- Completed a multi-tier AWS architecture eliminating data loss risks during EC2 instance replacement.
- Heightened system security: database is completely isolated in private subnets, while AWS service authorization is handled via temporary IAM role credentials.
- Enabled centralized observability and log diagnostics via CloudWatch Logs without needing SSH access into individual servers.
