---
title: "🚀 Tự động kiểm duyệt và trả lời bình luận Facebook bằng AI (Gemini & Notion)"
description: "Xây dựng hệ thống tự động hóa quản lý bình luận Facebook Fanpage sử dụng AI Agent Gemini và Notion Knowledge Base giúp trả lời khách hàng 24/7."
slug: "facebook-comment-ai-moderator-notion-gemini"
tags: [n8n, automation, facebook, ai, gemini, notion, chatbot]
keywords: [n8n workflow, facebook comment ai, gemini ai agent, notion database, tu dong hoa facebook]
---

# 🚀 Tự động kiểm duyệt và trả lời bình luận Facebook bằng AI (Gemini & Notion)

Các sếp đang quản lý Fanpage chắc chắn sẽ gặp tình trạng "đau đầu" khi lượng bình luận tăng vọt, khách hàng hỏi dồn dập các câu hỏi về sản phẩm, giá cả, chính sách... Việc trả lời thủ công không chỉ tốn thời gian, dễ bỏ sót mà còn khiến khách hàng phàn nàn vì phản hồi chậm trễ.

Giải pháp ở đây là gì? Workflow n8n tích hợp **AI Agent (Google Gemini)** kết hợp với **Notion Knowledge Base** sẽ giúp các sếp tự động quét, kiểm duyệt và trả lời bình luận của khách hàng một cách thông minh, chính xác 24/7 mà không cần tốn một xu chi phí nhân sự trực page ban đêm.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Khách hàng bình luận là AI trả lời ngay lập tức, không để khách phải chờ đợi.
- **Thông tin chính xác 100%:** AI lấy dữ liệu trực tiếp từ cơ sở kiến thức Notion (giá, tính năng, chính sách bảo hành...) nên không lo bịa đặt thông tin (hallucination).
- **Chống trùng lặp thông minh:** Hệ thống tự động kiểm tra ID bình luận qua Notion, đảm bảo không trả lời 1 bình luận quá nhiều lần.
- **Tiết kiệm thời gian nhân sự:** Giảm tải đến 80 khối lượng công việc cho đội ngũ chăm sóc khách hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Facebook Developer / Meta App** (với quyền truy cập Facebook Graph API để đọc bài viết và bình luận).
- **Tài khoản Google Cloud / Google AI Studio** để lấy API Key cho **Google Gemini**.
- **Tài khoản Notion** với 2 Database: 1 lưu Knowledge Base (thông tin sản phẩm/dịch vụ) và 1 lưu lịch sử Comment ID đã xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây trong workflow:

- **Posts Fetcher & Last Post Fetcher (HTTP Request):** Kết nối với Facebook Graph API để lấy danh sách bài đăng mới nhất trên Fanpage. Cần cấu hình Access Token của Facebook Page.
- **Latest Comment (Facebook Graph API):** Node này trích xuất nội dung và metadata của bình luận mới nhất trên bài đăng.
- **CommentID Checker & CommentID to DB (Notion):** Kết nối với Notion Database dùng để lưu trữ ID các bình luận đã được xử lý. Node *Checker* sẽ tra cứu xem ID bình luận hiện tại đã tồn tại chưa, node *To DB* sẽ ghi nhận lại sau khi đã trả lời xong để tránh lặp.
- **Knowledge Base & KB Arrange (Notion & Code):** 
  - *Knowledge Base*: Truy vấn database Notion chứa thông tin sản phẩm, kịch bản chăm sóc khách hàng.
  - *KB Arrange*: Xử lý dữ liệu thô từ Notion thành định dạng chuẩn để AI dễ dàng đọc hiểu và tra cứu.
- **AI Agent & AI Chat Model (Google Gemini):** 
  - Cấu hình credentials cho Google Gemini.
  - Viết System Prompt cho AI Agent, định hình tính cách nhân viên tư vấn, yêu cầu AI đọc dữ liệu từ Knowledge Base và trả lời lịch sự, đúng trọng tâm.
- **Reply Writer (Facebook Graph API):** Node thực hiện nhiệm vụ đăng câu trả lời do AI tạo ra trực tiếp xuống dưới bình luận của khách hàng trên Facebook.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) với một bài viết và bình luận mẫu trên Page thử nghiệm để kiểm tra luồng dữ liệu.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy theo lịch của Schedule Trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node thông báo về Telegram cá nhân của quản lý mỗi khi AI không trả lời được hoặc gặp câu hỏi khó từ khách hàng.
- **Gắn nhãn phân loại:** Sử dụng thêm một bước AI phụ để phân loại bình luận (Tích cực, Tiêu cực, Hỏi giá, Khiếu nại) để có hướng xử lý phù hợp trong Notion.
- **Lưu log chi tiết:** Lưu toàn bộ lịch sử hỏi-đáp của khách hàng vào Google Sheets hoặc Airtable để phân tíchInsight sản phẩm sau này.

### 📌 Kết luận
Workflow **Facebook Comment AI Moderator with Notion & Gemini** là một mảnh ghép hoàn hảo cho các doanh nghiệp vừa và nhỏ muốn tự động hóa quy trình chăm sóc khách hàng mạng xã hội mà không tốn kém chi phí lập trình phức tạp. Hãy "lên đồ" ngay hôm nay để tối ưu hóa Fanpage của các sếp nhé!