---
title: "📁 Tự Động Tạo Cấu Trúc Thư Mục Google Drive Từ Đường Dẫn (N8n) - Khắc Phục Nỗi Đau Quản Lý File Phức Tạp"
description: "Workflow tự động hóa 100% không code giúp các sếp tạo hệ thống thư mục Google Drive có cấu trúc từ đường dẫn text (ví dụ: 'Projects/Clients/Reports') và trả về ID folder cuối cùng để upload file tự động. Giúp tiết kiệm thời gian lên đến 80% so với cách thủ công."
slug: "tao-thu-muc-google-drive-tu-duong-dan-n8n"
tags: [n8n, automation, google-drive, it-ops, no-code, workflow-templates]
keywords: [tự động hóa google drive, tạo thư mục google drive từ đường dẫn, n8n workflow google drive, quản lý file tự động, lưu trữ cloud hiệu quả]
---

# 🚀 **Tự Động Tạo Cấu Trúc Thư Mục Google Drive Từ Đường Dẫn (N8n)**

### **Giải Pháp Cho Nỗi Đau "Quản Lý File Trên Google Drive Làm Mệt Mỏi"**
Các sếp đã từng gặp phải tình huống này chưa?
- **Tạo thư mục Google Drive thủ công** mất nhiều thời gian, đặc biệt khi có **cấu trúc phức tạp** như `Projects/Clients/Reports/2024/Q1`?
- **Không biết folder nào đã tồn tại**, dẫn đến **trùng lặp** hoặc **quên tạo thư mục con**?
- **Không thể tự động hóa** vì không biết code hoặc không muốn phức tạp hóa hệ thống?

**Workflow này giải quyết tất cả!** Chỉ cần cung cấp **đường dẫn text** (ví dụ: `Projects/Clients/Reports`), nó sẽ:
✅ **Tự động tạo toàn bộ cấu trúc thư mục** trên Google Drive (bao gồm cả thư mục cha và con).
✅ **Tránh trùng lặp** bằng cách kiểm tra folder đã tồn tại trước khi tạo mới.
✅ **Trả về ID folder cuối cùng** để các sếp **upload file tự động** vào đúng vị trí.
✅ **Hoạt động 24/7** khi được self-host trên VPS, không phụ thuộc vào thời gian làm việc.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, phù hợp với Google Drive API)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách tạo thủ công.
- **Tránh lỗi nhân viên** (không còn quên tạo thư mục hoặc tạo trùng).
- **Cấu trúc file thống nhất** trên toàn bộ team, dễ quản lý.
- **Hoạt động tự động** khi kết hợp với các workflow khác (ví dụ: upload file từ Slack/Email).
- **Dễ dàng mở rộng** cho các dự án mới (chỉ cần thay đổi đường dẫn).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** và **API Key OAuth2** (để n8n kết nối với Google Drive).
✔ **Dữ liệu đầu vào** (đường dẫn thư mục) khi gọi workflow từ bên ngoài.
🔹 **Lưu ý**: Workflow này **không tự động kích hoạt** khi import. Các sếp phải **gọi từ workflow khác** hoặc sử dụng **Manual Trigger** để test.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/3709](https://n8n.io/workflows/3709) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Create Workflow** trong n8n.

📌 **Lưu ý khi import**:
- **Không copy/paste workflow này một cách trực tiếp** từ trang n8n.io (do nó được thiết kế để **được gọi từ workflow khác**).
- **Không sử dụng Manual Trigger** để chạy workflow này **trực tiếp** (nếu không muốn, nó sẽ không hoạt động như dự kiến).

---

#### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflows này **không tự động chạy** khi import. Các sếp phải **cấu hình và gọi từ workflow khác** hoặc sử dụng **Manual Trigger** để test.

##### **A. Cấu Hình Credentials Google Drive**
1. **Tạo OAuth2 Credential** trong n8n:
   - Đi đến **Credentials** → **Add Credential** → Chọn **Google Drive OAuth2**.
   - Theo hướng dẫn để **đăng nhập Google** và cấp quyền cho n8n.
   - **Lưu credential** với tên: `googleDriveOAuth2Api` (đây là tên được sử dụng trong workflow).

2. **Kiểm tra node "Check if top folder exists"**:
   - Node này sử dụng credential `googleDriveOAuth2Api` để **kiểm tra folder cha** (ví dụ: `Projects`).
   - Nếu folder **không tồn tại**, nó sẽ **tạo mới** thông qua node **"Create new subfolder"**.

##### **B. Cấu Hình Input Data**
Workflows này **không tự động chạy** khi import. Các sếp phải **gọi từ workflow khác** với **2 tham số bắt buộc**:
- **`google_drive_folder_id`**: ID folder cha (có thể là `"root"` nếu muốn tạo từ root).
- **`desired_path`**: Đường dẫn thư mục muốn tạo (ví dụ: `Projects/Clients/Reports`).

🔹 **Ví dụ dữ liệu đầu vào**:
```json
{
  "google_drive_folder_id": "root",
  "desired_path": "Projects/Clients/Reports/2024/Q1"
}
```

##### **C. Kích Hoạt Workflow**
1. **Test Run** (nếu gọi từ workflow khác):
   - Chạy workflow cha (gọi workflow này) với dữ liệu mẫu.
   - Kiểm tra **log** để xác nhận folder được tạo thành công.

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow này.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Kết Hợp Với Workflow Upload File**
Sau khi tạo folder, các sếp có thể **gọi workflow này từ workflow upload file** để **tự động đưa file vào đúng thư mục**:
- **Input**: `desired_path` = `Projects/Clients/Reports/2024/Q1`
- **Output**: Lấy `google_drive_folder_id` từ kết quả của workflow này để upload file vào.

#### **2. Gửi Báo Cáo Thư Mục Đã Tạo**
Sử dụng **node Slack/Telegram** để **gửi thông báo** khi folder được tạo thành công:
```json
{
  "text": `📁 Thư mục "${desired_path}" đã được tạo thành công!\nID folder cuối cùng: ${google_drive_folder_id}`
}
```

#### **3. Lưu Log Tạo Folder**
Sử dụng **node Database (PostgreSQL/MySQL)** hoặc **Google Sheets** để **lưu lịch sử** các folder được tạo:
- Cột: `desired_path`, `created_at`, `folder_id`.

#### **4. Tự Động Tạo Folder Khi Có File Mới**
Kết hợp với **node File System** hoặc **Google Drive API** để:
- Khi có file mới được upload, **tách đường dẫn** và gọi workflow này để tạo folder tương ứng.

---

### 📌 **Kết Luận**
Workflow **"Create Google Drive Folders by Path"** là **giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** trong việc quản lý file.
✔ **Tránh lỗi nhân viên** khi tạo thư mục.
✔ **Tự động hóa toàn bộ quy trình** từ tạo folder đến upload file.

**Hành động ngay hôm nay!**
1. **Self-host n8n** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình credentials Google Drive.
3. **Kết hợp với workflow upload file** để **tự động hóa hoàn toàn** quy trình quản lý file.

🚀 **Bắt đầu tự động hóa ngay bây giờ!** Các sếp sẽ **không bao giờ phải tạo thư mục thủ công lại**.