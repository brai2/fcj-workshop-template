---
title: "Kiểm thử"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Smoke Test

Truy cập URL CloudFront và kiểm tra các luồng chính:

#### 1. Frontend

- Mở `https://<cloudfront-domain>/` → trang chủ WebFood hiển thị.
- Đăng ký / đăng nhập tài khoản khách hàng.

#### 2. API REST

- Duyệt menu, thêm món vào giỏ hàng.
- Đặt hàng → kiểm tra đơn xuất hiện trong lịch sử.

#### 3. Thanh toán MoMo (sandbox)

- Chọn thanh toán MoMo → redirect sandbox → quay về app.

#### 4. Event-driven

- Sau khi đặt hàng: kiểm tra email SES (nếu đã cấu hình).
- Admin publish voucher → client nhận toast qua WebSocket.

#### 5. Merchant / Admin

- Đăng nhập merchant → quản lý sản phẩm, cập nhật trạng thái đơn.
- Đăng nhập admin → duyệt nhà hàng, quản lý voucher.

Tiếp theo: [5.9 Dọn dẹp](../5.9-Teardown/).
