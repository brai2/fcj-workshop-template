---
title: "Blog 1 — AI Agent trên Amazon Bedrock"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AI Agent trên Amazon Bedrock & AgentCore — AI không chỉ trả lời, mà còn làm được việc

Xin chào mọi người,

Trong quá trình tìm hiểu về AWS và Generative AI, mình thường đọc các bài viết trên AWS Blog để hiểu cách các doanh nghiệp ứng dụng công nghệ vào thực tế. Gần đây mình có tìm hiểu về cách AWS xây dựng hệ thống AI Agent sử dụng **Amazon Bedrock** và **AgentCore**, và nhận ra đây là một hướng tiếp cận rất đáng chú ý.

Ban đầu mình nghĩ các bài viết này sẽ tập trung vào mô hình AI hoặc độ mạnh của LLM. Nhưng sau khi tìm hiểu kỹ hơn, điều mình thấy giá trị nhất lại không nằm ở model, mà nằm ở **cách AWS thiết kế một hệ thống để AI có thể tự thực hiện công việc**.

### AI Agent không chỉ là chatbot

Trước đây, khi nhắc đến AI, mình thường nghĩ đến chatbot hoặc hệ thống trả lời câu hỏi.

Nhưng với kiến trúc AI Agent trên AWS, AI không chỉ dừng lại ở việc trả lời, mà còn có thể:

- Hiểu mục tiêu
- Lập kế hoạch
- Thực hiện từng bước
- Quan sát kết quả
- Và tiếp tục điều chỉnh hành động

Điều này khiến AI hoạt động giống như một **“người vận hành hệ thống”** hơn là một công cụ hỗ trợ đơn thuần.

### Kiến trúc hệ thống: Không phải AI làm tất cả

Điểm mình thấy thú vị nhất là cách AWS thiết kế kiến trúc.

AI không trực tiếp xử lý toàn bộ hệ thống, mà được đặt vào một flow rõ ràng:

1. User gửi request qua CloudFront + API Gateway  
2. Lambda xử lý logic trung gian  
3. Request được chuyển vào AgentCore Runtime  
4. Một Orchestrator Agent sẽ điều phối các sub-agent  
5. Các agent này sử dụng Tools (API / service) để thực hiện hành động  

![Kiến trúc AI Agent trên AWS](/images/3-BlogsPosted/ai-agent-architecture.png)

Điều quan trọng là: **AI không thay thế hệ thống, mà hoạt động cùng hệ thống thông qua API**.

### Multi-Agent: Chia nhỏ nhiệm vụ giống con người

Một điểm mình thấy rất hay là hệ thống không chỉ có 1 AI, mà có nhiều agent:

- Agent tìm thông tin (**Find**)
- Agent lập kế hoạch (**Create**)
- Agent thực thi (**Execute**)

Cách này giống như trong team thật: người phân tích, người thiết kế, người triển khai. Nhờ đó dễ mở rộng, dễ debug, và logic rõ ràng hơn rất nhiều.

### Tool Use — chìa khóa quan trọng nhất

Một điều mình rút ra là: **AI chỉ thực sự “hữu dụng” khi nó có thể sử dụng công cụ**.

Trong kiến trúc này:

- AI không thao tác trực tiếp vào hệ thống
- Mọi hành động đều thông qua API, Database, External service

Điều này giúp hệ thống ổn định hơn, dễ thay đổi AI model, và không bị phụ thuộc vào một công nghệ.

### Ứng dụng không chỉ dừng ở AI hay DevOps

Sau khi hiểu mô hình này, mình nhận ra nó có thể áp dụng vào rất nhiều bài toán:

- Tự động test website / app (giống QA)
- Tự động xử lý ticket support
- DevOps automation (deploy, monitor)
- Data pipeline thông minh
- AI assistant cho doanh nghiệp

Chỉ cần thay đổi tool mà agent được phép sử dụng, toàn bộ hệ thống có thể dùng lại.

### Góc nhìn cá nhân

Điều mình thấy quan trọng nhất sau khi tìm hiểu là: **giá trị của AI không nằm ở việc “trả lời thông minh”, mà nằm ở việc làm được việc thực tế**.

Amazon Bedrock trong hệ thống này không chỉ là nơi chạy model, mà là nền tảng để xây dựng AI Agent, kết nối với hệ thống, và tự động hóa quy trình.

Điều này thay đổi hoàn toàn cách mình nhìn về AI: **không còn là tool → mà là một thành phần trong hệ thống**.

### Kết luận

Đối với mình, đây không đơn thuần là một kiến trúc AI, mà là một cách tiếp cận mới trong việc xây dựng hệ thống:

- AI không đứng riêng lẻ
- AI không thay thế hệ thống
- AI trở thành một **“worker”** trong hệ thống

Nếu bạn đang tìm hiểu về Amazon Bedrock, AI Agent, hoặc Generative AI trên AWS, thì đây là một hướng rất đáng để nghiên cứu — vì nó cho thấy cách công nghệ này được áp dụng vào thực tế, không chỉ dừng lại ở demo.

---

**Link bài viết trên Facebook:**  
[https://www.facebook.com/groups/awsstudygroupfcj/permalink/2210158863082407/](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2210158863082407/)
