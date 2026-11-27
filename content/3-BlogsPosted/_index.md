---
title: "Blogs Posted"
date: 2026-11-26
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Below is the list of in-depth technical blogs authored and shared with the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) community during the internship:

### [Blog 1 - LOCAL SERVERLESS & EVENT-DRIVEN TESTING WITH LOCALSTACK AND JAVA 21](3.1-blog1/)
Details a local-first testing workflow combining LocalStack, Docker, and Java 21 (AWS SDK v2) to thoroughly validate standard event flows and Dead-Letter Queue (DLQ) routing at zero cost before deploying via AWS SAM.

### [Blog 2 - LAMBDA + EVENTBRIDGE: DAILY DATA AUTOMATION WITH EVENT-DRIVEN ARCHITECTURE](3.2-blog2/)
Demonstrates an event-driven serverless architecture on AWS connecting Amazon EventBridge Scheduler, AWS Lambda, and Amazon S3/CloudFront to automatically aggregate and render multi-source data feeds independently in near real-time.

### [Blog 3 - DESIGNING A COST-OPTIMIZED IOT DATA PIPELINE (MQTT → AWS IOT CORE → GLUE → S3) FOR SMALL-SCALE PROJECTS](3.3-blog3/)
Solves the "small files nightmare" in IoT telemetry on AWS: leveraging IoT Core Rule Engine, S3 Lifecycle rules, and AWS Glue ETL to compact millions of small JSON records into columnar Apache Parquet, cutting ~85% in storage footprint and ~98% in Athena query costs.
