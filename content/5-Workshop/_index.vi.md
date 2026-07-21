---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai WebFood trên AWS Serverless

Workshop hướng dẫn triển khai **toàn bộ** kiến trúc WebFood trên AWS Management Console (click-ops), có screenshot minh họa từng bước. Các mục được nhóm theo **chức năng** để dễ theo dõi và không bỏ sót bước.

> **Demo trực tiếp (để đánh giá):** [https://dh9xhc3jrccu4.cloudfront.net/](https://dh9xhc3jrccu4.cloudfront.net/)  
> Người đánh giá có thể mở link này để xem và trải nghiệm hệ thống WebFood đã triển khai trên AWS.

> Region bắt buộc: **us-east-1** (WAF gắn CloudFront chỉ tạo được ở us-east-1).

#### Mục lục

| # | Phần | Nội dung |
|---|------|----------|
| 5.1 | [Tổng quan](5.1-Workshop-overview/) | Mục tiêu, kiến trúc, luồng xử lý |
| 5.2 | [Chuẩn bị](5.2-Prerequisites/) | Tài khoản, công cụ, checklist |
| 5.3 | [Bí mật & Lưu trữ](5.3-Secrets-Storage/) | Secrets Manager, S3 |
| 5.4 | [Dữ liệu & Messaging](5.4-Data-Messaging/) | DynamoDB, SQS, EventBridge, SNS |
| 5.5 | [Lambda](5.5-Lambda/) | IAM, đóng gói code, functions, trigger |
| 5.6 | [API & Sự kiện](5.6-API-Gateway/) | EventBridge rules, REST API, WebSocket |
| 5.7 | [CDN & Vận hành](5.7-CDN-Operations/) | WAF, CloudFront, CloudWatch, SES, frontend |
| 5.8 | [Kiểm thử](5.8-Smoke-Test/) | Smoke test các luồng chính |
| 5.9 | [Dọn dẹp](5.9-Teardown/) | Xóa resources, tránh phát sinh chi phí |
