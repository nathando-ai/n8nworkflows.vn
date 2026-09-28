---
title: "🚀 Tự Động Hóa Chuyển Đổi Lead Facebook Sang Cuộc Gọi AI & Đặt Lịch Hẹn - Không Cần Code"
description: "Workflow này tự động nhận lead từ Facebook Ads, gọi AI bằng ElevenLabs để phỏng vấn và đặt lịch hẹn trên Cal, sau đó thông báo kết quả qua Slack và Email. Giúp doanh nghiệp tiết kiệm 80% thời gian chăm sóc khách hàng và tăng tỷ lệ chuyển đổi lead thành khách hàng."
slug: "tieu-dong-hoa-chuyen-doi-lead-facebook-sang-ai-call"
tags: [n8n, automation, lead-nurturing, ai-chatbot, facebook-ads, elevenlabs, supabase, slack, gmail]
keywords: [n8n workflow lead facebook, tự động hóa cuộc gọi ai, đặt lịch hẹn tự động, ElevenLabs n8n, Supabase tự động hóa, Slack và Email thông báo]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Lead Facebook Sang Cuộc Gọi AI & Đặt Lịch Hẹn**

## **💡 Nỗi Đau Của Các Sếp: "Tôi Mất Giờ Để Chăm Sóc Mỗi Lead"**
Hàng ngày, các sếp phải:
- **Làm thủ công** theo dõi hàng trăm lead từ Facebook Ads.
- **Gọi điện** để phỏng vấn và xác nhận thông tin, mất từ 15-30 phút/lead.
- **Đặt lịch hẹn** trên Cal hoặc Google Calendar, dễ bị quên hoặc trùng lịch.
- **Thông báo kết quả** cho team qua Slack/Email, dễ bị lỡ hoặc sai thông tin.

**Kết quả?** Tỷ lệ chuyển đổi lead thấp, chi phí nhân sự cao, và khách hàng cảm thấy không được quan tâm.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** chăm sóc lead (AI gọi và phỏng vấn thay vì bạn).
✅ **Tăng tỷ lệ chuyển đổi** lên **50-70%** (do cuộc gọi AI chuyên nghiệp, không bỏ lỡ lead).
✅ **Lịch hẹn tự động** trên Cal, không bị trùng hoặc quên.
✅ **Thông báo tự động** qua Slack và Email với **báo cáo chi tiết** (transcript, kết quả phỏng vấn).
✅ **Dữ liệu lead được lưu trữ** trên Supabase, dễ dàng phân tích và báo cáo.

