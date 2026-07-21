---
title: "Smoke Test"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Smoke Test

Access CloudFront URL and verify main flows:

#### 1. Frontend

- Open `https://<cloudfront-domain>/` → WebFood homepage displays.
- Register / login as customer.

#### 2. REST API

- Browse menu, add items to cart.
- Place order → verify order appears in history.

#### 3. MoMo Payment (sandbox)

- Select MoMo payment → sandbox redirect → return to app.

#### 4. Event-driven

- After placing order: check SES email (if configured).
- Admin publishes voucher → client receives toast via WebSocket.

#### 5. Merchant / Admin

- Login as merchant → manage products, update order status.
- Login as admin → approve restaurants, manage vouchers.

Next: [5.9 Teardown](../5.9-Teardown/).
