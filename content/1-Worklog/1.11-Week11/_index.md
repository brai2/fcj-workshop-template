---
title: "Worklog Week 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Full system testing of WebFood on AWS.
* Verify CloudFront, API Gateway, Lambda, EventBridge, SQS, SES, WebSocket.
* Enable CloudWatch Alarms, X-Ray tracing.
* Complete `DEPLOY_CONSOLE.md` and workshop report documentation.

### Tasks for this week:
| Day | Task | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| 1 | Smoke test frontend via CloudFront; verify API `/api/*`. | 29/06/2026 | 29/06/2026 | https://000045.awsstudygroup.com/ |
| 2 | Test EventBridge → SQS Worker → SES; WebSocket voucher notify. | 30/06/2026 | 30/06/2026 | https://000045.awsstudygroup.com/ |
| 3 | Verify MongoDB Atlas, DynamoDB connections, Secrets Manager. | 01/07/2026 | 01/07/2026 | https://000045.awsstudygroup.com/ |
| 4 | CloudWatch Alarms + SNS; X-Ray traces; complete `DEPLOY_CONSOLE.md`. | 02/07/2026 | 02/07/2026 | https://000045.awsstudygroup.com/ |
| 5 | Team project review; prepare Proposal and Workshop for FCAJ report. | 03/07/2026 | 03/07/2026 | https://000045.awsstudygroup.com/ |

### Week 11 Achievements:

* Successfully tested CloudFront → API Gateway → Lambda → MongoDB flow.
* Confirmed event-driven pipeline: EventBridge, SQS, SES, WebSocket stable.
* Verified WAF, Secrets Manager, DynamoDB connections.
* Enabled CloudWatch/X-Ray and completed deployment documentation.
* Prepared Proposal + Workshop content for Hugo report.
