---
title: "🚀 Tự Động Hóa Đặt Lại Docker Grafana + Backend API cho WHMCS/WISECP - Không Cần Code"
description: "Workflow này tự động hóa việc triển khai Docker Grafana và backend API cho WHMCS/WISECP, giúp các sếp quản lý dịch vụ cloud một cách nhanh chóng, chính xác và không cần viết dòng code nào. Giảm thời gian triển khai từ 30 phút xuống chỉ 10 giây!"
slug: "tieu-dong-hoa-deploy-docker-grafana-api-whmcs-wisecp"
tags: [n8n, automation, docker, whmcs, wisecp, ssh, api-backend, no-code]
keywords: [n8n workflow docker grafana, tự động hóa whmcs wisecp, deploy backend api không code, quản lý container docker tự động, tự động hóa cloud hosting]
---

# 🚀 **Tự Động Hóa Triển Khai Docker Grafana + Backend API cho WHMCS/WISECP - Không Cần Code**

### **🔥 Giải Pháp Cho Nỗi Đau Của Các Sếp Hosting**
Bạn đã bao giờ phải **tốn thời gian thủ công** để cài đặt lại Docker Grafana và backend API cho WHMCS/WISECP mỗi khi có yêu cầu mới? Hoặc phải **lo lắng về sự cố** khi cấu hình sai dẫn đến downtime? Với workflow này, các sếp sẽ:
✅ **Triển khai Docker Grafana + Backend API chỉ trong 10 giây** thay vì 30 phút thủ công.
✅ **Tự động quản lý container** (start/stop, mount/unmount disk, thay đổi ACL, password...) chỉ bằng API.
✅ **Không cần viết code** - toàn bộ logic được tự động hóa qua n8n.
✅ **Giảm thiểu lỗi nhân sự** khi cấu hình thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh phụ thuộc vào phiên bản miễn phí có giới hạn.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Tiết Kiệm Thời Gian**   | Triển khai Docker Grafana + Backend API chỉ trong **10 giây** thay vì 30 phút thủ công. |
| **Chính Xác 100%**        | Không còn lo lắng về **cấu hình sai** dẫn đến lỗi hoặc downtime.           |
| **Quản Lý Tự Động**      | Start/stop container, thay đổi ACL, password, mount disk... **chỉ bằng API**. |
| **Hoạt Động 24/7**       | Workflow chạy **liên tục** mà không cần can thiệp của con người.            |
| **Cá Nhân Hóa**           | Mỗi khách hàng có thể **cấu hình riêng** container của mình một cách dễ dàng. |

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
✔ **Một máy chủ VPS** với Docker đã cài đặt (Ubuntu/CentOS).
✔ **Tài khoản SSH** có quyền root hoặc sudo để quản lý Docker.
✔ **Domain WHMCS/WISECP** đã cấu hình sẵn.
✔ **API Key** cho n8n (để tạo credential Basic Auth).
✔ **Dữ liệu cấu hình** sau (sẽ được điền trong workflow):
   - `server_domain` (phải khớp với domain của WHMCS/WISECP).
   - `clients_dir` (thư mục lưu trữ dữ liệu Docker).
   - `mount_dir` (điểm mount mặc định cho disk container).

