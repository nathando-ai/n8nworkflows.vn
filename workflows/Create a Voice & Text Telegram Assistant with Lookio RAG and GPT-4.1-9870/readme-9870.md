---
title: "🤖 **Tạo Trợ Lý Telegram Hỗ Trợ Văn Bản & Âm Thanh Với Lookio RAG + GPT-4.1 (Miễn Code!)**"
description: "Workflow tự động hóa Telegram bot thông minh hỗ trợ cả văn bản và âm thanh, kết hợp Lookio RAG và GPT-4.1 để trả lời câu hỏi chính xác từ cơ sở tri thức cá nhân. Giúp các sếp tiết kiệm thời gian tra cứu thông tin và tự động hóa hỗ trợ khách hàng 24/7."
slug: "tao-tro-ly-telegram-voice-text-lookio-rag-gpt-4-1"
tags: [n8n, automation, no-code, telegram-bot, lookio, gpt-4.1, ai-agent, voice-assistant]
keywords: [n8n workflow telegram bot, tự động hóa trợ lý âm thanh, Lookio RAG, GPT-4.1 tự động hóa, bot hỗ trợ khách hàng, chuyển đổi âm thanh thành văn bản, AI agent Telegram]
---

# 🚀 **Tạo Trợ Lý Telegram Hỗ Trợ Văn Bản & Âm Thanh Với Lookio RAG + GPT-4.1**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, khi làm việc với lượng thông tin lớn hoặc hỗ trợ khách hàng qua Telegram, các sếp thường phải:
- **Tra cứu thủ công** thông tin từ cơ sở dữ liệu hoặc tài liệu nội bộ.
- **Chuyển đổi âm thanh thành văn bản** để phân tích (tốn thời gian và dễ sai sót).
- **Phản hồi chậm** do phải chuyển đổi giữa nhiều công cụ khác nhau.

**Workflow này giúp giải quyết tất cả bằng cách:**
✅ **Tự động chuyển đổi âm thanh thành văn bản** (thông qua Mistral AI).
✅ **Trả lời câu hỏi chính xác** từ cơ sở tri thức cá nhân (Lookio RAG).
✅ **Hỗ trợ cả văn bản và âm thanh** trong Telegram.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến 80% trong việc tra cứu và phản hồi.
- **Chính xác cao** nhờ kết hợp Lookio RAG (Retrieval-Augmented Generation) và GPT-4.1.
- **Hỗ trợ đa dạng** (văn bản + âm thanh) cho khách hàng hoặc đồng nghiệp.
- **Hoạt động tự động** mà không cần can thiệp thủ công.
- **Cá nhân hóa** với khả năng lọc tin nhắn riêng tư (nếu cần).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **API Token** (để kết nối bot).
2. **Tài khoản OpenAI** với **API Key** (hoặc thay thế bằng LLM khác).
3. **Tài khoản Mistral Cloud** với **API Key** (để chuyển đổi âm thanh thành văn bản).
4. **Tài khoản Lookio** với:
   - **API Key** của Lookio.
   - **ID của Trợ Lý Lookio** (đã xây dựng cơ sở tri thức).
5. **Thiết bị** để test bot (máy tính hoặc điện thoại có Telegram).

