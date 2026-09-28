---
title: "🤖 Tự Động Tóm Tắt Cuộc Họp Hàng Ngày với Google Calendar + Gemini AI (Slack → Discord → WhatsApp)"
description: "Workflow tự động hóa tóm tắt cuộc họp hàng ngày từ Google Calendar, sử dụng AI Gemini để tổng hợp nội dung và gửi kết quả đến Slack, Discord hoặc WhatsApp - tiết kiệm thời gian lên đến 30% cho các sếp."
slug: "tom-tat-cuoc-hop-hang-ngay-google-calendar-gemini"
tags: [n8n, automation, ai-summarization, google-calendar, slack-discord-whatsapp, gemini-ai]
keywords: [n8n workflow tự động hóa, tóm tắt cuộc họp AI, google calendar + gemini, gửi báo cáo cuộc họp slack discord whatsapp, tự động hóa cuộc họp hàng ngày]
---

# 🚀 **Tự Động Tóm Tắt Cuộc Họp Hàng Ngày với AI Gemini (Google Calendar → Slack/Discord/WhatsApp)**

### **Nỗi Đau Của Các Sếp**
Làm việc với nhiều cuộc họp hàng ngày khiến các sếp phải mất **giờ đồng hồ** để ghi chép, tổng hợp và chia sẻ kết quả. Thậm chí, nhiều thông tin quan trọng còn bị "lọt" trong quá trình ghi nhớ hoặc ghi chép thủ công. **Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động** lấy thông tin cuộc họp từ Google Calendar.
✅ **Sử dụng AI Gemini** để tóm tắt nội dung chi tiết, chính xác.
✅ **Gửi báo cáo** đến **Slack, Discord hoặc WhatsApp** một cách cá nhân hóa.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải ghi chép thủ công sau mỗi cuộc họp (giảm **30% thời gian**).
- **Tóm tắt AI chính xác**: Gemini AI phân tích và tổng hợp nội dung **không bỏ sót chi tiết**.
- **Gửi báo cáo tự động**: Kết quả được chia sẻ ngay lập tức đến **Slack, Discord hoặc WhatsApp**.
- **Hoạt động liên tục**: Workflow chạy **mỗi ngày tự động** mà không cần can thiệp.
- **Cá nhân hóa**: Thêm tên người tham dự vào báo cáo để tăng tính chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Calendar** (để lấy thông tin cuộc họp).
✔ **API Key của Google Calendar** (cấu hình trong n8n).
✔ **Credentials của Slack/Discord/WhatsApp**:
   - **Slack**: Token OAuth (cấp quyền `chat:write`).
   - **Discord**: Token Bot (cấp quyền `send_messages`).
   - **WhatsApp**: Số điện thoại + mã xác minh (nếu sử dụng API WhatsApp Business).
