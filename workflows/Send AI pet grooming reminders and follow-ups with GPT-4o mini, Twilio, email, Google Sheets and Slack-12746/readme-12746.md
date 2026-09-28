---
title: "🐾 **Tự Động Hóa Lời Nhắc Chăm Sóc Thú Cưng AI + Theo Dõi Khách Hàng - Không Cần Code!**"
description: "Workflow tự động hóa gửi lời nhắc chăm sóc thú cưng cá nhân hóa bằng GPT-4o mini, SMS (Twilio), email, Google Sheets và thông báo Slack cho nhân viên. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng, tăng tỷ lệ xác nhận hẹn và cải thiện trải nghiệm khách hàng."
slug: "tieu-dong-hoa-loi-nhac-cham-soc-thu-cung-ai"
tags: [n8n, automation, no-code, pet-grooming, ai-summarization, google-sheets, twilio, slack, email-marketing]
keywords: [tự động hóa chăm sóc thú cưng, n8n workflow pet grooming, gửi lời nhắc SMS email AI, tự động hóa khách hàng, GPT-4o mini trong n8n]
---

# 🚀 **Tự Động Hóa Lời Nhắc Chăm Sóc Thú Cưng AI: Từ Hẹn Đến Thực Hiện - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Chăm Sóc Thú Cưng**
Hàng ngày, các sếp phải:
- **Gọi điện/SMS nhắc nhở** khách hàng về lịch hẹn chăm sóc thú cưng (tốn thời gian, dễ quên).
- **Gửi email thông tin chuẩn bị** trước khi đến cửa hàng (nhân viên phải copy-paste, mất hiệu quả).
- **Theo dõi trạng thái xác nhận** của khách hàng (rủi ro mất khách do không nhắc nhở kịp thời).
- **Cập nhật lịch làm việc** cho nhân viên chăm sóc thú cưng (thông báo thủ công, dễ sai sót).
- **Tạo báo cáo tuần** để đánh giá hiệu suất (tốn công tính toán, dễ lỗi).

