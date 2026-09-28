---
title: "🛡️ **Tự Động Quét & Phân Loại Tệ Năng trong Email Gmail bằng VirusTotal + AI (GPT-4o-mini) - An Toàn Mật Mã & Phishing 24/7**"
description: "Workflow tự động hóa kiểm tra tất cả các file đính kèm trong Gmail bằng VirusTotal (quét virus/malware) và AI (phân tích nguy cơ phishing), tự động phân loại thành 3 trạng thái: **Quarantine**, **Review Queue** hoặc **Safe Drive**. Giúp các sếp tiết kiệm thời gian, giảm rủi ro an toàn thông tin và tự động hóa quy trình bảo mật."
slug: "tieu-dong-quet-phan-loai-te-nang-gmail-virus-total-ai"
tags: [n8n, automation, secops, ai-summarization, virus-total, gmail-automation, google-drive, slack-alert, openai]
keywords: [tự động hóa gmail, quét virus email, phân loại phishing, virus total n8n, ai phân tích an toàn, tự động hóa bảo mật, n8n workflow secops, google sheets review queue]
---

# 🚀 **Tự Động Quét & Phân Loại Tệ Năng trong Email Gmail bằng VirusTotal + AI (GPT-4o-mini)**

### **Nỗi Đau Của Các Sếp**
Trong môi trường làm việc hiện đại, **email vẫn là vector tấn công phổ biến nhất** với:
- **Malware/vi-rút** trong file đính kèm (PDF, DOCX, EXE, ZIP...) lây lan qua email.
- **Phishing** (giả mạo email từ ngân hàng, quản lý, hoặc đồng nghiệp) lừa người dùng tiết lộ thông tin nhạy cảm.
- **Thời gian mất mát** để thủ công kiểm tra từng file đính kèm và phân loại nguy cơ.

