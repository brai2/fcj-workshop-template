---
title: "EventBridge & SNS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### EventBridge Custom Event Bus

**Console:** EventBridge → **Event buses** → **Create event bus**

| Trường | Giá trị |
|--------|---------|
| Name | `webfood-events-prod` |

Bấm **Create**. 📌 Ghi lại **ARN** bus (dạng `arn:aws:events:us-east-1:<ACCOUNT_ID>:event-bus/webfood-events-prod`).

> Chưa tạo **Rules** ở bước này — Lambda `webfood-ws-notify` chưa tồn tại. Rules sẽ cấu hình ở [5.6.1 EventBridge Rules](../../5.6-API-Gateway/5.6.1-eventbridge-rules/).

![EventBridge 1](/images/5-Workshop/5.4-Data-Messaging/eventbridge-1.png)

![EventBridge 2](/images/5-Workshop/5.4-Data-Messaging/eventbridge-2.png)

### SNS Topic cảnh báo

**Console:** SNS → **Topics** → **Create topic**

| Trường | Giá trị |
|--------|---------|
| Type | Standard |
| Name | `webfood-alarms-prod` |

Bấm **Create topic**. 📌 Ghi lại **ARN**.

Tab **Subscriptions** → **Create subscription**:

| Trường | Giá trị |
|--------|---------|
| Protocol | Email |
| Endpoint | email nhận cảnh báo CloudWatch |

Bấm **Create subscription** → mở email → **Confirm subscription** (bắt buộc, nếu không sẽ không nhận cảnh báo).

![SNS 1](/images/5-Workshop/5.4-Data-Messaging/sns-1.png)

![SNS 2](/images/5-Workshop/5.4-Data-Messaging/sns-2.png)

![SNS 3](/images/5-Workshop/5.4-Data-Messaging/sns-3.png)

![SNS 4](/images/5-Workshop/5.4-Data-Messaging/sns-4.png)

Tiếp theo: [5.5 Lambda](../../5.5-Lambda/).
