---
title: "📁 Tự Động Sắp Xếp File Đính Kèm Gmail Vào Google Drive Theo Người Gửi - Không Cần Code"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp tự động lấy tất cả file đính kèm từ Gmail và sắp xếp vào các thư mục Google Drive riêng biệt theo địa chỉ email của người gửi, tránh trùng lặp và tiết kiệm thời gian lên đến 10 giờ/tuần."
slug: "tieu-dong-sap-xep-file-dinh-kem-gmail-google-drive"
tags: [n8n, tự động hóa email, google drive, file management, gmail automation]
keywords: [n8n workflow gmail google drive, tự động sắp xếp file đính kèm, sắp xếp thư mục theo email, tự động hóa văn phòng, tiết kiệm thời gian quản lý file]
---

# 🚀 **Tự Động Sắp Xếp File Đính Kèm Gmail Vào Google Drive Theo Người Gửi**

## **💡 Giải Pháp Cho Nỗi Đau "Tìm File Đính Kèm Trong Gmail Làm Sao?"**
Các sếp đã từng gặp tình huống này chưa?
- **Tìm kiếm file đính kèm trong hàng trăm email** mất nhiều thời gian hơn là tạo file mới.
- **Không biết sắp xếp file vào đâu** vì không có hệ thống thư mục logic.
- **Lo ngại trùng lặp file** khi copy paste từ Gmail vào Google Drive thủ công.
- **Không thể tự động hóa** vì không biết code hoặc không có thời gian học.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tất cả email mới** từ Gmail (hoặc chỉ email có đính kèm).
✅ **Tách file đính kèm** ra khỏi email.
✅ **Tạo thư mục Google Drive riêng** cho mỗi người gửi (ví dụ: `nguyenvananh@gmail.com`).
✅ **Upload file vào thư mục đúng** mà **không trùng lặp**.
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** không phải tìm kiếm và sắp xếp file thủ công.
- **Tránh trùng lặp file** nhờ kiểm tra thư mục trước khi tạo.
- **Tự động hóa hoàn toàn** – không cần nhớ hoặc làm lại.
- **Cá nhân hóa thư mục** theo người gửi, giúp quản lý dễ dàng hơn.
- **Hoạt động liên tục** ngay cả khi bạn ngủ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
2. **Tài khoản Google Drive** (đã cấp quyền OAuth2 API cho n8n).
3. **API Key** của Google Drive (nếu sử dụng API trực tiếp).
4. **Thư mục cha trong Google Drive** (workflow sẽ tạo các thư mục con bên trong).

---
:::info[CHUẨN BỊ]
- **N8n Editor** (cài đặt từ [n8n.io](https://n8n.io/) hoặc self-hosted).
- **Credentials OAuth2** cho Gmail và Google Drive (cấu hình trong **Credentials** của n8n).
- **Dữ liệu mẫu** (nếu test, có thể lấy từ email cá nhân).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6277).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
   *Hoặc* copy toàn bộ JSON và paste vào **Import Workflow** trong menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **16 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node "Gmail Trigger" (GmailTrigger)**
- **Chọn credentials**: `gmailOAuth2` (đã cấu hình trước).
- **Lọc email**:
  - **Label**: Chọn `INBOX` hoặc tạo một label riêng (ví dụ: `Auto-Organize`).
  - **Has attachment**: **Bật** để chỉ lấy email có file đính kèm.

##### **🔹 Node "Get emails" (Gmail)**
- **Credentials**: `gmailOAuth2`.
- **Operation**: `getAll` (lấy tất cả email mới).
- **Lọc email**:
  - **After**: Chọn ngày bắt đầu (ví dụ: 7 ngày trước).
  - **Label**: `INBOX` hoặc label đã chọn ở trên.

##### **🔹 Node "Contain attachments?" (If)**
- **Kiểm tra**: `$json["hasAttachments"]` == `true`.
- **Nếu true**, chuyển sang node tiếp theo để xử lý đính kèm.

##### **🔹 Node "Create folder" (Google Drive)**
- **Credentials**: `googleDriveOAuth2Api`.
- **Tên thư mục**: `$json["sender"]["email"]` (ví dụ: `nguyenvananh@gmail.com`).
- **Thư mục cha**: Chọn thư mục cha đã định trước (ví dụ: `Auto-Organized Files`).

##### **🔹 Node "Exist?" (If)**
- **Kiểm tra**: Thư mục đã tồn tại chưa?
  - **Nếu không tồn tại**, node `Create folder` sẽ tạo mới.
  - **Nếu tồn tại**, node `Folder ID` sẽ lấy ID của thư mục đó.

##### **🔹 Node "Get attachments" (Code)**
- **Mã JavaScript**:
  ```javascript
  // Lấy danh sách file đính kèm từ email
  const attachments = $input.all().map(item => {
    return {
      name: item.attachments[0].filename,
      mimeType: item.attachments[0].mimeType,
      data: item.attachments[0].data, // Base64 encoded
    };
  });
  return { json: { attachments } };
  ```
  *Lưu ý*: Các sếp có thể cần chỉnh sửa nếu email có nhiều file đính kèm.

##### **🔹 Node "Upload attachment" (Google Drive)**
- **Credentials**: `googleDriveOAuth2Api`.
- **File**: `$json["data"]` (dữ liệu base64 từ node `Get attachments`).
- **Tên file**: `$json["name"]`.
- **Thư mục**: `$json["folderId"]` (ID của thư mục người gửi).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Execute Workflow** và chọn email mẫu để kiểm tra.
   - Kiểm tra Google Drive xem file đã upload vào thư mục đúng chưa.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: `Gửi tin nhắn: "Đã tự động sắp xếp file từ [sender] vào Google Drive!"`.

2. **Lưu Log**:
   - Thêm node **Google Sheets** để ghi log tất cả file đã xử lý (ngày, người gửi, tên file).

3. **Chạy định kỳ**:
   - Sử dụng **n8n Cloud** hoặc **cron job** để chạy workflow hàng ngày/lần tuần.

4. **Tự động xóa email đã xử lý**:
   - Thêm node **Gmail** với operation `delete` để xóa email sau khi đã upload file.

5. **Tạo nhiều thư mục cha**:
   - Ví dụ: Tạo thư mục `2024` và `2025` để phân loại theo năm.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quản lý file đính kèm Gmail mà **không cần code**. Với chỉ vài bước cấu hình, bạn sẽ:
✔ **Tiết kiệm thời gian** không phải tìm kiếm file.
✔ **Tránh trùng lặp** nhờ kiểm tra thư mục.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy import ngay và bắt đầu tự động hóa ngay hôm nay!** 🚀
Nếu có vấn đề, các sếp có thể liên hệ tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza) hoặc email `info@n3w.it`.

---
**💡 Mẹo cuối**: Nếu muốn tối ưu hơn, các sếp có thể **tạo nhiều workflow** cho từng loại file (PDF, Excel, Image) với logic xử lý riêng biệt.