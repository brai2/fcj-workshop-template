---
title: "EventBridge & SNS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### EventBridge Custom Event Bus

**Console:** EventBridge → **Event buses** → **Create event bus**

| Field | Value |
|-------|-------|
| Name | `webfood-events-prod` |

Click **Create**. 📌 Note the bus **ARN** (`arn:aws:events:us-east-1:<ACCOUNT_ID>:event-bus/webfood-events-prod`).

> Do not create **Rules** yet — Lambda `webfood-ws-notify` does not exist. Configure rules in [5.6.1 EventBridge Rules](../../5.6-API-Gateway/5.6.1-eventbridge-rules/).

![EventBridge 1](/images/5-Workshop/5.4-Data-Messaging/eventbridge-1.png)

![EventBridge 2](/images/5-Workshop/5.4-Data-Messaging/eventbridge-2.png)

### SNS Alert Topic

**Console:** SNS → **Topics** → **Create topic**

| Field | Value |
|-------|-------|
| Type | Standard |
| Name | `webfood-alarms-prod` |

Click **Create topic**. 📌 Note the **ARN**.

**Subscriptions** tab → **Create subscription**:

| Field | Value |
|-------|-------|
| Protocol | Email |
| Endpoint | your CloudWatch alert email |

Click **Create subscription** → open email → **Confirm subscription** (required to receive alerts).

![SNS 1](/images/5-Workshop/5.4-Data-Messaging/sns-1.png)

![SNS 2](/images/5-Workshop/5.4-Data-Messaging/sns-2.png)

![SNS 3](/images/5-Workshop/5.4-Data-Messaging/sns-3.png)

![SNS 4](/images/5-Workshop/5.4-Data-Messaging/sns-4.png)

Next: [5.5 Lambda](../../5.5-Lambda/).
