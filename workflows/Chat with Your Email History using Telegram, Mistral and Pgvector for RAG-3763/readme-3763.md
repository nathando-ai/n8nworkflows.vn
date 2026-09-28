---
title: "🤖 Tự Động Hóa Trợ Lý AI Chat Trên Telegram Từ Lịch Sử Email Bằng Mistral & PGVector - RAG 100% Không Code"
description: "Workflow này giúp các sếp tự động hóa việc truy vấn và trả lời các câu hỏi liên quan đến lịch sử email thông qua Telegram, kết hợp AI Mistral và cơ sở dữ liệu vector PGVector. Giúp tiết kiệm thời gian tìm kiếm thông tin và cải thiện hiệu suất công việc hàng ngày."
slug: "tự-dộng-hoa-trợ-ly-ai-chat-telegram-email-mistral-pgvector"
tags: [n8n, automation, ai, telegram-bot, pgvector, rag, no-code, email-automation, mistral-ai]
keywords: [n8n workflow telegram ai, tự động hóa email bằng ai, chatbot email sử dụng mistral, pgvector n8n, rag với email, tự động hóa công việc office]
---

# 🚀 **Trợ Lý AI Chat Trên Telegram Từ Lịch Sử Email - Cải Thiện Hiệu Suất Công Việc Bằng RAG**

## **Nỗi Đau Thực Tế Của Các Sếp**
Các sếp thường phải mất nhiều thời gian để tìm kiếm thông tin trong lịch sử email, đặc biệt khi phải tra cứu nhiều cuộc trò chuyện hoặc nội dung cũ. Thông thường, việc này yêu cầu:
- **Tìm kiếm thủ công** trong hàng trăm email, mất thời gian và dễ bỏ lỡ thông tin quan trọng.
- **Không thể truy vấn logic** trên dữ liệu email (ví dụ: "Hãy cho tôi biết tất cả các đơn hàng từ khách hàng ABC trong tháng 12").
- **Không có cách nào để tự động hóa** việc trả lời các câu hỏi liên quan đến lịch sử email một cách nhanh chóng và chính xác.

