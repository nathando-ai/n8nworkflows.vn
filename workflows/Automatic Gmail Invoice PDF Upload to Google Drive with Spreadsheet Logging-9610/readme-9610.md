---
title: "🚀 Tự Động Hóa Tải Invoice PDF Từ Gmail Vào Google Drive Và Theo Dõi Trên Bảng Excel - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn tự động tải tất cả các file PDF invoice từ Gmail vào Google Drive, đồng thời ghi log chi tiết vào Google Sheets để theo dõi. Giúp các sếp tiết kiệm 10+ giờ/tháng và tránh mất mát dữ liệu."
slug: "tieu-dong-hoa-tai-invoice-pdf-tu-gmail-vao-google-drive"
tags: [n8n, automation, no-code, google-drive, gmail, google-sheets]
keywords: [tự động hóa gmail, tải invoice pdf tự động, google drive automation, google sheets logging, n8n workflow gmail]
---

# 🚀 **Tự Động Hóa Tải Invoice PDF Từ Gmail Vào Google Drive Và Theo Dõi Trên Bảng Excel**

## **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
✅ **Quét email** để tìm các invoice mới từ các nhà cung cấp.
✅ **Tải xuống** file PDF từ email và lưu vào Google Drive.
✅ **Ghi log** vào Excel để theo dõi: ngày nhận, người gửi, tên file, link Drive...
✅ **Xóa email** sau khi xử lý để tránh trùng lặp.

**Kết quả?** Tốn **10-15 phút/ngày** (hoặc hơn) và dễ **quên hoặc sai sót** khi làm thủ công.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quá trình chỉ trong 5 phút cài đặt!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** (không cần quét email thủ công).
- **Không bao giờ quên** tải file vì hệ thống chạy **24/7**.
- **Dữ liệu chính xác** với log tự động trên Google Sheets.
- **Email tự động được đánh dấu là đã đọc** sau khi xử lý.
- **Tất cả file PDF được tổ chức** trong Google Drive (hoặc folder cụ thể).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản Gmail** (để trigger và xử lý email).
2. **Tài khoản Google Drive** (để upload file PDF).
3. **Tài khoản Google Sheets** (để ghi log).
4. **Mã Spreadsheet ID** (tìm trong URL của Google Sheets).
5. **Email mẫu** có từ khóa **"invoice"** trong tiêu đề và **đính kèm file PDF**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/9610) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9610) và paste vào **Create Workflow** → **Import from JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **6 node chính**, các sếp cần cấu hình như sau:

##### **📧 Node 1: Gmail Trigger (n8n-nodes-base.gmailTrigger)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Gmail đã kết nối (OAuth2).
  - **Label:** Đặt tên dễ nhận biết (ví dụ: "Invoice Trigger").
  - **Trigger:** Chọn **"Watch for new emails"** (theo dõi email mới).
  - **Filter:** Điền **`subject`** chứa từ khóa **"invoice"** (hoặc **"invoice"** + tên công ty nếu cần).
  - **Polling Interval:** Đặt **60 giây** (check mỗi phút).

##### **🔍 Node 2: Filter (n8n-nodes-base.filter)**
- **Cấu hình:**
  - **Expression:** `$.attachments && $.attachments.length > 0`
  - **Lý do:** Chỉ cho phép email **có đính kèm file PDF** vào workflow.

##### **📁 Node 3: Upload to Google Drive (n8n-nodes-base.googleDrive)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Google Drive đã kết nối.
  - **Operation:** Chọn **"Upload file"**.
  - **Folder ID:** Đặt mặc định là **"root"** (hoặc thay bằng folder cụ thể).
  - **File Name:** Sử dụng **`$.attachments[0].filename`** (tên file gốc).
  - **Mime Type:** Chọn **"application/pdf"** (nếu cần).

##### **📊 Node 4: Log to Google Sheets (n8n-nodes-base.googleSheets)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Google Sheets đã kết nối.
  - **Spreadsheet ID:** Dán từ URL của Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name:** Đặt tên sheet (ví dụ: **"Invoice Log"**).
  - **Operation:** Chọn **"Append"** (thêm mới).
  - **Headers:** Đảm bảo sheet có các cột sau:
    | Date | Sender | Subject | Filename | Drive_Link | File_ID | Email_ID |
    |------|-------|---------|----------|-----------|---------|----------|
  - **Data Mapping:**
    - `Date`: `$.date`
    - `Sender`: `$.sender.email`
    - `Subject`: `$.subject`
    - `Filename`: `$.attachments[0].filename`
    - `Drive_Link`: `$.json.googleDrive.fileLink`
    - `File_ID`: `$.json.googleDrive.fileId`
    - `Email_ID`: `$.id`

##### **✅ Node 5: Mark Email as Read (n8n-nodes-base.gmail)**
- **Cấu hình:**
  - **Credentials:** Sử dụng cùng tài khoản Gmail như **Node 1**.
  - **Operation:** Chọn **"Mark as read"**.
  - **Email ID:** Sử dụng `$.id` (ID của email từ Gmail Trigger).

##### **🔄 Node 6: If (n8n-nodes-base.if)**
- **Cấu hình:**
  - **Condition:** `$.json.googleDrive.fileId` (kiểm tra nếu upload thành công).
  - **True Branch:** Chỉ định **Node 5 (Mark as Read)**.
  - **False Branch:** Bỏ trống (hoặc thêm node báo lỗi).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Gửi email mẫu (có từ khóa **"invoice"** và đính kèm PDF).
   - Kiểm tra:
     - File PDF đã upload vào Google Drive.
     - Log đã được thêm vào Google Sheets.
     - Email đã được đánh dấu là đã đọc.
2. **Bật Active:**
   - Chuyển trạng thái workflow từ **"Draft"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tự động gửi thông báo Slack/Telegram** khi có invoice mới:
   - Thêm **Node Slack/Telegram** sau **Node 4 (Google Sheets)** để báo cáo ngay khi có file mới.
2. **Lưu log vào Google Drive** thay vì Sheets:
   - Thay vì ghi vào bảng Excel, có thể lưu file log là **Excel/CSV** vào Google Drive.
3. **Xóa email sau khi xử lý** (nếu không muốn giữ lại):
   - Thêm **Node Gmail** với operation **"Delete"** sau khi đánh dấu là đã đọc.
4. **Tự động tạo folder mới** cho mỗi tháng:
   - Sử dụng **Node Google Drive (Create Folder)** với tên folder là `Invoice_YYYY-MM`.
5. **Kết hợp với Zapier/Integromat** (nếu cần):
   - Nếu muốn thêm tính năng khác (ví dụ: gửi email tự động cho bộ phận kế toán), có thể kết nối với các dịch vụ khác.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, **giảm thiểu sai sót** và **tự động hóa toàn bộ chu trình invoice**. **Chỉ cần 5 phút cài đặt**, hệ thống sẽ chạy **24/7** mà không cần can thiệp.

**Bắt đầu ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (để chạy ổn định).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với email mẫu** và **bật Active**.

**🎁 Mã giảm giá VPS cho n8n:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**Hãy tự động hóa ngay hôm nay!** 🚀