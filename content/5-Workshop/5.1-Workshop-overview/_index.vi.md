---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Demo dự án đã triển khai

Người đánh giá có thể truy cập trực tiếp hệ thống WebFood tại:

**[https://dh9xhc3jrccu4.cloudfront.net/](https://dh9xhc3jrccu4.cloudfront.net/)**

Link này là CloudFront distribution của dự án (frontend + API) sau khi hoàn thành các bước workshop.

#### Mục tiêu workshop

Sau khi hoàn thành workshop, bạn sẽ:

- Triển khai được nền tảng WebFood đầy đủ trên AWS Serverless.
- Hiểu luồng request từ CloudFront → API Gateway → Lambda → MongoDB Atlas.
- Cấu hình event-driven pipeline: EventBridge → SQS/Worker/SES và WebSocket notify.
- Vận hành frontend React trên S3 + CloudFront với WAF bảo vệ.

#### Kiến trúc tổng quan

WebFood sử dụng mô hình serverless: không có EC2, toàn bộ compute chạy trên Lambda. Frontend là SPA React được build tĩnh và host trên S3, phân phối qua CloudFront.

![Kiến trúc WebFood](/images/5-Workshop/5.1-Workshop-overview/webfood_architecture.png)

#### Luồng xử lý chính

1. **Đặt hàng (REST)**: Browser → CloudFront `/api/*` → API Gateway REST → Lambda `webfood-api` → MongoDB → publish EventBridge.
2. **Email (async)**: EventBridge rule → SQS → Lambda `webfood-worker` → SES gửi email xác nhận.
3. **Real-time (WebSocket)**: EventBridge rule → Lambda `webfood-ws-notify` → API Gateway WebSocket → client nhận toast voucher/đơn hàng.
4. **Kết nối WS**: Client mở WebSocket → Lambda `webfood-ws-connect` → lưu `connectionId` vào DynamoDB.

#### Các Lambda function

| Function | Handler | Vai trò |
|----------|---------|---------|
| `webfood-api` | `src/lambda.handler` | REST API (Express app) |
| `webfood-worker` | `src/lambda-worker.handler` | Xử lý SQS, gửi email SES |
| `webfood-ws-connect` | `src/lambda-ws-connect.handler` | Route `$connect` |
| `webfood-ws-disconnect` | `src/lambda-ws-disconnect.handler` | Route `$disconnect` |
| `webfood-ws-notify` | `src/lambda-ws-notify.handler` | Push message qua WebSocket |

#### Event types trên EventBridge

- `OrderCreated` — đơn hàng mới
- `OrderStatusChanged` — cập nhật trạng thái
- `PaymentSucceeded` — thanh toán MoMo thành công
- `VoucherPublished` — admin publish voucher (chỉ gửi WebSocket)

#### Lộ trình workshop

| Mục | Nội dung |
|-----|----------|
| [5.2 Chuẩn bị](../5.2-Prerequisites/) | Tài khoản, công cụ |
| [5.3 Bí mật & Lưu trữ](../5.3-Secrets-Storage/) | Secrets Manager, S3 |
| [5.4 Dữ liệu & Messaging](../5.4-Data-Messaging/) | DynamoDB, SQS, EventBridge, SNS |
| [5.5 Lambda](../5.5-Lambda/) | IAM, functions, SQS trigger |
| [5.6 API & Sự kiện](../5.6-API-Gateway/) | Rules, REST, WebSocket |
| [5.7 CDN & Vận hành](../5.7-CDN-Operations/) | WAF, CloudFront, SES, frontend |
| [5.8 Kiểm thử](../5.8-Smoke-Test/) | Smoke test |
| [5.9 Dọn dẹp](../5.9-Teardown/) | Xóa resources |
