---
title: "📄 Chat với PDF qua Telegram - Tự động hóa hoàn toàn bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa chat với tài liệu PDF qua Telegram bằng n8n, tích hợp AI LangChain và Pinecone. Giải phóng thời gian và nâng cao hiệu suất làm việc."
slug: "chat-voi-pdf-qua-telegram-n8n"
tags: [n8n, automation, no-code, ai, langchain, pinecone, telegram]
keywords: [n8n workflow, tự động hóa, chat pdf, telegram bot, langchain, pinecone, groq]
---

# 📄 Chat với PDF qua Telegram - Tự động hóa hoàn toàn bằng n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình chat với tài liệu PDF qua Telegram
- Tiết kiệm thời gian xử lý tài liệu lên tới 90%
- Tăng hiệu suất làm việc nhờ AI LangChain và Pinecone
- Hỗ trợ nhiều định dạng tài liệu khác nhau
- Tích hợp dễ dàng với các công cụ khác trong hệ sinh thái n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API key từ OpenAI (cho embeddings)
- API key từ Pinecone (cho vector store)
- API key từ Groq (cho AI model)
- Tài liệu PDF mẫu để test workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** (Node đầu tiên):
   - Cấu hình credentials với Telegram API
   - Điền bot token và chat ID của bạn

2. **Embeddings OpenAI** (2 node):
   - Cấu hình credentials với OpenAI API
   - Điền API key từ OpenAI
   - Chọn model phù hợp (ví dụ: text-embedding-ada-002)

3. **Pinecone Vector Store** (2 node):
   - Cấu hình credentials với Pinecone API
   - Điền API key và environment từ Pinecone
   - Tạo index mới hoặc sử dụng index đã có

4. **Groq Chat Model**:
   - Cấu hình credentials với Groq API
   - Điền API key từ Groq
   - Chọn model (đã được cấu hình sẵn là llama-3.1-70b-versatile)

5. **Telegram get File**:
   - Đảm bảo bot có quyền truy cập file từ Telegram
   - Kiểm tra quyền của bot trong nhóm/cuộc trò chuyện

6. **Telegram Response** (2 node):
   - Cấu hình tương tự như Telegram Trigger
   - Đảm bảo bot có quyền gửi tin nhắn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu (gửi một tài liệu PDF qua Telegram để kiểm tra quá trình lưu trữ)
- Test chat với tài liệu đã lưu (gửi câu hỏi liên quan đến nội dung PDF)
- Bật Active workflow sau khi kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các câu hỏi và câu trả lời
- Tích hợp với Slack/Teams để thông báo khi có yêu cầu mới
- Thêm node để gửi báo cáo định kỳ về hoạt động của bot
- Tối ưu hóa model Groq để phù hợp với loại tài liệu cụ thể
- Thêm tính năng xác thực người dùng trước khi cho phép chat

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa chat với tài liệu PDF qua Telegram, giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất làm việc. Với sự kết hợp của AI LangChain và Pinecone, hệ thống có thể xử lý và trả lời các câu hỏi liên quan đến nội dung tài liệu một cách chính xác và nhanh chóng.