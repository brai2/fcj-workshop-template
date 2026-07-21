---
title: "Dọn dẹp"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Teardown — Dọn dẹp tài nguyên

Khi không cần dùng nữa (tránh phát sinh chi phí), xóa theo thứ tự **ngược** với deploy:

1. CloudFront Distribution (disable → delete, đợi deployed)
2. WAF WebACL
3. API Gateway REST + WebSocket
4. Lambda functions (5)
5. EventBridge rules + event bus
6. SQS queues + DLQ
7. DynamoDB table
8. SNS topic + subscriptions
9. S3 buckets (phải empty trước)
10. Secrets Manager secret
11. IAM Role `webfood-lambda-role-prod`
12. CloudWatch Alarms

> **Lưu ý:** MongoDB Atlas cluster nằm ngoài AWS — xóa riêng trên Atlas nếu không dùng.

### Kết luận workshop

Sau workshop, bạn đã triển khai thành công nền tảng WebFood với kiến trúc AWS Serverless đầy đủ: CDN, API, real-time WebSocket, event-driven email và observability.
