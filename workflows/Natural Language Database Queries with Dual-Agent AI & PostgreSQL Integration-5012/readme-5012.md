---
title: "🚀 Truy vấn cơ sở dữ liệu bằng ngôn ngữ tự nhiên với Dual-Agent AI và PostgreSQL trong n8n"
description: "Hướng dẫn cấu hình hệ thống Dual-Agent AI trên n8n giúp tra cứu dữ liệu PostgreSQL cực nhanh qua tin nhắn Telegram bằng cả văn bản và giọng nói."
slug: "truy-van-co-so-du-lieu-bang-ngon-ngu-tu-nhien-voi-dual-agent-ai-postgres"
tags: [n8n, automation, ai-agent, postgresql, telegram, openrouter]
keywords: [n8n workflow, dual-agent ai, truy vấn database bằng ngôn ngữ tự nhiên, postgresql n8n, telegram bot ai]
---

# 🚀 Truy vấn cơ sở dữ liệu bằng ngôn ngữ tự nhiên với Dual-Agent AI và PostgreSQL

Các sếp có bao giờ cảm thấy mệt mỏi mỗi khi cần tra cứu dữ liệu từ cơ sở dữ liệu (PostgreSQL) nhưng lại phải phiền đến lập trình viên viết câu lệnh SQL thủ công, hay tự mình loay hoay với các cú pháp phức tạp? Việc này không chỉ tốn thời gian mà còn làm gián đoạn mạch công việc kinh doanh.

Đừng lo, workflow n8n với kiến trúc **Dual-Agent AI (Hệ thống 2 trợ lý AI phối hợp)** này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống cho phép các sếp trò chuyện trực tiếp với Database qua Telegram (gửi cả tin nhắn văn bản lẫn Voice), AI sẽ tự động hiểu ý định, viết câu lệnh SQL tối ưu, truy vấn dữ liệu và trả về kết quả mượt mà như đang chat với một chuyên gia dữ liệu thực thụ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu không cần biết SQL:** Hỏi gì đáp nấy bằng ngôn ngữ tự nhiên thông qua Telegram.
- **Hỗ trợ tin nhắn thoại (Voice-to-Text):** Gửi voice note qua Telegram, AI tự động nghe hiểu và chuyển hóa thành câu truy vấn.
- **Kiến trúc Dual-Agent thông minh:** Một agent chịu trách nhiệm tương tác và hiểu ý người dùng, một sub-agent chuyên biệt lo việc generate và chạy câu lệnh SQL an toàn.
- **Bảo mật và giới hạn an toàn:** Hệ thống tự động giới hạn số lượng bản ghi trả về (LIMIT 10-50) để tránh làm sập database.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted).
- **PostgreSQL Database:** Nơi lưu trữ dữ liệu cần truy vấn.
- **OpenRouter API Key:** Để sử dụng các mô hình AI cao cấp (Claude 3.5 Sonnet).
- **OpenAI API Key:** Dùng cho node chuyển đổi giọng nói thành văn bản (Whisper).
- **Telegram Bot Token:** Tạo qua BotFather để nhận tin nhắn từ người dùng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow, mở n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Telegram Trigger1 & SEND MESSAGE:** Kết nối với `telegramApi` credentials bằng Bot Token của các sếp. Node này nhận câu hỏi và gửi câu trả lời về Telegram.
- **Voice or Text & Transcribe1:** Xử lý tin nhắn thoại từ Telegram. Node **Transcribe1** (OpenAI) cần `openAiApi` để chuyển đổi file âm thanh `.ogg` thành text.
- **Main agent & Query agent (AI Agents):** Sử dụng **OpenRouter Chat Model** (`openRouterApi`) với model `anthropic/claude-3.5-sonnet`. Các sếp cần cấu hình System Prompt cho AI hiểu rõ cấu trúc bảng dữ liệu của mình:
  - Thay thế `[YOUR_DATABASE_SCHEMA]` bằng cấu trúc bảng thực tế.
  - Định nghĩa rõ các trường như `[YOUR_ITEMS]`, `[CATEGORY_FIELD]`, `[PRICE_FIELD]`.
- **Postgres Chat Memory & ACCES DATABASE WITH DYNAMIC QUERYS:** 
  - Kết nối credentials `postgres`.
  - Node **ACCES DATABASE WITH DYNAMIC QUERYS** thực thi câu lệnh SQL do agent tạo ra.
  - ⚠️ **LƯU Ý CỰC KỲ QUAN TRỌNG:** Luôn giới hạn kết quả trả về (`DEFAULT LIMIT: 10`, `MAX LIMIT: 50`) và bắt buộc sử dụng `ORDER BY` cùng `LIMIT` để tránh quá tải database!
- **CALL QUERY AGENT (`toolWorkflow`):** Kết nối Main Agent gọi đến Sub-Agent (Query agent) để xử lý logic sinh câu lệnh SQL.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một tin nhắn đến Telegram Bot của các sếp (ví dụ: *"Tìm cho tôi 5 sản phẩm có giá rẻ nhất"*).
- Kiểm tra kết quả trả về trên Telegram và bật **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Microsoft Teams:** Ngoài Telegram, các sếp có thể nhân bản nhánh Trigger để nhận câu hỏi từ kênh chat nội bộ công ty.
- **Lưu lịch sử truy vấn:** Thêm một node Google Sheets hoặc ghi log vào bảng PostgreSQL riêng để theo dõi các câu hỏi mà nhân viên/sếp hay tra cứu.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để tự động tổng hợp các số liệu hot trong tuần và gửi báo cáo chủ động qua Telegram.

### 📌 Kết luận
Với workflow **Natural Language Database Queries with Dual-Agent AI & PostgreSQL**, việc khai thác dữ liệu trong doanh nghiệp chưa bao giờ dễ dàng đến thế. Không cần SQL, không cần dashboard phức tạp, chỉ cần chat với Telegram là có ngay câu trả lời. Triển khai ngay hôm nay để tối ưu hóa năng suất vận hành các sếp nhé!