**Giải pháp?** Một **workflow tự động hóa 100% không cần code** sử dụng:
✅ **VirusTotal** (quét virus/malware trong file đính kèm)
✅ **GPT-4o-mini (OpenAI)** (phân tích nguy cơ phishing trong nội dung email)
✅ **Google Sheets** (đăng ký review cho các trường hợp nghi ngờ)
✅ **Google Drive** (lưu file an toàn nếu không nguy hiểm)
✅ **Slack/Email** (cảnh báo tức thời cho đội ngũ IT/Security)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động quét tất cả email có đính kèm** (không bỏ sót một file nào).
- **Phân loại nguy cơ chính xác** (Danger → Quarantine, Suspicious → Review, Safe → Drive).
- **Cảnh báo tức thời** trên Slack/Email khi phát hiện nguy cơ cao.
- **Giảm thiểu rủi ro phishing** bằng AI phân tích nội dung email.
- **Tiết kiệm thời gian** (không cần kiểm tra thủ công hàng ngày).
- **Lưu trữ an toàn** file hợp lệ vào Google Drive.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **Gmail** (để truy cập email và thêm nhãn).
   - **Google Drive** (để lưu file an toàn).
   - **Google Sheets** (để đăng ký review).
   - **Slack** (để cảnh báo nguy cơ cao).
   - **VirusTotal** ([đăng ký miễn phí](https://www.virustotal.com/gui/signup/challenge)) → **API Key** (để quét virus).
   - **OpenAI** ([đăng ký miễn phí](https://platform.openai.com/signup)) → **API Key** (để phân tích phishing).
2. **Cấu trúc Google Sheets**:
   - **Cột cần thiết**:
     - `timestamp` (thời gian phát hiện)
     - `email_from` (người gửi)
     - `email_subject` (tiêu đề email)
     - `attachment` (tên file đính kèm)
     - `malicious_count` (số lượng virus phát hiện)
     - `ai_verdict` (phán đoán AI về nguy cơ phishing).
3. **Google Drive**:
   - **Tạo 1 thư mục** để lưu file an toàn (ví dụ: `Safe_Attachments`).
4. **Gmail**:
   - **Tạo nhãn mới** gọi là `QUARANTINE` (để đánh dấu email nguy cơ cao).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15207](https://n8n.io/workflows/15207) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15207) và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **13 node**, các sếp cần **cấu hình chính xác** các node sau:

##### **A. Node "Set Configuration" (Cấu Hình)**
- **Điền các giá trị sau** vào **JSON Data**:
  ```json
  {
    "sheetId": "YOUR_GOOGLE_SHEET_ID",  // ID của Google Sheet review queue
    "driveFolderId": "YOUR_DRIVE_FOLDER_ID",  // ID của thư mục Safe Drive
    "slackChannel": "#security-alerts",  // Channel Slack để cảnh báo
    "quarantineLabel": "QUARANTINE"  // Tên nhãn Quarantine trong Gmail
  }
  ```
  - **Lấy `sheetId` và `driveFolderId`**:
    - Mở Google Sheets → URL sẽ có dạng: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/edit` → Copy `SHEET_ID`.
    - Mở Google Drive → Thư mục Safe → URL sẽ có dạng: `https://drive.google.com/drive/folders/[FOLDER_ID]` → Copy `FOLDER_ID`.

##### **B. Node "Poll Gmail for New Attachments" (GmailTrigger)**
- **Chọn credential Gmail** đã cấu hình trước đó.
- **Cài đặt**:
  - **Label**: `unread` (để lấy tất cả email chưa đọc).
  - **Attachments**: `true` (để lấy file đính kèm).

##### **C. Node "Look Up Hash in VirusTotal" (httpRequest)**
- **Thêm Header Auth**:
  - **Key**: `x-apikey`
  - **Value**: `YOUR_VIRUSTOTAL_API_KEY` (đăng ký tại [VirusTotal](https://www.virustotal.com/gui/signup/challenge)).
- **URL Template**:
  ```
  https://www.virustotal.com/api/v3/files/{$json["sha256"]}
  ```
  (Node này sẽ tự động lấy `sha256` từ file đính kèm).

##### **D. Node "Classify Phishing Risk with OpenAI" (openAi)**
- **Chọn credential OpenAI** đã cấu hình.
- **Prompt mẫu** (có thể tùy chỉnh):
  ```
  Analyze the following email for phishing risk. Return a verdict with confidence score (0-100):
  - Subject: {$json["email_subject"]}
  - Body: {$json["email_body"]}
  Verdict format:
  {
    "verdict": "safe|suspicious|phishing",
    "confidence": 0-100
  }
  ```
  - **Lưu ý**: Nếu AI trả về `phishing` với `confidence > 70`, sẽ được coi là nguy cơ cao.

##### **E. Node "Apply Quarantine Label on Gmail" (gmail)**
- **Chọn credential Gmail**.
- **Điền nhãn**: `QUARANTINE` (nhãn đã tạo trước đó).

##### **F. Node "Send Security Alert to Slack" (slack)**
- **Chọn credential Slack**.
- **Message Template** (có thể tùy chỉnh):
  ```
  *🚨 SECURITY ALERT 🚨*
  **Email từ**: {$json["email_from"]}
  **Tiêu đề**: {$json["email_subject"]}
  **File đính kèm**: {$json["attachment_name"]}
  **Nguy cơ VirusTotal**: {$json["malicious_count"]} malware detected
  **Nguy cơ AI**: {$json["ai_verdict"]} (confidence: {$json["ai_confidence"]}%)
  **Hành động**: Quarantined
  ```

##### **G. Node "Log to Review Queue on Google Sheets" (googleSheets)**
- **Chọn credential Google Sheets**.
- **Sheet Name**: Tên của Google Sheet review queue.
- **Range**: `Sheet1!A1` (đảm bảo cột đầu tiên trống).

##### **H. Node "Save Attachment to Safe Drive Folder" (googleDrive)**
- **Chọn credential Google Drive**.
- **Folder ID**: `YOUR_DRIVE_FOLDER_ID` (đã lấy ở phần "Set Configuration").

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một email mẫu có đính kèm file (ví dụ: một file PDF có virus hoặc email phishing).
  - Kiểm tra **Google Sheets** (đã đăng ký review?), **Slack** (có cảnh báo không?), **Google Drive** (file an toàn có được lưu không?).
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để chạy tự động mỗi phút.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Google Calendar**:
   - Tự động gửi **báo cáo hàng tuần** về các trường hợp nghi ngờ qua email hoặc Slack.
2. **Lưu Log Chi Tiết**:
   - Sử dụng **Google Sheets** để lưu tất cả lịch sử quét (ngày giờ, file, nguy cơ, hành động).
3. **Cảnh Báo Trực Tuyến**:
   - Thêm **node Telegram Bot** để cảnh báo ngay khi phát hiện nguy cơ cao.
4. **Tự Động Xóa Email Quarantine**:
   - Thêm **node Gmail** để **xóa email** sau 7 ngày nếu không được review.
5. **Tùy Chỉnh Ngưỡng Nguy Cơ**:
   - Sử dụng **node Code** để điều chỉnh ngưỡng phân loại (ví dụ: `malicious_count > 3` hoặc `ai_confidence > 80`).

---

### 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn tự động** vấn đề **an toàn email** với:
✔ **Quét virus/malware** bằng VirusTotal.
✔ **Phân tích phishing** bằng AI (GPT-4o-mini).
✔ **Phân loại tự động** thành **Quarantine**, **Review Queue** hoặc **Safe Drive**.
✔ **Cảnh báo tức thời** trên Slack/Email.

**Hành động ngay**:
1. **Chuẩn bị tài khoản & API Keys** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với email mẫu** trước khi bật chạy thực tế.
4. **Bật workflow** và **quên đi lo lắng về an toàn email!**

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy **ổn định 24/7** mà không lo gián đoạn!