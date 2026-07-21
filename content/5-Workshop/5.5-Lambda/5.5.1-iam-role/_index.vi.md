---
title: "IAM Role"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### IAM Role cho Lambda

**Console:** IAM → **Roles** → **Create role** `webfood-lambda-role-prod`

Attach `AWSLambdaBasicExecutionRole`, `AWSXRayDaemonWriteAccess` và inline policy (Secrets Manager, S3, EventBridge, DynamoDB, SES, SQS, WebSocket).

![IAM Role 1](/images/5-Workshop/5.5-Lambda/iam-1.png)

![IAM Role 2](/images/5-Workshop/5.5-Lambda/iam-2.png)

![IAM Role 3](/images/5-Workshop/5.5-Lambda/iam-3.png)

![IAM Role 4](/images/5-Workshop/5.5-Lambda/iam-4.png)

Tiếp theo: [5.5.2 Lambda Functions](../5.5.2-lambda-functions/).
