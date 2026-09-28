---
title: "🚀 Tự Động Hóa Chuyển Đổi Lead Tiềm Năng - AI Scoring + Theo Dõi Google Sheets + Cảnh Báo Multi-Channel (Slack/Gmail)"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp B2B/SaaS **lọc lead chất lượng cao**, **phân loại rủi ro gian lận** (email giả, IP không hợp lệ), **nurture tự động** qua email cá nhân hóa và **báo cáo tuần định kỳ** - tiết kiệm 15-20 giờ/tháng cho đội ngũ sales."
slug: "tieu-dong-hoa-chuyen-doi-lead-ai-scoring"
tags: [n8n, automation, no-code, ai-scoring, google-sheets, slack-integration, gmail-automation, lead-nurturing, fraud-detection]
keywords: [n8n workflow lead capture, tự động hóa chuyển đổi lead, AI đánh giá chất lượng lead, theo dõi lead google sheets, cảnh báo sales slack, email tự động nurture, báo cáo tuần định kỳ]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Lead Tiềm Năng - AI Scoring + Theo Dõi Google Sheets + Cảnh Báo Multi-Channel**

## **Nỗi Đau Của Các Sếp Sales**
Hàng ngày, đội ngũ sales phải:
- **Lọc thủ công** hàng trăm lead từ form website, chỉ để lại 10-20% lead có chất lượng.
- **Phải kiểm tra từng email** để phát hiện gian lận (email giả, IP không hợp lệ).
- **Gửi email nurture** một cách không đồng bộ, dẫn đến tỷ lệ mở thấp.
- **Báo cáo tuần** phải tổng hợp từ nhiều nguồn khác nhau, mất thời gian và dễ sai sót.

**Kết quả?** Tốn **15-20 giờ/tháng** cho công việc lặp đi lặp lại, trong khi lead chất lượng bị "chìm" trong luồng thông tin.

---
### **🎯 Giải Pháp: Workflow Tự Động Hóa Lead Chất Lượng Cao**
Workflow này **giải quyết toàn bộ vấn đề** bằng cách:
✅ **Lọc lead tự động** với AI Scoring (đánh giá chất lượng email, IP, và hành vi).
✅ **Phát hiện gian lận** (email giả, IP không hợp lệ) bằng **Verifi Email API**.
✅ **Nurture lead tự động** qua email cá nhân hóa (welcome + follow-up).
✅ **Cảnh báo sales** trên Slack khi có lead "hot" (score cao).
✅ **Theo dõi lead** trên Google Sheets với lịch sử tương tác.
✅ **Báo cáo tuần tự động** gửi cho trưởng sales.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 15-20 giờ/tháng** cho đội ngũ sales.
- **Tăng tỷ lệ chuyển đổi lead** lên **30-50%** (do lọc lead chất lượng cao).
- **Giảm rủi ro gian lận** (email giả, IP không hợp lệ) xuống **<5%**.
- **Email nurture tự động** với nội dung cá nhân hóa.
- **Báo cáo tuần định kỳ** tự động gửi cho trưởng sales.
- **Cảnh báo Slack** khi có lead "hot" cần ưu tiên.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản n8n Self-hosted** (cài trên VPS).
✔ **Credentials sau**:
   - **Google Sheets OAuth2** (để ghi lead vào bảng tính).
   - **Gmail OAuth2** (để gửi email welcome + follow-up).
   - **Slack API** (để cảnh báo lead "hot").
   - **Verifi Email API** (để kiểm tra email hợp lệ).
