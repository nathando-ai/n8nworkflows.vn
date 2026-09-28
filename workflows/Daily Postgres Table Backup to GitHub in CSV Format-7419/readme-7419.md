---
title: "💾 **Tự Động Hoàn Chỉnh Sao Lưu Bảng PostgreSQL Sang GitHub Hàng Ngày (CSV) - Không Cần Code!**"
description: "Workflow tự động hóa sao lưu toàn bộ dữ liệu bảng PostgreSQL sang GitHub dưới dạng CSV hàng ngày, đảm bảo an toàn, dễ theo dõi và cập nhật tự động. Giúp các sếp DevOps tiết kiệm thời gian và tránh mất mát dữ liệu."
slug: "tự-dộng-hoàn-chỉnh-sao-lưu-postgres-sang-github"
tags: [n8n, automation, devops, postgres, github, backup-automation]
keywords: [tự động hóa sao lưu postgres, backup postgres sang github, n8n workflow postgres, sao lưu dữ liệu hàng ngày, tự động hóa devops]
---

# 🚀 **Tự Động Hoàn Chỉnh Sao Lưu Bảng PostgreSQL Sang GitHub Hàng Ngày (CSV)**

### **🔥 Nỗi Đau Của Các Sếp DevOps**
Các sếp đang phải **thủ công** sao lưu dữ liệu PostgreSQL hàng ngày? Hay phải **lo lắng** về việc mất mát dữ liệu khi không sao lưu kịp thời? Hoặc **phải quản lý thủ công** các file CSV trên GitHub, dẫn đến **trùng lặp, lỗi hoặc mất dữ liệu cũ**?

**Workflow này giải quyết tất cả!**
- **Sao lưu tự động** tất cả bảng PostgreSQL sang GitHub **hàng ngày** dưới dạng CSV.
- **Cập nhật chỉ khi có thay đổi** (không sao lưu trùng lặp).
- **Dễ theo dõi** với lịch sử thay đổi trên GitHub.
- **Không cần viết code** – chỉ cần cấu hình n8n là xong!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không phải thủ công sao lưu hàng ngày.
✅ **An toàn tuyệt đối** – Dữ liệu được sao lưu tự động hàng ngày.
✅ **Cập nhật chỉ khi có thay đổi** – Không tốn dung lượng GitHub không cần thiết.
✅ **Dễ theo dõi** – Tất cả lịch sử thay đổi được lưu trên GitHub.
✅ **Hoàn toàn tự động** – Chỉ cần bật workflow là xong!
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
- **Tài khoản GitHub** (và **Personal Access Token** với quyền `repo`).
- **Tài khoản PostgreSQL** (cung cấp **host, port, username, password, database name**).
- **Repository GitHub** để lưu trữ file CSV (cấu trúc: `postgres-backup/`).
- **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo an toàn và tự động hóa 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/7419](https://n8n.io/workflows/7419) và import vào n8n Editor.
- **Copy toàn bộ JSON** từ trang trên và **dán vào n8n Editor** (tab `Import`).

:::note[LƯU Ý]
- **Không chỉnh sửa cấu trúc** của workflow, chỉ cần **cấu hình credentials** như hướng dẫn dưới đây.
- **Không sử dụng phiên bản n8n cloud** – workflow này yêu cầu **self-hosted** để chạy 24/7.
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **12 node**, nhưng chỉ **3 node quan trọng** cần cấu hình kỹ:

##### **A. Cấu Hình Credentials PostgreSQL**
- **Node:** `List tables` và `List tables1` (cả hai đều dùng **credentials "postgres"**).
- **Cách cấu hình:**
  1. Vào **Credentials** trong n8n Editor.
  2. Tạo **mới một credential** với tên `"postgres"`.
  3. Điền thông tin:
     - **Host:** `your-postgres-host.com` (hoặc IP)
     - **Port:** `5432` (mặc định)
     - **Database:** `your-database-name`
     - **Username:** `your-postgres-username`
     - **Password:** `your-postgres-password`
  4. **Lưu** và **gán** cho cả hai node `List tables`.

##### **B. Cấu Hình Credentials GitHub**
- **Node:** `List files from repository [GITHUB]`, `Update file [GITHUB]`, `Upload file [GITHUB]` (cả ba đều dùng **credentials "githubOAuth2Api"**).
- **Cách cấu hình:**
  1. Vào **Credentials** trong n8n Editor.
  2. Tạo **mới một credential** với tên `"githubOAuth2Api"`.
  3. Chọn **GitHub OAuth 2.0 API**.
  4. **Login vào GitHub** và cấp quyền:
     - `repo` (để đọc và viết file).
     - `admin:repo_hook` (nếu cần thiết).
  5. **Lưu** và **gán** cho tất cả các node GitHub.

##### **C. Cấu Hình Repository GitHub**
- **Node:** `List files from repository [GITHUB]`.
- **Cách cấu hình:**
  - Trong **keyParameters**, điền:
    - **Repository:** `your-username/your-repo-name` (ví dụ: `jayemp0/postgres-backup`).
    - **Path:** `postgres-backup/` (đây là thư mục sẽ lưu file CSV).
  - **Lưu ý:** Nếu thư mục chưa tồn tại, **tạo nó trước** trên GitHub.

##### **D. Cấu Hình Lịch Trình Chạy (Schedule Trigger)**
- **Node:** `Daily Schedule`.
- **Cách cấu hình:**
  - Chọn **`Daily`** (hàng ngày).
  - **Time:** Đặt giờ sao lưu (ví dụ: **2 giờ sáng** để tránh ảnh hưởng đến hoạt động).
  - **Time Zone:** Chọn **UTC** hoặc **múi giờ của bạn**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **`Test`** trên node `Daily Schedule`.
   - Kiểm tra **log** để đảm bảo workflow chạy đúng.
2. **Bật Active workflow**:
   - Chuyển **switch Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi sao lưu thành công/lỗi:**
   - Thêm **node `slack`** hoặc **`telegram`** sau node `Upload file [GITHUB]` để báo cáo kết quả.

2. **Lưu log sao lưu vào file CSV riêng:**
   - Thêm **node `code`** để ghi log vào file `backup_log.csv` trong thư mục `postgres-backup/`.

3. **Sao lưu chỉ các bảng quan trọng:**
   - Thêm **node `if`** để lọc chỉ sao lưu các bảng có tên bắt đầu từ `tbl_` (hoặc tên cụ thể).

4. **Tự động xóa file cũ sau 30 ngày:**
   - Sử dụng **node `github`** với **operation `delete`** để xóa file CSV cũ hơn 30 ngày.

5. **Kết hợp với n8n Webhook để kích hoạt thủ công:**
   - Thêm **node `webhook`** để có thể kích hoạt sao lưu bất kỳ lúc nào.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp** khỏi việc **sao lưu thủ công hàng ngày**, đồng thời **đảm bảo dữ liệu an toàn** với lịch sử thay đổi rõ ràng trên GitHub.

**👉 Hãy áp dụng ngay để:**
✔ **Tiết kiệm thời gian** cho các công việc DevOps.
✔ **Tránh mất mát dữ liệu** nhờ sao lưu tự động.
✔ **Cập nhật chỉ khi có thay đổi** để tiết kiệm dung lượng.

**🚀 Bắt đầu tự động hóa ngay hôm nay!**
Nếu có bất kỳ câu hỏi, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Jay Emp0](https://n8n.io/workflows/7419) để hỗ trợ!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::