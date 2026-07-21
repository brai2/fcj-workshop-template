---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

Before deploying WebFood, prepare the following accounts, tools, and information.

#### 1. AWS Account & Region

- Sign in to [AWS Management Console](https://console.aws.amazon.com).
- Select region **us-east-1** (N. Virginia) — **required** for CloudFront WAF.
- Note your `<ACCOUNT_ID>` (12 digits) from the account menu.

#### 2. Local Environment

| Requirement | Details |
|-------------|---------|
| Node.js | Version **20+** |
| Git | Clone WebFood repository |
| PowerShell / Terminal | `npm install`, `Compress-Archive` |

#### 3. MongoDB Atlas

- MongoDB Atlas cluster (free tier works), database `webappfood`.
- Connection string `mongodb+srv://user:pass@cluster.xxx.mongodb.net/webappfood`.
- **Network Access**: add `0.0.0.0/0`.

#### 4. MoMo Sandbox

- `partnerCode`, `accessKey`, `secretKey`
- Endpoint: `https://test-payment.momo.vn/v2/gateway/api/create`

#### 5. Amazon SES

- 1 **sender** email (FROM_EMAIL) — verify in SES.
- 1 email for **CloudWatch alerts** via SNS.

#### 6. IAM Permissions

Permissions to create/manage: Lambda, API Gateway, S3, CloudFront, WAF, DynamoDB, SQS, EventBridge, SNS, Secrets Manager, IAM Role, CloudWatch.

#### Checklist

- [ ] Region = us-east-1
- [ ] MongoDB Atlas connection string ready
- [ ] MoMo sandbox credentials
- [ ] SES email verified
- [ ] Node.js 20+ installed
- [ ] WebFood source code (`backend/`, `frontend/`) on local machine

Next: [5.3 Secrets & Storage](5.3-Secrets-Storage/).
