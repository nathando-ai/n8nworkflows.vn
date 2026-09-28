---
title: "🤖 **Tự Động Hóa Bot Gọi Điện Multilingual với GPT-4o, ElevenLabs & Twilio – Không Cần Code!**"
description: "Xây dựng bot gọi điện thông minh đa ngôn ngữ tự động trả lời, chuyển đổi văn bản thành giọng nói và lưu lịch hẹn vào Google Sheets. Giúp doanh nghiệp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tự động hóa dịch vụ hỗ trợ 24/7."
slug: "tự-dộng-hoa-bot-goi-dien-multilingual-gpt-4o-elevenlabs-twilio"
tags: [n8n, automation, ai-chatbot, twilio, elevenlabs, google-sheets, no-code]
keywords: [n8n workflow gọi điện tự động, bot gọi điện multilingual, tự động hóa dịch vụ khách hàng, GPT-4o ElevenLabs Twilio, lưu lịch hẹn tự động]
---

# 🚀 **Bot Gọi Điện Multilingual Tự Động Hóa với GPT-4o, ElevenLabs & Twilio**

### **Giải pháp cho doanh nghiệp muốn tự động hóa dịch vụ hỗ trợ khách hàng qua điện thoại mà không cần nhân viên 24/7!**
Hiện nay, nhiều doanh nghiệp gặp khó khăn khi phải trả tiền cho nhân viên hỗ trợ khách hàng qua điện thoại, đặc biệt là trong giờ cao điểm. Thay vì phải gọi điện thủ công, **bot gọi điện thông minh** này sẽ:
- **Trả lời tự động** với giọng nói ấn tượng (dựa trên GPT-4o + ElevenLabs).
- **Hiểu và phản hồi** theo nhiều ngôn ngữ (Tiếng Việt, Anh, Nhật, Hàn, Trung...).
- **Lưu lịch hẹn** vào Google Sheets để quản lý dễ dàng.
- **Hoạt động liên tục** mà không cần ngủ nghỉ!

Nếu các sếp đang tìm cách **tiết kiệm chi phí nhân sự, cải thiện trải nghiệm khách hàng và tự động hóa dịch vụ hỗ trợ**, thì **workflow này chính là giải pháp hoàn hảo!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm chi phí nhân sự** – Không cần thuê thêm nhân viên hỗ trợ điện thoại.
✅ **Hỗ trợ khách hàng 24/7** – Bot hoạt động liên tục, không cần nghỉ ngơi.
✅ **Trải nghiệm khách hàng tốt hơn** – Giọng nói tự nhiên, phản hồi nhanh chóng và chính xác.
✅ **Quản lý lịch hẹn tự động** – Tất cả cuộc gọi và lịch hẹn được lưu vào Google Sheets.
✅ **Hỗ trợ nhiều ngôn ngữ** – Khách hàng có thể gọi bằng tiếng Việt, Anh, Nhật, Hàn, Trung...
✅ **Dễ dàng mở rộng** – Có thể kết nối với Slack, Telegram hoặc hệ thống CRM khác.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Twilio** (để tạo số điện thoại và webhook gọi điện).
2. **API Key OpenAI** (để sử dụng GPT-4o).
3. **API Key ElevenLabs** (để chuyển đổi văn bản thành giọng nói).
4. **Tài khoản Google Sheets** (để lưu log cuộc gọi và lịch hẹn).
5. **VPS n8n** (để chạy workflow 24/7).

---
:::info[CHUẨN BỊ]
- **Twilio**:
  - Tạo một **Twilio Phone Number** (để bot gọi điện).
  - Cấu hình **Voice URL** trong Twilio Dashboard để trỏ đến `https://<your-n8n-domain>/voice-webhook`.
- **OpenAI**:
  - Tạo **API Key** tại [OpenAI Platform](https://platform.openai.com/).
- **ElevenLabs**:
  - Tạo **API Key** tại [ElevenLabs](https://elevenlabs.io/).
- **Google Sheets**:
  - Tạo một **Google Sheet** mới để lưu log cuộc gọi và lịch hẹn.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import Workflow** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/6309)).
3. Chọn **Create New Workflow** và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **🔹 Twilio Voice Webhook**
- **Path**: `voice-webhook` (không thay đổi).
- **HTTP Method**: `POST`.
- **Credentials**: Đảm bảo đã kết nối tài khoản Twilio trong **n8n Credentials**.

##### **🔹 OpenAI GPT-4o Response**
- **Model**: `gpt-4o` (không thay đổi).
- **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
- **Prompt**:
  ```json
  "You are a multilingual customer support bot. Respond in the same language as the user. If the user asks for an appointment, reply with 'Thank you for your request. I will schedule it for you. What is your preferred date and time?'"
  ```
