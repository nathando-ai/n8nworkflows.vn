---
title: "📤 **Tự Động Lưu & Sắp Xếp Tệp Tin LINE Vào Google Drive Với Báo Cáo Chi Tiết (Không Cần Code!)**"
description: "Workflow này tự động nhận file từ LINE (ảnh, video, audio...), lưu vào Google Drive theo ngày/thuộc loại, đồng thời ghi log chi tiết vào Google Sheets. Giúp các sếp tiết kiệm thời gian quản lý file và tăng cường tính chuyên nghiệp cho team."
slug: "tieu-dong-luu-sap-xep-file-line-google-drive"
tags: [n8n, automation, no-code, google-drive, google-sheets, line-bot, file-management]
keywords: [tự động hóa lưu file LINE, lưu file vào Google Drive tự động, quản lý file theo ngày/thuộc loại, n8n workflow LINE, tự động hóa chatbot LINE]
---

# 🚀 **Tự Động Lưu & Sắp Xếp Tệp Tin LINE Vào Google Drive Với Báo Cáo Chi Tiết**

### **Giải pháp cho vấn đề:**
Các sếp và team thường phải mất thời gian thủ công:
- **Nhận file từ LINE** (ảnh, video, audio, tài liệu...) và **lưu vào Google Drive** theo ngày/thuộc loại.
- **Quản lý rối loạn** vì file không được sắp xếp logic (mất thời gian tìm kiếm).
- **Không có báo cáo** về lịch sử upload, dẫn đến khó theo dõi và chia sẻ.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Nhận file từ LINE** → **Lưu vào Google Drive** theo cấu trúc ngày/thuộc loại.
✅ **Ghi log chi tiết** vào Google Sheets (tên file, ngày upload, URL, loại file...).
✅ **Trả lời tự động** cho người dùng LINE (xác nhận thành công/loại file không hợp lệ).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công chuyển file từ LINE sang Google Drive.
- **Sắp xếp logic**: File được lưu theo **ngày** và **loại file** (ảnh, video, audio...), dễ dàng tìm kiếm.
- **Báo cáo chi tiết**: Google Sheets tự động ghi log tất cả file (tên, ngày, URL, trạng thái).
- **Trả lời tự động**: Người dùng LINE nhận phản hồi ngay lập tức (thành công/loại file không hợp lệ).
- **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần can thiệp.
- **Tăng cường chuyên nghiệp**: Team có hệ thống quản lý file tự động, giảm rủi ro mất file.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản LINE Developer**:
   - [Đăng ký tại LINE Developers](https://developers.line.biz/) để lấy **Channel Secret** và **Channel Access Token**.
   - Cấu hình **Webhook URL** của n8n (ví dụ: `https://[your-domain]/line-webhook`).

2. **Google Drive & Google Sheets**:
   - **Google Drive OAuth 2.0 API**: Cấu hình trong n8n để lưu file.
   - **Google Sheets OAuth 2.0 API**: Cấu hình để ghi log file.
   - **Bảng Google Sheets** với cấu trúc như sau (cột: `File Name`, `Upload Date`, `URL`, `File Type`, `Status`).
   - **Thư mục cha (Parent Folder)** trong Google Drive để lưu file (cấu hình trong Google Sheets).

3. **Cấu hình trong Google Sheets**:
   - Tạo một **bảng cấu hình** với các thông tin sau (để workflow lấy tham số):
     | Key               | Value                          |
     |-------------------|--------------------------------|
     | `parent_folder_id`| ID của thư mục cha trong Google Drive |
     | `allowed_file_types`| `["image/jpeg", "image/png", "video/mp4", "audio/mpeg"]` (danh sách MIME type cho phép) |
     | `store_by_date`   | `true`/`false` (bật/tắt lưu theo ngày) |
     | `store_by_type`   | `true`/`false` (bật/tắt lưu theo loại file) |
     | `reply_enabled`   | `true`/`false` (bật/tắt trả lời LINE) |

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3191) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Credentials**
- **LINE Webhook Listener**:
  - Đảm bảo **URL Webhook** trong n8n trùng với URL đã đăng ký trên **LINE Developers**.
  - Sử dụng **HTTP Header Auth** với `Authorization: Bearer [Channel Access Token]`.

