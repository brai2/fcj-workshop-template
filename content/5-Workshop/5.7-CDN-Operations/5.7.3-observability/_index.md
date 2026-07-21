---
title: "Observability & SES"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### Update Secrets Manager

After CloudFront domain is ready, update secret `webfood/prod/app-secrets`:

- `MOMO_REDIRECT_URL` = `https://<cloudfront-domain>/payment-result`
- `MOMO_IPN_URL` = `https://<cloudfront-domain>/api/payment/momo/ipn`
- `FRONTEND_URL` = `https://<cloudfront-domain>`

Lambda `webfood-api` → Environment variables → `MEDIA_CDN_URL` = `https://<cloudfront-domain>`.

> Force new cold start: re-save Lambda environment variables so cached secrets refresh.

### CloudWatch Alarms

**Console:** CloudWatch → **Alarms** → **Create alarm** (3 times). Each alarm notifies SNS topic `webfood-alarms-prod` from [5.4.3](../5.4-Data-Messaging/5.4.3-eventbridge-sns/).

#### Alarm 1 — `webfood-api` errors

- Metric: Lambda → `webfood-api` → **Errors**, Statistic **Sum**, Period **5 minutes**
- Condition: **Greater/Equal** **1**
- Missing data: **Treat missing data as good**
- Notification: SNS `webfood-alarms-prod`
- Name: `webfood-api-errors-prod`

![CloudWatch Alarm 1](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-1.png)

![CloudWatch Alarm 2](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-2.png)

![CloudWatch Alarm 3](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-3.png)

![CloudWatch Alarm 4](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-4.png)

![CloudWatch Alarm 5](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-5.png)

![CloudWatch Alarm 6](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-6.png)

#### Alarm 2 — `webfood-worker` errors

Same as Alarm 1, change Function → `webfood-worker`, alarm name → `webfood-worker-errors-prod`.

![CloudWatch Alarm 7](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-7.png)

![CloudWatch Alarm 8](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-8.png)

![CloudWatch Alarm 9](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-9.png)

![CloudWatch Alarm 10](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-10.png)

![CloudWatch Alarm 11](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-11.png)

#### Alarm 3 — DLQ messages

- Metric: SQS → `webfood-order-events-dlq-prod` → **ApproximateNumberOfMessagesVisible**
- Statistic: **Maximum**, Period **5 minutes**
- Condition: **Greater/Equal** **1**
- Notification: SNS `webfood-alarms-prod`
- Name: `webfood-dlq-messages-prod`

![CloudWatch Alarm 12](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-12.png)

![CloudWatch Alarm 13](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-13.png)

![CloudWatch Alarm 14](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-14.png)

![CloudWatch Alarm 15](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-15.png)

![CloudWatch Alarm 16](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-16.png)

![CloudWatch Alarm 17](/images/5-Workshop/5.7-CDN-Operations/cloudwatch-17.png)

### Verify SES

SES → **Verified identities** → verify `FROM_EMAIL` and test recipient emails (SES Sandbox only sends to verified addresses).

Next: [5.7.4 Frontend Deploy](../5.7.4-frontend-deploy/).