- **Temperature**: 0.7 (để bot phản hồi tự nhiên).

##### **🔹 ElevenLabs Text-to-Speech**
- **Credentials**: Chọn `elevenLabsApi` (đã cấu hình trước).
- **Voice Settings**:
  - **Voice ID**: Chọn một giọng nói phù hợp (ví dụ: `21m00Tcm4TlvDq8ikWAM` – giọng nam Mỹ).
  - **Stability**: 0.5 (để giọng nói không quá cơ giới).
  - **Similarity Boost**: 0.75 (để giọng nói gần giống với người thật).

##### **🔹 Upload Audio to Storage (HTTP Request)**
- **URL**: Điền địa chỉ URL của **Twilio Media Server** (nếu cần lưu audio).
- **Headers**:
  ```json
  {
    "Content-Type": "audio/mpeg"
  }
  ```
- **Body**: `$node["ElevenLabs Text-to-Speech"].json["audio"]` (audio được tạo từ ElevenLabs).

##### **🔹 Twilio TwiML Response**
- **Twilio Response**:
  ```xml
  <Response>
    <Say voice="alice">$json["response"]</Say>
    <Play>$json["audioUrl"]</Play>
  </Response>
  ```
- **Lưu ý**: Đảm bảo `$json["response"]` và `$json["audioUrl"]` được truyền từ node trước.

##### **🔹 Log Conversation (Google Sheets)**
- **Sheet Name**: Điền tên sheet (ví dụ: `Bot_Goi_Dien_Log`).
- **Range**: `A1` (để bắt đầu ghi từ ô A1).
- **Data**:
  ```json
  {
    "Timestamp": "$node["Twilio Voice Webhook"].json["timestamp"]",
    "Caller": "$node["Twilio Voice Webhook"].json["caller"]",
    "Message": "$node["OpenAI GPT-4o Response"].json["response"]",
    "Appointment": "$node["Check for Appointment"].json["appointment"]"
  }
  ```

##### **🔹 Check for Appointment & Save Appointment Request**
- **Condition**:
  ```json
  "$node["OpenAI GPT-4o Response"].json["response"].includes('appointment')"
  ```
- **Google Sheets Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Data**:
  ```json
  {
    "Timestamp": "$node["Twilio Voice Webhook"].json["timestamp"]",
    "Caller": "$node["Twilio Voice Webhook"].json["caller"]",
    "Appointment": "$node["Twilio Voice Webhook"].json["appointment"]"
  }
  ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gọi từ số điện thoại Twilio để kiểm tra bot phản hồi như thế nào.
   - Kiểm tra Google Sheets để đảm bảo log được lưu chính xác.
2. **Bật Active Workflow**:
   - Nhấn **Active** để workflow bắt đầu hoạt động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết nối với Slack/Telegram**:
   - Sau khi bot xử lý xong cuộc gọi, có thể gửi thông báo về Slack/Telegram để quản lý dễ dàng.
   - Sử dụng **n8n-nodes-slack** hoặc **n8n-nodes-telegram**.

2. **Lưu audio cuộc gọi**:
   - Thay vì chỉ lưu log văn bản, có thể lưu **audio cuộc gọi** vào **Google Drive** hoặc **AWS S3**.
   - Sử dụng **n8n-nodes-google-drive** hoặc **n8n-nodes-aws-s3**.

3. **Báo cáo tự động hàng ngày**:
   - Sử dụng **n8n-nodes-email** hoặc **n8n-nodes-slack** để gửi báo cáo tổng hợp về số cuộc gọi, lịch hẹn và phản hồi của khách hàng.

4. **Hỗ trợ nhiều ngôn ngữ hơn**:
   - Cập nhật **prompt** của GPT-4o để hỗ trợ thêm ngôn ngữ (ví dụ: tiếng Đức, tiếng Pháp).

5. **Tích hợp với CRM**:
   - Nếu doanh nghiệp sử dụng **HubSpot, Salesforce** hoặc **Zoho CRM**, có thể kết nối để cập nhật thông tin khách hàng tự động.

---

### 📌 **Kết luận**
**Bot gọi điện multilingual tự động hóa này là giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm chi phí nhân sự** và **tăng hiệu suất dịch vụ hỗ trợ**.
✔ **Cải thiện trải nghiệm khách hàng** với giọng nói tự nhiên và phản hồi nhanh chóng.
✔ **Quản lý lịch hẹn một cách tự động** và dễ dàng.

**Hãy áp dụng ngay workflow này và tự động hóa dịch vụ hỗ trợ của doanh nghiệp trong vài phút!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/6309)**
**📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/)** (nếu chưa có)