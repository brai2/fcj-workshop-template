---
title: "SQS"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### SQS (DLQ + Main Queue)

Create DLQ `webfood-order-events-dlq-prod` first, then main queue `webfood-order-events-prod` with Redrive policy (max receives = 3).

📌 Note the **ARN** of both queues.

![SQS 1](/images/5-Workshop/5.4-Data-Messaging/sqs-1.png)

![SQS 2](/images/5-Workshop/5.4-Data-Messaging/sqs-2.png)

![SQS 3](/images/5-Workshop/5.4-Data-Messaging/sqs-3.png)

![SQS 4](/images/5-Workshop/5.4-Data-Messaging/sqs-4.png)

![SQS 5](/images/5-Workshop/5.4-Data-Messaging/sqs-5.png)

Next: [5.4.3 EventBridge & SNS](../5.4.3-eventbridge-sns/).
