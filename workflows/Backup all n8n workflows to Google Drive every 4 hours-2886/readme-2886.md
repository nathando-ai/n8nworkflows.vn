---
title: "🗄️ **Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang Google Drive Mỗi 4 Giây (Không Cần Code!)**"
description: "Giải pháp tự động hóa hoàn hảo để sao lưu tất cả workflow n8n của bạn sang Google Drive tự động, an toàn và định kỳ. Đảm bảo không mất dữ liệu dù có sự cố nào xảy ra!"
slug: "backup-n8n-workflows-to-google-drive"
tags: [n8n, automation, backup, google-drive, no-code, self-hosted]
keywords: [backup workflow n8n, tự động hóa lưu trữ, sao lưu n8n sang google drive, tự động hóa định kỳ, lưu trữ an toàn workflow]
---

# 🚀 **Backup Tất Cả Workflow n8n Sang Google Drive Mỗi 4 Giây – Không Cần Code!**

### **💥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã bao giờ lo lắng về việc **mất dữ liệu workflow n8n** do lỗi hệ thống, xóa nhầm, hoặc không sao lưu định kỳ? Hay phải **tốn thời gian thủ công** sao lưu từng workflow vào Google Drive, Dropbox, hoặc máy chủ? Với **tự động hóa hoàn hảo này**, các sếp sẽ **không bao giờ phải lo lắng** về mất dữ liệu nữa!

Workflow này **tự động**:
✅ **Lấy tất cả workflow** từ n8n (self-hosted hoặc cloud) và **sao lưu vào Google Drive** định kỳ (mỗi 4 giờ).
✅ **Tạo thư mục riêng biệt** cho mỗi lần backup, giúp quản lý dễ dàng.
✅ **Chuyển đổi dữ liệu thành file JSON** để dễ dàng phục hồi.
✅ **Xóa thư mục cũ** (nếu muốn) để tiết kiệm không gian lưu trữ.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Không bao giờ mất dữ liệu workflow do lỗi hệ thống.
- **Tiết kiệm thời gian**: Không cần sao lưu thủ công, hệ thống làm tự động.
- **Quản lý dễ dàng**: Tất cả backup được lưu trong **Google Drive**, dễ dàng truy cập và phục hồi.
- **Tự động hóa hoàn hảo**: Chỉ cần **bật workflow**, nó sẽ hoạt động **mỗi 4 giờ** mà không cần can thiệp.
- **Tiết kiệm không gian**: Có thể **xóa thư mục cũ** để giữ lại chỉ những backup mới nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (và **OAuth 2.0 API Key** đã cấu hình trong n8n).
✔ **n8n API Key** (để workflow có thể lấy dữ liệu từ n8n của mình).
✔ **Google Drive OAuth 2.0 Credentials** (đã cấu hình trong n8n để truy cập Google Drive).

---
:::info[CHUẨN BỊ]
1. **Cấu hình OAuth 2.0 cho Google Drive** trong n8n:
   - Tạo **Google Cloud Project** và bật **Google Drive API**.
   - Tạo **OAuth 2.0 Client ID** và cấu hình trong n8n.
2. **Lấy API Key của n8n**:
   - Mở **Settings → API → Generate API Key**.
3. **Chọn thư mục Google Drive** để lưu backup (cần tạo trước hoặc workflow sẽ tạo mới).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2886).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **8 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: Schedule Trigger (Giai đoạn tự động hóa)**
- **Cấu hình thời gian chạy**: Mặc định là **mỗi 4 giờ**, nhưng các sếp có thể điều chỉnh theo nhu cầu.
- **Lưu ý**: Nếu muốn **chạy ngay lập tức**, các sếp có thể **bỏ qua node này** và sử dụng **Manual Trigger** thay thế.

##### **🔹 Node 2: Manual Trigger (Nếu không dùng Schedule)**
- **Nếu không muốn tự động**, các sếp có thể **bỏ node Schedule** và sử dụng **Manual Trigger** để chạy thủ công.

