---
title: "🚀 Tự Động Hóa Nhận Lead HVAC + Lập Lịch Hẹn với AI OpenAI, Google Sheets, Slack & SMS – Không Cần Code"
description: "Giải pháp tự động hóa 100% tự động nhận lead HVAC từ form, phân loại ưu tiên, lập lịch hẹn và thông báo tự động qua Slack, email, SMS và Google Calendar – tiết kiệm 80% thời gian cho đội ngũ bán hàng."
slug: "tu-dong-hoa-lead-hvac-ai-openai-google-sheets-slack-sms"
tags: [n8n, automation, lead-generation, ai-summarization, hvac-business]
keywords: [tự động hóa lead HVAC, n8n workflow, AI phân loại lead, lập lịch hẹn tự động, Slack + SMS + Email, Google Sheets + Google Calendar]
---

# 🚀 **Tự Động Hóa Nhận Lead HVAC + Lập Lịch Hẹn với AI – Không Cần Code**

### **🔥 Nỗi Đau Của Các Sếp HVAC**
Hàng ngày, đội ngũ bán hàng của các sếp phải:
- **Nhập liệu thủ công** lead từ form website vào Google Sheets, CRM hoặc hệ thống quản lý.
- **Phân loại lead** theo ưu tiên (cấp thiết, thường, thấp) và loại dịch vụ (lắp đặt, sửa chữa, bảo trì).
- **Gọi điện/SMS** để xác nhận và lập lịch hẹn, dễ bị quên hoặc trùng lịch.
- **Gửi thông báo nội bộ** qua Slack/email cho các đội ngũ kỹ thuật, dẫn đến trễ thời gian phản hồi.
- **Tốn thời gian** lên đến **8-10 giờ/tuần** cho mỗi nhân viên, trong khi lead có thể "lạnh" chỉ sau vài giờ.

**Kết quả?** Lead trôi đi, doanh thu giảm, và đội ngũ mệt mỏi.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động nhận lead** từ form website 24/7, không cần nhân viên.
- **AI phân loại lead** theo ưu tiên và loại dịch vụ (lắp đặt, sửa chữa, bảo trì) với độ chính xác **90%+**.
- **Lập lịch hẹn tự động** trên Google Calendar và gửi SMS/email nhắc nhở cho khách hàng.
- **Thông báo nội bộ** qua Slack cho đội ngũ kỹ thuật (lắp đặt, sửa chữa, bảo trì) với thông tin chi tiết.
- **Lưu trữ lead** trên Google Sheets với cấu trúc sẵn sàng cho CRM.
- **Tiết kiệm 80% thời gian** cho đội ngũ bán hàng, tập trung vào bán hàng chứ không phải nhập liệu.
- **Khách hàng được phục vụ nhanh chóng** với lịch hẹn tự động và thông báo nhắc nhở.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu lead và lịch hẹn):
   - Một bảng Google Sheets với cấu trúc sẵn sàng (các cột: `Name`, `Phone`, `Email`, `Service Type`, `Urgency`, `Notes`, `Appointment Time`).
   - **Credentials**: `googleSheetsOAuth2Api` (cài đặt trong n8n).
2. **Tài khoản Slack** (để thông báo nội bộ):
   - Webhook URL từ Slack (cài đặt trong `Slack App`).
