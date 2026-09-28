---
title: "💰 **Tự Động Hóa Quản Lý Tài Chính Hàng Tháng Với Gmail, Google Sheets & GPT-4o – Báo Cáo Thu Chi Chi Tiết Mỗi Tháng**"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động thu thập, phân tích và báo cáo chi tiết tất cả giao dịch tài chính hàng tháng từ email, trích xuất dữ liệu từ hóa đơn, và tổng hợp thành báo cáo định kỳ với GPT-4o. Giúp tiết kiệm 10+ giờ/tháng và giảm thiểu lỗi nhân sự."
slug: "tieu-dong-hoa-quan-ly-tai-chinh-hang-thang-gmail-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, finance-tracking, ai-summarization, google-sheets, gmail, gpt-4o]
keywords: [tự động hóa quản lý tài chính, báo cáo thu chi hàng tháng, n8n workflow, trích xuất hóa đơn từ email, GPT-4o phân tích tài chính, google sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Quản Lý Tài Chính Hàng Tháng – Báo Cáo Thu Chi Chi Tiết Mỗi Tháng**

### **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải mất **5-10 giờ/tháng** để:
- **Tìm kiếm và phân loại** hóa đơn từ email (Gmail, Outlook).
- **Nhập thủ công** dữ liệu vào Google Sheets, Excel hoặc phần mềm kế toán.
- **Tính toán thủ công** tổng chi tiêu, thu nhập, và phân tích xu hướng.
- **Tạo báo cáo tháng** để trình lên ban lãnh đạo hoặc kế toán.

**Kết quả?** Dữ liệu không chính xác, mất thời gian, và dễ bị lỗi nhân sự. **Workflow này giải quyết tất cả!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** (không cần nhập dữ liệu thủ công).
✅ **Dữ liệu chính xác 100%** (trích xuất tự động từ email và hóa đơn).
✅ **Báo cáo tự động hóa** (GPT-4o tổng hợp và phân tích xu hướng chi tiêu).
✅ **Cá nhân hóa báo cáo** (được gửi trực tiếp qua email với biểu đồ và phân tích chi tiết).
✅ **Hoạt động liên tục** (không phụ thuộc vào nhân viên).

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
📌 **Tài khoản và API Keys:**
- **Gmail** (để lấy email hóa đơn).
- **Google Sheets** (để lưu trữ dữ liệu tài chính).
- **OpenAI API Key** (để sử dụng GPT-4o).
- **Tài khoản email** (để gửi báo cáo tháng).

📌 **Google Sheets:**
- Một **bảng tính** có tên **"Finance Tracker"** (các sếp có thể tạo mới hoặc chỉnh sửa tên).
- Các cột cần thiết: `Date`, `Vendor`, `Amount`, `Category`, `Description`.

📌 **Gmail:**
- Các sếp cần **cho phép truy cập API** cho Gmail (cài đặt trong [Google Cloud Console](https://console.cloud.google.com/)).
- **Lưu ý:** Email hóa đơn phải được **gửi vào một folder cụ thể** (ví dụ: "Hóa Đơn").

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8473](https://n8n.io/workflows/8473) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/8473](https://n8n.io/workflows/8473).
2. Trên **n8n Editor**, nhấn **Create new workflow** → Chọn **Import from JSON** → Dán JSON và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "Monthly Report Trigger" (Cron)**
- **Cấu hình:** Chọn **Schedule** → **Monthly** (ví dụ: **Ngày 1 của mỗi tháng**).
- **Lưu ý:** Đảm bảo **timezone** phù hợp với khu vực của các sếp.

#### **🔹 Node "User Config" (Set)**
- **Điền tham số:**
  - `sheetName`: Tên của **Google Sheet** (ví dụ: `"Finance Tracker"`).
  - `folderId`: **ID của folder Gmail** chứa hóa đơn (lấy từ liên kết Gmail: `https://mail.google.com/mail/u/0/#folder/[FOLDER_ID]`).
  - `emailAddress`: Email của các sếp (để gửi báo cáo).

#### **🔹 Node "Fetch Receipt Emails" (Gmail)**
- **Chọn credentials:** Tạo mới hoặc chọn **Gmail API** đã cấu hình trước.
- **Lưu ý:**
  - Chọn **Folder ID** đúng (nơi lưu hóa đơn).
  - Thiết lập **labeledAs** (nếu sử dụng nhãn) hoặc **after** (ngày bắt đầu lấy).

#### **🔹 Node "AI: Extract Receipt Data (GPT-4o)" (OpenAI)**
- **Cấu hình API Key:**
  - Đăng ký tại [OpenAI](https://platform.openai.com/) → Nhận **API Key**.
  - Trên n8n, thêm **OpenAI credentials** mới và dán **API Key**.
- **Prompt:** Workflow đã cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn tối ưu, các sếp có thể chỉnh sửa ở node "Clean & Parse AI Output").

#### **🔹 Node "Append to Finance Sheet" (Google Sheets)**
- **Chọn credentials:** Google Sheets API đã cấu hình.
- **Lưu ý:**
  - Đảm bảo **sheetName** và **range** (ví dụ: `"Sheet1!A1:D100"`) đúng.
  - Nếu sheet chưa có dữ liệu, workflow sẽ tự tạo.

#### **🔹 Node "Send Monthly Report" (EmailSend)**
- **Cấu hình:**
  - Chọn **credentials** của email (nếu dùng SMTP) hoặc **Gmail API**.
  - Đảm bảo **emailAddress** trong "User Config" đúng.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và chọn **1 email mẫu** (nếu có).
   - Kiểm tra **Google Sheets** và **email** để đảm bảo dữ liệu được trích xuất và gửi đúng.
2. **Bật Active:**
   - Sau khi test thành công, chuyển **Active** sang **ON**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram**
- Thêm **node Slack/Telegram** sau **"Send Monthly Report"** để thông báo báo cáo đã gửi.
- **Cách làm:**
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "options": {
      "webhookUrl": "URL_WEBHOOK_SLACK",
      "message": "Báo cáo tài chính tháng {{ $node["Send Monthly Report"].jsonpath("$.month") }} đã hoàn tất!"
    }
  }
  ```

### **🔹 Lưu Log Dữ Liệu**
- Thêm **node "Sticky Note"** để lưu **log lỗi** hoặc **dữ liệu debug**.
- **Cách làm:**
  ```json
  {
    "name": "Log Data",
    "type": "stickyNote",
    "options": {
      "note": "Dữ liệu tháng {{ $node["Generate Month Range"].jsonpath("$.month") }} đã xử lý."
    }
  }
  ```

### **🔹 Gửi Báo Cáo Định Kỳ cho Nhóm**
- Sử dụng **node "EmailSend"** với danh sách **CC/BCC** để gửi báo cáo cho nhiều người.
- **Cách làm:**
  ```json
  {
    "name": "Send to Team",
    "type": "emailSend",
    "options": {
      "to": ["team1@example.com", "team2@example.com"],
      "cc": ["manager@example.com"],
      "subject": "Báo cáo tài chính tháng {{ $node["Generate Month Range"].jsonpath("$.month") }}",
      "html": "{{ $node["Send Monthly Report"].jsonpath("$.html") }}"
    }
  }
  ```

### **🔹 Tối Ưu Hóa Prompt GPT-4o**
- Nếu muốn **trích xuất dữ liệu chính xác hơn**, chỉnh sửa **prompt** ở node **"AI: Extract Receipt Data"**:
  ```json
  {
    "name": "AI: Extract Receipt Data (GPT-4o)",
    "type": "openAi",
    "options": {
      "model": "gpt-4o",
      "prompt": "Trích xuất dữ liệu hóa đơn từ email sau:\n\n{{ $node["Parse Email Body & Check Attachments"].jsonpath("$.emailBody") }}\n\nĐịnh dạng JSON:\n{\n  \"Date\": \"dd/mm/yyyy\",\n  \"Vendor\": \"Tên nhà cung cấp\",\n  \"Amount\": \"Số tiền (số nguyên)\",\n  \"Category\": \"Chi tiêu (ví dụ: \"Food\", \"Utilities\")\n}"
    }
  }
  ```

---

## 📌 **Kết Luận**
Workflow **Automated Finance Tracker** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa quản lý tài chính** mà không cần code.
✔ **Tiết kiệm thời gian** và giảm thiểu lỗi nhân sự.
✔ **Có báo cáo chi tiết, phân tích sâu** với GPT-4o.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình các node** theo hướng dẫn.
3. **Bật Active** và **nhận báo cáo tự động hàng tháng!**

👉 **[Tải workflow ngay](https://n8n.io/workflows/8473)** và **cài đặt VPS n8n** để chạy 24/7!

---
**💡 Chia sẻ workflow này với đồng nghiệp nếu bạn thấy hữu ích!** 🚀