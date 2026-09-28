---
title: "🎬 **Tự Động Hoàn Thành Thư Viện Clip Phỏng Vấn AI với WayinVideo, Google Drive & Sheets - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn cho nhà sản xuất podcast, content team và biên tập video để tự động trích xuất những khoảnh khắc hay nhất từ các bài phỏng vấn qua AI. Tiết kiệm 80% thời gian biên tập thủ công!"
slug: "tieu-dong-hoan-thanh-thu-vien-clip-phong-van-ai"
tags: [n8n, automation, content-creation, multimodal-ai, google-drive, google-sheets, wayinvideo, podcast]
keywords: [tự động hóa clip phỏng vấn, wayinvideo n8n, lưu trữ clip video tự động, google sheets tự động hóa, tiết kiệm thời gian biên tập video]
---

# 🚀 **Tự Động Hoàn Thành Thư Viện Clip Phỏng Vấn AI - Không Cần Code!**

### **Giải pháp cho ai?**
Các **sếp podcast, biên tập video, content team** đang mệt mỏi với việc **tìm kiếm thủ công** những khoảnh khắc hay nhất trong các bài phỏng vấn dài? Hay phải **cắt video, lưu trữ và quản lý** hàng trăm clip một cách thủ công? **Workflow này sẽ tự động hóa toàn bộ quy trình** chỉ với một URL phỏng vấn và một câu hỏi mô tả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian biên tập**: Không cần tìm kiếm thủ công clip hay cắt video.
✅ **Tự động lưu trữ trên Google Drive**: Tất cả clip được tự động upload vào thư mục riêng.
✅ **Danh sách clip quản lý trên Google Sheets**: Theo dõi tất cả clip với metadata chi tiết (tên khách, chủ đề, thời gian, link).
✅ **Báo cáo tự động qua email**: Nhận email tổng kết với link trực tiếp đến clip và thư mục Drive.
✅ **Hoạt động liên tục 24/7**: Không cần can thiệp thủ công, chỉ cần submit form.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản WayinVideo** (đăng ký tại [wayin.video](https://wayin.video/)) và **API Key**.
✔ **Tài khoản Google Drive** với **Folder ID** để lưu clip.
✔ **Tài khoản Google Sheets** và **Sheet ID** của bảng **"Interview Clip Library"**.
✔ **Tài khoản Gmail** để gửi email báo cáo tự động.
✔ **URL phỏng vấn** (có thể là YouTube, Vimeo, hoặc file trực tiếp).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/14713](https://n8n.io/workflows/14713) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **🔹 Node 2 & 4: WayinVideo API**
- **Thao tác**: Vào **Authorization Header** của hai node này và thay thế:
  ```
  YOUR_WAYIN_API_KEY
  ```
  bằng **API Key** của WayinVideo (tìm trong **Settings** của tài khoản WayinVideo).
- **Lưu ý**:
  - Đảm bảo **URL phỏng vấn** được submit là **đủ dài** (tránh bị cắt).
  - **Query mô tả** phải **rất cụ thể** (ví dụ: *"cách xây dựng sự nghiệp thành công"* thay vì *"tips"*).

#### **🔹 Node 9: Google Drive**
- **Thao tác**: Vào **Folder ID** và thay thế:
  ```
  YOUR_GDRIVE_FOLDER_ID
  ```
  bằng **ID thư mục** của bạn (tìm trong liên kết Google Drive: `https://drive.google.com/drive/folders/[ID]`).
- **Lưu ý**:
  - Chọn **Folder ID** là thư mục **mới tạo** để tránh trùng lặp.
  - Cấp quyền **n8n** truy cập vào thư mục này.

#### **🔹 Node 10: Google Sheets**
- **Thao tác**:
  1. Tạo một **Google Sheet mới** và đặt tên **exactly** là: **"Interview Clip Library"**.
  2. Thay thế:
     ```
     YOUR_GOOGLE_SHEET_ID
     ```
     bằng **Sheet ID** (tìm trong liên kết: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  3. Chọn **tab "Interview Clip Library"** trong node.
- **Lưu ý**:
  - **Cấu trúc cột** sẽ tự động tạo ra (n8n sẽ thêm cột mới nếu cần).
  - Đảm bảo **n8n có quyền chỉnh sửa** bảng này.

#### **🔹 Node 11: Gmail**
- **Thao tác**: Kết nối **tài khoản Gmail** của bạn với n8n.
- **Lưu ý**:
  - **Không sử dụng tài khoản Gmail cá nhân** (dùng tài khoản công việc để tránh bị block).
  - **Email template** sẽ tự động tạo ra với nội dung:
    ```
    "Xin chào [Tên khách], clip phỏng vấn đã được lưu trữ tại:
    - Link Drive: [LINK]
    - Bảng Google Sheets: [LINK]
    ```

#### **🔹 Node 7: Code (Split Each Clip)**
- **Lưu ý**: Node này **không cần chỉnh sửa**, nhưng nếu muốn **tùy chỉnh cách split clip**, các sếp có thể mở **Code Editor** và thay đổi logic.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một **URL phỏng vấn mẫu** và **query mô tả** (ví dụ: *"một khoảnh khắc quyết định trong sự nghiệp"*).
2. **Bật Active** workflow sau khi kiểm tra thành công.
3. **Mở Form URL** (tìm trong node **Form Trigger**) để submit thử.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Kết hợp với Slack/Telegram**
- Thêm **node Slack/Telegram** sau **Gmail** để thông báo kết quả ngay khi clip được xử lý.
- **Cách làm**:
  ```json
  {
    "nodeType": "n8n-nodes-base.slack",
    "name": "Slack Notification",
    "operation": "sendMessage",
    "webhookUrl": "YOUR_SLACK_WEBHOOK_URL",
    "message": "🎬 Clip đã được xử lý! Kiểm tra tại: {{ $json["driveLink"] }}"
  }
  ```

### **🔹 Lưu log hoạt động**
- Thêm **node StickyNote** sau **Gmail** để ghi lại **log error** (nếu có):
  ```json
  {
    "nodeType": "n8n-nodes-base.stickyNote",
    "name": "Log Error",
    "content": "Workflow failed for URL: {{ $json["url"] }}. Error: {{ $json["error"] }}"
  }
  ```

### **🔹 Gửi báo cáo định kỳ**
- Sử dụng **node Schedule** (n8n Pro) để gửi **báo cáo tổng hợp** hàng tuần về **tất cả clip mới** được lưu trữ.

### **🔹 Tối ưu query AI**
- **Tránh query quá rộng** (ví dụ: *"tips"* → **rỗng kết quả**).
- **Sử dụng từ khóa cụ thể**:
  - ✅ *"cách xây dựng sự nghiệp thành công trong 5 năm đầu"*
  - ❌ *"tips xây dựng sự nghiệp"*

---

## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi việc **tìm kiếm, cắt và lưu trữ clip phỏng vấn thủ công**. **Chỉ cần submit URL và mô tả**, AI WayinVideo sẽ tự động **trích xuất, download, lưu trữ và báo cáo** tất cả clip hay nhất.

👉 **Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với một bài phỏng vấn mẫu**.
3. **Bật Active** và **tự động hóa toàn bộ quy trình**!

**Nếu có vấn đề**, các sếp có thể comment bên dưới hoặc liên hệ **isaWOW** (tác giả) qua [n8n Community](https://community.n8n.io/). **Chúc các sếp thành công!** 🚀