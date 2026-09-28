---
title: "🤖 **Tự Động Hóa Outreach Gọi Điện AI: Từ Airtable → Bolna → Brevo → Twilio (Không Cần Code!)**"
description: "Workflow tự động gọi điện AI hàng ngày từ Airtable, phân loại phản hồi thông qua Groq, gửi email tự động qua Brevo và cập nhật trạng thái trên Airtable. Giúp doanh nghiệp tiết kiệm 80% thời gian gọi điện thủ công và tối ưu hóa quy trình outreach bán hàng."
slug: "tự-dộng-hoa-outreach-gọi-điện-ai-airtable-bolna-brevo-twilio"
tags: [n8n, automation, sales-outreach, ai-voice, airtable, brevo, twilio, groq, no-code]
keywords: [n8n workflow gọi điện tự động, tự động hóa outreach bán hàng, Bolna AI voice, Brevo email tự động, Twilio WhatsApp, Groq AI phân tích cuộc gọi]
---

# 🚀 **Tự Động Hóa Outreach Gọi Điện AI: Giải Pháp "0-Touch" Cho Sales & Bán Hàng**

### **Nỗi Đau Của Các Sếp Trong Outreach Bán Hàng**
Gọi điện thủ công là một trong những công việc **tốn thời gian nhất** trong sales, đặc biệt khi danh sách khách hàng dài hàng trăm hoặc ngàn người. Các vấn đề thường gặp:
- **Tốn nhiều thời gian**: Một nhân viên sales có thể chỉ gọi được 20-30 cuộc trong một ngày.
- **Không đồng nhất**: Mỗi người gọi có cách tiếp cận khác nhau → hiệu quả thấp.
- **Không theo dõi được**: Không biết ai đã trả lời, ai không quan tâm, ai là lead hot.
- **Lặp lại công việc**: Phải ghi chép lại trạng thái cuộc gọi vào Airtable/Excel sau mỗi cuộc gọi.

**Workflow này giải quyết tất cả đó!** Với **AI Voice Outreach**, các sếp sẽ:
✅ **Gọi điện tự động** hàng ngày từ Airtable (không cần nhân viên).
✅ **Phân loại phản hồi** thông qua AI (Groq) để biết ai **quan tâm**, ai **không quan tâm**, ai là **dead contact**.
✅ **Gửi email tự động** qua Brevo (cũng là Sendinblue) phù hợp với từng trường hợp.
✅ **Cập nhật trạng thái** trên Airtable để theo dõi hiệu quả.
✅ **Gửi tin nhắn WhatsApp** cho lead hot (quan tâm) qua Twilio.
✅ **Không cần code** – chỉ cần cài đặt và chạy!

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian** gọi điện thủ công.
- **Tăng hiệu quả outreach** với AI phân loại tự động.
- **Cập nhật trạng thái chính xác** trên Airtable (không sai sót).
- **Tự động gửi email & WhatsApp** cho lead hot.
- **Hoạt động 24/7** mà không cần nhân viên.
- **Dễ dàng mở rộng** cho nhiều team sales.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Airtable**:
   - Một bảng **Contacts** với các trường:
     - `Name` (Tên)
     - `Phone` (Số điện thoại)
     - `Email` (Email)
     - `Call Status` (Trạng thái cuộc gọi: *Chưa gọi, Đã gọi, Quan tâm, Không quan tâm, Dead Contact*)
     - `Call Attempts` (Số lần gọi)
     - `Last Called` (Ngày gọi cuối cùng)
   - **Cấp quyền API** cho n8n truy cập bảng này.

2. **Bolna.ai** (hoặc Vapi.ai):
   - Tài khoản **Bolna** với một **voice agent** đã cấu hình (nếu chưa có, tạo mới).
   - **API Key** của Bolna (được cung cấp khi đăng ký).

