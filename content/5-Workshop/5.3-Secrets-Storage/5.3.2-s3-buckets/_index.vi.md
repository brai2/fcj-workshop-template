---
title: "S3 Buckets"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### S3 Buckets

**Console:** S3 → **Create bucket** (tạo 2 bucket)

| Bucket | Tên | Ghi chú |
|--------|-----|---------|
| Frontend | `webfood-frontend-<ACCOUNT_ID>-prod` | Block Public Access bật, truy cập qua CloudFront OAC |
| Media | `webfood-media-<ACCOUNT_ID>-prod` | Thêm CORS cho GET |

![S3 bucket 1](/images/5-Workshop/5.3-Secrets-Storage/s3-frontend-1.png)

![S3 bucket 2](/images/5-Workshop/5.3-Secrets-Storage/s3-frontend-2.png)

![S3 bucket 3](/images/5-Workshop/5.3-Secrets-Storage/s3-media-1.png)

![S3 bucket 4](/images/5-Workshop/5.3-Secrets-Storage/s3-media-2.png)

> Bucket policy cho CloudFront sẽ thêm ở [5.7.2 CloudFront](../../5.7-CDN-Operations/5.7.2-cloudfront/).

Tiếp theo: [5.4 Dữ liệu & Messaging](../../5.4-Data-Messaging/).