---
:::note[Lưu Ý Quan Trọng]
- **Không thay đổi** các tham số kỹ thuật như `screen_left` và `screen_right` (được thiết kế sẵn cho module PUQcloud).
- **Domain `server_domain` phải chính xác** để API hoạt động.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải workflow từ [n8n.io/workflows/4011](https://n8n.io/workflows/4011) hoặc copy JSON từ file.
**Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
**Bước 3:** Chọn **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **32 node** với logic phức tạp. Các bước quan trọng cần chú ý:

##### **A. Cấu Hình Credential API Webhook (Node: "API")**
- **Tạo credential Basic Auth** trong n8n:
  1. Vào **Credentials** → **"Add"** → Chọn **"HTTP Basic Auth"**.
  2. Đặt tên credential (ví dụ: `whmcs-api-cred`).
  3. Nhập **Username & Password** (sẽ được sử dụng cho API).
- **Cấu hình Node "API":**
  - **Credentials:** Chọn credential Basic Auth vừa tạo.
  - **Path:** Đặt là `docker-grafana`.
  - **HTTP Method:** Chỉ chọn `POST`.

##### **B. Cấu Hình Credential SSH (Node: "SSH")**
- **Tạo credential SSH Password** trong n8n:
  1. Vào **Credentials** → **"Add"** → Chọn **"SSH Password"**.
  2. Đặt tên credential (ví dụ: `vps-ssh-cred`).
  3. Nhập:
     - **Host:** IP hoặc domain của VPS.
     - **Port:** 22 (mặc định).
     - **Username:** Tài khoản SSH (thường là `root` hoặc `ubuntu`).
     - **Password:** Mật khẩu SSH.
- **Cấu hình Node "SSH":**
  - **Credentials:** Chọn credential SSH vừa tạo.

##### **C. Cấu Hình Tham Số (Node: "Parameters")**
- Mở node **"Parameters"** và cập nhật các giá trị sau:
  ```json
  {
    "server_domain": "domain-cua-ban.com", // Thay bằng domain WHMCS/WISECP
    "clients_dir": "/var/docker/clients", // Thư mục lưu dữ liệu Docker
    "mount_dir": "/mnt/docker-disks"      // Điểm mount mặc định (không thay đổi)
  }
  ```
  - **Không chỉnh sửa** `screen_left` và `screen_right`.

##### **D. Cấu Hình Node "If" & "Switch"**
- Node **"If"** kiểm tra điều kiện trước khi thực hiện hành động (ví dụ: kiểm tra container có tồn tại không).
- Node **"Switch"** quyết định hành động dựa trên input (ví dụ: start/stop container, mount/unmount disk).
  - **Cấu hình các case trong "Switch":**
    - **Container Actions:** Chỉnh sửa logic start/stop/inspect container.
    - **Service Actions:** Chỉnh sửa logic quản lý dịch vụ (deploy, suspend, unsuspend).
    - **Grafana:** Chỉnh sửa logic liên quan đến Grafana (GET/SET ACL, NET).

##### **E. Cấu Hình Node "Code" (Node: "Code1")**
- Node này xử lý logic **xử lý lỗi 422 (Invalid server domain)**.
- **Mở node "Code1"** và kiểm tra code JavaScript:
  ```javascript
  // Kiểm tra nếu server_domain không hợp lệ
  if (!json.server_domain || json.server_domain === "") {
    return { json: { error: "Invalid server domain" } };
  }
  return { json: {} };
  ```
  - **Không chỉnh sửa** nếu không hiểu code.

##### **F. Cấu Hình Node "Deploy-docker-compose"**
- Node này **triển khai Docker Compose** từ file `docker-compose.yml`.
- **Kiểm tra file `docker-compose.yml`** trên VPS:
  ```yaml
  version: '3'
  services:
    grafana:
      image: grafana/grafana
      ports:
        - "3000:3000"
      volumes:
        - grafana-storage:/var/lib/grafana
    backend:
      image: puqcloud/backend-api
      ports:
        - "8080:8080"
      volumes:
        - ./clients:/var/clients
  volumes:
    grafana-storage:
  ```
  - **Nếu file khác**, cần cập nhật trong node **"Deploy-docker-compose"**.

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** **Test Run** với dữ liệu mẫu:
1. Gửi một **request POST** đến Webhook API (địa chỉ: `http://<n8n-domain>/docker-grafana`).
2. Nhập payload ví dụ:
   ```json
   {
     "action": "deploy",
     "server_domain": "domain-cua-ban.com",
     "client_id": "12345"
   }
   ```
3. Kiểm tra **log** trong n8n để xác nhận workflow chạy thành công.

**Bước 2:** Bật **Active** workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram để báo cáo trạng thái:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo khi triển khai thành công/thất bại.
   - Ví dụ: Khi `action: "deploy"`, gửi tin nhắn: *"✅ Docker Grafana đã triển khai thành công cho domain: domain-cua-ban.com"*.

2. **Lưu Log Triển Khai:**
   - Sử dụng node **Set** kết hợp với **Google Sheets** hoặc **AWS S3** để lưu lịch sử triển khai.
   - Cập nhật các thông tin như:
     - Thời gian triển khai.
     - ID khách hàng.
     - Trạng thái (success/failure).

3. **Tự Động Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **n8n Cron** để chạy workflow hàng ngày và gửi báo cáo tổng hợp về trạng thái container.
   - Ví dụ: *"Báo cáo trạng thái Docker Grafana - Ngày 10/10/2024"* với danh sách container đang hoạt động.

4. **Cá Nhân Hóa Cho Khách Hàng:**
   - Cho phép khách hàng **chỉnh sửa cấu hình container** thông qua một **form web** kết nối với n8n.
   - Ví dụ: Khách hàng có thể yêu cầu **thay đổi password**, **mount disk mới** chỉ bằng một cú click.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp hosting muốn **tự động hóa triển khai Docker Grafana + Backend API cho WHMCS/WISECP** mà **không cần viết code**. Với chỉ **10 giây**, các sếp có thể triển khai container một cách **nhanh chóng, chính xác và an toàn**.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho đội ngũ IT của mình!**
Nếu có vấn đề, hãy tham khảo [đọc tài liệu chính thức của PUQcloud](https://doc.puq.info/books/docker-grafana-whmcs-module) hoặc liên hệ với [PUQcloud](https://puqcloud.com/) để hỗ trợ kỹ thuật.

---
**💡 Mẹo cuối:** Nếu workflow gặp lỗi, hãy kiểm tra **log SSH** và **log n8n** để xác định nguyên nhân. Thường là do **credential sai** hoặc **cấu hình Docker không đúng**.