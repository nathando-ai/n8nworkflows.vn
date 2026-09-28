---
title: "🚀 Tự Động Hóa Kiểm Tra Sử Dụng Tài Nguyên VPS Mỗi 15 Phút - Giám Sát CPU, RAM & Disk 24/7"
description: "Workflow tự động hóa kiểm tra sử dụng tài nguyên VPS (CPU, RAM, Disk) mỗi 15 phút và cảnh báo qua email khi vượt ngưỡng 80%. Giúp các sếp quản lý hiệu suất server an toàn, tránh tình trạng overloading và downtime."
slug: "tieu-dong-hoa-kiem-tra-su-dung-tai-nguyen-vps"
tags: [n8n, devops, tự động hóa, giám sát server, vps, ssh]
keywords: [n8n workflow giám sát VPS, tự động hóa kiểm tra tài nguyên server, cảnh báo CPU RAM Disk, tự động hóa DevOps, n8n scheduleTrigger]
---

# 🚀 **Giám Sát Tài Nguyên VPS 24/7 - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Quản Lý VPS**
Quản lý một VPS hiệu quả không chỉ là vấn đề về chi phí mà còn liên quan trực tiếp đến **trải nghiệm người dùng**, **tính ổn định của ứng dụng** và **tính kinh tế** của doanh nghiệp. Các tình huống thường gặp:
- **CPU overloading**: Ứng dụng chậm, người dùng bị timeout, mất doanh thu.
- **RAM đầy**: Server bị treo, dịch vụ ngừng hoạt động đột ngột.
- **Disk nearly full**: Không thể lưu log, backup hoặc cài đặt mới.
- **Không cảnh báo kịp thời**: Tình trạng xấu đi mà không biết, dẫn đến downtime không cần thiết.

**Workflow này giải quyết tất cả!** Nó tự động **kiểm tra CPU, RAM và Disk usage** mỗi **15 phút**, so sánh với ngưỡng **80%** và **gửi email cảnh báo** nếu tài nguyên bị quá tải. **Không cần viết một dòng code**, chỉ cần **cấu hình SSH và email** là xong!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát liên tục**: Kiểm tra tài nguyên **mỗi 15 phút** mà không cần can thiệp thủ công.
- **Cảnh báo kịp thời**: Nhận email ngay khi CPU/RAM/Disk vượt ngưỡng **80%** (có thể điều chỉnh).
- **Tiết kiệm chi phí**: Tránh tình trạng **overloading** dẫn đến **downtime** hoặc **upgrade VPS không cần thiết**.
- **Tự động hóa DevOps**: Giúp các sếp **focusing** vào chiến lược kinh doanh thay vì quản lý server.
- **An toàn và tin cậy**: Không phụ thuộc vào công cụ giám sát bên thứ ba (n8n self-hosted).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản email** (để nhận cảnh báo):
   - **SMTP credentials** (tên miền, port, username, password, SSL/TLS).
   - **Email From** và **Email To** (cần cập nhật trong node `Send Email`).
2. **Thông tin SSH để kết nối VPS**:
   - **Hostname/IP** của VPS.
   - **Username** và **Password** (hoặc **SSH Key** nếu ưu tiên).
   - **Port SSH** (thường là `22`).
