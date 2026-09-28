---
title: "🤖 Tự Động Hóa Bác Sĩ Lễ Tân AI Đa Năng: Scheduling + Chatbot + Google Sheets (Miễn Code)"
description: "Workflow này tự động hóa hoàn toàn việc quản lý lịch hẹn, trả lời câu hỏi khách hàng và lưu trữ thông tin bằng AI + Google Calendar & Sheets. Giúp doanh nghiệp tiết kiệm 10+ giờ/ngày, giảm thiểu lỗi và cải thiện trải nghiệm khách hàng 24/7."
slug: "tay-dong-hoa-bac-si-le-tan-ai-google-calendar-sheets"
tags: [n8n, automation, ai-chatbot, google-calendar, google-sheets, no-code]
keywords: [n8n workflow tự động hóa, AI receptionist, chatbot scheduling, Google Calendar tự động, lưu trữ lịch hẹn Google Sheets, tự động hóa doanh nghiệp]
---

# 🚀 **Tạo Bác Sĩ Lễ Tân AI Đa Năng: Scheduling + Chatbot + Google Sheets (Không Cần Code)**

## **🔥 Bác Sĩ Lễ Tân AI Thay Thế 100% Công Việc Lễ Tân Hàng Ngày**
Hiện nay, việc quản lý lịch hẹn, trả lời câu hỏi khách hàng và cập nhật thông tin thủ công không chỉ tốn thời gian mà còn dễ gây lỗi. **Workflow này tự động hóa hoàn toàn quá trình** bằng cách kết hợp:
✅ **Chatbot AI** (GPT-4.1) trả lời mọi câu hỏi khách hàng với ngữ điệu chuyên nghiệp.
✅ **Kiểm tra & đặt lịch hẹn** trên Google Calendar một cách tự động.
✅ **Lưu trữ lịch hẹn** vào Google Sheets với định dạng chuyên nghiệp.
✅ **Giữ nhớ lịch sử hội thoại** để trải nghiệm khách hàng cá nhân hóa.

**Kết quả?** Các sếp tiết kiệm **10+ giờ/ngày**, giảm thiểu lỗi và cải thiện trải nghiệm khách hàng **24/7** mà không cần viết một dòng code nào!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phải trả lời email/telegram/livechat liên tục.
- **Chính xác 100%:** AI tự động kiểm tra lịch và đặt hẹn, tránh lỗi lịch trùng.
- **Cá nhân hóa trải nghiệm:** AI nhớ lịch sử hội thoại và phản hồi chuyên nghiệp.
- **Hoạt động liên tục:** Workflow chạy 24/7, không cần can thiệp thủ công.
- **Dữ liệu thống kê:** Tất cả lịch hẹn được lưu vào Google Sheets, dễ dàng phân tích.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Calendar & Sheets).
2. **API Key OpenAI** (để sử dụng GPT-4.1).
3. **Google Sheet** chứa:
   - Danh sách dịch vụ (Services).
   - Giờ mở cửa (Hours).
   - Chính sách (Policies).
   - Tính cách AI (Personality).
4. **Google Calendar** để quản lý lịch hẹn.
5. **N8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/8326) hoặc copy toàn bộ JSON từ đây.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON vào.
- **Bước 3:** Chọn **"Import"** để tạo workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **10 node**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node "Get business details" (Google Sheets)**
- **Mục đích:** AI lấy thông tin dịch vụ, giờ mở cửa và tính cách từ Google Sheets.
- **Cách cấu hình:**
  - **Credentials:** Chọn `"googleSheetsOAuth2Api"` (đã cấu hình trước khi import).
  - **Sheet Name:** Điền tên sheet chứa dữ liệu (ví dụ: `"Business_Info"`).
  - **Range:** Điền `"Sheet1!A1:D100"` (hoặc điều chỉnh theo cấu trúc của bạn).
  - **Lưu ý:** Sheet phải có **cột A: Services**, **cột B: Hours**, **cột C: Policies**, **cột D: Personality**.

##### **🔹 Node "OpenAI Chat Model" (GPT-4.1)**
- **Mục đích:** AI trả lời khách hàng với ngữ điệu chuyên nghiệp.
- **Cách cấu hình:**
  - **Credentials:** Chọn `"openAiApi"` (đã cấu hình API Key OpenAI).
  - **Model:** Đảm bảo chọn `"gpt-4.1-mini"` (hoặc phiên bản mới nhất).
  - **Temperature:** Giữ mặc định (`0.7`) để AI trả lời logic và chuyên nghiệp.