---
### 🎯 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/9870) hoặc copy toàn bộ JSON từ đây.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create Workflow"** để lưu.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **13 node** quan trọng, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **🔹 Node "Telegram Trigger"**
- **Chức năng:** Khởi động bot khi nhận tin nhắn từ Telegram.
- **Cấu hình:**
  - Đảm bảo **credentials `telegramApi`** đã được thêm vào n8n (cài đặt trong **Credentials → Add Credential → Telegram**).
  - **Username bot:** Sử dụng `@YourBotName` (đã tạo trên [@BotFather](https://t.me/BotFather)).

##### **🔹 Node "Query knowledge base" (HTTP Request Tool)**
- **Chức năng:** Gọi API Lookio để tra cứu thông tin từ cơ sở tri thức.
- **Cấu hình:**
  - Thay thế `<your-lookio-api-key>` bằng **API Key Lookio** của bạn.
  - Thay thế `<your-assistant-id>` bằng **ID của Trợ Lý Lookio** (tìm trong Lookio Dashboard).
  - **URL mẫu:**
    ```json
    "url": "https://api.lookio.app/v1/assistants/<your-assistant-id>/query"
    ```
  - **Headers:**
    ```json
    "Authorization": "Bearer <your-lookio-api-key>"
    ```

##### **🔹 Node "Mistral transcribe" (HTTP Request)**
- **Chức năng:** Chuyển đổi âm thanh thành văn bản (thông qua Mistral AI).
- **Cấu hình:**
  - Thay thế `<your-mistral-api-key>` bằng **API Key Mistral Cloud**.
  - **URL mẫu:**
    ```json
    "url": "https://api.mistral.ai/v1/audio/transcriptions"
    ```
  - **Headers:**
    ```json
    "Authorization": "Bearer <your-mistral-api-key>"
    ```
  - **Body (JSON):**
    ```json
    {
      "model": "whisper-large-v3",
      "file": "{{ $node["Get Audio File"].json["file"]["file_id"] }}"
    }
    ```

##### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Chức năng:** Sử dụng GPT-4.1 để xử lý logic và trả lời.
- **Cấu hình:**
  - Đảm bảo **credentials `openAiApi`** đã được thêm vào n8n.
  - **Model:** Đặt mặc định là `gpt-4.1-mini` (hoặc thay thế bằng model khác như `gpt-4` nếu có).

##### **🔹 Node "Myself?" (If Condition)**
- **Chức năng:** Lọc tin nhắn riêng tư (nếu muốn bot chỉ hoạt động với tài khoản cá nhân).
- **Cấu hình:**
  - Thay thế `{{ $json["from"]["username"] }}` bằng **username Telegram của bạn** (ví dụ: `username_cua_ban`).
  - **Nếu muốn bot công khai:** Xóa node này hoặc thay thế điều kiện thành `true`.

##### **🔹 Node "AI Agent" (Agent)**
- **Chức năng:** Quản lý logic của bot (gọi Lookio khi cần tra cứu).
- **Cấu hình:**
  - **System Message (gợi ý):**
    ```json
    "You are a helpful assistant that uses Lookio RAG to answer questions based on a knowledge base. Always refer to the knowledge base first before providing an answer."
    ```
  - **Tools:** Đảm bảo **"Query knowledge base"** được thêm vào danh sách tools.

---
#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1:** Test run với **dữ liệu mẫu** (gửi tin nhắn văn bản hoặc âm thanh đến bot).
- **Bước 2:** Kiểm tra:
  - Bot có chuyển đổi âm thanh thành văn bản không?
  - Bot có trả lời chính xác từ Lookio không?
  - Tin nhắn có được gửi lại Telegram không?
- **Bước 3:** Nếu test thành công, **bật Active workflow**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram Group:**
   - Thêm node **Slack** hoặc **Telegram Broadcast** để gửi thông báo quan trọng đến nhóm.

2. **Lưu Log & Báo Cáo:**
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử tin nhắn và phản hồi của bot.

3. **Cập Nhật Lookio RAG:**
   - Khi cơ sở tri thức Lookio được cập nhật, bot sẽ tự động phản hồi mới nhất.

4. **Thay Thế Mistral bằng OpenAI Whisper:**
   - Nếu không muốn dùng Mistral, có thể thay thế bằng **OpenAI Whisper** (cần cấu hình node `httpRequest` tương tự).

5. **Tự Động Phản Hồi Email:**
   - Kết hợp với node **Gmail** để bot cũng trả lời email khi nhận được tin nhắn từ Telegram.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa hỗ trợ khách hàng hoặc tra cứu thông tin nhanh chóng trên Telegram. Với sự kết hợp giữa **Lookio RAG, GPT-4.1 và Mistral**, bot không chỉ trả lời chính xác mà còn hỗ trợ cả âm thanh và văn bản.

**🚀 Hãy thử ngay và tiết kiệm thời gian cho công việc hàng ngày!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://discord.gg/n8n).