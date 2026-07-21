---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, I present the workshop proposal for **WebFood** — an online food ordering platform deployed on AWS Serverless architecture.

# WebFood — Online Food Ordering Platform
## AWS Serverless Solution for F&B E-Commerce

### 1. Executive Summary

WebFood is an online food ordering platform supporting three user roles: **Customer** (browse menu, cart, MoMo payment), **Merchant** (manage products, orders, statistics), and **Admin** (approve restaurants, vouchers, platform finances). The application is built with React (frontend) and Node.js/Express (backend), with business data stored on MongoDB Atlas.

Within the workshop scope, the project is deployed on AWS using a full serverless architecture: CloudFront + WAF for frontend and media delivery, API Gateway REST + Lambda for APIs, API Gateway WebSocket + DynamoDB for real-time notifications, and EventBridge + SQS + Lambda Worker for asynchronous processing (SES email). The solution is suitable for demo/learning environments with low operating costs and request-based scalability.

### 2. Problem Statement

*Current Problem*

Traditional food ordering often relies on phone calls, manual chat, or fragmented systems between customers and restaurants. As the number of restaurants and orders grows, tracking order status, sending notifications, and managing vouchers becomes difficult to control. Deploying on fixed servers (EC2) also requires maintenance costs even without traffic.

*Solution*

WebFood centralizes the ordering flow on a multi-role web platform, combined with MoMo sandbox payment and an event-driven architecture on AWS. When business events occur (order created, status changed, payment succeeded, voucher published), the system publishes events to EventBridge while sending email via SQS/Worker/SES and pushing real-time notifications via WebSocket.

*Benefits and ROI*

- Reduced infrastructure costs through pay-per-use model (Lambda, API Gateway, S3).
- Separation of static frontend (S3/CloudFront) and API backend (Lambda), easier to maintain and scale.
- Event-driven design enables feature extension (email, notifications) without modifying core API.
- Estimated cost of approximately **$8–15/month** for demo workload (see section 6), significantly lower than maintaining EC2 24/7.

### 3. Solution Architecture

WebFood applies serverless architecture per `docs/wedfood.drawio`, deployed in **us-east-1** region (required for WAF on CloudFront).

![WebFood Architecture on AWS](/images/2-Proposal/webfood_architecture.png)

*AWS Services Used*

| Group | Service | Role |
|-------|---------|------|
| Edge | CloudFront, WAF, CloudFront Functions | CDN, protection, SPA routing |
| Storage | S3 (frontend + media) | Host React build, store product images |
| Compute | Lambda (5 functions) | Express API, email worker, WebSocket handlers |
| API | API Gateway REST + WebSocket | REST `/api/*`, real-time `$connect`/`$disconnect` |
| Database | DynamoDB | Store WebSocket connectionId by userId |
| Messaging | EventBridge, SQS + DLQ, SNS | Event bus, worker queue, alerts |
| Security | Secrets Manager, IAM, OAC | JWT/MoMo/MongoDB credentials, bucket policy |
| Observability | CloudWatch, X-Ray | Logs, alarms, distributed tracing |
| Email | SES | Order confirmation, password reset |

*Component Design*

- **Frontend**: React 19 + Vite, static build uploaded to S3, served via CloudFront.
- **ApiFunction** (`webfood-api`): Wraps Express app via `@codegenie/serverless-express`, connects to MongoDB Atlas, publishes events to EventBridge.
- **WorkerFunction** (`webfood-worker`): SQS trigger, sends email via SES on `OrderCreated`, `OrderStatusChanged`, `PaymentSucceeded`.
- **WebSocket Lambdas**: `ws-connect`/`ws-disconnect` manage DynamoDB; `ws-notify` receives EventBridge events, pushes messages to clients.
- **MongoDB Atlas**: Primary database (User, Restaurant, Product, Order, Voucher, etc.) — outside AWS VPC.

### 4. Technical Implementation

*Implementation Phases*

