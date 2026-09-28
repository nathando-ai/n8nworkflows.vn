---
title: "🚀 Tự Động Cập Nhật n8n Self-Hosted Với Coolify – Không Cần Code!"
description: "Workflow tự động so sánh phiên bản n8n hiện tại với phiên bản mới nhất trên GitHub, tự động triển khai cập nhật qua Coolify khi có phiên bản mới. Giúp các sếp tiết kiệm thời gian và đảm bảo hệ thống luôn chạy phiên bản mới nhất."
slug: "tu-dong-cap-nhat-n8n-coolify"
tags: [n8n, automation, devops, self-hosted, coolify, github-api]
keywords: [tự động hóa n8n, cập nhật phiên bản n8n, coolify api, devops tự động, n8n self-hosted, github releases]
---

# 🚀 **Tự Động Cập Nhật n8n Self-Hosted Với Coolify – Không Cần Code!**

### **Nỗi Đau Của Các Sếp**
Làm thủ công việc kiểm tra và cập nhật phiên bản n8n trên máy chủ tự host là một công việc **tẻ nhạt, dễ quên** và **tốn thời gian**. Mỗi khi có phiên bản mới của n8n được phát hành trên GitHub, các sếp phải:
- **Tìm phiên bản mới nhất** trên GitHub.
- **So sánh phiên bản hiện tại** của n8n trên máy chủ.
- **Thực hiện thủ công** các bước cập nhật qua Coolify (hoặc dịch vụ tương tự).
- **Lo lắng** rằng có thể bỏ lỡ phiên bản mới và hệ thống không được tối ưu.

**Workflow này giải quyết tất cả!** Nó **tự động** kiểm tra phiên bản mới nhất trên GitHub, so sánh với phiên bản hiện tại của n8n trên máy chủ, và **triển khai cập nhật tự động** nếu có phiên bản mới hơn – **không cần code, không cần can thiệp thủ công!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra phiên bản thủ công hàng tuần.
- **Cập nhật tự động**: Hệ thống luôn chạy phiên bản mới nhất của n8n.
- **An toàn và ổn định**: Tránh bỏ lỡ các bản cập nhật quan trọng.
- **Hoạt động liên tục**: Dùng **Schedule Trigger** để chạy định kỳ (ví dụ: mỗi 6 giờ).
- **Hoàn toàn tự động**: Sau khi cấu hình, workflow **chạy một mình** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Coolify** (hoặc dịch vụ tương tự như Docker Compose, Rancher).
2. **API Token của Coolify** (để triển khai cập nhật).
3. **Địa chỉ URL của n8n self-hosted** (ví dụ: `https://n8n.tuduy.com`).
4. **Thông tin đăng nhập vào GitHub** (nếu cần, mặc dù workflow không yêu cầu auth cho API GitHub).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8118) hoặc copy/paste JSON từ đây vào **n8n Editor**.
- **Nhấp vào "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node**, nhưng các node quan trọng nhất cần cấu hình là:

##### **A. Node `Schedule Trigger` (Đặt lịch chạy)**
- Mở **Rule → Interval** và đặt thời gian chạy (ví dụ: **every 6 hours**).
- **Lưu ý**: Nếu muốn chạy ngay lập tức, có thể **bỏ qua node này** và dùng **Manual Trigger** (node sau).

##### **B. Node `HTTP Request` (Lấy phiên bản n8n hiện tại)**
- **URL**: `https://<your-n8n-domain>/rest/settings`
  - Ví dụ: `https://n8n.tuduy.com/rest/settings`
- **Method**: `GET`
- **Headers**: Không cần thêm (n8n mặc định cho phép truy cập công khai).
- **Output cần**: `data.versionCli` (phiên bản hiện tại của n8n).

##### **C. Node `HTTP Request` (Lấy phiên bản mới nhất từ GitHub)**
- **URL**: `https://api.github.com/repos/n8n-io/n8n/releases/latest`
- **Method**: `GET`
- **Headers**: Không cần auth (GitHub cho phép truy cập công khai).
- **Output cần**: `name` (ví dụ: `n8n@1.60.0`).

##### **D. Node `Set` (Normalize biến)**
- **Cấu hình 2 biến**:
  - `actualn8nversion = $json.versionCli` (phiên bản hiện tại).
  - `newn8nversion = $json.name.split('@')[1]` (phiên bản mới, lấy phần sau `@`).
  - **Kiểu dữ liệu**: **String**.

##### **E. Node `IF` (So sánh phiên bản)**
- **Điều kiện**: `actualn8nversion !== newn8nversion`
  - Nếu **true** → Triển khai cập nhật.
  - Nếu **false** → **Không làm gì** (`No-Op`).

##### **F. Node `HTTP Request` (Triển khai cập nhật qua Coolify)**
- **URL**: `https://<your-coolify-domain>/api/v1/services/<APP_UUID>/restart?latest=true`
  - Ví dụ: `https://coolify.tuduy.com/api/v1/services/12345678-1234-1234-1234-123456789abc/restart?latest=true`
- **Auth**: Chọn **HTTP Bearer Auth** và điền **API Token** của Coolify.
- **Headers**:
  - `Authorization: Bearer <your-coolify-token>`
- **Method**: `POST`

##### **G. Node `Manual Trigger` (Chạy thủ công)**
- Nếu muốn **test ngay lập tức**, nhấn **"Execute workflow"** mà không cần đợi lịch.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow và kiểm tra **node `IF`** có so sánh phiên bản đúng không.
   - Nếu có phiên bản mới, **node `HTTP Request` (Coolify)** sẽ tự động triển khai.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để nó hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu log cập nhật**:
   - Thêm **node `Slack`** hoặc **node `Email`** để thông báo khi có phiên bản mới được triển khai.
   - Ví dụ: Gửi tin nhắn Slack: *"n8n đã được cập nhật từ v1.59.0 → v1.60.0!"*

2. **Kết hợp với Telegram Bot**:
   - Sử dụng **node `Telegram Bot`** để nhận thông báo khi có phiên bản mới.

3. **Cài đặt alert cho phiên bản mới**:
   - Thêm **node `Webhook`** để khi có phiên bản mới, hệ thống tự động gửi email hoặc báo động.

4. **Chạy trên nhiều máy chủ**:
   - Sử dụng **node `Loop`** để chạy workflow cho nhiều instance n8n khác nhau.

5. **Backup trước khi cập nhật**:
   - Trước khi triển khai, thêm **node `Backup`** (nếu sử dụng Docker) để sao lưu trước.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp** khỏi việc phải kiểm tra và cập nhật phiên bản n8n thủ công. Với **tự động hóa hoàn toàn**, hệ thống của các sếp sẽ **luôn chạy phiên bản mới nhất**, an toàn và hiệu quả hơn.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình URL và API Token** của Coolify.
3. **Bật Schedule Trigger** để nó chạy tự động.
4. **Thưởng thức sự tự động hóa** mà không cần can thiệp!

**Nếu có vấn đề**, các sếp có thể liên hệ với tác giả [Edoardo Guzzi](https://n8n.io/workflows/8118) để hỗ trợ thêm! 🚀

---
**Chúc các sếp thành công với n8n và Coolify!** 💻✨