---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploy WebFood on AWS Serverless

This workshop guides you through deploying the **complete** WebFood architecture on AWS Management Console (click-ops) with screenshots for each step. Sections are grouped by **function** for clarity.

> **Live demo (for reviewers):** [https://dh9xhc3jrccu4.cloudfront.net/](https://dh9xhc3jrccu4.cloudfront.net/)  
> Reviewers can open this URL to explore the WebFood system deployed on AWS.

> Required region: **us-east-1** (WAF for CloudFront must be created in us-east-1).

#### Table of Contents

| # | Section | Contents |
|---|---------|----------|
| 5.1 | [Overview](5.1-Workshop-overview/) | Goals, architecture, main flows |
| 5.2 | [Prerequisites](5.2-Prerequisites/) | Accounts, tools, checklist |
| 5.3 | [Secrets & Storage](5.3-Secrets-Storage/) | Secrets Manager, S3 |
| 5.4 | [Data & Messaging](5.4-Data-Messaging/) | DynamoDB, SQS, EventBridge, SNS |
| 5.5 | [Lambda](5.5-Lambda/) | IAM, package code, functions, trigger |
| 5.6 | [API & Events](5.6-API-Gateway/) | EventBridge rules, REST API, WebSocket |
| 5.7 | [CDN & Operations](5.7-CDN-Operations/) | WAF, CloudFront, CloudWatch, SES, frontend |
| 5.8 | [Smoke Test](5.8-Smoke-Test/) | Verify main application flows |
| 5.9 | [Teardown](5.9-Teardown/) | Delete resources to avoid ongoing costs |