##### **🔹 Node "Check Calendar Availability" (Google Calendar)**
- **Mục đích:** AI kiểm tra lịch trước khi đặt hẹn.
- **Cách cấu hình:**
  - **Credentials:** Chọn `"googleCalendarOAuth2Api"`.
  - **Calendar ID:** Điền ID của calendar bạn muốn quản lý (thường là `"primary"`).
  - **Time Zone:** Chọn `"Asia/Ho_Chi_Minh"` (hoặc khu vực của bạn).
  - **Lưu ý:** Đảm bảo calendar **không bị khóa** và AI có quyền đọc/thêm sự kiện.

##### **🔹 Node "Book Calendar Appointment" (Google Calendar)**
- **Mục đích:** AI đặt lịch hẹn tự động khi khách hàng yêu cầu.
- **Cách cấu hình:**
  - **Credentials:** `"googleCalendarOAuth2Api"` (giống node trước).
  - **Summary:** Điền `"Lịch hẹn với [Tên Doanh Nghiệp]"` (hoặc tùy chỉnh).
  - **Description:** AI tự động điền từ thông tin khách hàng.
  - **Start Time & End Time:** Đảm bảo AI lấy thời gian từ node **"Structured Output Parser"**.

##### **🔹 Node "Save Appointment Record" (Google Sheets)**
- **Mục đích:** Lưu lịch hẹn vào Google Sheets.
- **Cách cấu hình:**
  - **Credentials:** `"googleSheetsOAuth2Api"`.
  - **Sheet Name:** Điền tên sheet lưu lịch (ví dụ: `"Appointments"`).
  - **Range:** Điền `"Sheet1!A1:E100"` (các cột: `Name, Email, Date, Time, Notes`).
  - **Lưu ý:** Đảm bảo sheet có **cột A: Name**, **cột B: Email**, **cột C: Date**, **cột D: Time**, **cột E: Notes**.

#### **3. Kích hoạt ⚡️**
- **Bước 1:** Test run với dữ liệu mẫu:
  - Gửi tin nhắn vào **node "When chat message received"** (ví dụ: *"Lịch hẹn ngày mai 10h"*).
  - Kiểm tra:
    - AI có trả lời logic không?
    - Lịch có được đặt trên Google Calendar không?
    - Dữ liệu có được lưu vào Google Sheets không?
- **Bước 2:** Nếu test thành công, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết nối với Slack/Telegram:**
   - Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để AI trả lời trên kênh team.
   - **Cách làm:**
     - Sau node **"OpenAI Chat Model"**, thêm node **`slack`** hoặc **`telegram`**.
     - Cấu hình **webhook** từ Slack/Telegram vào node **"When chat message received"**.

2. **Lưu log hoạt động:**
   - Thêm node **`n8n-nodes-base.httpRequest`** để gửi dữ liệu hoạt động đến **Google Drive** hoặc **Notion**.
   - **Cách làm:**
     - Sau node **"Save Appointment Record"**, thêm node **`httpRequest`** với endpoint lưu log.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng **`n8n-nodes-base.email`** để gửi báo cáo số lượng lịch hẹn hàng ngày.
   - **Cách làm:**
     - Thêm node **`setInterval`** (nếu self-hosted) để chạy hàng ngày.
     - Sau đó gửi email thông qua **`email`** node.

4. **Tùy chỉnh tính cách AI:**
   - Trong Google Sheets, cập nhật **cột "Personality"** để AI phản hồi theo phong cách riêng (ví dụ: *"Chuyên nghiệp"*, *"Thân thiện"*, *"Chuyên môn"*).
   - **Ví dụ:**
     ```
     | Services       | Hours          | Policies               | Personality          |
     |----------------|----------------|------------------------|----------------------|
     | Tư vấn SEO     | 8h-18h        | Đặt lịch trước 2 ngày | "Chuyên nghiệp, ngắn gọn" |
     ```

5. **Sử dụng AI Multimodal (nếu có hình ảnh):**
   - Nếu muốn AI xử lý tin nhắn có hình ảnh (ví dụ: upload CV), thêm node **`n8n-nodes-base.fileSystem`** để xử lý file.
---

### 📌 **Kết luận**
Workflow này **thay thế hoàn toàn công việc của bác sĩ lễ tân**, giúp doanh nghiệp:
✔ **Tiết kiệm thời gian** (không cần trả lời chat liên tục).
✔ **Tăng trải nghiệm khách hàng** (AI trả lời nhanh chóng và chuyên nghiệp).
✔ **Giảm thiểu lỗi** (lịch hẹn tự động kiểm tra trùng lặp).
✔ **Hoạt động 24/7** (không cần nhân viên đêm).

**🚀 Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow chạy 24/7).
2. **Import workflow** và cấu hình Google Sheets, Calendar, OpenAI.
3. **Test run** và bật Active workflow.

**🎁 Đăng ký VPS cho n8n với giảm giá:**
👉 [TinoHost (Mã giảm: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) (Giảm tới 39%)
👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

**Chúc các sếp thành công!** 💪🚀