3. **Groq API Key**:
   - Đăng ký miễn phí tại [console.groq.com](https://console.groq.com) và lấy **API Key**.

4. **Brevo (Sendinblue) API Key**:
   - Đăng ký miễn phí tại [brevo.com](https://www.brevo.com) và lấy **API Key**.

5. **Twilio Account**:
   - Tài khoản Twilio với **WhatsApp Sandbox** (hoặc số điện thoại đã được xác thực).
   - **API Key** và **Auth Token** từ Twilio Console.

6. **Thời gian khu vực**:
   - Cấu hình **Schedule Trigger** theo **múi giờ IST** (hoặc múi giờ của bạn).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow đã được chia sẻ trên [n8n.io](https://n8n.io/workflows/16192). Các sếp có thể:
- **Tải file JSON** và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::note[**Lưu Ý**]
- **Không sử dụng phiên bản Community của n8n** (nên dùng **Self-hosted** để ổn định).
- **Không xóa node nào** trừ khi biết rõ tác dụng của nó.
:::

---

### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**

#### **A. Cấu Hình Airtable**
- **Node: "Airtable — Get Contacts"**
  - **Base ID**: Lấy từ URL của bảng Airtable (vd: `https://airtable.com/abc123...` → `abc123...`).
  - **Table Name**: Đặt là **"Contacts"** (hoặc tên bảng của bạn).
  - **View**: Chọn **"All"** (hoặc view phù hợp).
  - **Filter**: Thêm điều kiện để **bỏ qua** những contact đã gọi trong ngày:
    ```json
    { "property": "Call Status", "operator": "does_not_equal", "value": "Dead Contact" }
    { "property": "Call Status", "operator": "does_not_equal", "value": "Interested" }
    { "property": "Call Status", "operator": "does_not_equal", "value": "Not Interested" }
    ```

#### **B. Cấu Hình Bolna.ai**
- **Node: "Bolna — Place Call"**
  - **URL**: Lấy từ Bolna Dashboard (vd: `https://api.bolna.ai/v1/calls`).
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_BOLNA>`
    - `Content-Type`: `application/json`
  - **Body**:
    ```json
    {
      "phone": "{{$json['Phone']}}",
      "agent_id": "<AGENT_ID_BOLNA>",
      "callback_url": "https://<YOUR_N8N_URL>/webhook/call-status"  // Cần cấu hình Webhook sau
    }
    ```

- **Node: "Bolna — Get Call Status"**
  - **URL**: `https://api.bolna.ai/v1/calls/{{$json['CallId']}}` (lấy từ response của node trước).
  - **Headers**: `Authorization: Bearer <API_KEY_BOLNA>`

#### **C. Cấu Hình Groq AI**
- **Node: "Groq — Analyze Transcript"**
  - **URL**: `https://api.groq.com/v1/chat/completions`
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_GROQ>`
    - `Content-Type`: `application/json`
  - **Body**:
    ```json
    {
      "model": "llama3-70b-8192",
      "messages": [
        {
          "role": "system",
          "content": "You are an AI assistant that analyzes call transcripts and classifies the outcome. Respond with ONLY JSON: {\"classification\": \"interested/not_interested\"}"
        },
        {
          "role": "user",
          "content": "{{$json['Transcript']}}"
        }
      ]
    }
    ```

#### **D. Cấu Hình Brevo (Email)**
- **Node: "Brevo — Opportunity Email" / "Brevo — Reassurance Email" / "Brevo — No Answer Email" / "Brevo — Dead Contact Email"**
  - **URL**: `https://api.brevo.com/v3/smtp/email`
  - **Headers**:
    - `api-key`: `<API_KEY_BREVO>`
    - `Content-Type`: `application/json`
  - **Body** (vd cho email **Opportunity**):
    ```json
    {
      "sender": {
        "name": "Your Company",
        "email": "no-reply@yourcompany.com"
      },
      "to": [
        {
          "email": "{{$json['Email']}}",
          "name": "{{$json['Name']}}"
        }
      ],
      "subject": "🚀 Opportunity: Let's Talk!",
      "text": "Hi {{$json['Name']}}, ...",
      "html": "<p>Hi {{$json['Name']}}, ...</p>"
    }
    ```

#### **E. Cấu Hình Twilio (WhatsApp)**
- **Node: "Whatsapp msg from Twilio"**
  - **URL**: `https://api.twilio.com/2010-04-01/Accounts/<ACCOUNT_SID>/Messages.json`
  - **Headers**:
    - `Authorization`: `Basic <ACCOUNT_SID>:<AUTH_TOKEN>`
    - `Content-Type`: `application/x-www-form-urlencoded`
  - **Body**:
    ```json
    {
      "From": "whatsapp:<YOUR_TWILIO_NUMBER>",
      "To": "whatsapp:{{$json['Phone']}}",
      "Body": "Hi {{$json['Name']}}, thank you for your interest! Let's schedule a call."
    }
    ```

#### **F. Cấu Hình Schedule Trigger**
- **Node: "Schedule — Daily 11AM IST"**
  - **Time Zone**: Chọn **Asia/Kolkata** (hoặc múi giờ của bạn).
  - **Time**: `11:00:00` (hoặc thời gian phù hợp).

#### **G. Cấu Hình "Skip if Called Recently"**
- **Node: "Skip if Called Recently"**
  - **Condition**:
    - **If**: `{{$json['Call Status']}}` **does not equal** `"Chưa gọi"`.
    - **Or**: `{{$json['Last Called']}}` **is after** `{{$now}}` (trong cùng ngày).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 contact mẫu để kiểm tra:
   - Call có được đặt không?
   - Groq phân loại đúng không?
   - Email được gửi không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa AI Voice Agent**
- **Tạo script gọi điện chuyên nghiệp** cho Bolna/Vapi:
  - Ví dụ: *"Chào {{Name}}, tôi là {{Your Name}} từ {{Company}}. Chúng tôi đang tìm kiếm giải pháp {{Product}} để giúp {{Industry}} của bạn tiết kiệm thời gian. Bạn có thể dành 2 phút để nghe về nó không?"*
- **Test nhiều lần** để cải thiện tỷ lệ trả lời.

### **2. Tăng Tỷ Lệ Trả Lời**
- **Gọi vào giờ làm việc** (vd: 9-12 AM hoặc 2-5 PM).
- **Sử dụng số điện thoại địa phương** (nếu có) để tăng tỷ lệ trả lời.

### **3. Theo Dõi & Log**
- **Thêm node "StickyNote"** để ghi chú lỗi hoặc cải tiến.
- **Sử dụng Google Sheets** để lưu log chi tiết (nếu cần).

### **4. Kết Hợp Slack/Telegram**
- **Thêm node "Slack/Telegram"** để thông báo kết quả cuộc gọi:
  ```json
  {
    "text": "📞 Call to {{Name}}: {{Call Status}}",
    "attachments": [
      {
        "color": "{{$json['Call Status'] === 'Interested' ? '#28a745' : '#dc3545'}}",
        "title": "Status",
        "text": "{{$json['Call Status']}}"
      }
    ]
  }
  ```

### **5. Tự Động Gửi Báo Cáo Hàng Tuần**
- **Thêm node "Schedule Trigger"** chạy hàng tuần và gửi báo cáo qua Brevo:
  - Dữ liệu: Số cuộc gọi, tỷ lệ trả lời, lead hot, lead cold.

---
## 📌 **Kết Luận: Áp Dụng Ngay & Tiết Kiệm Thời Gian!**
Workflow **AI Voice Outreach** này là **giải pháp hoàn hảo** cho các team sales, recruiters và outreach managers muốn:
✔ **Tự động hóa 80% công việc gọi điện**.
✔ **Phân loại lead chính xác** với AI Groq.
✔ **Gửi email & WhatsApp tự động** cho lead hot.
✔ **Cập nhật trạng thái trên Airtable** một cách chính xác.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để ổn định 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 1-2 contact** trước khi chạy toàn bộ.

:::success[**Khuyến nghị hạ tầng**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng**:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công với quy trình outreach tự động hóa!** 🚀