3. **Tài khoản OpenAI API** (để phân loại lead):
   - **API Key** từ [OpenAI](https://platform.openai.com/account/api-keys).
   - Model: `gpt-4.1-mini` (được cấu hình sẵn trong workflow).
4. **Tài khoản Twilio** (để gửi SMS nhắc nhở):
   - **API Key** và **Auth Token** từ [Twilio](https://www.twilio.com/).
   - Số điện thoại Twilio (để gửi SMS).
5. **Tài khoản Google Calendar** (để lập lịch hẹn):
   - **Credentials OAuth2** (cài đặt trong n8n).
6. **Tài khoản Email** (để gửi xác nhận):
   - Thông tin SMTP (hoặc sử dụng Gmail với OAuth2).
7. **Form nhận lead** (để trigger workflow):
   - Form trên website (có thể là Google Form, Typeform, hoặc form tùy chỉnh).
   - **Webhook URL** từ n8n (được tạo tự động khi import workflow).
8. **(Tùy chọn) CRM/Dispatch System**:
   - API URL của hệ thống CRM (ví dụ: HubSpot, Zoho, hoặc hệ thống nội bộ).
---

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/12742](https://n8n.io/workflows/12742) (hoặc copy JSON từ link này).
- **Bước 2**: Mở **n8n Editor** (trên n8n Self-hosted hoặc n8n Cloud).
- **Bước 3**: Nhấn **Import Workflow** và dán JSON vào.
- **Bước 4**: Chọn **Create Workflow** và đặt tên (ví dụ: `HVAC Lead Automation`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này được chia thành **5 phần chính** (được phân loại trên canvas). Các sếp cần chú ý cấu hình các node sau:

##### **📌 Phần 1: Trigger & Config (Form + Cấu Hình)**
- **Node: Lead Submission Form (formTrigger)**
  - **Cấu hình**:
    - Thiết lập **Webhook URL** từ n8n (sau khi import) trong form nhận lead.
    - Kiểm tra **Payload** từ form (các trường: `name`, `phone`, `email`, `serviceType`, `urgency`, `notes`).
  - **Lưu ý**: Nếu sử dụng Google Form, các sếp cần chuyển đổi thành webhook bằng cách sử dụng **Make (Integromat)** hoặc **Zapier**.

- **Node: Workflow Configuration (set)**
  - **Cấu hình**:
    - Điền các **tham số mặc định** (nếu có) như tên đội ngũ Slack, email mặc định, hoặc thông tin lịch hẹn.

##### **📌 Phần 2: AI Logic (Phân Loại Lead)**
- **Node: Classify Lead Urgency and Service Type (agent)**
  - **Cấu hình**:
    - **Prompt AI**: Được cấu hình sẵn trong workflow để phân loại lead theo:
      - **Loại dịch vụ**: Lắp đặt (`Installation`), Sửa chữa (`Repair`), Bảo trì (`Maintenance`).
      - **Ưu tiên**: Cấp thiết (`Urgent`), Thường (`Standard`), Thấp (`Low`).
    - **Model**: `gpt-4.1-mini` (được chọn trong `OpenAI Chat Model`).
  - **Lưu ý**:
    - Nếu API Key OpenAI hết hạn, các sếp cần **cập nhật lại** trong `Credentials` của n8n.
    - Test với **dữ liệu mẫu** để đảm bảo AI phân loại chính xác.

- **Node: OpenAI Chat Model (lmChatOpenAi)**
  - **Cấu hình**:
    - Chọn **model**: `gpt-4.1-mini` (hoặc `gpt-4` nếu muốn độ chính xác cao hơn).
    - Đảm bảo **credentials `openAiApi`** được cài đặt đúng.

- **Node: Structured Output Parser (outputParserStructured)**
  - **Cấu hình**:
    - Kiểm tra **schema output** để đảm bảo AI trả về dữ liệu theo định dạng:
      ```json
      {
        "serviceType": "Installation|Repair|Maintenance",
        "urgency": "Urgent|Standard|Low",
        "notes": "string"
      }
      ```

##### **📌 Phần 3: Notify (Thông Báo Nội Bộ)**
- **Node: Route by Service Type (switch)**
  - **Cấu hình**:
    - Chọn **criterion**: `serviceType` (để phân loại lead cho đội ngũ phù hợp).
    - Kết nối với các node:
      - `Notify Installation Team` (Slack).
      - `Notify Repair Team` (Slack).
      - `Notify Maintenance Team` (Slack).

- **Node: Notify [Team] (slack)**
  - **Cấu hình**:
    - Chọn **Slack Webhook URL** (đã cài đặt trước).
    - **Message Template**:
      ```json
      {
        "text": "🚨 New {{serviceType}} Lead: {{name}} (Phone: {{phone}})",
        "blocks": [
          {
            "type": "section",
            "text": {
              "type": "mrkdwn",
              "text": "*New Lead:*\n*Name:* {{name}}\n*Phone:* {{phone}}\n*Service:* {{serviceType}}\n*Urgency:* {{urgency}}"
            }
          }
        ]
      }
      ```

##### **📌 Phần 4: Appointment & Reminder (Lập Lịch + SMS)**
- **Node: Schedule Appointment (googleCalendar)**
  - **Cấu hình**:
    - Chọn **Google Calendar** (cần OAuth2).
    - **Event Details**:
      - Tiêu đề: `HVAC Appointment with {{name}}`
      - Thời gian: `{{appointmentTime}}` (được AI tính toán).
      - Thông tin chi tiết: `Service: {{serviceType}}, Urgency: {{urgency}}`.

- **Node: Send SMS Reminder (twilio)**
  - **Cấu hình**:
    - Điền **Twilio Account SID** và **Auth Token**.
    - **Message Template**:
      ```json
      "Hello {{name}}, your HVAC appointment is scheduled for {{appointmentTime}}. Please confirm."
      ```
    - **Lưu ý**: Các sếp cần **cài đặt số Twilio** và **kiểm tra số điện thoại** của khách hàng.

- **Node: Send Confirmation Email (emailSend)**
  - **Cấu hình**:
    - Chọn **SMTP Provider** (Gmail, SendGrid, hoặc Mailgun).
    - **Email Template**:
      ```html
      <p>Hello {{name}},</p>
      <p>Thank you for your interest in our HVAC services!</p>
      <p>Your appointment is scheduled for <strong>{{appointmentTime}}</strong>.</p>
      <p>Service: <strong>{{serviceType}}</strong></p>
      <p>Urgency: <strong>{{urgency}}</strong></p>
      <p>Best regards,<br>Your HVAC Team</p>
      ```

##### **📌 Phần 5: Main (Lưu Lead + CRM)**
- **Node: Store Lead in Google Sheets (googleSheets)**
  - **Cấu hình**:
    - Chọn **Google Sheets** và **Sheet Name** (ví dụ: `HVAC_Leads`).
    - **Operation**: `appendOrUpdate` (để cập nhật lead mới).
    - **Headers**: Đảm bảo các cột trong Sheets trùng khớp với dữ liệu từ form.

- **Node: Send to CRM/Dispatch System (httpRequest)**
  - **Cấu hình**:
    - **URL**: API của CRM (ví dụ: `https://api.hubspot.com/v3/objects/contacts`).
    - **Headers**: `Content-Type: application/json`.
    - **Body**:
      ```json
      {
        "properties": {
          "name": "{{name}}",
          "phone": "{{phone}}",
          "email": "{{email}}",
          "service_type": "{{serviceType}}",
          "urgency": "{{urgency}}",
          "appointment_time": "{{appointmentTime}}"
        }
      }
      ```
    - **Lưu ý**: Các sếp cần **kiểm tra API docs** của CRM để điều chỉnh.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu:
  - Gửi một lead mẫu qua form (hoặc gọi API webhook).
  - Kiểm tra các node:
    - AI có phân loại lead chính xác không?
    - Slack có nhận được thông báo không?
    - Email/SMS có được gửi không?
    - Google Calendar có lập lịch không?
- **Bước 2**: **Bật Active Workflow**:
  - Sau khi test thành công, chuyển workflow từ **Draft** sang **Active**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Kết nối với CRM**:
   - Nếu chưa có CRM, các sếp có thể sử dụng **Google Sheets** như CRM tạm thời, sau đó chuyển sang **HubSpot** hoặc **Zoho** khi cần.
2. **Lưu Log**:
   - Thêm **Sticky Note** (`stickyNote`) để ghi lại lỗi hoặc thông tin debug.
3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo số lead/ngày qua email.
4. **Tích Hợp với WhatsApp**:
   - Thay vì SMS, các sếp có thể gửi thông báo qua **WhatsApp Business API** (nếu khách hàng ưa thích).
5. **Tự động Chuyển Lead "Lạnh"**:
   - Sử dụng **n8n + Twilio** để gọi điện tự động sau 24h nếu lead không xác nhận.
6. **Duy Trì Dữ Liệu**:
   - Xóa lead cũ hơn 30 ngày trong Google Sheets bằng **n8n + Google Sheets API**.
:::

---

### **📌 Kết Luận**
Workflow này **giải phóng đội ngũ bán hàng** khỏi công việc nhập liệu và quản lý lead thủ công, đồng thời **tăng hiệu suất bán hàng** với AI phân loại và lập lịch tự động. Các sếp chỉ cần **cấu hình 1 lần** và workflow sẽ hoạt động **24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động ổn định):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test và bật Active** để bắt đầu tự động hóa ngay!

**🚀 Hãy để AI và n8