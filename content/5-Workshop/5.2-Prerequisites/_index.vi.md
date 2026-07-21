---
title: "Chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

Trước khi deploy WebFood, chuẩn bị đầy đủ tài khoản, công cụ và thông tin sau.

#### 1. AWS Account & Region

- Đăng nhập [AWS Management Console](https://console.aws.amazon.com).
- Chọn region **us-east-1** (N. Virginia) — **bắt buộc** vì WAF cho CloudFront chỉ tạo được ở region này.
- Ghi lại `<ACCOUNT_ID>` (12 số) từ menu tài khoản góc trên-phải.

#### 2. Môi trường local

| Yêu cầu | Chi tiết |
|---------|----------|
| Node.js | Phiên bản **20+** |
| Git | Clone repo WebFood |
| PowerShell / Terminal | `npm install`, `Compress-Archive` |

#### 3. MongoDB Atlas

- Cluster MongoDB Atlas (free tier được), database `webappfood`.
- Connection string `mongodb+srv://user:pass@cluster.xxx.mongodb.net/webappfood`.
- **Network Access**: thêm `0.0.0.0/0`.

#### 4. MoMo Sandbox

- `partnerCode`, `accessKey`, `secretKey`
- Endpoint: `https://test-payment.momo.vn/v2/gateway/api/create`

#### 5. Amazon SES

- 1 email **người gửi** (FROM_EMAIL) — verify trong SES.
- 1 email nhận **cảnh báo CloudWatch** qua SNS.

#### 6. Quyền IAM

Quyền tạo/quản lý: Lambda, API Gateway, S3, CloudFront, WAF, DynamoDB, SQS, EventBridge, SNS, Secrets Manager, IAM Role, CloudWatch.

#### Checklist

- [ ] Region = us-east-1
- [ ] MongoDB Atlas connection string sẵn sàng
- [ ] MoMo sandbox credentials
- [ ] Email SES đã verify
- [ ] Node.js 20+ đã cài
- [ ] Source code WebFood (`backend/`, `frontend/`) trên máy local

Tiếp theo: [5.3 Bí mật & Lưu trữ](5.3-Secrets-Storage/).
