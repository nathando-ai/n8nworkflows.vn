---
title: "🔥 Tự Động Nén PDF Trên Google Drive Với iLovePDF – Giảm Thể Tích File 80% Miễn Phí"
description: "Workflow tự động hóa nén PDF từ Google Drive sang iLovePDF, giảm thể tích file lên đến 80% và tự động lưu kết quả vào thư mục mới – giải pháp hoàn hảo cho doanh nghiệp quản lý hàng ngàn tài liệu PDF lớn."
slug: "tu-dong-nen-pdf-google-drive-ilovepdf"
tags: [n8n, tự động hóa, Google Drive, iLovePDF, file management, nén file]
keywords: [n8n workflow PDF, tự động hóa nén PDF, giảm kích thước file Google Drive, iLovePDF API, tự động hóa lưu trữ]
---

# 🚀 **Tự Động Nén PDF Trên Google Drive Với iLovePDF – Giảm Thể Tích File 80% Miễn Phí**

### **Giải pháp nào cho các sếp khi:**
- **Tốn thời gian** phải nén từng file PDF thủ công?
- **Lưu trữ Google Drive** bị quá tải vì file PDF lớn?
- **Không biết cách tự động hóa** quá trình này mà không cần code?

Workflow này **tự động nén PDF từ Google Drive** sang iLovePDF (miễn phí), giảm thể tích file lên đến **80%** và **tự động lưu kết quả** vào thư mục mới – giúp tiết kiệm không gian lưu trữ và thời gian cho các sếp.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Giảm thể tích file lên đến 80%** – tiết kiệm không gian lưu trữ Google Drive.
✅ **Tự động hóa hoàn toàn** – không cần can thiệp thủ công.
✅ **Chỉnh sửa dễ dàng** – thay đổi thư mục nguồn/đích mà không cần biết code.
✅ **Hoạt động 24/7** – chạy liên tục trên VPS tự host (không phụ thuộc vào n8n Cloud).
✅ **Miễn phí** – sử dụng API iLovePDF không tính phí cho các file nhỏ/mittel.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive** (đã cấp quyền API).
- **Tài khoản iLovePDF** (đăng ký tại [ilovepdf.com](https://www.ilovepdf.com/)).
- **API Key của iLovePDF** (lấy từ [Dashboard iLovePDF](https://www.ilovepdf.com/api/)).
- **Thư mục nguồn** (chứa file PDF cần nén).
- **Thư mục đích** (để lưu file PDF đã nén).
- **n8n Self-hosted** (khuyến nghị để workflow hoạt động liên tục).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/10766) hoặc copy toàn bộ JSON từ link trên.
- **Mở n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **10 node** chính, các sếp cần cấu hình như sau:

##### **A. Cấu hình Google Drive**
1. **Node "Upload your file to Google Drive" (Google Drive Trigger)**
   - **Chọn credentials**: Tạo mới hoặc chọn credentials Google Drive đã có.
   - **Folder ID**: Nhập ID của thư mục **nguồn** (file PDF cần nén).
     - *Lấy ID folder*: Mở Google Drive → Chọn thư mục → URL sẽ có dạng `https://drive.google.com/drive/folders/[FOLDER_ID]` → Copy `FOLDER_ID`.
   - **File Type**: Chọn `PDF`.

2. **Node "Download file" (Google Drive)**
   - **Credentials**: Chọn cùng credentials Google Drive như trên.
   - **File ID**: Sẽ tự động lấy từ trigger (không cần chỉnh).

3. **Node "Move compressed file to new Google Drive folder" (Google Drive)**
   - **Credentials**: Cùng credentials Google Drive.
   - **Folder ID**: Nhập ID của thư mục **đích** (để lưu file PDF đã nén).
   - **Destination Path**: Điền `/compressed-files/` (hoặc tên thư mục tùy chỉnh).

##### **B. Cấu hình iLovePDF API**
1. **Node "Send your iLoveAPI public key to their server" (HTTP Request)**
   - **URL**: `https://api.ilovepdf.com/v1/auth`
   - **Method**: `POST`
   - **Headers**:
     - `Content-Type: application/json`
   - **Body**:
     ```json
     {
       "publicKey": "YOUR_PUBLIC_KEY_HERE"
     }
     ```
     - *Lấy `publicKey`*: Vào [Dashboard iLovePDF](https://www.ilovepdf.com/api/) → Copy `Public Key`.

2. **Node "Upload PDF to iLoveAPI server" (HTTP Request)**
   - **URL**: `https://api.ilovepdf.com/v1/upload`
   - **Method**: `POST`
   - **Headers**:
     - `Authorization: Bearer YOUR_TOKEN_HERE` (lấy từ response của node trước).
     - `Content-Type: multipart/form-data`
   - **Body**: Chọn `File` từ node "Download file" (trước đó đã tải file PDF từ Google Drive).

3. **Node "Compress your file" (HTTP Request)**
   - **URL**: `https://api.ilovepdf.com/v1/compress`
   - **Method**: `POST`
   - **Headers**:
     - `Authorization: Bearer YOUR_TOKEN_HERE`
     - `Content-Type: application/json`
   - **Body**:
     ```json
     {
       "taskId": "{{$node["Get task from iLoveAPI server"].json()["taskId"]}}"
     }
     ```
     - *Lưu ý*: Node này cần kết nối với node "Get task from iLoveAPI server" để lấy `taskId`.

4. **Node "Download compressed file" (HTTP Request)**
   - **URL**: `https://api.ilovepdf.com/v1/download/{{$node["Get task from iLoveAPI server"].json()["taskId"]}}`
   - **Method**: `GET`
   - **Headers**:
     - `Authorization: Bearer YOUR_TOKEN_HERE`

##### **C. Kết nối các node**
- **Node "Group public key, task and downloaded file data" (Merge)**
  - **Chọn các input**:
    - `iLoveAPI Public Key` (từ node "Send your iLoveAPI public key").
    - `Task ID` (từ node "Get task from iLoveAPI server").
    - `Downloaded File` (từ node "Download file").

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test Workflow** → Chọn file PDF mẫu trong thư mục nguồn.
   - Kiểm tra:
     - File đã được nén thành công?
     - File đã được lưu vào thư mục đích?
     - File gốc đã được di chuyển đến thư mục archive?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có file mới.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÀY ĐỂ TIẾT KIỆM THÊM]
- **Thêm thông báo Slack/Telegram**:
  - Sau khi nén thành công, thêm node **Slack/Telegram** để báo cáo kết quả.
  - *Cách thêm*: Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

- **Lưu log hoạt động**:
  - Thêm node **Google Sheets** để ghi lại lịch sử nén file (tên file, kích thước trước/sau, thời gian).

- **Tự động xóa file gốc sau 7 ngày**:
  - Thêm node **Google Drive** với operation `delete` để xóa file gốc sau khi đã nén và lưu kết quả.

- **Nén nhiều loại file**:
  - Thay đổi node trigger thành `fileType: ["pdf", "docx", "pptx"]` để nén nhiều định dạng.

- **Tùy chỉnh tên file**:
  - Sử dụng node **Set** để thêm prefix/suffix cho file đã nén (ví dụ: `Compressed_OriginalFile.pdf`).
:::

---
### 📌 **Kết luận**
Workflow này **giải quyết hoàn toàn vấn đề nén PDF thủ công** trên Google Drive, giúp các sếp:
✔ **Tiết kiệm thời gian** (không cần làm thủ công).
✔ **Giảm không gian lưu trữ** (file nén nhỏ hơn 80%).
✔ **Hoạt động tự động** (không cần can thiệp).

**👉 Bắt đầu ngay!**
1. **Cài n8n Self-hosted** trên VPS (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để nó làm việc 24/7!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Chia sẻ & phản hồi:**
Nếu các sếp có bất kỳ câu hỏi hoặc muốn tùy chỉnh workflow này cho phù hợp với doanh nghiệp, hãy để lại comment bên dưới! 🚀