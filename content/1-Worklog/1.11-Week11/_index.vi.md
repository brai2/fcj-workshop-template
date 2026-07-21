---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Kiểm thử tổng thể hệ thống WebFood trên AWS.
* Kiểm tra CloudFront, API Gateway, Lambda, EventBridge, SQS, SES, WebSocket.
* Bật CloudWatch Alarms, X-Ray tracing.
* Hoàn thiện tài liệu `DEPLOY_CONSOLE.md` và workshop báo cáo.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 1 | Smoke test frontend qua CloudFront; kiểm tra API `/api/*`. | 29/06/2026 | 29/06/2026 | https://000045.awsstudygroup.com/ |
| 2 | Kiểm thử EventBridge → SQS Worker → SES; WebSocket voucher notify. | 30/06/2026 | 30/06/2026 | https://000045.awsstudygroup.com/ |
| 3 | Kiểm tra MongoDB Atlas, DynamoDB connections, Secrets Manager. | 01/07/2026 | 01/07/2026 | https://000045.awsstudygroup.com/ |
| 4 | CloudWatch Alarms + SNS; X-Ray traces; hoàn thiện `DEPLOY_CONSOLE.md`. | 02/07/2026 | 02/07/2026 | https://000045.awsstudygroup.com/ |
| 5 | Rà soát dự án nhóm; chuẩn bị Proposal và Workshop cho báo cáo FCAJ. | 03/07/2026 | 03/07/2026 | https://000045.awsstudygroup.com/ |

### Kết quả đạt được tuần 11:

* Đã kiểm thử thành công luồng CloudFront → API Gateway → Lambda → MongoDB.
* Đã xác nhận event-driven: EventBridge, SQS, SES, WebSocket hoạt động ổn định.
* Đã kiểm tra WAF, Secrets Manager, DynamoDB connections.
* Đã bật CloudWatch/X-Ray và hoàn thiện tài liệu deploy.
* Đã chuẩn bị nội dung Proposal + Workshop cho báo cáo Hugo.
