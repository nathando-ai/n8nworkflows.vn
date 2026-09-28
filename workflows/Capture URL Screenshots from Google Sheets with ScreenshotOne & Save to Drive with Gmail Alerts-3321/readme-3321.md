---
title: "📸 [Tự Động Chụp Ảnh Web từ Google Sheets & Lưu Trên Google Drive + Gửi Email Cảnh Báo] - N8N Workflow"
description: "Giải pháp tự động hóa hoàn toàn không code để chụp ảnh tất cả URL trong Google Sheets, lưu kết quả vào Google Drive và gửi email cảnh báo cho team. Tiết kiệm thời gian lên đến 80% cho công việc chụp ảnh web hàng loạt."
slug: "tu-dong-chup-anh-web-googlesheets-google-drive-email"
tags: [n8n, automation, google-sheets, google-drive, screenshot, email-alert, no-code]
keywords: [n8n workflow chụp ảnh web, tự động hóa chụp screenshot, google sheets tự động hóa, lưu ảnh vào google drive, cảnh báo email tự động]
---

# 🚀 **Tự Động Chụp Ảnh Web từ Google Sheets & Lưu Trên Google Drive + Gửi Email Cảnh Báo**

### **Giải pháp cho các sếp bị "chán ngấy" việc chụp ảnh web thủ công**
Hãy tưởng tượng một tình huống: Bạn phải chụp ảnh cho **50+ URL** để so sánh UI/UX, theo dõi thay đổi trang web, hoặc chuẩn bị tài liệu marketing. Thời gian mất đi? **Tối thiểu 2-3 tiếng** nếu làm thủ công! Với workflow này, **n8n sẽ tự động hóa toàn bộ quy trình** chỉ trong vài giây sau khi bạn thêm URL mới vào Google Sheets.

