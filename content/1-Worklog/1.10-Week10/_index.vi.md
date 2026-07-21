---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Triển khai 5 Lambda functions và API Gateway REST + WebSocket.
* Cấu hình EventBridge rules, SQS trigger, WAF, CloudFront.
* Tích hợp MoMo sandbox và SES email.
* Kiểm thử luồng đặt hàng end-to-end.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 1 | Tạo 5 Lambda: api, worker, ws-connect/disconnect/notify. | 22/06/2026 | 22/06/2026 | https://000045.awsstudygroup.com/ |
| 2 | API Gateway REST + WebSocket; EventBridge rules. | 23/06/2026 | 23/06/2026 | https://000045.awsstudygroup.com/ |
| 3 | WAF WebACL; CloudFront Distribution; OAC bucket policy. | 24/06/2026 | 24/06/2026 | https://000045.awsstudygroup.com/ |
| 4 | Build & upload frontend; cập nhật secrets CloudFront/MoMo URLs. | 25/06/2026 | 25/06/2026 | https://000045.awsstudygroup.com/ |
| 5 | Kiểm thử đặt hàng, thanh toán MoMo, email SES, WebSocket notify. | 26/06/2026 | 26/06/2026 | https://000045.awsstudygroup.com/ |

### Kết quả đạt được tuần 10:

* Đã triển khai đầy đủ Lambda, API Gateway REST/WebSocket trên AWS.
* Đã cấu hình EventBridge → SQS/Worker/SES và WebSocket notify.
* Đã hoàn thành CloudFront + WAF + deploy frontend.
* Đã kiểm thử luồng đặt hàng và xử lý lỗi phát sinh.
* Đã trình bày tiến độ với mentor FCAJ và nhận góp ý tối ưu.
