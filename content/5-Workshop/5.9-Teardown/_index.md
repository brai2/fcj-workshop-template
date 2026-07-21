---
title: "Teardown"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Teardown — Resource Cleanup

When no longer needed (avoid ongoing costs), delete in **reverse** deploy order:

1. CloudFront Distribution (disable → delete, wait for deployed)
2. WAF WebACL
3. API Gateway REST + WebSocket
4. Lambda functions (5)
5. EventBridge rules + event bus
6. SQS queues + DLQ
7. DynamoDB table
8. SNS topic + subscriptions
9. S3 buckets (must be empty first)
10. Secrets Manager secret
11. IAM Role `webfood-lambda-role-prod`
12. CloudWatch Alarms

> **Note:** MongoDB Atlas cluster is outside AWS — delete separately on Atlas if not needed.

### Workshop Conclusion

After this workshop, you have successfully deployed the WebFood platform with a complete AWS Serverless architecture: CDN, API, real-time WebSocket, event-driven email, and observability.
