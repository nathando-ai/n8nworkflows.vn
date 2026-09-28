---
title: "💾 **Hướng Dẫn Tự Động Hoàn Chỉnh Sách Lập Lại Tất Cả Workflow & Credentials n8n Với Lưu Trữ Cục Bộ + FTP**"
description: "Giải pháp tự động hóa 100% không code để sao lưu toàn bộ workflow và thông tin đăng nhập n8n hàng ngày lên máy chủ cục bộ và FTP, đảm bảo an toàn dữ liệu và phục hồi nhanh chóng khi xảy ra lỗi. Khắc phục hoàn toàn nỗi lo mất dữ liệu quan trọng khi n8n bị crash hoặc bị xóa."
slug: "huan-chinh-sach-lap-lai-n8n-workflow-credentials"
tags: [n8n, automation, backup, ftp, no-code, self-hosted, n8n-workflows]
keywords: [sao lưu n8n, backup workflow n8n, tự động hóa backup credentials, lưu trữ FTP n8n, giải pháp an toàn dữ liệu n8n]
---

# 🚀 **Sao Lưu Tự Động Toàn Bộ Workflow & Credentials n8n: Khắc Phục Nỗi Lo Mất Dữ Liệu Vĩnh Viên**

## **🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hãy tưởng tượng một ngày nọ, máy chủ n8n của bạn bị **crash**, **xóa nhầm** hoặc **bị hacker tấn công** – tất cả những **workflow** và **credentials** (thông tin đăng nhập API, keys, secrets) mà bạn đã xây dựng trong nhiều tháng, nhiều năm sẽ **mất vĩnh viễn**! Không chỉ tốn thời gian xây dựng lại, mà còn gây **gián đoạn hoạt động** của toàn bộ hệ thống tự động hóa.

