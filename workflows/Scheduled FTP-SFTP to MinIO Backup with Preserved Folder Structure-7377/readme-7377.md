---
title: "🚀 Tự Động Hoàn Hảo: Backup FTP-SFTP Sang MinIO (Giữ Nguồn Cấu Trúc Thư Mục) Với n8n - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn để sao lưu dữ liệu từ FTP/SFTP sang MinIO (hoặc AWS S3, Azure Blob) với cấu trúc thư mục nguyên vẹn, chạy 24/7 mà không tốn chi phí code. Phù hợp cho doanh nghiệp lưu trữ dữ liệu lớn, website WordPress, hoặc hệ thống archival storage."
slug: "tieu-dong-hoan-hao-backup-ftp-sftp-sang-minio"
tags: [n8n, automation, file-management, minio, sftp, backup-automation, no-code]
keywords: [tự động hóa backup ftp sftp, backup minio với n8n, lưu trữ dữ liệu tự động, sao lưu website wordpress, backup s3 compatible]
---

# 🚀 **Backup FTP-SFTP Sang MinIO (Giữ Nguồn Cấu Trúc Thư Mục) Với n8n – Không Cần Code!**

### **🔥 Nỗi Đau Của Các Sếp Khi Sao Lưu Dữ Liệu FTP/SFTP**
Các sếp đang phải:
- **Thủ công tải xuống** hàng ngàn file từ FTP/SFTP mỗi ngày, tốn thời gian và dễ sai sót.
- **Không bảo toàn cấu trúc thư mục**, dẫn đến mất mát dữ liệu khi sao lưu.
- **Phải nhớ nhặt** các file quan trọng giữa hàng trăm GB dữ liệu, tăng rủi ro mất mát.
- **Không có lịch trình tự động**, phải làm thủ công mỗi khi có dữ liệu mới.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** với n8n, sao lưu **tất cả dữ liệu từ FTP/SFTP sang MinIO (hoặc AWS S3, Azure Blob)** **với cấu trúc thư mục nguyên vẹn**, **không cần code**, và **chạy 24/7**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** – Không phải tải xuống thủ công hàng ngày.
✅ **Bảo toàn cấu trúc thư mục** – File và folder được sao lưu theo nguyên vị trí.
✅ **Tự động hóa hoàn toàn** – Chỉ cần cấu hình 1 lần, workflow chạy tự động theo lịch.
✅ **Dữ liệu an toàn** – MinIO (hoặc S3-compatible) cung cấp lưu trữ ổn định, bảo mật.
✅ **Dễ mở rộng** – Thay đổi từ MinIO sang AWS S3, Azure Blob chỉ với 1 click.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần:
✔ **Tài khoản FTP/SFTP** (ví dụ: FTP của WordPress, server lưu trữ website).
✔ **Thông tin kết nối MinIO** (hoặc AWS S3, Azure Blob):
   - **Endpoint MinIO** (ví dụ: `http://192.168.1.123:9000`).
   - **Bucket Name** (ví dụ: `ftp-backup`).
   - **Access Key & Secret Key** của MinIO.
✔ **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7377](https://n8n.io/workflows/7377) hoặc copy toàn bộ JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Create New Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Lịch Triggers)**
- **Configure this trigger**:
  - Chọn **Cron Expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - **Lưu ý**: Nếu muốn chạy **ngay lập tức**, chọn **Manual Trigger** và kích hoạt sau.

##### **🔹 Node 2: List FTP Folder Contents (Liệt Kê File Trong Thư Mục FTP)**
- **Credentials**:
  - Chọn **SFTP** (hoặc FTP nếu không sử dụng SSL).
  - Điền **Host**, **Port**, **Username**, **Password**.
- **Key Parameters**:
  - **Operation**: `list` (để liệt kê file).
  - **Path**: `/bitnami/wordpress/wp-content/uploads/2025/04` (thay đổi thành đường dẫn thư mục cần sao lưu).
  - **Recursive**: **Bật** (để sao lưu tất cả file con trong thư mục).

##### **🔹 Node 3: Download Content (Tải Xuống File)**
- **Path**: `={{ $('List FTP Folder contents').item.json.path }}`
  - Node này tự động lấy đường dẫn từ node trước và tải xuống file.
- **Lưu ý**:
  - Nếu muốn tải xuống **tất cả file trong thư mục**, **Recursive** phải được bật ở node 2.

##### **🔹 Node 4: Create Path for MinIO (Tạo Đường Dẫn Cho MinIO)**
- **Operation**: `set`
- **Key Parameters**:
  - **Path**: `={{ $('Download content').item.json.path }}`
    - Node này **tạo đường dẫn tương ứng** trong MinIO để bảo toàn cấu trúc thư mục.

##### **🔹 Node 5: Upload on MinIO with Correct Path (Upload Sang MinIO)**
- **Credentials**:
  - Chọn **S3** (n8n hỗ trợ MinIO, AWS S3, Azure Blob, GCP Storage).
  - Điền **Endpoint**, **Access Key**, **Secret Key**, **Region**.
- **Key Parameters**:
  - **Operation**: `upload`
  - **Bucket**: `ftp-backup` (thay đổi theo bucket của bạn).
  - **File**: `={{ $('Download content').item.json.file }}`
  - **Path**: `={{ $('Create Path for MinIO').json.path }}`
    - **Đây là khóa quan trọng**: Node này **giữ nguyên cấu trúc thư mục** khi upload.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và kiểm tra **log** để đảm bảo không có lỗi.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM TIẾP THEO**]
🔹 **Thay đổi từ MinIO sang AWS S3/Azure Blob**:
   - Chỉ cần thay đổi **credentials** ở node **Upload on MinIO** sang **S3** (AWS) hoặc **Azure Blob**.
   - **Endpoint AWS S3**: `https://s3.<region>.amazonaws.com`
   - **Endpoint Azure Blob**: `https://<storage-account>.blob.core.windows.net`

🔹 **Gửi thông báo khi backup thành công/lỗi**:
   - Thêm **node Slack/Email** sau node **Upload on MinIO** để nhận báo cáo tự động.

🔹 **Lưu log backup**:
   - Thêm **node StickyNote** hoặc **Google Sheets** để ghi lại lịch sử backup (file nào, thời gian, trạng thái).

🔹 **Sao lưu nhiều thư mục FTP khác nhau**:
   - Sao chép workflow và thay đổi **path** ở node **List FTP Folder Contents**.
   - Sử dụng **node Set** để phân loại dữ liệu theo thư mục.
:::

---

### 📌 **Kết Luận**
**Workflow này là giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa sao lưu FTP/SFTP sang MinIO** (hoặc AWS S3, Azure Blob) **không cần code**.
✔ **Bảo toàn cấu trúc thư mục** để dễ quản lý dữ liệu.
✔ **Chạy 24/7** mà không tốn chi phí nhân sự.

**Hãy áp dụng ngay và tiết kiệm thời gian, giảm rủi ro mất mát dữ liệu!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Nếu có thắc mắc, hãy để lại comment dưới đây. 👇