---
title: "Week 4 Worklog"
date: 2026-10-12
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
- Master the architecture, component concepts, and operational mechanisms of 6 core AWS services: **EC2, S3, RDS, VPC, IAM, and CloudWatch**.
- Be able to read and interpret a complete AWS architecture diagram and explain the function of each service block within the system.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Studied **Amazon EC2 (Elastic Compute Cloud)**: <br>&emsp; + Hardware configuration via **Instance Types** (`t2.micro`, `t3.small`, etc.) and operating systems via **AMIs** (Amazon Machine Images) <br>&emsp; + Securing connections using **Key Pairs** and virtual firewalls via **Security Groups** (Stateful firewall) <br>&emsp; + Persistent storage with **EBS** (Elastic Block Store) and differences in data/billing across **Stop**, **Start**, and **Terminate** states | 12/10/2026 | 12/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - Studied **Amazon S3 (Simple Storage Service)**: <br>&emsp; + Flat storage structure consisting of **Buckets** (globally unique names) and **Objects** (data + metadata + key) <br>&emsp; + Access control mechanisms via Block Public Access, Bucket Policies, and Presigned URLs <br>&emsp; + Data lifecycle management with **Versioning** (retaining multiple versions to prevent accidental deletion) and **Lifecycle Rules** (automatically transitioning objects to lower-cost storage classes like S3 Glacier or expiring old files) | 13/10/2026 | 13/10/2026 | AWS Documentation |
| Wed | - Studied **Amazon RDS (Relational Database Service)**: <br>&emsp; + Benefits of an AWS-managed database service (automated OS patching, scheduled backups) with the **PostgreSQL** engine <br>&emsp; + How applications connect via the DNS **Endpoint** and default **Port 5432** <br>&emsp; + **Automated Backups**, Manual Snapshots, and the importance of disabling **Public Access** to isolate the database | 14/10/2026 | 14/10/2026 | AWS Documentation |
| Thu | - Studied **Amazon VPC (Virtual Private Cloud)**: <br>&emsp; + Designing virtual private network ranges using **CIDR blocks** (e.g., `10.0.0.0/16`) <br>&emsp; + Segmenting **Public Subnets** (with routes pointing to an **Internet Gateway - IGW**, intended for Web Servers/Load Balancers) and **Private Subnets** (not directly exposed to the Internet, intended for internal Databases/Backends) <br>&emsp; + Configuring **Route Tables** and combining **Security Groups** (instance-level) with NACLs (subnet-level) | 15/10/2026 | 15/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - Studied **AWS IAM**: distinguishing **Root User** (full privileges, used only for initial setup), **IAM User** (for human users), **IAM Group** (permission groups), **IAM Role** (granting temporary permissions to AWS services such as EC2 accessing S3 without hardcoding credentials), **Policy** (JSON documents defining `Allow`/`Deny` permissions), the **Least Privilege** principle, and **MFA** (Multi-Factor Authentication) <br> - Studied **Amazon CloudWatch**: collecting **Logs** (application logs), monitoring **Metrics** (CPU, RAM, Network utilization), and configuring automated **Alarms** | 16/10/2026 | 16/10/2026 | AWS Skill Builder |

### Week 4 Achievements:
- Systematized comprehensive theoretical knowledge of the 6 foundational services in the AWS ecosystem.
- Understood how to combine VPC + Security Groups + IAM Roles to implement a multi-layered defense (Defense in Depth) for applications.
- Confidently read and interpreted basic AWS architecture diagrams, tracing data flows and security mechanisms between components.