✔ **URL Webhook** để form website gửi lead (cấu trúc: `https://[your-n8n-url]/webhook/lead-capture`).
✔ **Mẫu email welcome & follow-up** (sẵn sàng trong node `Auto-Send Welcome Email` và `Auto Follow-Up Email`).
✔ **Bảng Google Sheets** để lưu lead (cấu trúc sẽ tự động tạo).
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/8879](https://n8n.io/workflows/8879) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Import** → **Paste JSON** → **Import**.
3. **Kích hoạt workflow** (bật nút **Active** ở góc trên bên phải).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/8879](https://n8n.io/workflows/8879).
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON** → **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "Capture Leads" (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `lead-capture` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL**: `https://[your-n8n-url]/webhook/lead-capture` (thay `[your-n8n-url]` bằng URL VPS của bạn).
- **Lưu ý**:
  - **Kết nối form website** với Webhook này bằng cách gửi **POST request** khi người dùng submit form.
  - **Dữ liệu input**: Workflow kỳ vọng dữ liệu có các trường:
    ```json
    {
      "email": "user@example.com",
      "name": "John Doe",
      "ip": "123.45.67.89",
      "company": "ABC Corp",
      "message": "Tôi muốn thử dịch vụ..."
    }
    ```

#### **🔹 Node "Validate Email" (VerifiEmail)**
- **Cài đặt Node VerifiEmail** (nếu chưa có):
  ```bash
  npm install n8n-nodes-verifi-email
  ```
- **Thiết lập Credential**:
  - **Tên Credential**: `verifiEmailApi`.
  - **API Key**: Nhập **API Key** từ tài khoản [Verifi Email](https://verifi.com/).
- **Lưu ý**:
  - **Self-hosted chỉ hỗ trợ** (không có trên n8n.cloud).
  - **Tốc độ kiểm tra**: ~1-2 giây/email.

#### **🔹 Node "Lead Quality Score" (Code)**
- **Logic mặc định**:
  - **Điểm cao (80-100)**: Email hợp lệ + IP hợp lệ + không có từ khóa spam.
  - **Điểm trung bình (50-79)**: Email hợp lệ nhưng IP không rõ ràng.
  - **Điểm thấp (<50)**: Email giả hoặc IP không hợp lệ.
- **Customize**:
  - Mở node **Code** → **Edit JavaScript** → **Sửa logic** theo nhu cầu (ví dụ: thêm trọng số cho trường `company`).

#### **🔹 Node "Append row in sheet" (Google Sheets)**
- **Chọn Credential**: `googleSheetsOAuth2Api`.
- **Bảng Sheets**:
  - Workflow sẽ **tự động tạo** bảng mới nếu chưa có.
  - **Tên Sheet**: `Leads` (không đổi).
  - **Cột tự động tạo**: `email`, `name`, `ip`, `company`, `score`, `status`, `last_contact`.
- **Lưu ý**:
  - **Quản trị viên Sheets** phải chia sẻ bảng với **n8n OAuth2** (quyền chỉnh sửa).

#### **🔹 Node "Notify Sales Team" (Slack)**
- **Thiết lập Credential**:
  - **Tên Credential**: `slackApi`.
  - **URL Slack**: `https://hooks.slack.com/services/[YOUR_SLACK_HOOK]` (tạo từ **Apps > Incoming Webhooks**).
- **Cấu hình thông báo**:
  - **Message**: `🚨 **HOT LEAD ALERT** 🚨\n*Name*: {{ $node["Set User Config"].json["name"] }\n*Email*: {{ $node["Set User Config"].json["email"] }\n*Score*: {{ $node["Lead Quality Score"].json["score"] }} (High Risk)`.
  - **Customize**: Thay đổi **cách thức cảnh báo** (ví dụ: thêm emoji, thay đổi màu sắc).

#### **🔹 Node "Auto-Send Welcome Email" (Gmail)**
- **Thiết lập Credential**:
  - **Tên Credential**: `gmailOAuth2`.
  - **Tài khoản Gmail**: Sử dụng **tài khoản chính thức** của doanh nghiệp (không Gmail cá nhân).
- **Mẫu email**:
  - **Subject**: `Welcome to [Your Company]! 🎉`
  - **Body**:
    ```html
    <p>Hi {{ $node["Set User Config"].json["name"] }},</p>
    <p>Thank you for reaching out! We're excited to help you with {{ $node["Set User Config"].json["company"] }}.</p>
    <p>Best regards,<br>Your Team</p>
    ```
- **Lưu ý**:
  - **Không sử dụng Gmail cá nhân** (có thể bị block).
  - **Test email** trước khi kích hoạt workflow.

#### **🔹 Node "Weekly Report Trigger" (ScheduleTrigger)**
- **Cấu hình lịch**:
  - **Cron**: `0 0 * * 1` (chạy **mỗi thứ 2 lúc 00:00**).
  - **Customize**: Thay đổi ngày giờ theo nhu cầu (ví dụ: `0 0 * * 0` để chạy **mỗi chủ nhật**).
- **Lưu ý**:
  - **Kiểm tra thời gian UTC** (n8n sử dụng UTC).
  - **Test run** trước khi kích hoạt.

#### **🔹 Node "Set User Config" (Set)**
- **Cấu hình biến**:
  - **`sales_head_email`**: Email của trưởng sales (ví dụ: `trung.sales@yourcompany.com`).
  - **`welcome_email_template`**: Nội dung email welcome (sẵn sàng trong node `Auto-Send Welcome Email`).
  - **`followup_email_template`**: Nội dung email follow-up.
  - **`ip_lookup_url`**: URL API để tra cứu IP (mặc định: `https://ipapi.co/{ip}/json/`).
- **Lưu ý**:
  - **Sửa đổi** các biến này để phù hợp với doanh nghiệp.

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - **Gửi request POST** đến Webhook với dữ liệu mẫu:
     ```json
     {
       "email": "john.doe@example.com",
       "name": "John Doe",
       "ip": "123.45.67.89",
       "company": "ABC Corp",
       "message": "Tôi muốn thử dịch vụ..."
     }
     ```
   - **Kiểm tra**:
     - Email có được **validate** không?
     - Lead có được **ghi vào Sheets** không?
     - Email welcome có được **gửi thành công** không?
     - Cảnh báo Slack có xuất hiện không?

2. **Bật Active workflow**:
   - Sau khi test thành công, **bật nút Active** ở góc trên bên phải.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **1. Kết hợp với CRM (Zoho/HubSpot/Pipedrive)**
- **Thêm node `HTTP Request`** để push lead vào CRM.
- **Ví dụ**:
  ```javascript
  // Node Code (n8n-nodes-base.code)
  const response = await fetch("https://api.zoho.com/crm/Records/Leads", {
    method: "POST",
    headers: { "Authorization": "Bearer YOUR_ZOHO_API_KEY" },
    body: JSON.stringify({
      data: [
        {
          "email": $node["Set User Config"].json["email"],
          "first_name": $node["Set User Config"].json["name"],
          "company": $node["Set User Config"].json["company"],
          "status": "New Lead"
        }
      ]
    })
  });
  return { json: await response.json() };
  ```

### **2. Lưu log hoạt động**
- **Thêm node `Set`** sau `Append row in sheet` để lưu **log chi tiết**:
  ```json
  {
    "action": "log",
    "message": `Lead ${$node["Set User Config"].json["name"]} (${$node["Set User Config"].json["email"]}) đã được ghi vào Sheets. Score: ${$node["Lead Quality Score"].json["score"]}`
  }
  ```
- **Kết nối với node `Slack`** để **cảnh báo lỗi** nếu ghi Sheets thất bại.

### **3. Tăng cường AI Scoring**
- **Thêm node `LLM` (n8n-nodes-ai.llm)** để **phân tích nội dung message**:
  ```javascript
  // Node Code (n8n-nodes-base.code)
  const response = await fetch("https://api.openai.com/v1/chat/completions", {
    method: "POST",
    headers: { "Authorization": "Bearer YOUR_OPENAI_API_KEY", "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "gpt-3.5-turbo",
      messages: [{ role: "user", content: `Analyze this lead message for intent: "${$node["Set User Config"].json["message"]}"` }]
    })
  });
  const data = await response.json();
  $node["Set"].json["message_intent"] = data.choices[0].message.content;
  return $node["Set"].json;
  ```
- **Sử dụng kết quả** để **cập nhật score** trong node `Lead Quality Score`.

### **4. Báo cáo chi tiết hơn**
- **Thêm node `Google Sheets`** để **tạo bảng báo cáo tuần**:
  - **Cột**: `week_start_date`,