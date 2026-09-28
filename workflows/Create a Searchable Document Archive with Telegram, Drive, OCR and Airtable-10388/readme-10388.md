---
title: "📄 Tự Động Hoàn Thành Thư Viện Tài Liệu Tìm Kiếm Được với Telegram, Google Drive, OCR & Airtable"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp lưu trữ, quét chữ (OCR) và tìm kiếm tài liệu từ Telegram vào Google Drive, đồng thời lưu metadata vào Airtable. Giúp tiết kiệm thời gian tìm kiếm lên đến 90% và duy trì hệ thống 24/7."
slug: "tieu-dong-hoan-thanh-thu-vien-tai-lieu-tim-kiem-voi-telegram-google-drive-ocr-airtable"
tags: [n8n, automation, no-code, document-extraction, multimodal-ai, google-drive, airtable, telegram-bot, ocr, google-vision]
keywords: [n8n workflow tự động hóa tài liệu, lưu trữ tài liệu Telegram, OCR tự động hóa, tìm kiếm tài liệu Airtable, tự động hóa Google Drive, giải pháp lưu trữ thông minh]
---

# 🚀 **Tự Động Hoàn Thành Thư Viện Tài Liệu Tìm Kiếm Được với Telegram, Google Drive, OCR & Airtable**

### **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải đối mặt với những vấn đề sau khi quản lý tài liệu:
- **Tìm kiếm mất thời gian**: Đôi khi mất hàng giờ để tìm kiếm một tài liệu trong hàng trăm file trên Telegram hoặc Google Drive.
- **Không tìm kiếm được nội dung**: Không thể tìm kiếm nội dung trong hình ảnh hoặc PDF (OCR).
- **Lưu trữ rối loạn**: Tài liệu phân tán trên nhiều nền tảng (Telegram, Drive, email...).
- **Không có hệ thống tìm kiếm thông minh**: Không thể tra cứu nhanh chóng thông qua từ khóa.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động lưu trữ** tất cả tài liệu từ Telegram vào Google Drive.
✅ **Quét chữ (OCR)** cho hình ảnh và PDF để tìm kiếm nội dung.
✅ **Lưu metadata + nội dung** vào Airtable để tìm kiếm nhanh.
✅ **Tìm kiếm thông minh** bằng cách nhập `/search <từ khóa>` trên Telegram.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** khi tìm kiếm tài liệu.
- **Tìm kiếm nội dung trong hình ảnh/PDF** nhờ OCR.
- **Duy trì hệ thống tự động** mà không cần code.
- **Tìm kiếm nhanh chóng** bằng cách nhập `/search <từ khóa>` trên Telegram.
- **Lưu trữ trung tâm** tất cả tài liệu trên Google Drive và Airtable.
- **Gửi thông báo tự động** khi lưu trữ thành công hoặc lỗi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Một bot Telegram đã tạo và có `API Token`.
   - Một chat group hoặc cá nhân để nhận tài liệu.
2. **Tài khoản Google Drive**:
   - `OAuth 2.0 API Key` để upload file.
3. **Tài khoản Airtable**:
   - `API Token` và một bảng (`base`) để lưu metadata.
4. **Google Vision API** (để OCR):
   - `API Key` từ [Google Cloud Console](https://console.cloud.google.com/).
5. **N8n Self-hosted** (không dùng n8n.cloud để tránh giới hạn):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/10388](https://n8n.io/workflows/10388).
2. Nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **🔹 Node Telegram Trigger**
- **Cấu hình**:
  - Chọn `telegramApi` (credentials đã tạo trước).
  - Chỉnh `chatId` để workflow chỉ hoạt động trong group/cá nhân cụ thể (nếu cần).

##### **🔹 Node Download File from Telegram**
- **Cấu hình**:
  - Chọn `telegramApi` (credentials).
  - Đảm bảo `fileId` được truyền từ `Telegram Trigger`.

##### **🔹 Node Upload to Google Drive**
- **Cấu hình**:
  - Chọn `googleDriveOAuth2Api` (credentials).
  - Chọn `folderId` là `root` (để lưu vào thư mục gốc).
  - Đảm bảo `fileName` và `fileBinary` được truyền từ node trước.

##### **🔹 Node Google Vision OCR**
- **Cấu hình**:
  - Chọn `httpRequest`.
  - Điền `API Key` từ Google Cloud Console.
  - Tham số `url` phải là:
    ```
    https://vision.googleapis.com/v1/images:annotate?key={API_KEY}
    ```
  - Body JSON:
    ```json
    {
      "requests": [
        {
          "image": {
            "content": "{{$json.fileBinary}}"
          },
          "features": [
            {
              "type": "TEXT_DETECTION"
            }
          ]
        }
      ]
    }
    ```

##### **🔹 Node Index in Airtable**
- **Cấu hình**:
  - Chọn `airtableTokenApi` (credentials).
  - Chọn `baseId` và `tableName` (bảng lưu metadata).
  - Đảm bảo truyền các trường sau:
    - `name` (tên file)
    - `fileId` (ID Telegram)
    - `driveFileId` (ID Google Drive)
    - `extracted_text` (nội dung OCR, nếu có)
    - `mimeType` (loại file)

##### **🔹 Node Send Success/Error Message**
- **Cấu hình**:
  - Chọn `telegramApi` (credentials).
  - Đảm bảo `chatId` là group/cá nhân cần thông báo.
  - Thông điệp mẫu:
    - **Thành công**:
      ```
      📄 File "{{$json.name}}" đã lưu thành công!
      🔗 Link: https://drive.google.com/file/d/{{$json.driveFileId}}/view
      ```
    - **Lỗi**:
      ```
      ❌ Lỗi khi lưu file "{{$json.name}}": {{$json.error}}
      ```

##### **🔹 Node Search in Airtable**
- **Cấu hình**:
  - Chọn `airtableTokenApi` (credentials).
  - Chọn `baseId` và `tableName` (bảng lưu metadata).
  - Tham số `operation` là `search`.
  - Đảm bảo truyền `query` từ node `Extract Search Query`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một file mẫu:
   - Gửi một file PDF/hình ảnh lên Telegram bot.
   - Kiểm tra log trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng node `setDateTime` + `set` để gửi báo cáo số lượng file mới được lưu mỗi ngày qua Telegram.
2. **Lưu log chi tiết**:
   - Sử dụng node `stickyNote` để lưu log lỗi hoặc thành công vào một sheet Google Sheets.
3. **Kết hợp với Slack**:
   - Thay vì Telegram, có thể sử dụng node `slack` để thông báo kết quả.
4. **Tìm kiếm nâng cao**:
   - Sử dụng node `googleSearch` để tra cứu thêm thông tin từ web khi tìm kiếm trong Airtable.
5. **Duy trì danh sách file cũ**:
   - Sử dụng node `airtable` với `operation: list` để lấy danh sách file cũ và gửi cho người dùng khi họ yêu cầu.
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình lưu trữ, quét chữ (OCR) và tìm kiếm tài liệu** từ Telegram, đồng thời lưu metadata vào Airtable. **Không cần code, không cần quản lý thủ công** – chỉ cần import và chạy 24/7.

**🚀 Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!**
Nếu có vấn đề, các sếp có thể tham khảo [hướng dẫn chi tiết của The AI Squad](https://n8n.io/workflows/10388) hoặc liên hệ cộng đồng n8n trên [Discord](https://discord.gg/n8n).

---
**💡 Lưu ý cuối cùng:**
- Để workflow hoạt động ổn định, **không nên dùng n8n.cloud** (có giới hạn request).
- **Self-hosted trên VPS** là lựa chọn tối ưu nhất. 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**.