---
title: "🔥 Tự Động Hóa Phân Loại Email Lạnh & Thông Báo Trên Telegram Với OpenAI & Instantly (Không Cần Code)"
description: "Workflow tự động phân loại phản hồi email lạnh thành HOT/WARM/COLD bằng AI, gửi thông báo ưu tiên trên Telegram và tự động xác nhận email cho leads có tiềm năng cao - tiết kiệm thời gian lên đến 80% cho đội ngũ Sales/Marketing."
slug: "tu-dong-hoa-phan-loai-email-lanh-notify-telegram"
tags: [n8n, automation, ai-summarization, cold-email, telegram-notification, openai, google-sheets]
keywords: [tự động hóa email lạnh, phân loại leads bằng AI, n8n workflow, telegram alert, instant reply automation, openai gpt-4o-mini]
---

# 🚀 **Tự Động Hóa Phân Loại Email Lạnh & Thông Báo Trên Telegram Với OpenAI & Instantly**

### **Giải pháp AI tự động hóa phản hồi email lạnh cho Sales/Marketing**
Các sếp đang mất **giờ đồng hồ** mỗi ngày để:
❌ Phân loại hàng trăm phản hồi email lạnh (HOT/WARM/COLD) thủ công
❌ Lo lắng bỏ lỡ leads tiềm năng vì không phản hồi kịp thời
❌ Không có hệ thống thống kê hoặc báo cáo tự động

**Workflow này giúp:**
✅ **Phân loại tự động** phản hồi email thành **HOT** (tiềm năng cao), **WARM** (tiềm năng trung bình), **COLD** (không tiềm năng) bằng **OpenAI GPT-4o-mini**
✅ **Gửi thông báo ưu tiên** trên Telegram cho từng loại leads
✅ **Tự động xác nhận email** (auto-ack) cho leads HOT/WARM để tăng tỷ lệ chuyển đổi
✅ **Lưu log toàn bộ dữ liệu** vào Google Sheets để phân tích sau này

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** phân loại và phản hồi email thủ công
- **Tăng tỷ lệ chuyển đổi** với auto-ack cho leads HOT/WARM
- **Báo cáo tự động** trên Google Sheets để theo dõi hiệu suất
- **Không bỏ lỡ leads** nhờ thông báo Telegram ưu tiên
- **Cá nhân hóa phản hồi** dựa trên phân loại AI
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Instantly** (để nhận webhook khi có phản hồi email)
✔ **API Key OpenAI** (để phân loại bằng AI)
✔ **Tài khoản Gmail** (để tự động xác nhận email)
✔ **Bot Telegram** (để gửi thông báo)
✔ **Google Sheet** (để lưu log phản hồi)
✔ **Credentials trong n8n**:
   - `openAiApi` (API Key OpenAI)
   - `gmail` (Tài khoản Gmail)
   - `telegram` (Token Bot Telegram)
   - `googleSheets` (Tài khoản Google)

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14220](https://n8n.io/workflows/14220)
- **Nhấn "Import"** trong n8n Editor và chọn file JSON
- **Hoặc copy/paste** JSON từ file vào n8n Editor

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook Instantly**
- Mở **Instantly Dashboard** → **Settings** → **Integrations** → **Webhooks**
- Chọn **reply_received** và **dán URL webhook** của workflow (đường dẫn: `https://[your-n8n-url]/webhook/instantly-reply`)
- **Kiểm tra** để đảm bảo webhook hoạt động

##### **B. Cấu hình OpenAI (Phân loại AI)**
- **Node: "Classify Reply - OpenAI"**
  - **Credentials**: Chọn `openAiApi`
  - **Prompt**: Để mặc định (có thể tùy chỉnh để thay đổi tiêu chí phân loại)
  - **Model**: Chọn `gpt-4o-mini` (mặc định)

##### **C. Cấu hình Telegram (Thông báo)**
- **Node: "Telegram - HOT Lead", "Telegram - WARM Lead", "Telegram - COLD Lead"**
  - **Credentials**: Chọn `telegram`
  - **Chat ID**: Thay thế `YOUR_TELEGRAM_CHAT_ID` bằng **Chat ID của cá nhân hoặc nhóm Telegram** (lấy từ `@userinfobot` trên Telegram)
  - **Message Template**: Để mặc định hoặc tùy chỉnh nội dung thông báo

##### **D. Cấu hình Gmail (Auto-Ack)**
- **Node: "Auto-Ack HOT Gmail" & "Auto-Ack WARM Gmail"**
  - **Credentials**: Chọn `gmail`
  - **Email Address**: Điền địa chỉ email của **tài khoản Gmail** sẽ gửi auto-ack
  - **Subject & Body**: Tùy chỉnh nội dung email (ví dụ: *"Xin chào [Name], cảm ơn phản hồi của bạn!"*)

##### **E. Cấu hình Google Sheets (Lưu log)**
- **Node: "Log Reply to Sheet"**
  - **Credentials**: Chọn `googleSheets`
  - **Sheet ID**: Thay thế `YOUR_GOOGLE_SHEET_ID` bằng **ID của Google Sheet** (lấy từ URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`)
  - **Sheet Name**: Điền tên **tab** trong Google Sheet (ví dụ: `Email_Replies`)
  - **Columns**: Đảm bảo Google Sheet có các cột sau:
    ```
    timestamp | lead_email | lead_name | classification | campaign | subject | reply_snippet | reasoning | auto_ack_sent | manual_reply_sent | manual_reply_at
    ```

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **"Run Workflow"** và gửi một phản hồi mẫu từ Instantly để kiểm tra
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh tiêu chí phân loại AI**
   - Mở node **"Classify Reply - OpenAI"** và chỉnh sửa **prompt** để thay đổi tiêu chí phân loại (ví dụ: thêm/loại bỏ các yếu tố như "người dùng đã đặt lịch hẹn" → **HOT**).

2. **Kết hợp với Slack thay vì Telegram**
   - Thay thế node Telegram bằng **Slack Webhook** để gửi thông báo trên Slack.

3. **Lưu log vào Database thay vì Google Sheets**
   - Thay node `googleSheets` bằng **MySQL/PostgreSQL** để lưu dữ liệu lâu dài.

4. **Gửi báo cáo định kỳ**
   - Sử dụng **n8n Schedule Node** để gửi báo cáo hàng tuần về leads HOT/WARM qua email.

5. **Tự động chuyển leads HOT sang CRM**
   - Kết nối với **HubSpot/Zoho CRM** để tự động thêm leads HOT vào pipeline.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc phân loại email lạnh thủ công, đồng thời **tăng tỷ lệ chuyển đổi** nhờ tự động xác nhận và báo cáo chi tiết. **Hãy áp dụng ngay** để tối ưu hóa quy trình Sales/Marketing của doanh nghiệp!

👉 **Bắt đầu tự động hóa ngay hôm nay!**
- [Tải workflow từ n8n.io](https://n8n.io/workflows/14220)
- [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting/)
- **Cần hỗ trợ?** Liên hệ với **Devon Toh** qua [Calendly](https://cal.com/devon-toh-vrmdab/30min) để tư vấn chi tiết!