Với **Complete Backup Solution for n8n Workflows & Credentials**, các sếp sẽ:
✅ **Sao lưu tự động** tất cả workflow và credentials **hàng ngày** (hoặc theo lịch bạn thiết lập).
✅ **Lưu trữ cục bộ** trên máy chủ (đảm bảo an toàn offline).
✅ **Upload lên FTP** để truy cập từ xa và phục hồi nhanh chóng.
✅ **Nhận thông báo email** khi backup thành công hoặc thất bại.
✅ **Không cần code** – chỉ cần cấu hình vài bước đơn giản!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính liên tục** và **an toàn dữ liệu**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho backup)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Không sợ mất dữ liệu**: Sao lưu tự động hàng ngày, phục hồi trong giây lát khi xảy ra lỗi.
- **Tiết kiệm thời gian**: Không phải thủ công export/import workflow và credentials.
- **An toàn tuyệt đối**: Dữ liệu được lưu trữ **cục bộ + FTP**, tránh rủi ro mất máy chủ.
- **Dễ dàng quản lý**: Gửi **email thông báo** khi backup thành công/thất bại.
- **Hoạt động 24/7**: Sử dụng **schedule trigger** để chạy tự động theo lịch.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Máy chủ VPS** (đã cài đặt n8n self-hosted).
✔ **Tài khoản FTP** (để upload backup).
✔ **Email admin** (để nhận thông báo).
✔ **Docker & FTP volume** (để lưu trữ backup).
✔ **Môi trường terminal** (để chạy lệnh `executeCommand`).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9151](https://n8n.io/workflows/9151).
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON và paste vào **Create New Workflow** → **Import from JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần cấu hình chính** trong node **`Init`** (type: **code**). Các sếp **cần thay đổi** như sau:

##### **📌 Phần 1: Workflow Standard Configuration**
```javascript
// Admin email cho thông báo
const N8N_ADMIN_EMAIL = $env.N8N_ADMIN_EMAIL || 'your-email@example.com';

// Tên workflow (auto-detect)
const WORKFLOW_NAME = $workflow.name;

// Thư mục gốc lưu dự án n8n (đường dẫn thực tế trên máy chủ)
const N8N_PROJECTS_DIR = $env.N8N_PROJECTS_DIR || '/files/n8n-projects-data';

// Tên thư mục dự án cho workflow backup này
const PROJECT_FOLDER_NAME = "Workflow-backups"; // ⚠️ Đổi thành tên thư mục của bạn
```
- **Lưu ý**:
  - `$env.N8N_ADMIN_EMAIL` là **email admin** để nhận thông báo.
  - `$env.N8N_PROJECTS_DIR` phải trùng với **thư mục lưu workflow** trên máy chủ (thường là `/files/n8n-projects-data` nếu dùng Docker).

##### **📌 Phần 2: Workflow Custom Configuration**
```javascript
// Thư mục backup cục bộ (phải tồn tại)
const BACKUP_FOLDER = $env.N8N_BACKUP_FOLDER || '/files/n8n-backups';

// Thư mục FTP để upload backup
const FTP_BACKUP_FOLDER = $env.N8N_FTP_BACKUP_FOLDER || '/n8n-backups';

// Tên FTP server (chỉ dùng để log)
const FTPName = 'Tên FTP của bạn'; // Ví dụ: 'FTP-Hosting.com'

// Thư mục lưu credentials
const credentials_backup_folder = "n8n-credentials";
```
- **Lưu ý**:
  - `BACKUP_FOLDER` phải là **thư mục đã tồn tại** trên máy chủ.
  - `FTP_BACKUP_FOLDER` là **đường dẫn trên FTP** (ví dụ: `/n8n-backups`).
  - **Không cần đổi `credentials_backup_folder`** trừ khi muốn thay đổi tên.

##### **📌 Cấu Hình Node FTP**
- Đi đến **node `Upload Workflows To FTP`** và **node `Upload Credentials To FTP`**.
- **Kiểm tra credentials FTP**:
  - Nhấn **Add Credential** → Chọn **FTP** → Điền:
    - **Host**: `ftp.example.com`
    - **Port**: `21` (hoặc `22` nếu FTP SSL)
    - **Username** & **Password**: Thông tin đăng nhập FTP.
    - **Protocol**: `FTP` hoặc `FTPS` (nếu dùng SSL).
- **Kiểm tra `FTP_BACKUP_FOLDER`**:
  - Đảm bảo đường dẫn trên FTP **tồn tại** (nếu không, tạo thư mục trước).

##### **📌 Node `Daily Backup` (Schedule Trigger)**
- Đi đến **node `Daily Backup`** → Nhấn **Edit**.
- Thiết lập **lịch chạy**:
  - **Cron expression**: `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Timezone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).

##### **📌 Node `Fetch Workflows` (n8n Node)**
- **Không cần cấu hình thêm**, node này tự động lấy tất cả workflow từ n8n.

##### **📌 Node `ExecuteCommand` (Create Date Folder & Export Credentials)**
- **Không cần thay đổi**, node này tự động tạo thư mục theo ngày và export credentials.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** → Chọn **Test Execution**.
   - Kiểm tra **log** trong node `Write Backup Log` và `Write Email Log`.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu log chi tiết**:
   - Thêm node **`stickyNote`** để ghi chú lỗi hoặc thành công.
   - Ví dụ: `Backup thành công vào ${new Date().toLocaleString()}`.

2. **Gửi báo cáo định kỳ**:
   - Kết hợp với **node `emailSend`** để gửi **báo cáo tổng hợp** hàng tuần/month.

3. **Backup lên nhiều FTP**:
   - Sử dụng **node `merge`** để upload cùng lúc lên **2 FTP khác nhau** (ví dụ: FTP chính + Google Drive).

4. **Khôi phục dữ liệu nhanh**:
   - Lưu **file backup** vào **Google Drive/Dropbox** để truy cập từ xa.

5. **Bảo mật credentials**:
   - Sử dụng **node `code`** để **mã hóa credentials** trước khi upload FTP.

---

### 📌 **Kết Luận**
**Workflow này là giải pháp hoàn hảo** để các sếp **không bao giờ lo mất dữ liệu** khi n8n bị lỗi. Với **sao lưu tự động hàng ngày**, **lưu trữ cục bộ + FTP**, và **thông báo email**, bạn có thể **yên tâm** rằng tất cả workflow và credentials của mình **luôn được bảo vệ**.

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n.
2. **Cấu hình email, FTP và đường dẫn** theo hướng dẫn.
3. **Bật Active** và **quên đi lo lắng về mất dữ liệu!**

---
**🚀 Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với Florent (tác giả) qua [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 💪