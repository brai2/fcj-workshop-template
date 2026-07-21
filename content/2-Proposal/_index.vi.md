---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

Tại phần này, tôi trình bày bản đề xuất workshop **WebFood** — nền tảng đặt đồ ăn trực tuyến triển khai trên kiến trúc AWS Serverless.

# WebFood — Nền tảng đặt đồ ăn trực tuyến
## Giải pháp AWS Serverless cho thương mại điện tử F&B

### 1. Tóm tắt điều hành

WebFood là nền tảng đặt đồ ăn trực tuyến hỗ trợ ba vai trò người dùng: **Khách hàng** (duyệt menu, giỏ hàng, thanh toán MoMo), **Chủ quán** (quản lý sản phẩm, đơn hàng, thống kê) và **Quản trị viên** (duyệt nhà hàng, voucher, tài chính hệ thống). Ứng dụng được phát triển bằng React (frontend) và Node.js/Express (backend), lưu trữ dữ liệu nghiệp vụ trên MongoDB Atlas.

Trong phạm vi workshop, dự án được triển khai lên AWS theo kiến trúc serverless đầy đủ: CloudFront + WAF phân phối frontend và media, API Gateway REST + Lambda xử lý API, API Gateway WebSocket + DynamoDB cho thông báo real-time, EventBridge + SQS + Lambda Worker cho xử lý bất đồng bộ (email SES). Giải pháp phù hợp cho môi trường demo/học tập với chi phí vận hành thấp và khả năng mở rộng theo lượng request.

### 2. Tuyên bố vấn đề

*Vấn đề hiện tại*

Các mô hình đặt đồ ăn truyền thống thường phụ thuộc vào gọi điện, chat thủ công hoặc hệ thống rời rạc giữa khách hàng và nhà hàng. Khi số lượng quán và đơn hàng tăng, việc theo dõi trạng thái đơn, gửi thông báo và quản lý voucher trở nên khó kiểm soát. Triển khai trên server cố định (EC2) cũng đòi hỏi chi phí duy trì ngay cả khi không có traffic.

*Giải pháp*

WebFood tập trung hóa luồng đặt hàng trên một nền tảng web đa vai trò, kết hợp thanh toán MoMo sandbox và kiến trúc event-driven trên AWS. Khi có sự kiện nghiệp vụ (tạo đơn, đổi trạng thái, thanh toán thành công, publish voucher), hệ thống publish event lên EventBridge, đồng thời gửi email qua SQS/Worker/SES và push thông báo real-time qua WebSocket.

*Lợi ích và hoàn vốn đầu tư (ROI)*

- Giảm chi phí hạ tầng nhờ mô hình pay-per-use (Lambda, API Gateway, S3).
- Tách biệt frontend tĩnh (S3/CloudFront) và backend API (Lambda), dễ bảo trì và scale.
- Event-driven giúp mở rộng tính năng (email, notification) mà không sửa core API.
- Chi phí ước tính khoảng **8–15 USD/tháng** cho workload demo (xem mục 6), thấp hơn đáng kể so với duy trì EC2 24/7.

### 3. Kiến trúc giải pháp

WebFood áp dụng kiến trúc serverless theo sơ đồ `docs/wedfood.drawio`, triển khai tại region **us-east-1** (yêu cầu của WAF gắn CloudFront).

![Kiến trúc WebFood trên AWS](/images/2-Proposal/webfood_architecture.png)

*Dịch vụ AWS sử dụng*

| Nhóm | Dịch vụ | Vai trò |
|------|---------|---------|
| Edge | CloudFront, WAF, CloudFront Functions | CDN, bảo vệ, SPA routing |
| Storage | S3 (frontend + media) | Host React build, lưu ảnh sản phẩm |
| Compute | Lambda (5 functions) | API Express, worker email, WebSocket handlers |
| API | API Gateway REST + WebSocket | REST `/api/*`, real-time `$connect`/`$disconnect` |
| Database | DynamoDB | Lưu WebSocket connectionId theo userId |
| Messaging | EventBridge, SQS + DLQ, SNS | Event bus, hàng đợi worker, cảnh báo |
| Security | Secrets Manager, IAM, OAC | JWT/MoMo/MongoDB credentials, bucket policy |
| Observability | CloudWatch, X-Ray | Logs, alarms, distributed tracing |
| Email | SES | Xác nhận đơn, reset password |

*Thiết kế thành phần*

- **Frontend**: React 19 + Vite, build tĩnh upload lên S3, phục vụ qua CloudFront.
- **ApiFunction** (`webfood-api`): Bọc Express app qua `@codegenie/serverless-express`, kết nối MongoDB Atlas, publish event lên EventBridge.
- **WorkerFunction** (`webfood-worker`): Trigger SQS, gửi email qua SES khi có `OrderCreated`, `OrderStatusChanged`, `PaymentSucceeded`.
- **WebSocket Lambdas**: `ws-connect`/`ws-disconnect` quản lý DynamoDB; `ws-notify` nhận event từ EventBridge, push message tới client.
- **MongoDB Atlas**: Database chính (User, Restaurant, Product, Order, Voucher, …) — nằm ngoài VPC AWS.

