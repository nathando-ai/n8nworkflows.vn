---
title: "📧 Tự Động Tạo Tóm Tắt Tin Tức Hàng Ngày Từ Gmail Bằng GPT-4.1-mini (Không Cần Code)"
description: "Workflow tự động hóa lấy tất cả email từ Gmail, tóm tắt nội dung bằng AI, và gửi tóm tắt định kỳ qua Telegram hoặc email. Giúp các sếp tiết kiệm 5+ giờ mỗi tuần theo dõi tin tức."
slug: "tự-dộng-tạo-tóm-tắt-tin-tức-hàng-ngày-từ-gmail-bằng-gpt-4-1-mini"
tags: [n8n, automation, gmail, ai, gpt-4, telegram, email, productivity]
keywords: [n8n workflow gmail, tự động hóa email, tóm tắt tin tức bằng AI, gpt-4.1-mini, tự động gửi tin tức hàng ngày, workflow n8n telegram]
---

# 🚀 **Tự Động Tạo Tóm Tắt Tin Tức Hàng Ngày Từ Gmail Bằng GPT-4.1-mini**

### **Giải pháp cho các sếp bị "ngập" email tin tức hàng ngày**
Hàng ngày, các sếp phải mở Gmail để đọc và tóm tắt hàng chục email tin tức từ các nguồn như *TechCrunch, Bloomberg, Reuters*... Thời gian này có thể lên đến **5-10 giờ/tuần** nếu làm thủ công. **Workflow này tự động hóa toàn bộ quá trình**:
- Lấy tất cả email từ Gmail (hoặc từ ngày cụ thể).
- Sử dụng **GPT-4.1-mini** tóm tắt nội dung email thành các điểm chính.
- **Tự động gửi tóm tắt** qua Telegram (hoặc email) với định dạng HTML đẹp mắt, phù hợp với giới hạn của Telegram.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** mà không gián đoạn, các sếp nên **self-host n8n** trên VPS.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 5-10 giờ/tuần** theo dõi email tin tức.
✅ **Tóm tắt chính xác** bằng GPT-4.1-mini (không bỏ sót điểm quan trọng).
✅ **Gửi tự động** qua Telegram (hoặc email) với định dạng HTML đẹp.
✅ **Lọc email từ ngày cụ thể** (ví dụ: chỉ lấy email từ ngày hôm qua).
✅ **Hoạt động liên tục** (không cần can thiệp thủ công).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
2. **API Key OpenAI** (để sử dụng GPT-4.1-mini).
3. **Bot Telegram** (nếu muốn gửi tóm tắt qua Telegram).
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào nhóm Telegram cá nhân để nhận tin nhắn.
4. **VPS** (nếu self-host n8n) hoặc tài khoản n8n Cloud (miễn phí cho workflow nhỏ).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7255](https://n8n.io/workflows/7255) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node**, các sếp cần chú ý cấu hình sau:

##### **A. Cấu hình Gmail OAuth2**
- **Node "Get many messages"** và **"Get a message"** cần **credentials `gmailOAuth2`**.
  - Đăng nhập vào n8n và tạo **credentials mới** (type: `Gmail OAuth2`).
  - Chọn **scope**: `https://www.googleapis.com/auth/gmail.readonly`.
  - Sau khi cấp quyền, lưu lại **Client ID** và **Client Secret**.

##### **B. Cấu hình OpenAI API**
- **Node "Message a model"** cần **credentials `openAiApi`**.
  - Tạo **credentials mới** (type: `OpenAI API`).
  - Điền **API Key** từ tài khoản OpenAI (truy cập [OpenAI Platform](https://platform.openai.com/)).
  - Chọn **model**: `gpt-4-1106-preview` (hoặc `gpt-4.1-mini` nếu có).

##### **C. Cấu hình Telegram (nếu muốn gửi qua Telegram)**
- **Node "Send a message"** (nếu muốn gửi qua email) hoặc **thêm node Telegram** (nếu muốn gửi qua Telegram).
  - **Nếu gửi qua email**:
    - Đảm bảo **credentials Gmail** đã cấu hình đúng.
  - **Nếu gửi qua Telegram**:
    - Thêm **node `HTTP Request`** (type: `Request`) với:
      - **Method**: `POST`
      - **URL**: `https://api.telegram.org/bot<API_TOKEN>/sendMessage`
      - **Headers**: `Content-Type: application/json`
      - **Body**:
        ```json
        {
          "chat_id": "<CHAT_ID>",
          "text": "{{ $json }}",
          "parse_mode": "HTML"
        }
        ```
    - Thay `<API_TOKEN>` bằng **API Token** của bot Telegram.
    - Thay `<CHAT_ID>` bằng **ID chat** của nhóm Telegram (lấy từ `@username_to_id_bot`).

##### **D. Cấu hình Schedule Trigger**
- **Node "Schedule Trigger"** quyết định khi nào workflow chạy.
  - Mặc định là **lúc 8h sáng hàng ngày**, nhưng các sếp có thể chỉnh sửa:
    - **Cron expression**: `0 8 * * *` (8h sáng hàng ngày).
    - Hoặc **chọn "Manual trigger"** để chạy thủ công.

##### **E. Cấu hình Code Nodes (đọc kỹ!)**
Workflow có **3 node Code** cần chỉnh sửa để phù hợp:
1. **"Get message data"**:
   - Lấy dữ liệu email (tiêu đề, nội dung, ngày gửi).
   - **Không cần chỉnh sửa** (n8n tự động hóa).
2. **"Merge"**:
   - Ghép các email thành một chuỗi JSON.
   - **Không cần chỉnh sửa** (n8n tự động).
3. **"Clean"**:
   - Lọc và chuẩn hóa dữ liệu trước khi gửi.
   - **Không cần chỉnh sửa** (n8n tự động).
4. **"Create template"**:
   - **Cần chỉnh sửa** nếu muốn thay đổi định dạng HTML của tin nhắn.
   - Mẫu HTML mặc định:
     ```javascript
     return {
       json: {
         body: `
           <b>📰 Tóm tắt tin tức hàng ngày (${new Date().toLocaleDateString()})</b>
           <hr>
           ${$input.all().map(item => `
             <b>${item.subject}</b>
             <p>${item.summary}</p>
             <hr>
           `).join('')}
         `
       }
     };
     ```

#### **3. Kích hoạt ⚡️**
- **Test run**:
  - Chọn **node "Schedule Trigger"** và nhấn **"Run Workflow"**.
  - Kiểm tra **log** để đảm bảo workflow chạy đúng.
- **Bật Active**:
  - Sau khi test thành công, **bật "Active"** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lọc email theo ngày cụ thể**:
   - Trong node **"Get many messages"**, thêm **filter** để lấy email từ ngày nhất định:
     ```json
     {
       "query": "after:${date}"
     }
     ```
   - Ví dụ: `after:2024-05-01T00:00:00Z` (lấy email từ ngày 1/5/2024).

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Thêm **node `Email`** (nếu muốn gửi qua email) hoặc **node `Slack`** (nếu muốn gửi qua Slack).
   - Ví dụ với Slack:
     - Tạo **credentials Slack** trong n8n.
     - Thêm node `HTTP Request` với URL: `https://slack.com/api/chat.postMessage`.
     - Body:
       ```json
       {
         "channel": "#tin-tuc",
         "text": "{{ $json.body }}"
       }
       ```

3. **Tăng độ chính xác của AI**:
   - Trong node **"Message a model"**, chỉnh sửa **prompt** để AI tóm tắt tốt hơn:
     ```json
     {
       "model": "gpt-4-1106-preview",
       "messages": [
         {
           "role": "system",
           "content": "Bạn là một trợ lý tóm tắt tin tức chuyên nghiệp. Hãy tóm tắt email này thành 3-5 điểm chính, không bao gồm nội dung không liên quan."
         },
         {
           "role": "user",
           "content": "{{ $json.body }}"
         }
       ]
     }
     ```

4. **Lưu log cho theo dõi**:
   - Thêm **node `StickyNote`** để lưu kết quả cuối cùng vào database hoặc file.
   - Ví dụ:
     ```javascript
     return {
       stickyNote: {
         data: {
           timestamp: new Date().toISOString(),
           summary: $input.all().map(item => item.json.body).join('\n')
         }
       }
     };
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc đọc email tin tức thủ công hàng ngày. Với **GPT-4.1-mini**, nội dung được tóm tắt **chính xác và ngắn gọn**, sau đó được gửi tự động qua **Telegram hoặc email**.

**Hành động ngay!**
1. **Import workflow** và cấu hình Gmail + OpenAI.
2. **Test run** và chỉnh sửa nếu cần.
3. **Bật Active** và bắt đầu tự động hóa!

👉 **[Tải workflow nguyên bản](https://n8n.io/workflows/7255)** và bắt đầu sử dụng ngay!