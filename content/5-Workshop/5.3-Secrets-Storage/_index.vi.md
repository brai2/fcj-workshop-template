---
title: "Bí mật & Lưu trữ"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

Tạo **Secrets Manager** (cấu hình ứng dụng) và **S3 buckets** (frontend + media). Đây là các resource độc lập, không phụ thuộc Lambda — tạo trước.

#### Mục con

1. [5.3.1 Secrets Manager](5.3.1-secrets-manager/)
2. [5.3.2 S3 Buckets](5.3.2-s3-buckets/)
> 📌 Ghi lại **ARN** của secret và tên bucket — các bước IAM, Lambda, CloudFront sẽ cần dùng.