### 4. Triển khai kỹ thuật

*Các giai đoạn triển khai*

1. **Phát triển local** (Tuần 4–6): React frontend + Express/Mongoose backend, auth JWT, luồng đặt hàng, tích hợp MoMo sandbox.
2. **Thiết kế kiến trúc AWS** (Tuần 7–8): Vẽ sơ đồ `wedfood.drawio`, viết SAM template (`infra/template.yaml`), chuẩn hóa Lambda handlers.
3. **Deploy AWS** (Tuần 9–10): Triển khai thủ công trên Console theo `DEPLOY_CONSOLE.md` (hoặc `sam deploy`) — Secrets Manager, S3, Lambda, API Gateway, CloudFront.
4. **Kiểm thử & tối ưu** (Tuần 11–12): Smoke test end-to-end, bật X-Ray, CloudWatch alarms, cập nhật biến môi trường CloudFront/MoMo.

*Yêu cầu kỹ thuật*

- **Local**: Node.js 20+, MongoDB, npm cho `backend/` và `frontend/`.
- **AWS**: Tài khoản với quyền tạo Lambda, API Gateway, S3, CloudFront, WAF, EventBridge, DynamoDB, SQS, SES.
- **Bên thứ ba**: MongoDB Atlas cluster, tài khoản MoMo Test, email đã verify trong SES.
- **IaC**: AWS SAM (`template.yaml`) hoặc click-ops Console cho mục đích báo cáo workshop.

### 5. Lộ trình & Mốc triển khai

| Giai đoạn | Thời gian | Mốc chính |
|-----------|-----------|-----------|
| Học AWS cơ bản | Tuần 1–3 (17/04 – 08/05/2026) | Free Tier, EC2, S3, VPC, IAM, CLI |
| Dev WebFood local | Tuần 4–8 (11/05 – 12/06/2026) | Học thêm Lightsail, ELB, CloudWatch; thiết kế WebFood |
| Thiết kế serverless | Tuần 8–9 (08/06 – 19/06/2026) | `wedfood.drawio`, SAM template, Lambda adapter |
| Deploy production | Tuần 9–10 (15/06 – 26/06/2026) | Deploy Console, CloudFront live |
| Kiểm thử & báo cáo | Tuần 11–14 (29/06 – 30/07/2026) | Smoke test, workshop doc, Hugo site |

### 6. Ước tính ngân sách

Chi tiết ước tính chi phí hàng tháng cho workload demo (~10.000 request API, ~5 GB CloudFront transfer):

| Dịch vụ | Chi phí ước tính/tháng |
|---------|------------------------|
| AWS Lambda (5 functions) | ~1,50 USD |
| API Gateway REST + WebSocket | ~2,00 USD |
| Amazon CloudFront | ~2,50 USD |
| Amazon S3 (frontend + media) | ~0,50 USD |
| DynamoDB (on-demand) | ~0,25 USD |
| EventBridge + SQS | ~0,10 USD |
| AWS WAF | ~5,00 USD |
| Amazon SES | ~0,10 USD |
| Secrets Manager | ~0,40 USD |
| **Tổng** | **~12,35 USD/tháng** (~148 USD/năm) |

Xem chi tiết trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=webfood-serverless-estimate).

Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).

### 7. Đánh giá rủi ro

*Ma trận rủi ro*

| Rủi ro | Ảnh hưởng | Xác suất |
|--------|-----------|----------|
| Cold start Lambda | Trung bình | Trung bình |
| MongoDB Atlas mất kết nối | Cao | Thấp |
| MoMo sandbox không phản hồi | Trung bình | Thấp |
| Chi phí WAF/CloudFront vượt Free Tier | Trung bình | Trung bình |
| Zip Lambda > 50 MB (node_modules) | Trung bình | Trung bình |

*Chiến lược giảm thiểu*

- Provisioned concurrency cho `webfood-api` nếu cần (production).
- MongoDB Atlas: whitelist IP, monitoring connection pool.
- CloudWatch billing alarm + SNS notification.
- `npm install --omit=dev` khi đóng gói Lambda; upload qua S3 nếu zip lớn.

*Kế hoạch dự phòng*

- Fallback chạy local (Express + MongoDB) khi AWS gặp sự cố trong giai đoạn demo.
- SAM template (`infra/template.yaml`) để tái tạo stack nhanh sau teardown.

### 8. Kết quả kỳ vọng

*Cải tiến kỹ thuật*

- Luồng đặt hàng end-to-end: khách đặt món → API Lambda → EventBridge → email SES + WebSocket toast voucher.
- Quản trị tập trung: admin duyệt nhà hàng, merchant cập nhật menu, khách theo dõi đơn real-time.
- Kiến trúc có thể mở rộng: thêm event type mới trên EventBridge mà không refactor API.

*Giá trị dài hạn*

- Nền tảng tham chiếu cho các dự án e-commerce serverless trên AWS.
- Kinh nghiệm thực hành đầy đủ: IaC (SAM), event-driven, CDN, WebSocket, observability.
- Có thể mở rộng sang production với Cognito auth, CI/CD pipeline và multi-region.