**Kết quả?** Khách hàng quên hẹn, nhân viên bận rộn, doanh thu giảm. **Workflow này giải quyết tất cả!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** (không cần gọi điện/SMS thủ công).
✅ **Tỷ lệ xác nhận hẹn tăng 30%** (lời nhắc tự động + cá nhân hóa).
✅ **Trải nghiệm khách hàng nâng cao** (email/SMS thông minh, không giống nhau).
✅ **Nhân viên được thông báo kịp thời** (lịch làm việc tự động cập nhật Slack).
✅ **Báo cáo tuần tự động** (không cần tính toán thủ công).
✅ **Hoạt động 24/7** (không phụ thuộc vào giờ làm việc của nhân viên).
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ               | Thông Tin Cần Thiết                          | Ghi Chú                          |
|-----------------------|-----------------------------------------------|-----------------------------------|
| **Google Sheets**     | OAuth 2.0 API Key (đăng ký tại [Google Cloud](https://console.cloud.google.com/)) | Cho phép đọc/giữa dữ liệu lịch hẹn. |
| **OpenAI (GPT-4o mini)** | API Key (mua tại [OpenAI](https://platform.openai.com/)) | Để tạo lời nhắc cá nhân hóa.      |
| **Twilio (SMS)**      | Account SID & Auth Token (đăng ký tại [Twilio](https://www.twilio.com/)) | Gửi SMS nhắc nhở khách hàng.     |
| **Email (SMTP)**      | Thông tin SMTP (tên miền, mật khẩu ứng dụng) | Gửi email chuẩn bị trước khi đến cửa hàng. |
| **Slack**             | Webhook URL (tạo tại [Slack API](https://api.slack.com/messaging/composing)) | Thông báo lịch làm việc cho nhân viên. |

### **2. Google Sheets**
- **Tạo 1 bảng Google Sheets** với cấu trúc sau (các sếp có thể sao chép mẫu từ [đây](https://docs.google.com/spreadsheets/d/1XYZ...)):
  | **Client Name** | **Pet Name** | **Appointment Date** | **Appointment Time** | **Status** (Pending/Confirmed/Cancelled) | **Notes** |
  |-----------------|--------------|----------------------|----------------------|------------------------------------------|-----------|
  | *Dữ liệu khách hàng* | *Tên thú cưng* | *Ngày hẹn* | *Giờ hẹn* | *Trạng thái* | *Ghi chú* |

### **3. Twilio & Email**
- **Số điện thoại Twilio** (để gửi SMS).
- **Địa chỉ email SMTP** (để gửi email chuẩn bị).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/12746](https://n8n.io/workflows/12746) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trang chủ của n8n) → Nhấn **Import** → Dán JSON và nhấn **Import**.
3. **Chọn "Create new workflow"** và đặt tên (ví dụ: **"Pet Grooming Reminders"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** → Nhấn **Create new workflow**.
2. **Nhấn "Import"** → Chọn **Paste JSON** → Dán JSON từ [đây](https://n8n.io/workflows/12746) (đã export trước).
3. **Nhấn "Import"** và tiếp tục cấu hình.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này được chia thành **5 phần chính** (theo canvas). Các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **📌 Phần 1: Trigger & Config (Daily Appointment Check)**
- **Node: "Daily Appointment Check" (scheduleTrigger)**
  - **Chọn "Daily"** và thời gian phù hợp (ví dụ: **7h sáng** để nhắc nhở khách hàng sớm).
  - **Lưu ý:** Nếu muốn chạy **ngày cụ thể** (ví dụ: thứ 2, thứ 4), chọn **"Custom"** và chọn ngày.

- **Node: "Workflow Configuration" (set)**
  - **Thêm biến toàn cầu** (Global Variables) để lưu thông tin chung:
    - `{{ $json("clientName") }}` → Tên khách hàng.
    - `{{ $json("petName") }}` → Tên thú cưng.
    - `{{ $json("appointmentDate") }}` → Ngày hẹn.
    - `{{ $json("appointmentTime") }}` → Giờ hẹn.

#### **📌 Phần 2: Sheets & AI Logic (Lấy Dữ liệu + Tạo Lời Nhắc Cá Nhân Hóa)**
- **Node: "Get Upcoming Appointments" (googleSheets)**
  - **Chọn credentials:** `googleSheetsOAuth2Api`.
  - **Tham số:**
    - **Sheet Name:** Tên bảng Google Sheets (ví dụ: **"Pet Grooming Appointments"**).
    - **Query:** `SELECT * WHERE Status = 'Pending' AND Appointment Date >= CURRENT_DATE()` (lấy chỉ những hẹn sắp tới).
  - **Lưu ý:** Nếu bảng có nhiều sheet, chọn **Sheet ID** chính xác.

- **Node: "Generate Personalized Reminder" (openAi)**
  - **Chọn credentials:** `openAiApi`.
  - **Prompt mẫu (các sếp có thể chỉnh sửa):**
    ```plaintext
    You are a pet grooming assistant. Generate a friendly and personalized SMS reminder for a pet owner.
    Client Name: {{ $json("clientName") }}
    Pet Name: {{ $json("petName") }}
    Appointment Date: {{ $json("appointmentDate") }}
    Appointment Time: {{ $json("appointmentTime") }}
    Instructions: "Please bring your pet's nails trimmed, brush their fur, and avoid feeding them 4 hours before the appointment."
    Tone: Friendly and encouraging.
    ```
  - **Model:** Chọn **gpt-4o-mini** (rẻ hơn và hiệu quả).
  - **Output Format:** Chọn **JSON** để dễ xử lý sau.

#### **📌 Phần 3: Communication (Gửi SMS, Email & Theo Dõi)**
- **Node: "Send SMS Reminder" (twilio)**
  - **Chọn credentials:** `twilioCredentials`.
  - **Tham số:**
    - **From:** Số điện thoại Twilio (ví dụ: `+1234567890`).
    - **To:** `{{ $json("clientPhone") }}` (lấy từ Google Sheets).
    - **Body:** `{{ $json("smsContent") }}` (nội dung từ OpenAI).

- **Node: "Send Grooming Prep Instructions" (emailSend)**
  - **Chọn credentials:** `emailCredentials`.
  - **Tham số:**
    - **To:** `{{ $json("clientEmail") }}`.
    - **Subject:** `Preparation Instructions for {{ $json("petName") }}'s Appointment`.
    - **HTML Content:** Nội dung email mẫu (có thể lấy từ OpenAI hoặc viết riêng).

- **Node: "Check Confirmation Status" (if)**
  - **Điều kiện:** Kiểm tra `{{ $json("status") }}`:
    - Nếu **không xác nhận (Pending)**, gửi SMS/email nhắc lại.
    - Nếu **xác nhận (Confirmed)**, chuyển sang node tiếp theo.

#### **📌 Phần 4: Log & Notify (Cập Nhật Google Sheets & Slack)**
- **Node: "Log Client Interactions" (googleSheets)**
  - **Chọn credentials:** `googleSheetsOAuth2Api`.
  - **Tham số:**
    - **Sheet Name:** Tên bảng (ví dụ: **"Interaction Log"**).
    - **Operation:** `appendOrUpdate`.
    - **Data:** Thêm cột mới như `Interaction Time`, `Message Sent`, `Response`.

- **Node: "Notify Groomers of Daily Schedule" (slack)**
  - **Chọn Webhook URL** từ Slack.
  - **Tham số:**
    - **Text:** `🐾 **Daily Schedule Update** 🐾
      - {{ $json("clientName") }}'s {{ $json("petName") }}: {{ $json("appointmentTime") }} on {{ $json("appointmentDate") }} (Status: {{ $json("status") }})`.

#### **📌 Phần 5: Weekly Summary (Báo Cáo Tuần)**
- **Node: "Compile Weekly Summary Data" (merge)**
  - **Kết hợp dữ liệu** từ các hẹn trong tuần.
- **Node: "Format Weekly Report" (set)**
  - **Tạo báo cáo dưới dạng JSON** (có thể chuyển sang Markdown cho Slack).
- **Node: "Send Weekly Summary Report" (slack)**
  - **Gửi báo cáo tuần** cho team quản lý.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu:**
   - Thêm **1 hẹn mẫu** vào Google Sheets (trạng thái `Pending`).
   - Chạy **Manual Trigger** (nhấn nút play trên node **"Daily Appointment Check"**).
   - Kiểm tra:
     - SMS/email có được gửi không?
     - Slack có thông báo không?
     - Google Sheets có cập nhật log không?

2. **Bật Active:**
   - Sau khi test thành công, **bật "Active"** trên workflow.
   - **Lưu ý:** Nếu dùng **scheduleTrigger**, workflow sẽ chạy tự động hàng ngày.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Cá Nhân Hóa Lời Nhắc Hơn**
- **Chỉnh sửa Prompt OpenAI** để thêm:
  - **Lịch sử tương tác** (nếu khách hàng đã hủy hẹn trước, nhắc nhở nhẹ nhàng hơn).
  - **Thông tin cá nhân** (ví dụ: nếu khách hàng có thú cưng loạn ăn, nhắc nhở không cho ăn trước khi đến).

### **2. Kết Nối với CRM (CRM Integration)**
- **Nếu dùng HubSpot/Zoho CRM**, thêm node **HubSpot API** để cập nhật trạng thái khách hàng tự động.

### **3. Gửi Báo Cáo Tuần qua Email**
- Thay vì Slack, **gửi báo cáo tuần qua email** bằng node **emailSend** với template HTML đẹp.

### **4. Thêm Hệ Thống Chatbot (Slack/Telegram)**
- **Tạo bot Slack/Telegram** để khách hàng **xác nhận hủy hẹn** qua tin nhắn (sử dụng node **slack** hoặc **telegram**).

### **5. Log Toàn Bộ Quá Trình**
- **Thêm node "stickyNote"** để ghi lại **lỗi hoặc sự cố** (ví dụ: SMS gửi thất bại).

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhắc nhở thủ công, đồng thời **tăng tỷ lệ xác nhận hẹn** và **cải thiện trải nghiệm khách hàng** nhờ lời nhắc **cá nhân hóa** bằng AI.

**Bước đầu tiên:** **Import workflow, cấu hình Google Sheets và API keys**, rồi **test với 1 hẹn mẫu**. Sau đó, **bật Active** và **nhận lợi ích ngay!**

👉 **Bắt đầu tự động hóa ngay hôm nay!** Nếu có vấn đề, liên hệ với tác giả **Hyrum Hurst** tại [hyrum@quartersmart.com](mailto:hyrum@quartersmart.com).

---
**🚀 CẬN THẬN, CẬN TẬN!** Workflow này sẽ **tự động hóa 80% công việc chăm sóc khách hàng