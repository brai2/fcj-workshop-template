---
title: "EventBridge Rules"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

### EventBridge Rules

**Console:** EventBridge → **Rules** → select bus `webfood-events-prod` → **Create rule** (twice).

#### Rule 1 — `webfood-to-queue-prod` → SQS Worker

| Field | Value |
|-------|-------|
| Name | `webfood-to-queue-prod` |
| Event bus | `webfood-events-prod` |
| Rule type | Rule with an event pattern |
| Event pattern (JSON) | see below |

```json
{
  "detail-type": ["OrderCreated", "OrderStatusChanged", "PaymentSucceeded"]
}
```

→ Target: **SQS queue** `webfood-order-events-prod` → **Create rule**.

![EventBridge Rule 1](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-1.png)

![EventBridge Rule 2](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-2.png)

![EventBridge Rule 3](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-3.png)

#### Rule 2 — `webfood-to-ws-prod` → Lambda WsNotify

| Field | Value |
|-------|-------|
| Name | `webfood-to-ws-prod` |
| Event bus | `webfood-events-prod` |
| Event pattern (JSON) | see below |

```json
{
  "detail-type": ["OrderCreated", "OrderStatusChanged", "PaymentSucceeded", "VoucherPublished"]
}
```

→ Target: **Lambda function** `webfood-ws-notify` → **Create rule**.

![EventBridge Rule 4](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-4.png)

![EventBridge Rule 5](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-5.png)

![EventBridge Rule 6](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-6.png)

![EventBridge Rule 7](/images/5-Workshop/5.6-API-Gateway/eventbridge-rules-7.png)

> Console adds EventBridge invoke permission automatically. If missing: Lambda `webfood-ws-notify` → **Permissions** → principal `events.amazonaws.com`.

Next: [5.6.2 REST API](../5.6.2-api-rest/).