1. **Local development** (Weeks 4–6): React frontend + Express/Mongoose backend, JWT auth, ordering flow, MoMo sandbox integration.
2. **AWS architecture design** (Weeks 7–8): Draw `wedfood.drawio`, write SAM template (`infra/template.yaml`), standardize Lambda handlers.
3. **AWS deployment** (Weeks 9–10): Manual Console deployment per `DEPLOY_CONSOLE.md` (or `sam deploy`) — Secrets Manager, S3, Lambda, API Gateway, CloudFront.
4. **Testing & optimization** (Weeks 11–12): End-to-end smoke test, enable X-Ray, CloudWatch alarms, update CloudFront/MoMo environment variables.

*Technical Requirements*

- **Local**: Node.js 20+, MongoDB, npm for `backend/` and `frontend/`.
- **AWS**: Account with permissions to create Lambda, API Gateway, S3, CloudFront, WAF, EventBridge, DynamoDB, SQS, SES.
- **Third-party**: MongoDB Atlas cluster, MoMo Test account, SES-verified email.
- **IaC**: AWS SAM (`template.yaml`) or Console click-ops for workshop reporting purposes.

### 5. Timeline & Milestones

| Phase | Timeline | Key Milestones |
|-------|----------|----------------|
| Learn AWS basics | Weeks 1–3 (17/04 – 08/05/2026) | Free Tier, EC2, S3, VPC, IAM, CLI |
| Develop WebFood locally | Weeks 4–8 (11/05 – 12/06/2026) | Learn Lightsail, ELB, CloudWatch; design WebFood |
| Design serverless | Weeks 8–9 (08/06 – 19/06/2026) | `wedfood.drawio`, SAM template, Lambda adapter |
| Deploy production | Weeks 9–10 (15/06 – 26/06/2026) | Console deploy, CloudFront live |
| Testing & reporting | Weeks 11–14 (29/06 – 30/07/2026) | Smoke test, workshop doc, Hugo site |

### 6. Budget Estimation

Estimated monthly cost for demo workload (~10,000 API requests, ~5 GB CloudFront transfer):

| Service | Estimated Cost/Month |
|---------|---------------------|
| AWS Lambda (5 functions) | ~$1.50 |
| API Gateway REST + WebSocket | ~$2.00 |
| Amazon CloudFront | ~$2.50 |
| Amazon S3 (frontend + media) | ~$0.50 |
| DynamoDB (on-demand) | ~$0.25 |
| EventBridge + SQS | ~$0.10 |
| AWS WAF | ~$5.00 |
| Amazon SES | ~$0.10 |
| Secrets Manager | ~$0.40 |
| **Total** | **~$12.35/month** (~$148/year) |

View details on [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=webfood-serverless-estimate).

Or download [budget estimation file](../attachments/budget_estimation.pdf).

### 7. Risk Assessment

*Risk Matrix*

| Risk | Impact | Probability |
|------|--------|-------------|
| Lambda cold start | Medium | Medium |
| MongoDB Atlas connection loss | High | Low |
| MoMo sandbox unresponsive | Medium | Low |
| WAF/CloudFront cost exceeds Free Tier | Medium | Medium |
| Lambda zip > 50 MB (node_modules) | Medium | Medium |

*Mitigation Strategies*

- Provisioned concurrency for `webfood-api` if needed (production).
- MongoDB Atlas: IP whitelist, connection pool monitoring.
- CloudWatch billing alarm + SNS notification.
- `npm install --omit=dev` when packaging Lambda; upload via S3 if zip is large.

*Contingency Plan*

- Fallback to local mode (Express + MongoDB) when AWS has issues during demo.
- SAM template (`infra/template.yaml`) for quick stack recreation after teardown.

### 8. Expected Outcomes

*Technical Improvements*

- End-to-end ordering flow: customer places order → API Lambda → EventBridge → SES email + WebSocket voucher toast.
- Centralized administration: admin approves restaurants, merchant updates menu, customer tracks orders in real-time.
- Scalable architecture: add new event types on EventBridge without API refactoring.

*Long-term Value*

- Reference platform for serverless e-commerce projects on AWS.
- Comprehensive hands-on experience: IaC (SAM), event-driven, CDN, WebSocket, observability.
- Can extend to production with Cognito auth, CI/CD pipeline, and multi-region.
