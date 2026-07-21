---
title: "DynamoDB"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

### DynamoDB

**Console:** DynamoDB → **Create table** `webfood-connections-prod`

- Partition key: `connectionId` (String)
- GSI: `byUserId` với partition key `userId`
- Capacity: **On-demand**; bật TTL attribute `ttl`

![DynamoDB 1](/images/5-Workshop/5.4-Data-Messaging/dynamodb-1.png)

![DynamoDB 2](/images/5-Workshop/5.4-Data-Messaging/dynamodb-2.png)

![DynamoDB 3](/images/5-Workshop/5.4-Data-Messaging/dynamodb-3.png)

![DynamoDB 4](/images/5-Workshop/5.4-Data-Messaging/dynamodb-4.png)

Tiếp theo: [5.4.2 SQS](../5.4.2-sqs/).