---
## **🎯 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **📌 Tài Khoản & API Keys**
| **Dịch Vụ**          | **Mô Tả**                                                                 | **Liên Kết Đăng Ký**                          |
|----------------------|--------------------------------------------------------------------------|-----------------------------------------------|
| **Facebook Ads**     | Tài khoản Facebook Ads + Business Page + Form Lead (đã cấu hình nhận lead) | [Facebook Business](https://www.facebook.com/business/) |
| **ElevenLabs**       | Tài khoản ElevenLabs (để gọi AI) + API Key                                | [ElevenLabs](https://elevenlabs.io/)         |
| **Cal**              | Tài khoản Cal (để đặt lịch hẹn) + API Key                                | [Cal](https://cal.com/)                      |
| **Supabase**         | Database lưu trữ lead + API Key                                          | [Supabase](https://supabase.com/)             |
| **Slack**            | Workspace Slack + Webhook URL                                            | [Slack API](https://api.slack.com/)           |
| **Gmail**            | Tài khoản Gmail (để gửi Email thông báo)                                | [Gmail](https://mail.google.com/)             |

### **📌 Cấu Hình Trước Khi Import**
1. **Facebook Lead Form**:
   - Đảm bảo form lead đã được cấu hình **gửi dữ liệu về n8n** (cần cài đặt Webhook trong Facebook Ads).
   - Thêm trường cần thiết: `phone`, `email`, `name`, `company`, `budget`, `pain_points`.

2. **ElevenLabs**:
   - Tạo **voice model** (giọng đọc) và lấy **API Key**.
   - Cấu hình **webhook** để nhận kết quả cuộc gọi (sẽ được sử dụng sau).

3. **Supabase**:
   - Tạo **table "leads"** với các cột: `id`, `facebook_id`, `phone`, `email`, `name`, `company`, `budget`, `pain_points`, `call_id`, `appointment_link`, `status` (e.g., "pending", "booked", "rejected").

4. **Slack & Gmail**:
   - Tạo **app Slack** để lấy Webhook URL (cho node Slack).
   - Cấu hình **Gmail API** để gửi Email (cần **OAuth 2.0**).

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/15677](https://n8n.io/workflows/15677) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. **Không cần chỉnh sửa** nếu đã có tất cả credentials.

#### **Phương Pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/15677](https://n8n.io/workflows/15677).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.

---
### **2. Các Bước Cấu Hình BẮT BUỘC 📌**
Workflow gồm **2 phần chính**:
- **Phần A: Nhận Lead & Gọi AI** (triggers khi lead mới đến).
- **Phần B: Xử Lý Kết Quả Cuộc Gọi** (lắng nghe webhook từ ElevenLabs).

#### **🔹 Phần A: Nhận Lead & Gọi AI**
| **Node**               | **Cấu Hình Cần Chỉnh**                                                                 | **Lưu Ý**                                                                 |
|------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Facebook Lead Ads**  | - Chọn **credentials** là tài khoản Facebook Ads của bạn.                          | Đảm bảo **Webhook URL** trong Facebook Ads trỏ đến `https://<your-n8n-url>/facebook-lead-ads-trigger`. |
| **Format Lead Data**   | - Chỉnh **mapping** để đảm bảo dữ liệu từ Facebook phù hợp với Supabase.            | Ví dụ: `{{$json["phone"]}}` → `phone`.                                    |
| **Insert Lead**        | - Chọn **credentials**: `supabaseApi`.                                               | Chọn **table**: `leads`.                                                  |
| **Trigger ElevenLabs Call** | - **URL**: `https://api.elevenlabs.io/v1/text-to-speech/<YOUR_VOICE_ID>` (lấy từ ElevenLabs).<br>- **Headers**:<br>  - `xi-api-key`: API Key ElevenLabs.<br>- **Body**:<br>  ```json<br>{<br>    "text": "Hello, this is an automated call from [Your Company]. We received your lead from Facebook. Could you confirm your availability for a meeting this week? Reply with 'yes' to book a call.",<br>    "model_id": "eleven_multilingual_v1"<br>}<br>``` | Thay `YOUR_VOICE_ID` và cấu hình **prompt** phù hợp với doanh nghiệp. |
| **Save Call ID**       | - Chọn **credentials**: `supabaseApi`.<br>- **Update record**: `id` (trường `id` trong Supabase).<br>- **Set**: `call_id` = `{{$json.call_id}}`. | Đảm bảo `call_id` được lưu vào lead tương ứng. |

#### **🔹 Phần B: Xử Lý Kết Quả Cuộc Gọi (Webhook ElevenLabs)**
| **Node**               | **Cấu Hình Cần Chỉnh**                                                                 | **Lưu Ý**                                                                 |
|------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **ElevenLabs Webhook** | - **Path**: `elevenlabs-call-complete`.<br>- **HTTP Method**: `POST`.<br>- **Credentials**: Không cần. | Đảm bảo **webhook URL** trong ElevenLabs trỏ đến `https://<your-n8n-url>/elevenlabs-call-complete`. |
| **Extract Call Data**  | - **Mapping**: Lấy dữ liệu từ ElevenLabs (ví dụ: `status`, `transcript`, `duration`). | Ví dụ: `{{$json.status}}` → `call_status`.                                |
| **Update Lead Row**    | - **Credentials**: `supabaseApi`.<br>- **Update record**: `id` (trường `id` trong Supabase).<br>- **Set**:<br>  - `call_status`: `{{$json.status}}`.<br>  - `transcript`: `{{$json.transcript}}`.<br>  - `appointment_link`: (nếu có). | Cập nhật lead với kết quả cuộc gọi. |
| **Appointment Booked?** | - **Condition**: Kiểm tra `call_status` có bằng `"booked"` không.                  | Nếu `true` → đi đến **Slack: Booked** & **Email: Booked**.<br>Nếu `false` → đi đến **Slack: Not Booked** & **Email: Not Booked**. |
| **Slack: Booked**      | - **Credentials**: Slack Webhook URL.<br>- **Message**:<br>  ```markdown<br>📅 **Lead đã đặt lịch!**<br><br>👤 **Tên**: {{$json.name}}<br>📞 **Số điện thoại**: {{$json.phone}}<br>💼 **Công ty**: {{$json.company}}<br>🔗 **Lịch hẹn**: {{$json.appointment_link}}<br>💬 **Ghi chú**: {{$json.transcript}}``` | Thay đổi template Slack theo yêu cầu. |
| **Email: Booked**      | - **Credentials**: Gmail OAuth.<br>- **To**: Email của team.<br>- **Subject**: `📅 Lead {{$json.name}} đã đặt lịch!`.<br>- **Body**:<br>  ```html<br><h1>Lead đã đặt lịch thành công!</h1><br><p><strong>Tên:</strong> {{$json.name}}</p><br><p><strong>Số điện thoại:</strong> {{$json.phone}}</p><br><p><strong>Lịch hẹn:</strong> <a href="{{$json.appointment_link}}">Xem lịch</a></p><br><p><strong>Ghi chú cuộc gọi:</strong></p><p>{{$json.transcript}}</p>``` | Thay đổi nội dung Email theo brand. |
| **Slack: Not Booked**  | - **Credentials**: Slack Webhook URL.<br>- **Message**:<br>  ```markdown<br>❌ **Lead không đặt lịch**<br><br>👤 **Tên**: {{$json.name}}<br>📞 **Số điện thoại**: {{$json.phone}}<br>💬 **Ghi chú**: {{$json.transcript}}``` | Cấu hình tương tự như **Slack: Booked**. |
| **Email: Not Booked**  | - **Credentials**: Gmail OAuth.<br>- **To**: Email của team.<br>- **Subject**: `❌ Lead {{$json.name}} không đặt lịch`.<br>- **Body**:<br>  ```html<br><h1>Lead không đặt lịch</h1><br><p><strong>Tên:</strong> {{$json.name}}</p><br><p><strong>Số điện thoại:</strong> {{$json.phone}}</p><br><p><strong>Ghi chú cuộc gọi:</strong></p><p>{{$json.transcript}}</p>``` | Thay đổi nội dung Email theo brand. |

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một lead mẫu:
   - Tạo một lead giả trên Facebook Ads (hoặc sử dụng **Sticky Note** để mock dữ liệu).
   - Chạy workflow và kiểm tra:
     - Lead có được lưu vào Supabase không?
     - Cuộc gọi AI có được trigger không?
     - Kết quả có được gửi Slack/Email không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Cuộc Gọi AI**
- **Cấu hình prompt** phù hợp với ngành nghề:
  - **Bán hàng**: `"Hello, this is [Company]. We noticed you're interested in [Product]. Could you confirm your budget and pain points?"`
  - **Dịch vụ**: `"Thank you for your lead. We’ll call you back within 24 hours. Please confirm your availability for a meeting this week."`
- **Sử dụng voice model** có giọng thân thiện (ví dụ: giọng Mỹ, Anh, Việt Nam).

### **2. Lưu Log & Báo Cáo**
- **Thêm node `set`** sau **Update Lead Row** để lưu log vào Supabase:
  ```json
  {
    "operation": "insert",
    "table": "call_logs",
    "data": {
      "lead_id": "{{$json.id}}",
      "call_date": "{{$json.call_date}}",
      "status": "{{$json.call_status}}",
      "duration": "{{$json.duration}}",
      "transcript": "{{$json.transcript}}"
    }
  }
  ```
- **Tạo dashboard** trên Supabase Studio để theo dõi:
  - Tỷ lệ lead đặt lịch.
  - Thời gian trung bình cuộc gọi.
  - Top lead có giá trị cao.

### **3. Kết Hợp Với CRM**
- **Nếu dùng HubSpot/Zoho**: Thêm node **HTTP Request** để sync lead vào CRM.
- **Ví dụ**:
  ```json
  {
    "url": "https://api.hubapi.com/crm/v3/objects/contacts",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer YOUR_HUBSPOT_API_KEY"
    },
    "body": {
      "properties": {
        "email": "{{$json.email}}",
        "phone": "{{$json.phone}}",
        "company": "{{$json.company}}",
        "status": "{{$json.call_status}}"
      }
    }
  }
  ```

### **4. Gửi Email Tự Động Sau Cuộc Gọi**
- **Nếu lead đặt lịch**: Gửi Email xác nhận với link lịch.
- **Nếu lead không đặt lịch**: Gửi Email follow-up với nội dung:
  ```html
  <h1>Chúng tôi chưa thể