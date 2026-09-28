---
title: "🤖 **Tự Động Xử Lý Tin Nhắn Trực Tiếp Rocket.Chat Với AI – Không Cần Code!**"
description: "Workflow này tự động thu thập, lọc và xử lý tin nhắn trực tiếp (DM) trên Rocket.Chat, đánh dấu là đã đọc và chuẩn bị trả lời thông minh. Giúp các sếp tiết kiệm thời gian phản hồi và cải thiện trải nghiệm khách hàng 24/7."
slug: "tu-dong-xu-ly-tin-nhan-rocketchat-ai"
tags: [n8n, automation, rocket.chat, ai-chatbot, no-code, support-chatbot]
keywords: [n8n workflow rocket chat, tự động hóa tin nhắn trực tiếp, chatbot rocket chat, xử lý tin nhắn tự động, tiết kiệm thời gian phản hồi]
---

# 🚀 **Tự Động Xử Lý Tin Nhắn Trực Tiếp Rocket.Chat Với AI – Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải mất thời gian quét qua hàng chục tin nhắn trực tiếp (DM) trên Rocket.Chat để trả lời, đánh dấu là đã đọc, và xử lý yêu cầu khách hàng. Điều này không chỉ tốn thời gian mà còn dễ gây lỡ sót, đặc biệt khi lượng tin nhắn tăng cao. **Workflow này giải quyết vấn đề đó bằng cách tự động:**
- **Thu thập** tất cả tin nhắn mới từ các kênh DM.
- **Lọc** và **xử lý** tin nhắn của người dùng (không phải bot).
- **Đánh dấu** tin nhắn là đã đọc để tránh nhầm lẫn.
- **Chuẩn bị trả lời** thông minh (có thể kết hợp với AI hoặc logic nghiệp vụ).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phản hồi** tin nhắn DM.
- **Tránh nhầm lẫn** với tin nhắn đã đọc hoặc bot.
- **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng.
- **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.
- **Dễ dàng mở rộng** với logic xử lý tin nhắn thông minh (AI, business rules).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Rocket.Chat** với quyền API (Admin hoặc có quyền truy cập API).
2. **API Key của Rocket.Chat** (tham khảo [hướng dẫn tạo API Key](https://rocket.chat/docs/developer-guides/api/)).
3. **Tên bot** (được cấu hình trong node `Only Users Prompt` để loại bỏ tin nhắn của bot).
4. **Thời gian lịch trình** (ví dụ: chạy hàng giờ để kiểm tra tin nhắn mới).
5. **(Tùy chọn) Logic xử lý tin nhắn** (có thể sử dụng node `code` để gọi API AI hoặc áp dụng quy tắc nghiệp vụ).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15775](https://n8n.io/workflows/15775) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-hosted** (nếu tự cài đặt trên VPS).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **13 node** với logic phân chia rõ ràng. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Credentials Rocket.Chat**
- **Node `RocketChat`** (tên node: `RocketChat`):
  - Chọn **credentials** là `rocketchatApi`.
  - Điền **API Key** và **URL Rocket.Chat** (ví dụ: `https://tên_domains.rocket.chat`).
  - Kiểm tra lại **scope** (nên chọn `all` để có quyền truy cập đầy đủ).

##### **B. Cấu Hình Lịch Trình (Schedule Trigger)**
- **Node `Schedule Trigger`**:
  - Thiết lập **thời gian chạy** (ví dụ: `0 * * * *` để chạy hàng giờ).
  - **Lưu ý**: Thời gian này quyết định tần suất kiểm tra tin nhắn mới.

##### **C. Lọc Tin Nhắn Của Người Dùng (Loại Bỏ Bot)**
- **Node `Only Users Prompt` (Filter)**:
  - Cấu hình **filter expression** như sau:
    ```json
    {{ $json["message"]["sender"]["username"] }} != "bot_username"
    ```
    (Thay `bot_username` bằng tên bot của Rocket.Chat).
  - **Mục đích**: Loại bỏ tin nhắn của bot để chỉ xử lý tin nhắn của người dùng.

##### **D. Lọc Tin Nhắn Mới & Đã Đọc**
- **Node `Unread and Direct Messages` (Filter)**:
  - Cấu hình **filter expression** để chỉ lấy tin nhắn:
    ```json
    {{ $json["message"]["type"] == "message" && $json["message"]["unread"] == true }}
    ```
  - **Lưu ý**: Node này đảm bảo chỉ lấy tin nhắn **chưa đọc** và **trực tiếp (DM)**.

##### **E. Đánh Dấu Tin Nhắn Là Đã Đọc**
- **Node `Mark as Read` (HTTP Request)**:
  - Sử dụng **method `PUT`** và **URL**:
    ```
    https://tên_domains.rocket.chat/api/v1/messages/{{ $json["_id"] }}/read
    ```
  - **Headers**:
    ```
    Authorization: Bearer {{ $credentials["rocketchatApi"]["apiKey"] }}
    ```
  - **Mục đích**: Đánh dấu tin nhắn là đã đọc ngay sau khi xử lý.

##### **F. Xử Lý Tin Nhắn (Node `code`)**
- **Node `Get last` (Code)**:
  - Đây là nơi **các sếp có thể thêm logic xử lý tin nhắn** (ví dụ: gọi API AI, trích xuất thông tin, xây dựng phản hồi).
  - **Ví dụ code đơn giản** (có thể mở rộng):
    ```javascript
    // Trích xuất nội dung tin nhắn
    const messageContent = $input.all()[0].json.message.text;

    // Xử lý với AI (ví dụ: gọi API OpenAI)
    const aiResponse = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: { "Authorization": `Bearer {{ $credentials["openaiApi"]["apiKey"] }}` },
      body: JSON.stringify({ messages: [{ role: "user", content: messageContent }] })
    });

    // Trả về kết quả để gửi lại Rocket.Chat
    return { json: { reply: await aiResponse.json() } };
    ```
  - **Lưu ý**: Nếu không cần AI, có thể bỏ qua node này và sử dụng **node `No Operation`** để chuyển tiếp tin nhắn.

##### **G. Gửi Trả Lời Lại Rocket.Chat**
- **Node `RocketChat` (cuối workflow)**:
  - Chọn **action** là `sendMessage`.
  - **Tham số cần điền**:
    - **Room ID**: ID của kênh DM (có thể lấy từ tin nhắn trước đó).
    - **Message**: Nội dung trả lời (có thể lấy từ node `code` hoặc `stickyNote`).
  - **Ví dụ**:
    ```json
    {
      "roomId": "{{ $json["roomId"] }}",
      "message": "{{ $json["reply"] }}"
    }
    ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **node `Schedule Trigger`** > **Run Workflow**.
   - Kiểm tra **log** để đảm bảo workflow chạy đúng logic.
2. **Bật Active**:
   - Đánh dấu workflow là **Active** để chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với AI (LLM) để Trả Lời Thông Minh**:
   - Sử dụng node `code` để gọi API AI (OpenAI, Mistral, hoặc các model khác).
   - **Ví dụ**: Trích xuất yêu cầu khách hàng và trả lời tự động với logic nghiệp vụ.

2. **Lưu Log Tin Nhắn**:
   - Thêm **node `stickyNote`** hoặc **Google Sheets** để ghi lại lịch sử tin nhắn và phản hồi.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `scheduleTrigger`** kết hợp với **node `email`** để gửi báo cáo tổng hợp tin nhắn hàng ngày.

4. **Tùy Chỉnh Lọc Tin Nhắn**:
   - Thêm **node `filter`** để lọc tin nhắn theo từ khóa (ví dụ: chỉ xử lý tin nhắn chứa "hỗ trợ").

5. **Kết Nối Với Slack/Telegram**:
   - Thêm **node `webhook`** để gửi tin nhắn mới đến Slack/Telegram để các sếp theo dõi.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa xử lý tin nhắn trực tiếp trên Rocket.Chat, giúp các sếp **tiết kiệm thời gian**, **cải thiện phản hồi** và **tăng cường trải nghiệm khách hàng**. Bằng cách cấu hình đơn giản và mở rộng logic xử lý, các sếp có thể **tạo ra một chatbot thông minh** mà không cần viết một dòng code nào!

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!** Nếu có thắc mắc, hãy để lại comment bên dưới. 👇