##### **🔹 Node 3: n8n (Lấy tất cả workflow)**
- **Credentials**: Chọn **n8nApi** (API Key đã tạo trước).
- **Lưu ý**: Nếu n8n ở **cloud**, các sếp cần **điền URL API** của n8n (ví dụ: `https://cloud.n8n.io`).
- **Nếu self-hosted**, URL sẽ là `http://<your-server-ip>:5678`.

##### **🔹 Node 4: Filter (Lọc workflow cần backup)**
- **Cấu hình**: Các sếp có thể **lọc workflow** theo tên, mô tả, hoặc trạng thái (Active/Inactive).
- **Lưu ý**: Nếu muốn **backup tất cả**, bỏ qua node này hoặc để mặc định.

##### **🔹 Node 5: Split In Batches (Chia thành batch)**
- **Cấu hình**: Nếu có **nhiều workflow**, node này sẽ **chia thành batch** để tránh quá tải.
- **Lưu ý**: Các sếp có thể **điều chỉnh size batch** (ví dụ: 10 workflow/lần).

##### **🔹 Node 6: Convert to File (Chuyển thành JSON)**
- **Operation**: Chọn **toJson** (để lưu workflow dưới dạng file JSON).
- **Lưu ý**: Nếu muốn lưu dưới dạng **YAML**, các sếp có thể thay đổi.

##### **🔹 Node 7: Google Drive (Tạo thư mục mới)**
- **Credentials**: Chọn **googleDriveOAuth2Api**.
- **Folder Name**: Các sếp có thể **đặt tên tự động** (ví dụ: `Backup_n8n_$(date)`).
- **Lưu ý**: Nếu muốn **tạo thư mục ở vị trí cụ thể**, các sếp cần **điền ID folder** vào `parentId`.

##### **🔹 Node 8: Google Drive (Upload file)**
- **Credentials**: Chọn **googleDriveOAuth2Api**.
- **File Content**: Chọn **data** từ node **Convert to File**.
- **File Name**: Các sếp có thể **đặt tên tự động** (ví dụ: `workflow_$(name).json`).
- **Lưu ý**: Nếu muốn **ghi đè file cũ**, các sếp cần **xóa node Delete Folder** (nếu có).

##### **🔹 Node 9: Delete Folder (Xóa thư mục cũ - Tùy chọn)**
- **Credentials**: Chọn **googleDriveOAuth2Api**.
- **Folder ID**: Các sếp cần **điền ID của thư mục cũ** (nếu muốn xóa).
- **Lưu ý**: **Không xóa node này** nếu muốn **giữ lại tất cả backup**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Chạy **Manual Trigger** để kiểm tra workflow hoạt động như thế nào.
   - Kiểm tra **Google Drive** xem có xuất hiện **thư mục backup** không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật node Schedule Trigger** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi backup thành công**:
   - Thêm **node Slack/Telegram Webhook** sau node **Google Drive Upload** để thông báo.
2. **Lưu log vào Google Sheets**:
   - Thêm **node Google Sheets** để ghi lại **thời gian backup, số lượng workflow, và trạng thái**.
3. **Backup định kỳ vào Dropbox/OneDrive**:
   - Thay thế **Google Drive** bằng **Dropbox/OneDrive** bằng cách thay đổi credentials.
4. **Chia sẻ thư mục backup với team**:
   - Sau khi backup, các sếp có thể **chia sẻ thư mục Google Drive** với team để **phục hồi dễ dàng**.
5. **Tự động xóa backup cũ sau 30 ngày**:
   - Sử dụng **node Google Drive** với **operation: deleteFile** để xóa file cũ.
:::

---

### 📌 **Kết Luận**
**Backup tự động workflow n8n sang Google Drive** là **giải pháp hoàn hảo** để các sếp **không bao giờ mất dữ liệu** do lỗi hệ thống, xóa nhầm, hoặc không sao lưu kịp thời. Với **tự động hóa này**, các sếp chỉ cần **bật workflow**, hệ thống sẽ **làm tất cả** cho mình!

**Hãy áp dụng ngay và bảo vệ dữ liệu n8n của mình!** 🚀

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/2886)**
**💬 Có thắc mắc? Hãy để lại comment bên dưới!**