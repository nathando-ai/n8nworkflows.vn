---
title: "🏗️ Tự Động Hóa Xử Lý Bản Vẽ Kiến Trúc Sang Google Sheets Với AI VLM Run - Giảm Thời Gian Làm Việc 90%"
description: "Workflow tự động hóa chuyển đổi bản vẽ kiến trúc (PDF, JPG, PNG) thành dữ liệu cấu trúc trên Google Sheets chỉ trong vài giây, giúp các sếp tiết kiệm thời gian kiểm tra, theo dõi và quản lý hồ sơ pháp lý. Giúp công ty giảm thiểu rủi ro vi phạm quy định và tăng cường hiệu quả làm việc."
slug: "tieu-dong-hoa-xu-ly-ban-ve-kien-truc-sang-google-sheets"
tags: [n8n, automation, ai-summarization, google-drive, google-sheets, vlm-run, no-code]
keywords: [tự động hóa bản vẽ kiến trúc, n8n workflow google drive, xử lý bản vẽ PDF bằng AI, tự động hóa quản lý hồ sơ xây dựng, AI tóm tắt bản vẽ kỹ thuật]
---

# 🚀 **Tự Động Hóa Xử Lý Bản Vẽ Kiến Trúc Sang Google Sheets Với AI VLM Run**

