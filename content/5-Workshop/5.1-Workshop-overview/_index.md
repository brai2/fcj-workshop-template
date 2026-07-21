---
title : "Overview"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Live deployed demo

Reviewers can open the running WebFood system at:

**[https://dh9xhc3jrccu4.cloudfront.net/](https://dh9xhc3jrccu4.cloudfront.net/)**

This is the CloudFront distribution for the project (frontend + API) after completing the workshop steps.

#### Workshop Objectives

After completing this workshop, you will:

- Deploy the full WebFood platform on AWS Serverless.
- Understand the request flow from CloudFront → API Gateway → Lambda → MongoDB Atlas.
- Configure event-driven pipeline: EventBridge → SQS/Worker/SES and WebSocket notify.
- Operate React frontend on S3 + CloudFront with WAF protection.

#### Architecture Overview

WebFood uses a serverless model: no EC2, all compute runs on Lambda. Frontend is a React SPA built statically and hosted on S3, distributed via CloudFront.

![WebFood Architecture](/images/5-Workshop/5.1-Workshop-overview/webfood_architecture.png)

#### Main Processing Flows

1. **Order (REST)**: Browser → CloudFront `/api/*` → API Gateway REST → Lambda `webfood-api` → MongoDB → publish EventBridge.
2. **Email (async)**: EventBridge rule → SQS → Lambda `webfood-worker` → SES sends confirmation email.
3. **Real-time (WebSocket)**: EventBridge rule → Lambda `webfood-ws-notify` → API Gateway WebSocket → client receives voucher/order toast.
4. **WS Connection**: Client opens WebSocket → Lambda `webfood-ws-connect` → saves `connectionId` to DynamoDB.

#### Lambda Functions

| Function | Handler | Role |
|----------|---------|------|
| `webfood-api` | `src/lambda.handler` | REST API (Express app) |
| `webfood-worker` | `src/lambda-worker.handler` | Process SQS, send SES email |
| `webfood-ws-connect` | `src/lambda-ws-connect.handler` | Route `$connect` |
| `webfood-ws-disconnect` | `src/lambda-ws-disconnect.handler` | Route `$disconnect` |
| `webfood-ws-notify` | `src/lambda-ws-notify.handler` | Push message via WebSocket |

#### EventBridge Event Types

- `OrderCreated` — new order
- `OrderStatusChanged` — status update
- `PaymentSucceeded` — successful MoMo payment
- `VoucherPublished` — admin publishes voucher (WebSocket only)

#### Workshop Roadmap

| Section | Contents |
|---------|----------|
| [5.2 Prerequisites](../5.2-Prerequisites/) | Accounts, tools |
| [5.3 Secrets & Storage](../5.3-Secrets-Storage/) | Secrets Manager, S3 |
| [5.4 Data & Messaging](../5.4-Data-Messaging/) | DynamoDB, SQS, EventBridge, SNS |
| [5.5 Lambda](../5.5-Lambda/) | IAM, functions, SQS trigger |
| [5.6 API & Events](../5.6-API-Gateway/) | Rules, REST, WebSocket |
| [5.7 CDN & Operations](../5.7-CDN-Operations/) | WAF, CloudFront, SES, frontend |
| [5.8 Smoke Test](../5.8-Smoke-Test/) | Smoke test |
| [5.9 Teardown](../5.9-Teardown/) | Delete resources |
