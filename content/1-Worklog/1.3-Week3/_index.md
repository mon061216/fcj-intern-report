---
title: "Week 3 Worklog"
date: 2026-10-05
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
- Grasp the mindset shift from physical on-premises infrastructure to Cloud Computing.
- Understand AWS global infrastructure architecture, the Shared Responsibility Model, basic access management mechanisms, and pricing principles.

### Tasks to Implement This Week:
| Day | Task | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Compared **On-premises** and **Cloud Computing** in detail across upfront capital expenditure (CapEx vs. OpEx), deployment speed, scalability, and hardware maintenance <br> - Categorized the 4 core cloud resource pillars: **Compute** (processing power), **Storage** (unstructured/block data storage), **Database** (structured databases), and **Networking** (network connectivity infrastructure) | 05/10/2026 | 05/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Tue | - Analyzed the management boundaries across the 3 service models: **IaaS** (Infrastructure as a Service – e.g., EC2), **PaaS** (Platform as a Service – e.g., Elastic Beanstalk, RDS), and **SaaS** (Software as a Service) <br> - Explored the characteristics and use cases of **Public Cloud**, **Private Cloud**, and **Hybrid Cloud** | 06/10/2026 | 06/10/2026 | AWS Skill Builder |
| Wed | - Distinguished key distributed system design concepts: <br>&emsp; + **Scalability** (upgrading resources vertically via Vertical Scaling or adding nodes horizontally via Horizontal Scaling) vs. **Elasticity** (automatically scaling resources dynamically based on actual traffic) <br>&emsp; + **High Availability** (minimizing downtime) vs. **Fault Tolerance** (ensuring continuous, uninterrupted operation even when a component fails) | 07/10/2026 | 07/10/2026 | AWS Documentation |
| Thu | - Studied AWS global infrastructure components: **AWS Region** (geographically isolated cluster of data centers), **Availability Zone - AZ** (each Region comprises multiple physically isolated AZs connected via ultra-high-speed fiber-optic networks for disaster recovery), and **Edge Location** (edge endpoints serving CloudFront CDN and Route 53 to reduce end-user latency) <br> - Analyzed the **Shared Responsibility Model**: AWS is responsible for security *of* the cloud (hardware, physical infrastructure, virtualization layer), while the customer is responsible for security *in* the cloud (data, source code, network configuration, IAM, guest OS) | 08/10/2026 | 08/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - Explored an overview of **AWS IAM** (Identity and Access Management) for controlling Authentication and Authorization <br> - Researched the primary cost drivers on AWS: Compute time (running hours/seconds), Storage volume (GB/month), Data Transfer Out (outbound Internet traffic), and the **AWS Free Tier** policy | 09/10/2026 | 09/10/2026 | AWS Pricing Calculator |

### Week 3 Achievements:
- Developed a cloud architecture mindset, learning how to deploy resources across multiple Availability Zones (Multi-AZ) to achieve High Availability.
- Clearly defined personal security responsibilities when deploying applications on AWS to avoid common misconfiguration vulnerabilities.
- Understood basic cost estimation and AWS bill optimization principles (shutting down unused resources, leveraging the Free Tier, and minimizing unnecessary Data Transfer Out).s