### **Giải Phẫu Nỗi Đau Của Các Sếp Xây Dựng**
Hàng ngày, các sếp kiến trúc sư và kỹ sư phải mất **từ 30 phút đến 2 giờ** để:
- **Tìm kiếm và kiểm tra** hàng trăm bản vẽ trong Google Drive.
- **Nhập thủ công** thông tin như tên dự án, số phép tạm, chi tiết kỹ thuật vào Google Sheets.
- **Trao đổi và cập nhật** dữ liệu giữa các bộ phận (kỹ thuật, pháp lý, quản lý).
- **Rủi ro vi phạm quy định** khi thiếu thông tin chi tiết trong bản vẽ (ví dụ: sai kích thước, thiếu giấy phép).

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!** Dữ liệu từ bản vẽ được **AI VLM Run** tóm tắt thành cấu trúc JSON, sau đó tự động ghi vào Google Sheets để các sếp **tìm kiếm, theo dõi và báo cáo** một cách nhanh chóng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Dữ liệu chính xác 100%** – AI VLM Run tự động trích xuất thông tin chi tiết từ bản vẽ.
✅ **Cập nhật tự động** – Mỗi khi có bản vẽ mới được upload vào Google Drive, dữ liệu sẽ tự động ghi vào Sheets.
✅ **Giảm rủi ro pháp lý** – Tránh lỗi vi phạm do thiếu thông tin trong hồ sơ.
✅ **Tích hợp với Slack/Email** – Có thể gửi báo cáo tự động cho các bộ phận liên quan.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản VLM Run** (đăng ký tại [vlm.run](https://vlm.run/)) và **API Key**.
2. **Google Drive + Sheets OAuth2**:
   - Tạo **OAuth2 Client ID** trong [Google Cloud Console](https://console.cloud.google.com/).
   - Cấu hình **Google Drive Trigger** để theo dõi folder chứa bản vẽ.
3. **n8n Server** (Self-hosted hoặc Cloud) với **n8n-nodes-vlmrun** (cài đặt từ npm: `npm install @vlm-run/n8n-nodes-vlmrun`).
4. **Google Sheet** đã sẵn sàng với các cột:
   - **Project Name**, **Document Type**, **Permit ID**, **Drawing Title**, **Author**, **Revision History**, **Annotations**, **Job Name**.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7956](https://n8n.io/workflows/7956) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  {
    "nodes": [
      {
        "parameters": {},
        "name": "Google Drive Trigger",
        "type": "googleDriveTrigger",
        "typeOptions": {
          "folderId": "YOUR_DRIVE_FOLDER_ID" // Thay bằng ID folder theo dõi bản vẽ
        }
      },
      {
        "parameters": {
          "fileId": "={{$node["Google Drive Trigger"].json["fileId"]}}",
          "operation": "download"
        },
        "name": "Download file",
        "type": "googleDrive"
      },
      {
        "parameters": {
          "apiKey": "YOUR_VLM_RUN_API_KEY", // Thay bằng API Key của bạn
          "model": "construction.blueprint",
          "file": "={{$node["Download file"].json["file"]}}"
        },
        "name": "VLM Run",
        "type": "@vlm-run/n8n-nodes-vlmrun.vlmRun"
      },
      {
        "parameters": {
          "sheetName": "Blueprint_Extract", // Tên sheet trong Google Sheets
          "credentials": "googleSheets", // Credential đã cấu hình trước
          "operation": "append",
          "data": "={{$node["VLM Run"].json}}"
        },
        "name": "Append row in sheet",
        "type": "googleSheets"
      }
    ],
    "connections": {
      "Google Drive Trigger": ["Download file"],
      "Download file": ["VLM Run"],
      "VLM Run": ["Append row in sheet"]
    }
  }
  ```
- **Lưu ý**:
  - **Không** để trống `YOUR_DRIVE_FOLDER_ID` và `YOUR_VLM_RUN_API_KEY`.
  - **Test run** với một bản vẽ mẫu trước khi bật **Active**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
| **Node**               | **Cần Chỉnh Sửa Gì?**                                                                 | **Hướng Dẫn**                                                                 |
|------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Google Drive Trigger** | `folderId`                                                                           | - Đăng nhập Google Drive → Chọn folder chứa bản vẽ → Copy **ID folder** từ URL. |
| **VLM Run**            | `apiKey` và `model`                                                                  | - Đăng ký API Key tại [VLM Run](https://vlm.run/).                           |
| **Append row in sheet** | `sheetName` và `credentials`                                                         | - Tạo **Google Sheets** mới hoặc chọn sheet đã có.                          |
| **Google Drive**       | **File format** (PDF, JPG, PNG)                                                      | - Chỉ hỗ trợ **PDF, JPG, PNG** (không hỗ trợ DOCX).                          |

#### **3. Kích Hoạt ⚡️**
1. **Test run** với một bản vẽ mẫu:
   - Upload một bản vẽ vào folder đã cấu hình.
   - Chờ workflow tự động trích xuất và ghi vào Sheets.
2. **Bật Active workflow** khi đã kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sau khi dữ liệu được ghi vào Sheets, **gửi thông báo tự động** qua Slack/Telegram bằng node `n8n-nodes-slack.webhook` hoặc `n8n-nodes-telegram.bot`.
   - **Cách làm**:
     ```json
     {
       "parameters": {
         "message": "📄 Bản vẽ mới được xử lý: {{$node["Append row in sheet"].json["Project Name"]}}",
         "webhookUrl": "YOUR_SLACK_WEBHOOK_URL"
       },
       "name": "Notify Slack",
       "type": "slack"
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Sử dụng node `n8n-nodes-base.stickyNote` để ghi **lịch sử xử lý** (ngày upload, tên file, trạng thái thành công/thất bại).
   - **Cách làm**:
     ```json
     {
       "parameters": {
         "note": "📄 {{$node["Google Drive Trigger"].json["fileName"]}} đã được xử lý vào {{$node["VLM Run"].json["timestamp"]}}",
         "folderId": "YOUR_STICKY_NOTE_FOLDER"
       },
       "name": "Log Processing",
       "type": "stickyNote"
     }
     ```

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để **tạo báo cáo tổng hợp** hàng tuần/month về số lượng bản vẽ đã xử lý, dự án mới, hoặc vi phạm phát hiện.
   - **Cách làm**:
     - Tạo một **workflow mới** với node `n8n-nodes-base.aggregate` để tổng hợp dữ liệu từ Sheets.
     - Sau đó gửi báo cáo qua **Email** (`n8n-nodes-base.email`) hoặc **Google Docs** (`n8n-nodes-base.googleDocs`).

4. **Xử Lý Nhiều Loại File**:
   - Nếu có **PDF và hình ảnh**, có thể thêm **node `n8n-nodes-base.pdf`** để trích xuất text từ PDF trước khi gửi cho VLM Run.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại, đồng thời **tăng cường độ chính xác** và **giảm rủi ro pháp lý** trong quản lý hồ sơ xây dựng. **Chỉ cần 5 phút setup**, các sếp đã có một **hệ thống tự động hóa hoàn chỉnh** để theo dõi tất cả bản vẽ một cách hiệu quả.

**🚀 Hành động ngay!**
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 1-2 bản vẽ** trước khi áp dụng toàn bộ.

**Nếu có vấn đề**, liên hệ với tác giả **Shahrear** qua:
- [LinkedIn](https://www.linkedin.com/in/shahrear-amin/)
- Email: **shahrearbinamin33@gmail.com**

---
**💡 Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa công việc!** 🚀