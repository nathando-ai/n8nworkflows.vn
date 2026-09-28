---
title: "🚀 Tự Động Hóa Đặt Lại Docker Immich Cho WHMCS/WISECP - API Backend Mạnh Mẽ Cho Doanh Nghiệp"
description: "Workflow này tự động hóa toàn bộ quy trình triển khai, quản lý và điều khiển Docker Immich từ xa thông qua API, giúp các sếp tiết kiệm thời gian và tối ưu hóa hiệu suất cho hệ thống lưu trữ ảnh cá nhân. Kết nối với WHMCS/WISECP để cung cấp dịch vụ lưu trữ đám mây tự động hóa 100%."
slug: "tieu-dong-hoa-deploy-docker-immich-cho-whmcs-wisecp"
tags: [n8n, automation, devops, docker, whmcs, wisecp, api-backend, self-hosted]
keywords: [tự động hóa docker immich, api backend cho whmcs, quản lý container docker, tự động hóa lưu trữ ảnh cá nhân, n8n workflow devops, triển khai docker từ xa]
---

# 🚀 **Tự Động Hóa Triển Khai Docker Immich Cho WHMCS/WISECP - API Backend Cho Doanh Nghiệp**

### **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Các sếp đang gặp khó khăn khi phải **quản lý thủ công** việc triển khai, khởi động, tắt, hoặc cập nhật Docker Immich (hệ thống lưu trữ ảnh cá nhân) cho khách hàng thông qua WHMCS/WISECP. Các thao tác này thường tốn thời gian, dễ sai sót, và không thể hoạt động liên tục 24/7. **Workflow này tự động hóa toàn bộ quy trình thông qua API**, giúp các sếp:
- **Khởi động/tắt container** chỉ với một cú nhấp chuột từ WHMCS/WISECP.
- **Quản lý tài nguyên** (disk, ACL, network) một cách tự động.
- **Cập nhật và triển khai** Docker Immich mới chỉ trong vài giây.
- **Tích hợp hoàn hảo** với hệ thống quản lý dịch vụ hiện có (WHMCS/WISECP).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên một VPS chuyên dụng với Docker sẵn có.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải login vào server mỗi khi quản lý container.
- **Chính xác 100%**: Tránh sai sót khi thực hiện các lệnh Docker thủ công.
- **Hoạt động liên tục**: API backend hoạt động 24/7, không phụ thuộc vào nhân viên.
- **Tích hợp hoàn hảo**: Kết nối trực tiếp với WHMCS/WISECP để tự động hóa dịch vụ lưu trữ ảnh.
- **An toàn và linh hoạt**: Sử dụng SSH và Basic Auth để bảo mật.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản WHMCS/WISECP** đã tích hợp với Docker Immich.
2. **Server Docker** đã cài đặt và chạy (cần hỗ trợ Docker API).
3. **Credentials cho n8n**:
   - **Basic Auth** (để API Webhook nhận dữ liệu từ WHMCS/WISECP).
   - **SSH Password** (để n8n kết nối và điều khiển Docker trên server).
4. **Tham số cấu hình** (cần chỉnh sửa trong node **Parameters**):
   - `server_domain` (phải khớp với domain của server Docker).
   - `clients_dir` (thư mục lưu trữ dữ liệu khách hàng).
   - `mount_dir` (điểm mount mặc định cho disk container).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không chỉnh sửa** các tham số kỹ thuật như `screen_left` và `screen_right`.