- **Google Drive OAuth 2.0 API**:
  - Cấu hình trong **Credentials** của n8n với quyền:
    - `Google Drive` → `Drive` (đọc/thêm/xóa file).
    - `Google Sheets` → `Sheets API` (đọc/thêm dữ liệu).

- **Google Sheets OAuth 2.0 API**:
  - Chọn **Google Sheet** chứa cấu hình và **Google Sheet** để ghi log.

##### **B. Cấu hình Node "Get Config"**
- Trong node này, chọn **Google Sheet** chứa cấu hình (cột `Key` và `Value`).
- Workflow sẽ lấy các tham số như `parent_folder_id`, `allowed_file_types`, `store_by_date`, `store_by_type`, `reply_enabled`.

##### **C. Cấu hình Node "Determine Folder Info" (Code)**
- Node này sử dụng **JavaScript** để tính toán tên thư mục:
  - Nếu `store_by_date` = `true`, tên thư mục sẽ là `YYYY-MM-DD`.
  - Nếu `store_by_type` = `true`, tên thư mục sẽ là tên loại file (ví dụ: `images`, `videos`).
- **Không cần chỉnh sửa** nếu cấu hình trong Google Sheets đã đúng.

##### **D. Cấu hình Node "Validate File Type" (Code)**
- Node này kiểm tra **MIME type** của file với danh sách cho phép (`allowed_file_types`).
- Nếu file không hợp lệ, workflow sẽ **ngừng và trả lời lỗi** cho LINE.

##### **E. Cấu hình Node "Log File Details to Google Sheet"**
- Chọn **Google Sheet** để ghi log (cột: `File Name`, `Upload Date`, `URL`, `File Type`, `Status`).
- **Operation**: Chọn `append` để thêm dữ liệu mới vào cuối bảng.

##### **F. Cấu hình Node "Send LINE Reply Message"**
- Nếu `reply_enabled` = `true`, node này sẽ gửi **trả lời tự động** cho người dùng LINE:
  - Thành công: `File uploaded successfully! URL: [link]`.
  - Thất bại: `File type not allowed. Allowed types: [danh sách]`.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một file từ LINE đến Webhook của n8n.
  - Kiểm tra **Google Drive** và **Google Sheets** để xác nhận file đã được lưu và ghi log.
- **Bật Active**:
  - Nhấn **Active** trên workflow để bắt đầu tự động hóa.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để báo cáo lỗi hoặc thành công lên nhóm chat.

2. **Lưu log vào Database**:
   - Thay vì Google Sheets, các sếp có thể sử dụng **MySQL/PostgreSQL** để lưu log chi tiết hơn.

3. **Báo cáo định kỳ**:
   - Sử dụng **n8n + Google Apps Script** để tạo báo cáo tổng hợp hàng tuần/month.

4. **Tự động xóa file cũ**:
   - Thêm logic trong **Code Node** để xóa file trong Google Drive sau một thời gian nhất định.

5. **Cấu hình đa channel**:
   - Nếu cần, các sếp có thể mở rộng workflow để hỗ trợ **Facebook Messenger** hoặc **WhatsApp** cùng một lúc.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp và team cần tự động hóa quá trình quản lý file từ LINE. Bằng cách **lưu file vào Google Drive theo ngày/thuộc loại** và **ghi log chi tiết**, các sếp sẽ tiết kiệm thời gian, tăng cường tính chuyên nghiệp và giảm thiểu rủi ro mất file.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa!

Nếu có bất kỳ vấn đề nào, hãy liên hệ với **Jaruphat J.** (tác giả của workflow) qua [LinkedIn](https://www.linkedin.com/in/jaruphat/) để hỗ trợ thêm. 🚀

---
**#Automation #NoCode #GoogleDrive #LINEBot #TựĐộngHóa**