👉 **Kết quả:**
- **Tự động chụp ảnh** tất cả URL trong Google Sheets.
- **Lưu ảnh vào Google Drive** theo folder tự động.
- **Gửi email cảnh báo** với link folder chứa ảnh mới.
- **Không cần code**, chỉ cần cấu hình 5 node đơn giản.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không còn phải chụp ảnh một URL một, mà chỉ cần thêm URL vào Google Sheets là xong.
✅ **Chính xác 100%:** Không lo quên chụp hoặc chụp sai URL.
✅ **Lưu trữ tự động:** Ảnh được lưu vào Google Drive theo folder riêng, dễ dàng theo dõi và chia sẻ.
✅ **Cảnh báo tức thời:** Nhận email ngay khi có ảnh mới được chụp và lưu.
✅ **Hoạt động 24/7:** Workflow chạy tự động mỗi khi có thay đổi trong Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Google** (để sử dụng Google Sheets, Google Drive và Gmail).
- **Tài khoản ScreenshotOne** ([đăng ký miễn phí](https://dash.screenshotone.com/)) để chụp ảnh web.
- **API Key của ScreenshotOne** (cần tạo ở [Dashboard](https://dash.screenshotone.com/access)).
- **Folder trong Google Drive** để lưu ảnh chụp (cần chia sẻ với n8n).
- **Google Sheet** có cột tên là **"Url."** (không dấu, không khoảng trắng) chứa danh sách URL cần chụp.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/3321) (nút "Download").
2. Trên **n8n Editor**, nhấn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **"Import"** → Chọn **"Paste JSON"** và dán nội dung từ [đây](https://n8n.io/workflows/3321) (nút "Export").
3. Nhấn **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này hoạt động theo **Google Drive Trigger** (khi có thay đổi trong file Google Sheets), nên các bước sau **quan trọng nhất**:

#### **🔹 Node 1: `spreadsheets file with urls created` (Google Drive Trigger)**
- **Chọn file Google Sheets** bạn muốn theo dõi (file này phải được lưu trong Google Drive).
- **Chọn "File updated"** (để workflow chạy khi file được chỉnh sửa).
- **Chọn "Google Sheets"** là loại file cần theo dõi.
- **Chọn cột "Url."** (n8n sẽ lấy URL từ cột này để chụp ảnh).

#### **🔹 Node 2: `Get Urls` (Google Sheets)**
- **Chọn Google Sheet** tương ứng (nếu khác với file trong Trigger).
- **Chọn sheet** và **cột "Url."** để lấy dữ liệu.
- **Lưu ý:** Nếu cột URL của bạn có tên khác, **cần chỉnh lại** trong node này.

#### **🔹 Node 3: `Get screenshots` (HTTP Request)**
- **Thay thế `ACCESS_KEY`** trong URL bằng **API Key của ScreenshotOne** (tạo ở [Dashboard](https://dash.screenshotone.com/access)).
  - URL mẫu:
    ```http
    https://api.screenshotone.com/v1/screenshot?url={$json["Url"]}&access_key=YOUR_ACCESS_KEY_HERE
    ```
- **Thêm tham số tùy chọn** (nếu cần):
  - `width`: Chiều rộng ảnh (ví dụ: `1920`).
  - `height`: Chiều cao ảnh (ví dụ: `1080`).
  - `delay`: Thời gian chờ trước khi chụp (ví dụ: `3000` ms).

#### **🔹 Node 4: `Upload images to the same folder` (Google Drive)**
- **Chọn folder** trong Google Drive để lưu ảnh.
- **Tên file:** Sử dụng **URL** hoặc **ID của URL** (ví dụ: `Screenshot_${json["Url"]}.png`).
- **Mime type:** Chọn `image/png` (hoặc `image/jpeg` nếu chụp thành JPEG).

#### **🔹 Node 5: `Send email with folder link` (Gmail)**
- **Chọn tài khoản Gmail** để gửi email.
- **Điền nội dung email:**
  - **Tiêu đề:** `"Ảnh mới được chụp từ Google Sheets - ${new Date().toLocaleDateString()}"`.
  - **Nội dung:**
    ```html
    <p>Xin chào team,</p>
    <p>Đã tự động chụp ảnh cho <strong>${json["Url"].length}</strong> URL mới từ Google Sheets.</p>
    <p>Link folder chứa ảnh mới: <a href="$json["folderLink"]">${json["folderLink"]}</a></p>
    <p>Trân trọng,</p>
    <p>n8n Automation</p>
    ```
- **Thêm file đính kèm (optional):** Nếu muốn gửi ảnh trực tiếp, thêm node `gmail` với phần **Attachments**.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với 1-2 URL mẫu để kiểm tra:
   - Nhấn **"Execute"** trên node `Get Urls` → Kiểm tra kết quả chụp ảnh.
   - Kiểm tra **Google Drive** và **Gmail** để xác nhận lưu và gửi email.
2. **Bật Active** workflow khi đã kiểm tra thành công.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢNH BÁO & MẶT BẬC]
- **Số lượng URL:** ScreenshotOne có giới hạn miễn phí (khoảng **500 screenshot/tháng**). Nếu vượt quá, cần nâng cấp tài khoản.
- **Tốc độ chụp:** Nếu có nhiều URL, **chờ đợi** giữa các request để tránh bị block API.
- **Lưu log:** Thêm node **StickyNote** để ghi lại lỗi hoặc thông tin debug.
- **Kết hợp Slack/Telegram:** Thay vì email, có thể gửi thông báo qua **Slack Webhook** hoặc **Telegram Bot**.
- **Tự động xóa URL đã chụp:** Thêm node **Google Sheets** để xóa hàng sau khi chụp thành công.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc chụp ảnh web thủ công, đồng thời **tăng cường độ chính xác** và **tự động hóa hoàn toàn**. **Chỉ cần thêm URL vào Google Sheets**, n8n sẽ tự động:
✔ Chụp ảnh.
✔ Lưu vào Google Drive.
✔ Gửi email cảnh báo.

👉 **Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Bật Active** và **nhận email đầu tiên** khi có ảnh mới!

**N8N không chỉ tự động hóa, mà còn làm cho công việc trở nên đơn giản hơn.** 🚀