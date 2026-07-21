---
title: "Frontend Deploy"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.7.4. </b> "
---

### Build & Upload Frontend

Tạo `.env` trong `frontend/`:

```
VITE_API_URL=https://<cloudfront-domain>/api
VITE_WS_URL=wss://<ws-api-id>.execute-api.us-east-1.amazonaws.com/prod
```

```powershell
cd E:\workshop\WebFood\frontend
npm run build
aws s3 sync dist/ s3://webfood-frontend-<ACCOUNT_ID>-prod/ --delete
```

![Frontend deploy 1](/images/5-Workshop/5.7-CDN-Operations/frontend-deploy.png)

Tiếp theo: [5.8 Kiểm thử](../../5.8-Smoke-Test/).