✔ **API Key của Google Gemini** (đăng ký tại [Google AI Studio](https://aistudio.google/)).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6934](https://n8n.io/workflows/6934) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **n8n Editor** → **Import Workflow**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Schedule Trigger (Động cơ lịch)**
- **Cấu hình**:
  - **Schedule**: Chọn **"Daily"** (hàng ngày) và thời gian phù hợp (ví dụ: **8h sáng**).
  - **Time Zone**: Đặt theo múi giờ của doanh nghiệp.

##### **🔹 Node 2: Google Calendar 1 (Lấy thông tin cuộc họp)**
- **Credentials**: Chọn tài khoản Google Calendar đã cấu hình.
- **Operation**: Chọn **"Get Events"** (lấy sự kiện).
- **Parameters**:
  - **Time Range**: Đặt từ **0h đến 24h** (hoặc tùy chỉnh theo giờ họp).
  - **Single Event**: Chọn **"No"** (lấy tất cả cuộc họp trong ngày).
  - **Filter**: Thêm điều kiện nếu cần (ví dụ: chỉ lấy cuộc họp có từ khóa "Meeting").

##### **🔹 Node 3: AI Agent (Gemini) - Tóm Tắt Nội Dung**
- **Credentials**: Chọn **Google Gemini API Key**.
- **Prompt Template** (cần chỉnh sửa để phù hợp):
  ```json
  {
    "role": "user",
    "content": "Tóm tắt cuộc họp {{event.title}} diễn ra vào {{event.start.dateTime}} với nội dung:
    - Thời gian: {{event.start.dateTime}}
    - Địa điểm: {{event.location}}
    - Người tham dự: {{event.attendees}}
    - Nội dung: {{event.description}}
    Hãy viết một bản tóm tắt ngắn gọn (5-7 câu) bao gồm:
    1. Mục tiêu cuộc họp
    2. Các quyết định chính
    3. Nhiệm vụ được giao
    4. Thời hạn hoàn thành
    5. Người chịu trách nhiệm
    Đảm bảo không bỏ sót chi tiết quan trọng."
  }
  ```
- **Lưu ý**:
  - Nếu cuộc họp có **file đính kèm (Google Drive)**, thêm vào prompt để AI phân tích.
  - **Limit API**: Nếu dùng miễn phí, hạn chế số cuộc họp quá nhiều/lần.

##### **🔹 Node 4-6: Gửi Báo Cáo (Slack/Discord/WhatsApp)**
- **Slack**:
  - **Credentials**: Chọn token OAuth đã cấp quyền.
  - **Channel**: Chọn `#general` hoặc channel riêng.
  - **Message Format**:
    ```json
    {
      "text": "📝 **Tóm tắt cuộc họp {{event.title}}**\n\n{{summary}}",
      "attachments": [
        {
          "title": "Thông tin cuộc họp",
          "fields": [
            { "title": "Thời gian", "value": "{{event.start.dateTime}}", "short": true },
            { "title": "Địa điểm", "value": "{{event.location}}", "short": true },
            { "title": "Người tham dự", "value": "{{event.attendees}}", "short": true }
          ]
        }
      ]
    }
    ```
- **Discord**:
  - **Credentials**: Token Bot đã cấp quyền `send_messages`.
  - **Channel**: Chọn `#meeting-summaries`.
  - **Message Format** tương tự Slack, nhưng có thể thêm **embed** cho hình ảnh.
- **WhatsApp**:
  - **Credentials**: Số điện thoại + mã xác minh.
  - **Message Format**:
    ```json
    {
      "text": "📝 **Tóm tắt cuộc họp {{event.title}}**\n\n{{summary}}\n\n📅 Thời gian: {{event.start.dateTime}}\n📍 Địa điểm: {{event.location}}"
    }
    ```
  - **Lưu ý**: WhatsApp có giới hạn **256 ký tự** cho tin nhắn, nên tóm tắt ngắn gọn.

##### **🔹 Node 7: StickyNote (Lưu Log - Tùy Chọn)**
- Nếu muốn **lưu lịch sử tóm tắt**, cấu hình node này để ghi vào **Google Sheets** hoặc **Notion**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **1 cuộc họp mẫu** để kiểm tra AI tóm tắt có chính xác không.
   - Kiểm tra **Slack/Discord/WhatsApp** có nhận được báo cáo không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Nhận Dạng (Pattern Matching)**:
   - Sử dụng **Expressions** trong node **Google Calendar** để chỉ lấy cuộc họp có từ khóa **"Meeting"** hoặc **"Project Update"**.
   - Ví dụ:
     ```json
     {{$json.event.title.includes("Meeting")}}
     ```

2. **Gửi Báo Cáo Định Kỳ (Weekly/Monthly)**:
   - Thay đổi **Schedule Trigger** thành **"Weekly"** hoặc **"Monthly"** để gửi báo cáo tổng hợp.
   - Sử dụng **Google Sheets** để lưu tất cả cuộc họp và tự động tạo báo cáo định kỳ.

3. **Kết Hợp với Notion/Google Docs**:
   - Thay vì gửi qua Slack/Discord, **ghi tự động vào Notion** hoặc **Google Docs** để dễ theo dõi.
   - Sử dụng node **n8n-nodes-base.notion** hoặc **n8n-nodes-base.googleDrive**.

4. **Thêm AI Chatbot Trả Lời**:
   - Sau khi tóm tắt, **AI Gemini** có thể trả lời các câu hỏi về cuộc họp (ví dụ: *"AI, nhiệm vụ của tôi là gì trong cuộc họp vừa rồi?"*).
   - Cấu hình **node `lmChatGoogleGemini`** với prompt:
     ```json
     {
       "role": "user",
       "content": "Trả lời câu hỏi của người dùng về cuộc họp {{event.title}}:\n\n- Nội dung cuộc họp: {{summary}}\n- Câu hỏi: {{userQuestion}}"
     }
     ```

5. **Lưu Trữ File Audio (Nếu Có)**:
   - Nếu cuộc họp có **file âm thanh (Zoom/Google Meet)**, sử dụng **node `n8n-nodes-base.googleDrive`** để tải xuống và **AI Gemini** có thể tóm tắt từ file đó.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công tẻ nhạt, đồng thời **tăng cường tính chuyên nghiệp** với báo cáo AI chính xác. **Chỉ cần 10 phút setup**, các sếp sẽ có **tóm tắt cuộc họp hàng ngày tự động** được gửi đến mọi kênh thông tin (Slack, Discord, WhatsApp).

👉 **Bắt đầu ngay** bằng cách import workflow và **cấu hình theo hướng dẫn trên**. Nếu cần hỗ trợ, hãy để lại comment bên dưới!

---
**#TựĐộngHóa #AIAutomation #N8N #GoogleCalendar #GeminiAI**