Workflow này giải quyết tất cả những vấn đề trên bằng cách **tự động hóa việc truy vấn và trả lời thông tin từ email** thông qua Telegram, kết hợp **AI Mistral** và **PGVector** để tạo ra một hệ thống **Retrieval-Augmented Generation (RAG)** hiệu quả.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trả lời các câu hỏi liên quan đến email chỉ trong vài giây thay vì mất nhiều giờ tìm kiếm thủ công.
- **Truy vấn logic**: Hỏi về dữ liệu email như một cơ sở dữ liệu (ví dụ: "Hãy liệt kê tất cả các đơn hàng từ năm 2023").
- **Cá nhân hóa**: Trợ lý AI hiểu ngữ cảnh và trả lời chính xác dựa trên lịch sử email của bạn.
- **Hoạt động 24/7**: Workflow chạy tự động trên Telegram, không cần can thiệp thủ công.
- **Tích hợp AI Mistral**: Sử dụng mô hình AI tiên tiến để phân tích và trả lời thông tin một cách tự nhiên.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - API Key từ [@BotFather](https://t.me/BotFather) để tạo bot Telegram.
   - Chat ID của bot (có thể lấy bằng cách gửi tin nhắn cho bot và copy link chat).

2. **Cơ sở dữ liệu PostgreSQL với PGVector**:
   - Cài đặt PostgreSQL và mở rộng **PGVector** để lưu trữ và truy vấn dữ liệu vector.
   - Đã có **lịch sử email** được chuyển đổi thành dữ liệu vector (cần import từ workflow khác: ["Translate questions about e-mails into SQL queries and run them"](https://n8n.io/workflows/3762)).

3. **API Key Ollama**:
   - Cài đặt [Ollama](https://ollama.ai/) và chạy mô hình `nomic-embed-text:latest` để tạo embedding cho văn bản.

4. **API Key Mistral (OpenAI Compatible)**:
   - Sử dụng mô hình `mistral-small3.1:latest` (hoặc mô hình tương thích khác) để chat AI.

5. **Workflow phụ trợ**:
   - **Workflow "Translate questions about e-mails into SQL queries and run them"** (của tác giả Alfonso Corretti) để chuyển đổi câu hỏi thành truy vấn SQL và lấy kết quả từ cơ sở dữ liệu.
   - [Tải workflow này tại đây](https://n8n.io/workflows/3762) và cấu hình để trỏ đến cơ sở dữ liệu email của bạn.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/3763](https://n8n.io/workflows/3763) (chọn "Export").
2. Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **"Import"** trong menu.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **16 node** và cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

#### **A. Cấu Hình Telegram Trigger**
- **Node**: `Telegram Trigger`
- **Tham số cần thiết**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình API Key từ BotFather).
  - **Chat ID**: Điền Chat ID của bot (có thể lấy bằng cách gửi tin nhắn cho bot và copy từ URL).
  - **Message Type**: Chọn `text` để nhận tin nhắn văn bản.

#### **B. Cấu Hình Workflow Phụ "Translate questions about e-mails into SQL queries and run them"**
- **Node**: `Call the SQL composer Workflow` (type: `toolWorkflow`)
- **Tham số cần thiết**:
  - **Workflow URL**: Điền URL của workflow phụ (ví dụ: `http://localhost:5678/workflow/3762`).
  - **Credentials**: Chọn `postgres` (nếu workflow phụ cần kết nối CSDL).
  - **Input Data**: Workflow này sẽ tự động truyền dữ liệu từ câu hỏi Telegram sang workflow phụ để chuyển đổi thành SQL và lấy kết quả.

#### **C. Cấu Hình PGVector Store**
- **Node**: `Postgres PGVector Store` (type: `vectorStorePGVector`)
- **Tham số cần thiết**:
  - **Credentials**: Chọn `postgres` (đã cấu hình kết nối đến CSDL PostgreSQL với PGVector).
  - **Collection Name**: Điền tên collection lưu trữ embedding (ví dụ: `email_embeddings`).
  - **Vector Dimension**: Điền `384` (do mô hình `nomic-embed-text` tạo ra).

#### **D. Cấu Hình Embeddings Ollama**
- **Node**: `Embeddings Ollama` (type: `embeddingsOllama`)
- **Tham số cần thiết**:
  - **Credentials**: Chọn `ollamaApi`.
  - **Model**: Đặt cố định là `nomic-embed-text:latest`.
  - **Input Text**: Dữ liệu từ email sẽ được chuyển vào đây để tạo embedding.

#### **E. Cấu Hình AI Agent (Mistral)**
- **Node**: `AI Agent` (type: `agent`)
- **Tham số cần thiết**:
  - **Tools**: Chọn `Postgres PGVector Store` và `Call the SQL composer Workflow`.
  - **Memory**: Chọn `Simple Memory` (type: `memoryBufferWindow`) để lưu trữ lịch sử chat.

- **Node**: `OpenAI Chat Model` (type: `lmChatOpenAi`)
  - **Credentials**: Chọn `openAiApi` (hoặc `mistralApi` nếu sử dụng API Mistral).
  - **Model**: Đặt `mistral-small3.1:latest` (hoặc mô hình tương thích).
  - **System Prompt**: Có thể tùy chỉnh để cải thiện chất lượng trả lời (ví dụ: "Bạn là trợ lý AI chuyên trả lời câu hỏi về lịch sử email.").

#### **F. Cấu Hình Telegram Response**
- **Node**: `Respond on Telegram in batches` (type: `telegram`)
  - **Credentials**: Chọn `telegramApi`.
  - **Chat ID**: Điền Chat ID của bot.
  - **Message**: Dữ liệu từ AI Agent sẽ được gửi về Telegram dưới dạng tin nhắn.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một câu hỏi mẫu đến bot Telegram (ví dụ: "Hãy cho tôi biết tất cả các đơn hàng từ khách hàng ABC trong tháng 12").
   - Kiểm tra kết quả trả lời và điều chỉnh nếu cần.

2. **Bật Active Workflow**:
   - Nhấn **"Active"** để workflow chạy liên tục.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích Hợp Slack/Email**:
   - Thay vì chỉ Telegram, các sếp có thể thêm node `email` hoặc `slack` để nhận câu hỏi từ nhiều kênh.

2. **Lưu Log Chat**:
   - Sử dụng node `stickyNote` hoặc `set` để lưu lịch sử chat vào cơ sở dữ liệu để phân tích sau này.

3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow riêng để tổng hợp và gửi báo cáo tổng hợp từ email hàng tuần/monthly.

4. **Cải Thiện Prompt AI**:
   - Tùy chỉnh `system prompt` trong node `OpenAI Chat Model` để AI trả lời chính xác hơn (ví dụ: "Bạn phải trả lời dựa trên dữ liệu từ email, không được invent").

5. **Sử Dụng Mô Hình AI Khác**:
   - Thay thế Mistral bằng mô hình khác như `llama3` hoặc `gemini` nếu có API tương thích.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc truy vấn và trả lời thông tin từ email một cách nhanh chóng và chính xác. Bằng cách kết hợp **Telegram, AI Mistral, PGVector và SQL**, bạn có thể:
✅ **Tiết kiệm thời gian** tìm kiếm email.
✅ **Truy vấn logic** trên dữ liệu email như một cơ sở dữ liệu.
✅ **Cải thiện hiệu suất công việc** với trợ lý AI 24/7.

**Hãy áp dụng ngay và tự động hóa công việc email của mình!** 🚀

---
:::note[CHÚ Ý]
- Để workflow chạy ổn định 24/7, các sếp nên **self-host n8n trên VPS** (không dùng phiên bản cloud).
- Nếu gặp lỗi, kiểm tra lại **credentials** và **cấu hình CSDL PostgreSQL**.
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::