- Server phải có **Docker Engine** và **Docker Compose** hoạt động.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3212](https://n8n.io/workflows/3212) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này sử dụng **34 node** để điều khiển Docker Immich. Các bước quan trọng cần chú ý:

##### **A. Cấu Hình Credentials**
1. **Webhook API (Basic Auth)**:
   - Tạo **new credential** trong n8n với loại **HTTP Basic Auth**.
   - Điền **Username** và **Password** (sẽ được sử dụng để xác thực API từ WHMCS/WISECP).
   - **Path**: `docker-immich` (được định nghĩa trong node **API**).
   - **HTTP Method**: `POST`.

2. **SSH Access**:
   - Tạo **new credential** với loại **SSH Password**.
   - Điền **Host**, **Port** (mặc định là 22), **Username**, và **Password** của server Docker.

##### **B. Cấu Hình Tham Số (Node "Parameters")**
- Mở node **"Parameters"** → Chỉnh sửa JSON như sau:
  ```json
  {
    "server_domain": "your-server-domain.com",  // Thay bằng domain của server Docker
    "clients_dir": "/var/docker-clients",      // Thư mục lưu trữ khách hàng
    "mount_dir": "/mnt/docker-disks",          // Điểm mount mặc định (không thay đổi)
    "screen_left": 100,                       // Không chỉnh sửa
    "screen_right": 200                       // Không chỉnh sửa
  }
  ```

##### **C. Cấu Hình Node "API"**
- Node này là **Webhook** nhận dữ liệu từ WHMCS/WISECP.
- **Credentials**: Chọn **HTTP Basic Auth** đã tạo trước đó.
- **Key Parameters**:
  - `path`: `docker-immich` (không đổi).
  - `httpMethod`: `POST` (không đổi).

##### **D. Cấu Hình Node "SSH"**
- Node này thực hiện các lệnh Docker trên server.
- **Credentials**: Chọn **SSH Password** đã tạo.
- **Command Template**: Sẽ tự động được xây dựng từ các node **Set** sau (không cần chỉnh sửa thủ công).

##### **E. Cấu Hình Node "Switch" (Container Actions & Service Actions)**
- Các node này **lựa chọn hành động** dựa trên input từ WHMCS/WISECP.
- Ví dụ:
  - Nếu input là `start`, workflow sẽ chạy node **Start**.
  - Nếu input là `stop`, workflow sẽ chạy node **Stop**.

##### **F. Cấu Hình Node "Set" (Các hành động cụ thể)**
Các node **Set** này định nghĩa **lệnh Docker** sẽ được gửi qua SSH:
- **Start**: Khởi động container.
- **Stop**: Dừng container.
- **Deploy**: Triển khai Docker Compose mới.
- **Inspect**: Kiểm tra thông tin container.
- **Log**: Lấy log container.
- **Mount Disk/Unmount Disk**: Quản lý disk mount.
- **GET ACL/SET ACL**: Quản lý quyền truy cập.
- **GET NET**: Kiểm tra mạng container.

##### **G. Node "If" & "If1"**
- Node này **kiểm tra điều kiện** trước khi thực hiện hành động.
- Ví dụ: Trước khi deploy, nó sẽ kiểm tra container có tồn tại không.

##### **H. Node "RespondToWebhook"**
- Sau khi hoàn thành hành động, node này **trả về phản hồi** cho WHMCS/WISECP.
- Ví dụ:
  - Nếu thành công: `{"status": "success", "message": "Container started"}`.
  - Nếu lỗi: `{"status": "error", "message": "Invalid server domain"}`.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với một **dữ liệu mẫu** (ví dụ: `{"action": "start"}`).
- **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động liên tục.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo kết quả triển khai cho team.
   - Ví dụ: Khi container khởi động thành công, gửi tin nhắn Slack: `🚀 Container Immich đã khởi động thành công cho khách hàng [Tên Khách Hàng]`.

2. **Lưu Log Tự Động**:
   - Sử dụng node **Set** kết hợp với **HTTP Request** để lưu log vào một file hoặc cơ sở dữ liệu (ví dụ: Google Sheets).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node **Schedule** để chạy workflow hàng ngày và gửi báo cáo tình trạng container cho quản lý.

4. **Quản Lý Múlti Server**:
   - Sử dụng **Credentials SSH khác** để quản lý nhiều server Docker từ một workflow duy nhất.

5. **Cập Nhật Docker Immich**:
   - Tạo một **button trong WHMCS/WISECP** gọi workflow với `{"action": "deploy"}` để cập nhật phiên bản mới.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc quản lý Docker Immich thủ công, đồng thời **tăng cường tính tự động hóa** cho hệ thống WHMCS/WISECP. Với **API backend mạnh mẽ**, các sếp có thể:
✅ **Khởi động/tắt container** chỉ với một cú nhấp chuột.
✅ **Quản lý tài nguyên** (disk, ACL, network) một cách tự động.
✅ **Cập nhật và triển khai** Docker Immich mới chỉ trong vài giây.
✅ **Tích hợp hoàn hảo** với hệ thống quản lý dịch vụ hiện có.

**Hãy áp dụng ngay workflow này và nâng cao hiệu suất dịch vụ lưu trữ ảnh của doanh nghiệp!** 🚀

---
:::note[Liên Hệ Với PUQcloud]
Nếu cần hỗ trợ thêm hoặc có yêu cầu tùy chỉnh, liên hệ với **PUQcloud** (công ty phát triển workflow này):
- [Trang web](https://puqcloud.com/)
- [Tài liệu chi tiết](https://doc.puq.info/books/docker-immich-whmcs-module)
- [Module WHMCS](https://puqcloud.com/whmcs-module-docker-immich.php)
:::