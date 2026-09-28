---
title: "🚀 Tự Động Chuyển Nhập Tệp FTP Sang Google Drive Với Batch Processing - Giảm Thời Gian Làm Việc 90%!"
description: "Workflow này tự động lấy tất cả file từ FTP server, xử lý theo batch để tránh quá tải, rồi chuyển nhập lên Google Drive một cách nhanh chóng và chính xác. Phù hợp cho các sếp quản lý nội dung, marketing hoặc IT cần lưu trữ an toàn và tự động hóa lưu trữ file."
slug: "tu-dong-chuyen-nhap-ftp-sang-google-drive-batch-processing"
tags: [n8n, automation, ftp, google-drive, batch-processing, content-creation, no-code]
keywords: [tự động hóa n8n, chuyển file ftp sang google drive, batch processing, lưu trữ tự động, tự động hóa nội dung, n8n workflow ftp]
---

# 🚀 **Tự Động Chuyển Nhập Tệp FTP Sang Google Drive Với Batch Processing**

### **Giải Phóng Tay Các Sếp Từ Công Việc Lặp Lại Mệt Mỏi!**
Các sếp đã bao giờ phải mất **giờ đồng hồ** để tải xuống từng file từ FTP, sau đó chuyển nhập lên Google Drive? Hay phải lo lắng về **quá tải server** khi xử lý hàng trăm file cùng một lúc? Workflow này sẽ **tự động hóa toàn bộ quy trình**, đảm bảo **tốc độ, chính xác và an toàn**, giúp các sếp tập trung vào những việc quan trọng hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần tải xuống từng file thủ công, giảm **90% thời gian làm việc**.
✅ **Xử lý batch hiệu quả**: Tránh quá tải server bằng cách chia nhỏ file thành batch.
✅ **Lưu trữ an toàn**: Tất cả file được tự động chuyển nhập lên Google Drive với tên gốc.
✅ **Hoạt động liên tục**: Dùng **Schedule Trigger** để chạy tự động hàng ngày/tuần.
✅ **Chính xác 100%**: Không sai sót do con người, đảm bảo tất cả file đều được xử lý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản FTP** (Host, Username, Password, Port, Path đến thư mục file).
✔ **Tài khoản Google Drive** (đã cấp quyền OAuth 2.0 cho n8n).
✔ **n8n Self-hosted** (đã cài đặt và cài đặt các node cần thiết: `n8n-nodes-base.ftp`, `n8n-nodes-base.googleDrive`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8703) và import vào n8n Editor.
- **Copy JSON** từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: ⏯️ Schedule Trigger**
- **Cấu hình thời gian chạy tự động**:
  - Chọn **cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - Nếu muốn chạy thủ công, có thể **bỏ qua** và dùng **Webhook** thay thế.

##### **🔹 Node 2: 📂 List Files from FTP**
- **Thiết lập credentials FTP**:
  - Vào **Credentials** → **Add Credentials** → Chọn **FTP**.
  - Điền thông tin:
    - **Host**: `ftp.example.com` (thay bằng host của sếp).
    - **Port**: `21` (mặc định) hoặc `22` (nếu sử dụng SFTP).
    - **Username** & **Password**: Tài khoản FTP của sếp.
    - **Path**: `/path/to/your/files` (đường dẫn thư mục cần lấy file).
- **Test connection** để đảm bảo kết nối thành công.

##### **🔹 Node 3: 🔀 Batch Files (splitInBatches)**
- **Cấu hình batch size**:
  - Mặc định là **1 file/batch**, nhưng có thể điều chỉnh lên (ví dụ: `5` file/batch) nếu server mạnh.
  - **Lưu ý**: Nếu batch quá lớn, có thể gây **quá tải** cho FTP/Google Drive.

##### **🔹 Node 4: ⬇️ Download File from FTP**
- **Sử dụng biến `$json.name`**:
  - Node này tự động lấy tên file từ danh sách ở **Node 2** và tải xuống.
  - **Không cần chỉnh sửa** nếu đã cấu hình FTP đúng.

##### **🔹 Node 5: ☁️ Upload to Google Drive**
- **Thiết lập credentials Google Drive**:
  - Vào **Credentials** → **Add Credentials** → Chọn **Google Drive OAuth 2.0 API**.
  - Theo hướng dẫn của n8n để cấp quyền (sẽ mở tab Google để xác nhận).
- **Chọn folder đích**:
  - Trong **Google Drive Node**, chọn **Folder ID** hoặc **Folder Name** để lưu file.
  - **Lưu ý**: Nếu folder chưa tồn tại, cần tạo trước.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Run** để kiểm tra workflow với 1-2 file mẫu.
  - Kiểm tra **log** để đảm bảo không có lỗi.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **Node Slack/Telegram** sau **Upload to Google Drive** để thông báo khi hoàn thành.
   - Ví dụ: `File [{{$json.name}}] đã được chuyển nhập thành công lên Google Drive!`

2. **Lưu log hoạt động**:
   - Sử dụng **Node StickyNote** hoặc **Node Google Sheets** để ghi lại lịch sử chuyển file.
   - Có thể theo dõi **thời gian, tên file, trạng thái** để debug nếu có lỗi.

3. **Xử lý file lớn**:
   - Nếu file quá lớn (trên 100MB), có thể chia nhỏ bằng **Node SplitInBatches** với size nhỏ hơn.
   - Hoặc sử dụng **Google Drive API** với **resumable upload** để tối ưu băng thông.

4. **Tự động xóa file sau khi upload**:
   - Thêm **Node FTP (Delete)** sau **Upload to Google Drive** để xóa file từ FTP sau khi chuyển thành công.
   - Cấu hình **path**: `={{ $json.path }}` và **operation**: `delete`.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa lưu trữ file** từ FTP sang Google Drive một cách **nhanh chóng, an toàn và không cần code**. Với **batch processing**, nó đảm bảo **không quá tải server** và **chỉnh sửa tối thiểu** khi cấu hình.

**Hãy áp dụng ngay và giải phóng thời gian cho những việc quan trọng hơn!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi Avkash Kakdiya** (tác giả workflow) qua [iTechNotion](https://itechnotion.com/).
- **Đăng ký VPS n8n** để chạy 24/7: [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã giảm **VPSN8N**).