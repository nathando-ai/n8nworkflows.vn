---
title: "🚀 Tự Động Hóa Quá Trình Nhận Lại Cuộc Gọi Trễ và Đặt Lịch Hẹn HVAC Với GoHighLevel, Twilio & AI Gemini (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code để nhận lại cuộc gọi trễ từ Twilio, phân tích nhu cầu HVAC thông qua AI Gemini, và tự động đặt lịch hẹn trong GoHighLevel. Giúp doanh nghiệp tiết kiệm thời gian, tăng tỷ lệ chuyển đổi và cá nhân hóa tương tác với khách hàng."
slug: "tu-dong-hoa-nhan-lai-cuoc-goi-tranh-dat-lich-hvac"
tags: [n8n, automation, no-code, crm, twilio, gohighlevel, ai-chatbot, gemini-ai, lead-nurturing]
keywords: [n8n workflow tự động hóa, nhận lại cuộc gọi trễ, đặt lịch hẹn HVAC, AI Gemini trong n8n, tự động hóa CRM GoHighLevel, Twilio SMS tự động]
---

# 🚀 **Tự Động Hóa Nhận Lại Cuộc Gọi Trễ & Đặt Lịch Hẹn HVAC Với AI Gemini**

## **📞 Nỗi Đau Của Doanh Nghiệp**
Bạn đã bao giờ bỏ lỡ cuộc gọi từ khách hàng tiềm năng vì không có thời gian phản hồi kịp thời? Hoặc phải mất nhiều giờ để phân tích nhu cầu của khách hàng qua SMS và đặt lịch hẹn thủ công? Với **workflow này**, các sếp sẽ:
- **Tự động nhận lại tất cả cuộc gọi trễ** từ Twilio và chuyển đổi chúng thành lead trong GoHighLevel.
- **Sử dụng AI Gemini** để phân tích nhu cầu HVAC từ tin nhắn của khách hàng và trả lời tự động.
- **Đặt lịch hẹn tự động** khi khách hàng đồng ý, đồng thời cập nhật trạng thái trong CRM.
- **Tiết kiệm thời gian** lên đến **80%** so với cách làm thủ công!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100% quá trình nhận lại cuộc gọi trễ** – Không bỏ lỡ khách hàng nào.
✅ **Phân tích nhu cầu khách hàng bằng AI** – Gemini tự động hiểu và trả lời tin nhắn một cách thông minh.
✅ **Đặt lịch hẹn tự động** – Khi khách hàng đồng ý, lịch hẹn được tạo ngay trong GoHighLevel.
✅ **Cập nhật CRM liên tục** – Trạng thái lead và cơ hội được tự động sync, không cần can thiệp thủ công.
✅ **Tăng tỷ lệ chuyển đổi** – Tương tác cá nhân hóa và nhanh chóng làm tăng khả năng khách hàng đồng ý đặt lịch.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
- **Twilio**:
  - **Account SID** và **Auth Token** (tải từ [Twilio Console](https://www.twilio.com/console)).
  - **Phone Number** để gửi/nhận SMS (cần kích hoạt cho Twilio).
- **GoHighLevel (GHL)**:
  - **OAuth 2.0 API Key** (tạo từ [GoHighLevel API Settings](https://app.gohighlevel.com/settings/api)).
  - **Pipeline ID** và **Status ID** trong GHL (cần xác định trước khi cấu hình).
- **Google Gemini API**:
  - **API Key** từ [Google Cloud Console](https://console.cloud.google.com/).
  - **Project ID** và **Location** của API (ví dụ: `us-central1`).

### **2. Cấu Hình N8N**
- **Self-hosted n8n** (khuyến nghị) để workflow hoạt động 24/7.
- **Node bổ sung**:
  - `@n8n/nodes-langchain` (để sử dụng Gemini AI).
  - **Twilio & GoHighLevel** đã được cài sẵn trong n8n.

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/15103) (hoặc copy JSON từ link trên).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** và dán toàn bộ mã JSON từ workflow.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "When Webhook Received" (Nhận Cuộc Gọi Trễ)**
- **Path**: Đặt là `twillio-missed-call` (không đổi).
- **HTTP Method**: POST (không đổi).
- **Lưu ý**:
  - Cấu hình **Twilio** để gửi POST request đến URL webhook này khi có cuộc gọi trễ.
  - Ví dụ: Trong Twilio Console → **Phone Numbers** → **Messaging** → **Webhooks** → Thêm URL webhook.

#### **🔹 Node "Create Lead in HighLevel" & "Create Opportunity in HighLevel"**
- **Credentials**: Chọn `highLevelOAuth2Api` (đã cấu hình trước).
- **Mapping Fields**:
  - **Lead**:
    - `firstName`, `lastName`, `phoneNumber`, `email` (nếu có).
    - **Pipeline**: Chọn pipeline phù hợp (ví dụ: "HVAC Leads").
    - **Status**: Chọn "New Lead" (hoặc tùy chỉnh).
  - **Opportunity**:
    - `pipelineId`: Điền ID pipeline từ GoHighLevel.
    - `statusId`: Điền ID trạng thái (ví dụ: "Contacted").
    - **Custom Fields**: Nếu cần, thêm trường như `source` (Twilio).

#### **🔹 Node "Send SMS via Twilio"**
- **Credentials**: Chọn `twilioApi`.
- **Message Content**:
  - Thay đổi template SMS theo nhu cầu (ví dụ:
    ```json
    "body": "Xin chào {{firstName}}, chúng tôi đã nhận được cuộc gọi của bạn về dịch vụ HVAC. Để đặt lịch hẹn, hãy gửi tin nhắn 'ĐẶT LỊCH'!"
    ```
  - Sử dụng **Dynamic Content** để trích xuất `firstName` từ lead.

#### **🔹 Node "Gemini Chat Model" (AI Phân Tích Tin Nhắn)**
- **Credentials**: Chọn `googlePalmApi`.
- **Prompt Template**:
  - Cấu hình prompt để Gemini phân tích nhu cầu HVAC từ tin nhắn khách hàng.
  - Ví dụ:
    ```json
    "prompt": "Analyze the following SMS from a customer about HVAC services:\n\n{{smsContent}}\n\nBased on this, what is the customer's likely need? Is it a repair, installation, or maintenance? Also, suggest a suitable appointment time based on their message."
    ```
- **Output Parser**: Chọn `outputParserStructured` để Gemini trả về kết quả có cấu trúc (ví dụ: JSON).

#### **🔹 Node "Twilio Trigger" (Nhận Tin Nhắn Trả Lời)**
- **Credentials**: Chọn `twilioApi`.
- **Webhook URL**: Đặt là `twillio-sms-reply` (không đổi).
- **Lưu ý**:
  - Cấu hình Twilio để gửi tin nhắn trả lời đến URL này.
  - Trong Twilio Console → **Phone Numbers** → **Messaging** → **Webhooks** → Thêm URL mới.

#### **🔹 Node "Update Opportunity Status"**
- **Operation**: Chọn `update`.
- **Resource**: `opportunity`.
- **Status ID**: Cập nhật thành trạng thái mới (ví dụ: "Scheduled" khi khách hàng đồng ý).

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một cuộc gọi trễ giả từ Twilio → Kiểm tra workflow tạo lead và gửi SMS.
   - Gửi tin nhắn từ Twilio → Kiểm tra AI Gemini phân tích và trả lời tự động.
2. **Bật Active**:
   - Nhấn **Active** trên workflow để chạy liên tục.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Slack/Telegram để Báo Cáo**
- Thêm node **Slack/Telegram Webhook** sau node **"Send SMS via Twilio"** để báo cáo khi có cuộc gọi trễ mới.
- Ví dụ:
  ```json
  "message": "🚨 New missed call from {{phoneNumber}}! Lead created: {{firstName}} {{lastName}}"
  ```

### **2. Lưu Log Tất Cả Các Cuộc Gọi**
- Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả cuộc gọi trễ và lịch sử tương tác.
- Cấu hình:
  - **Sheet Name**: `HVAC_Call_Log`.
  - **Columns**: `PhoneNumber`, `FirstName`, `LastName`, `CallDate`, `Status`, `SMSContent`.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Schedule Node** để gửi báo cáo hàng tuần về:
  - Số lượng cuộc gọi trễ được nhận lại.
  - Tỷ lệ chuyển đổi thành lead.
  - Số lượng lịch hẹn đã đặt.

### **4. Cập Nhật CRM Theo Dõi AI**
- Sau khi Gemini phân tích tin nhắn, cập nhật trường `notes` trong GoHighLevel để theo dõi nhu cầu khách hàng:
  ```json
  "notes": "Customer needs HVAC repair. Suggested time: {{suggestedTime}}"
  ```

---
## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa toàn bộ quá trình từ nhận lại cuộc gọi trễ đến đặt lịch hẹn HVAC, với sự hỗ trợ của **AI Gemini** để phân tích và tương tác thông minh. Các sếp chỉ cần **cấu hình 1 lần** và workflow sẽ hoạt động **liên tục 24/7**, tiết kiệm thời gian và tăng tỷ lệ chuyển đổi.

### **🚀 Bắt Đầu Ngay Hôm Nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (khuyến nghị).
2. **Import workflow** và cấu hình các API keys.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Cần hỗ trợ thêm?** Liên hệ tác giả Abhi Vaar qua [Calendly](https://cal.com/abhi.vaar/n8n) để tư vấn chi tiết!