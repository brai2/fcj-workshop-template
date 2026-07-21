---
title: "SQS"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### SQS (DLQ + Queue chính)

Tạo DLQ `webfood-order-events-dlq-prod` trước, sau đó queue chính `webfood-order-events-prod` với Redrive policy (max receives = 3).

📌 Ghi lại **ARN** của cả hai queue.

![SQS 1](/images/5-Workshop/5.4-Data-Messaging/sqs-1.png)

![SQS 2](/images/5-Workshop/5.4-Data-Messaging/sqs-2.png)

![SQS 3](/images/5-Workshop/5.4-Data-Messaging/sqs-3.png)

![SQS 4](/images/5-Workshop/5.4-Data-Messaging/sqs-4.png)

![SQS 5](/images/5-Workshop/5.4-Data-Messaging/sqs-5.png)

Tiếp theo: [5.4.3 EventBridge & SNS](../5.4.3-eventbridge-sns/).