3. **Ngưỡng cảnh báo** (mặc định là **80%** cho CPU/RAM/Disk, có thể điều chỉnh).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n Workflow](https://n8n.io/workflows/2951) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** (trang chủ của n8n) → **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình SSH (3 Node)**
Tất cả 3 node `Check RAM`, `Check CPU`, `Check Disk` **sử dụng cùng một credentials SSH**:
1. **Tạo credentials SSH**:
   - Trong n8n Editor → **Credentials** → **Add Credential** → Chọn **SSH Password**.
   - Điền:
     - **Host**: `IP_VPS` (ví dụ: `123.45.67.89`).
     - **Port**: `22` (mặc định).
     - **Username**: `root` hoặc tài khoản admin.
     - **Password**: Mật khẩu SSH của VPS.
     - **Private Key** (nếu sử dụng SSH Key, bỏ trống Password).
2. **Gán credentials cho 3 node SSH**:
   - Mở từng node (`Check RAM`, `Check CPU`, `Check Disk`) → **Credentials** → Chọn **sshPassword** vừa tạo.

##### **B. Cấu Hình Email (Node `Send Email`)**
1. **Tạo credentials SMTP**:
   - Trong n8n Editor → **Credentials** → **Add Credential** → Chọn **SMTP**.
   - Điền thông tin SMTP của nhà cung cấp email (ví dụ Gmail, Zoho, hoặc SMTP của VPS):
     - **Host**: `smtp.gmail.com` (hoặc `smtp.zoho.com`).
     - **Port**: `587` (hoặc `465` nếu SSL).
     - **Username**: `email@domain.com`.
     - **Password**: Mật khẩu ứng dụng (nếu sử dụng Gmail, tạo ở [My Account → Security](https://myaccount.google.com/security)).
     - **SSL/TLS**: `STARTTLS` (hoặc `SSL`).
2. **Cập nhật email From/To**:
   - Mở node `Send Email` → **Email From**: `noreply@domain.com` (email gửi).
   - **Email To**: `admin@domain.com` (email nhận cảnh báo).
   - **Subject**: `🚨 Cảnh báo: Tài Nguyên VPS Quá Tải!` (có thể chỉnh).
   - **Body**: Nội dung email mẫu (có thể chỉnh sửa để thêm thông tin chi tiết).

##### **C. Cấu Hình Ngưỡng Cảnh Báo (Node `Check results against thresholds`)**
1. Mở node `Check results against thresholds` (node `if`).
2. **Cập nhật ngưỡng**:
   - **CPU**: `80` (mặc định).
   - **RAM**: `80` (mặc định).
   - **Disk**: `80` (mặc định).
   - **Điều chỉnh** nếu cần (ví dụ: `90%` cho CPU).

##### **D. Kích Hoạt Schedule Trigger**
- Node `Schedule Trigger` đã được cấu hình **mỗi 15 phút** (`*/15 * * * *`).
- **Không cần chỉnh** trừ khi muốn thay đổi thời gian kiểm tra (ví dụ: `*/30 * * * *` để kiểm tra mỗi 30 phút).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra nếu cấu hình đúng.
   - Kiểm tra email nhận được cảnh báo (nếu có).
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Log Lịch Sử**:
   - Sử dụng **node `stickyNote`** để lưu lịch sử cảnh báo vào một file JSON hoặc Google Sheets.
   - **Cách làm**:
     - Thêm node `stickyNote` sau node `Send Email`.
     - Cấu hình để lưu dữ liệu vào một **stickyNote** với tên `vps_alerts`.
     - Sau đó, kết nối với **Google Sheets** hoặc **file JSON** để lưu trữ dài hạn.

2. **Gửi Cảnh Báo Đến Slack/Telegram**:
   - Thay thế node `Send Email` bằng **node `slack`** hoặc **node `telegram`**.
   - Cấu hình webhook từ Slack/Telegram và gửi thông báo tự động.

3. **Tự Động Scale Up VPS**:
   - Kết hợp với **node `httpRequest`** để gọi API của nhà cung cấp VPS (ví dụ: Cloudways, Vultr) để **upgrade tài nguyên** khi vượt ngưỡng.
   - Ví dụ: Nếu Disk > 90%, tự động **mở rộng ổ đĩa**.

4. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `scheduleTrigger`** khác để gửi **báo cáo tuần/month** về sử dụng tài nguyên qua email.
   - Nội dung bao gồm:
     - Thống kê CPU/RAM/Disk trong tuần.
     - Lịch sử cảnh báo.
     - Đề xuất tối ưu hóa.

5. **Kết Nối Với Monitoring Tools**:
   - Gửi dữ liệu đến **Prometheus**, **Grafana**, hoặc **Datadog** để tích hợp với hệ thống giám sát hiện có.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **giám sát VPS một cách tự động hóa**, **tiết kiệm thời gian** và **tránh downtime** không cần thiết. Với **n8n**, bạn không cần là nhà phát triển để xây dựng hệ thống giám sát chuyên nghiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình SSH và email** theo hướng dẫn.
3. **Bật Active** và **quên đi lo lắng** về tài nguyên VPS!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/). Chúc các sếp thành công! 🚀

---