---
title: "Week 5 Worklog"
date: 2026-10-19
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
- Set up a personal AWS account strictly following security principles and cost governance best practices.
- Practice hands-on operations directly via AWS Management Console: create an S3 bucket, provision an EC2 Linux instance, install an Nginx web server, and tear down resources cleanly.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Created an AWS account and enabled Multi-Factor Authentication (**MFA**) using a virtual MFA app on the **Root User** <br> - Created an administrative **IAM User** (attached `AdministratorAccess` policy) for daily operational tasks, strictly avoiding the use of Root User for routine work | 19/10/2026 | 19/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - Accessed AWS Billing & Cost Management to configure **AWS Budgets** (created a Zero-Spend Budget and email notification thresholds when forecasted spend exceeds $0) <br> - Selected the optimal **AWS Region** for low latency in Vietnam (`ap-southeast-1` - Singapore) | 20/10/2026 | 20/10/2026 | AWS Billing Console |
| Wed | - **Amazon S3 Hands-on:** <br>&emsp; + Created a globally unique S3 bucket with Block All Public Access enabled <br>&emsp; + Uploaded files (images, documents), verified Object URL behavior, downloaded files, and tested creating Presigned URLs for secure temporary file sharing | 21/10/2026 | 21/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Thu | - **Amazon EC2 Hands-on:** <br>&emsp; + Launched an EC2 instance with Ubuntu/Amazon Linux AMI (`t2.micro`/`t3.micro`) and generated a new Key Pair (`.pem`) <br>&emsp; + Configured a Security Group with an inbound SSH rule (Port 22) restricted to personal IP (`My IP`) <br>&emsp; + Successfully established an SSH connection from the local terminal to the EC2 instance | 22/10/2026 | 22/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - **Web Server Deployment & Resource Cleanup:** <br>&emsp; + Updated system packages (`sudo apt update`) and installed **Nginx** on EC2 <br>&emsp; + Modified Security Group inbound rules to allow HTTP (Port 80) from anywhere (`0.0.0.0/0`), successfully viewing the Nginx welcome page via public IP on a browser <br>&emsp; + **Terminated the EC2 instance** and deleted the test S3 bucket to ensure zero unexpected charges | 23/10/2026 | 23/10/2026 | Personal Practice |

### Week 5 Key Outcomes:
- Successfully configured a secure AWS sandbox environment with automated budget alerts.
- Gained initial hands-on experience provisioning a cloud server, connecting remotely via SSH, and serving a public website over Nginx.
- Formed the disciplined habit of auditing active dashboards (EC2, EBS, S3) and properly terminating unused resources after labs.
