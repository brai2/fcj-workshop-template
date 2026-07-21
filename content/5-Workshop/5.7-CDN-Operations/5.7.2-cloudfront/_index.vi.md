---
title: "CloudFront"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### CloudFront Distribution

Tạo OAC cho S3 frontend/media, CloudFront Function `webfood-spa-rewrite`, distribution với origins:

- S3 frontend (default)
- S3 media (`/media/*`)
- API Gateway (`/api/*`)

![CloudFront 1](/images/5-Workshop/5.7-CDN-Operations/cloudfront-1.png)

![CloudFront 2](/images/5-Workshop/5.7-CDN-Operations/cloudfront-2.png)

![CloudFront 3](/images/5-Workshop/5.7-CDN-Operations/cloudfront-3.png)

![CloudFront 4](/images/5-Workshop/5.7-CDN-Operations/cloudfront-4.png)

![CloudFront 5](/images/5-Workshop/5.7-CDN-Operations/cloudfront-5.png)

Tiếp theo: [5.7.3 Observability](../5.7.3-observability/).
