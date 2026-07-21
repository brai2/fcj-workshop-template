---
title: "Lambda Functions"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### Đóng gói code Lambda

```powershell
cd E:\workshop\WebFood\backend
npm install --omit=dev
Compress-Archive -Path .\* -DestinationPath ..\webfood-lambda.zip -Force
```

### Tạo 5 Lambda Functions

| Function | Handler |
|----------|---------|
| `webfood-api` | `src/lambda.handler` |
| `webfood-worker` | `src/lambda-worker.handler` |
| `webfood-ws-connect` | `src/lambda-ws-connect.handler` |
| `webfood-ws-disconnect` | `src/lambda-ws-disconnect.handler` |
| `webfood-ws-notify` | `src/lambda-ws-notify.handler` |

Runtime **Node.js 20.x**, Memory **512 MB**, X-Ray **Active**.

![Lambda 1](/images/5-Workshop/5.5-Lambda/lambda-1.png)

![Lambda 2](/images/5-Workshop/5.5-Lambda/lambda-2.png)

![Lambda 3](/images/5-Workshop/5.5-Lambda/lambda-3.png)

![Lambda 4](/images/5-Workshop/5.5-Lambda/lambda-4.png)

Tiếp theo: [5.5.3 SQS Trigger](../5.5.3-sqs-trigger/).
