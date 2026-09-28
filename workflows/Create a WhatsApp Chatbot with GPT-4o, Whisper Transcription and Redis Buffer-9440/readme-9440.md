---
title: "🤖 Tự Động Hóa Chatbot WhatsApp Siêu Năng với GPT-4o, Chuyển Văn Bản Audio & Redis Buffer - Không Cần Code!"
description: "Workflow tự động hóa chatbot WhatsApp thông minh hỗ trợ xử lý văn bản, âm thanh và hình ảnh bằng GPT-4o, chuyển văn bản từ âm thanh với Whisper, và bộ đệm Redis để xử lý luồng tin nhắn liên tục. Giúp các sếp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tự động hóa hỗ trợ 24/7."
slug: "tay-dong-hoa-chatbot-whatsapp-gpt-4o-whisper-redis"
tags: [n8n, automation, no-code, chatbot, ai, openai, redis, wasenderapi, gpt-4o, whisper]
keywords: [n8n workflow chatbot whatsapp, tự động hóa whatsapp với ai, chuyển văn bản từ âm thanh, gpt-4o xử lý hình ảnh, redis buffer tin nhắn, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Chatbot WhatsApp Siêu Năng với GPT-4o, Chuyển Văn Bản từ Âm Thanh và Bộ Đệm Redis**

## **💡 Bạn đã bao giờ mệt mỏi vì phải trả lời hàng trăm tin nhắn WhatsApp mỗi ngày?**
Hãy tưởng tượng một chatbot **tự động** xử lý **văn bản, âm thanh và hình ảnh** bằng trí tuệ nhân tạo GPT-4o, chuyển văn bản từ âm thanh bằng Whisper, và **bộ đệm Redis** để xử lý luồng tin nhắn liên tục mà không mất thời gian chờ đợi. **Không cần viết một dòng code nào!**

Workflow này giúp các sếp:
✅ **Tiết kiệm thời gian** – Chatbot tự động trả lời khách hàng 24/7.
✅ **Xử lý mọi loại tin nhắn** – Văn bản, âm thanh, hình ảnh.
✅ **Hiểu ngữ cảnh** – Nhớ lại lịch sử trò chuyện với bộ nhớ Redis.
✅ **Tránh bị chặn** – Thời gian chờ 6 giây giữa các phản hồi để tránh bị WhatsApp phát hiện là bot.
✅ **Tiết kiệm chi phí** – Chỉ trả tiền cho OpenAI khi thực sự cần.

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hỗ trợ khách hàng** – Chatbot trả lời tin nhắn văn bản, âm thanh và hình ảnh một cách tự động.
- **Chuyển văn bản từ âm thanh** – Khách hàng gửi âm thanh, chatbot tự động chuyển thành văn bản và xử lý.
- **Hiểu ngữ cảnh** – Chatbot nhớ lại lịch sử trò chuyện qua Redis, không cần khách hàng phải giải thích lại.
- **Tránh bị chặn** – Thời gian chờ 6 giây giữa các phản hồi để tránh bị WhatsApp phát hiện là bot.
- **Tiết kiệm chi phí** – Chỉ trả tiền cho OpenAI khi thực sự cần xử lý tin nhắn.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản WasenderAPI** (để kết nối WhatsApp):
   - Đăng ký tại [wasenderapi.com](https://wasenderapi.com)
   - Chọn gói từ **$6-$45/month**
   - Tạo session với số điện thoại WhatsApp của bạn
   - Quét mã QR để kết nối
   - **Lưu ý:** Đối với số mới, sử dụng thủ công trong **7 ngày đầu** để tránh bị phát hiện.

2. **Tài khoản OpenAI** (để sử dụng GPT-4o và Whisper):
   - Đăng ký tại [platform.openai.com](https://platform.openai.com)
   - Thêm phương thức thanh toán (OpenAI yêu cầu thanh toán trước khi sử dụng)
   - **Chi phí tham khảo:**
     - Chuyển văn bản từ âm thanh (~$0.006/phút)
     - Xử lý hình ảnh (~$0.01/hình)

3. **Bộ đệm Redis** (để lưu trữ tin nhắn và lịch sử trò chuyện):
   - Tạo tài khoản miễn phí tại [redis.io](https://redis.io)
   - Cấu hình Redis để lưu trữ dữ liệu tin nhắn và bộ nhớ chatbot.

4. **API Key của các dịch vụ**:
   - **OpenAI API Key** (từ OpenAI Dashboard)
   - **Redis URL & Password** (từ tài khoản Redis)
   - **WasenderAPI Credentials** (từ dashboard WasenderAPI)

---
---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import Workflow** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/9440)).
3. **Không cần chỉnh sửa cấu trúc**, chỉ cần **cấu hình credentials** như hướng dẫn dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **27 node**, nhưng chỉ có **5 node quan trọng cần cấu hình** để hoạt động:
##### **A. Cấu hình WasenderAPI (Node `manualTrigger` và `httpRequest`)**
- **Node `When clicking 'Execute workflow'` (manualTrigger)**:
  - **Lưu ý:** Trong môi trường sản xuất, **không nên dùng manual trigger**. Thay vào đó, **cấu hình Webhook** để WasenderAPI tự động kích hoạt workflow khi nhận tin nhắn.
  - **Cách cấu hình Webhook:**
    1. Trong **n8n**, mở **Settings > Webhooks**.
    2. Tạo một **Webhook mới** với URL như:
       ```
       https://tên-máy-chủ-n8n.com/webhook/your-webhook-id
       ```
    3. Trong **WasenderAPI Dashboard**, đi đến **Webhooks** và thêm:
       - **Event:** `messages.received`
       - **URL:** URL Webhook từ n8n
       - **Method:** `POST`
    4. **Kiểm tra:** Gửi tin nhắn WhatsApp, workflow sẽ tự động kích hoạt.

- **Node `Send Message to User` (httpRequest)**:
  - **URL:** `https://api.wasenderapi.com/v1/messages`
  - **Headers:**
    - `Authorization: Bearer YOUR_WASENDER_API_KEY`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "to": "CHAT_ID",
      "body": "RESPONSE_FROM_AI",
      "type": "text"
    }
    ```

##### **B. Cấu hình OpenAI (Node `openAi`, `lmChatOpenAi`)**
- **Node `Transcribe a recording` (openAi)**:
  - **Credentials:** `openAiApi` (đã cấu hình trước trong n8n)
  - **Key Parameters:**
    - `operation`: `transcribe`
    - `resource`: `audio`
    - **Model:** `whisper-1` (mặc định)
    - **File:** Được tải từ `Download the audio` (node `httpRequest`)

- **Node `Analyze image` (openAi)**:
  - **Credentials:** `openAiApi`
  - **Key Parameters:**
    - `operation`: `analyze`
    - `resource`: `image`
    - **Model:** `gpt-4o` (hoặc `gpt-4-vision-preview`)

- **Node `OpenAI Chat Model` (lmChatOpenAi)**:
  - **Credentials:** `openAiApi`
  - **Key Parameters:**
    - `model`: `gpt-4.1-mini` (hoặc `gpt-4o` nếu có)
    - **Prompt:** Được định nghĩa trong **AI Agent** (node `agent`).

##### **C. Cấu hình Redis (Node `redis`, `redis1`, `redis2`)**
- **Node `Redis` (push), `Redis1` (get), `Redis2` (delete)**:
  - **Credentials:** `redis` (đã cấu hình trước trong n8n)
  - **Key Parameters:**
    - `operation`: `push` (lưu tin nhắn), `get` (lấy tin nhắn), `delete` (xóa sau xử lý)
  - **Redis Key:** `chat_buffer:CHAT_ID` (để lưu trữ tin nhắn của từng chat)

##### **D. Cấu hình AI Agent (Node `agent`)**
- **Node `AI Agent`**:
  - **Credentials:** `openAiApi`
  - **Key Parameters:**
    - **System Prompt:** Cần tự định nghĩa (ví dụ:
      ```json
      {
        "role": "system",
        "content": "Bạn là một trợ lý hỗ trợ khách hàng chuyên nghiệp. Hãy trả lời tin nhắn một cách thân thiện và chuyên nghiệp. Nếu khách hàng gửi âm thanh, hãy chuyển thành văn bản trước khi trả lời."
      }
      ```
    - **Memory:** Sử dụng `Simple Memory` (node `memoryBufferWindow`) để lưu trữ lịch sử trò chuyện.

##### **E. Cấu hình Switch (Node `Switch Type`)**
- **Node `Switch Type`**:
  - **Condition:**
    - `content_type === "text"` → Xử lý văn bản.
    - `content_type === "audio"` → Chuyển âm thanh thành văn bản.
    - `content_type === "image"` → Xử lý hình ảnh.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra logic):
   - Nhấn **Execute Workflow** và gửi tin nhắn WhatsApp.
   - Kiểm tra **n8n Logs** để đảm bảo workflow chạy đúng.
2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động liên tục.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG NÂNG CAO]
1. **Kết nối với Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để gửi báo cáo hoặc thông báo lỗi.

2. **Lưu log tin nhắn**:
   - Thêm **node `set`** sau `Send Message to User` để lưu tin nhắn đã gửi vào **Google Sheets** hoặc **Airtable**.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `schedule`** để gửi báo cáo tổng hợp số lượng tin nhắn đã xử lý hàng ngày.

4. **Cải thiện prompt cho AI**:
   - Thay đổi **system prompt** trong **AI Agent** để chatbot trả lời phù hợp với ngành nghề của doanh nghiệp.

5. **Optimize chi phí OpenAI**:
   - Sử dụng **GPT-4.1-mini** thay vì GPT-4 để giảm chi phí.
   - **Bộ đệm Redis** giúp tránh xử lý tin nhắn trùng lặp.
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa chatbot WhatsApp với **GPT-4o, chuyển văn bản từ âm thanh và bộ đệm Redis**, giúp các sếp **tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tự động hóa hỗ trợ 24/7** mà **không cần viết một dòng code nào!**

**👉 Hãy áp dụng ngay và tự động hóa hỗ trợ khách hàng của bạn!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/9440)**