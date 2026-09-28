---
title: "🔄 **Sao lưu & Khôi phục Workflow & Credentials n8n Docker bằng GitHub & SSH - Giải pháp Tự động hóa 100% An toàn**"
description: "Workflow tự động sao lưu toàn bộ workflow và credentials của n8n Docker vào GitHub và khôi phục lại một cách an toàn khi cần. Giúp các sếp bảo vệ dữ liệu quan trọng, tránh mất mát do lỗi hệ thống hoặc xóa nhầm, đồng thời hỗ trợ quản lý phiên bản dễ dàng."
slug: "sao-luu-khoi-phuc-n8n-docker-voi-github-ssh"
tags: [n8n, automation, docker, backup-restore, github, ssh, no-code, business-automation]
keywords: [sao lưu n8n docker, khôi phục workflow n8n, backup credentials n8n, tự động hóa n8n docker, lưu trữ an toàn workflow, khôi phục dữ liệu n8n]
---

# 🔄 **Sao lưu & Khôi phục Workflow & Credentials n8n Docker bằng GitHub & SSH**

## **Giới thiệu: Tại sao các sếp cần sao lưu n8n Docker?**
Hiện nay, khi xây dựng hệ thống tự động hóa với **n8n Docker**, các sếp thường gặp phải những vấn đề sau:
- **Mất dữ liệu khi hệ thống bị lỗi**: Một lỗi hệ thống hoặc xóa nhầm container Docker có thể khiến toàn bộ workflow và credentials bị mất vĩnh viễn.
- **Không có bản sao dự phòng**: Nếu không có sao lưu, việc khôi phục lại trạng thái cũ sau một sự cố trở nên cực kỳ khó khăn.
- **Quản lý phiên bản khó khăn**: Khi có nhiều người làm việc trên cùng một hệ thống, việc theo dõi và khôi phục phiên bản cũ trở nên phức tạp.
- **Rủi ro khi sử dụng credentials không an toàn**: Nếu credentials bị lộ hoặc bị xóa, hệ thống tự động hóa sẽ ngừng hoạt động.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Sao lưu tự động** toàn bộ workflow và credentials của n8n Docker vào **GitHub** (private repository) theo lịch trình.
✅ **Khôi phục một cách an toàn** khi cần, chỉ với một vài bước nhấp chuột.
✅ **Bảo mật tuyệt đối** với SSH và Basic Auth, đảm bảo dữ liệu không bị lộ.
✅ **Hỗ trợ khôi phục từng workflow/credentials riêng lẻ** hoặc toàn bộ hệ thống.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ dữ liệu quan trọng**: Sao lưu tự động hàng ngày, tuần hoặc tháng tùy chọn.
- **Khôi phục nhanh chóng**: Khôi phục lại toàn bộ hệ thống hoặc chỉ một workflow/credentials cụ thể.
- **An toàn tuyệt đối**: Sử dụng **SSH** để kết nối Docker và **GitHub private repo** để lưu trữ.
- **Quản lý phiên bản dễ dàng**: Theo dõi lịch sử thay đổi và khôi phục bất kỳ phiên bản nào.
- **Tiết kiệm thời gian**: Không cần phải thủ công export/import dữ liệu khi có sự cố.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **n8n Docker** đang chạy trên một **Linux server** (Ubuntu, CentOS, etc.).
2. **GitHub Account** với một **private repository** để lưu trữ backup.
3. **SSH Access** đến máy chủ Docker (cần cấu hình **SSH Password Authentication** trong n8n).
4. **Basic Auth** cho form upload khôi phục (để bảo mật form restore).
5. **N8N_ENCRYPTION_KEY** (nếu đã cấu hình mã hóa cho credentials).
6. **Docker Container Name** của n8n (để workflow biết nơi import/export dữ liệu).
7. **Credentials trong n8n**:
   - `githubApi` (để push/pull dữ liệu từ GitHub).
   - `sshPassword` (để kết nối SSH với máy chủ Docker).
   - `httpBasicAuth` (để bảo mật form upload khôi phục).

**📌 Lưu ý quan trọng:**
- **Không sử dụng public repository** cho credentials (rủi ro bảo mật cao).
- **Không chia sẻ `N8N_ENCRYPTION_KEY`** với bất kỳ ai.
- **Test restore trên staging** trước khi áp dụng vào production.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/16191](https://n8n.io/workflows/16191) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (đảm bảo không có lỗi syntax).

:::note[LƯU Ý]
- **Không kích hoạt workflow ngay lập tức**! Các sếp cần cấu hình **credentials** trước.
- **Sử dụng phiên bản n8n mới nhất** để tránh lỗi tương thích.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Backup Configuration (Node `Backup Configuration`)**
- **Tham số cần điền:**
  - `githubOwner`: Tên chủ sở hữu GitHub repository.
  - `githubRepository`: Tên repository private.
  - `dockerContainerName`: Tên container Docker của n8n (vd: `n8n-main`).
  - `backupFolderName`: Tên folder backup (vd: `n8n-backups`).
  - `githubBranch`: Branch để lưu backup (vd: `main` hoặc `backup`).

#### **B. Cấu hình SSH (Node `sshPassword`)**
- **Tham số cần điền:**
  - **Host**: IP hoặc domain của máy chủ Linux.
  - **Port**: Cổng SSH (thường là `22`).
  - **Username**: Tên người dùng SSH (vd: `root` hoặc `ubuntu`).
  - **Password**: Mật khẩu SSH (hoặc sử dụng **SSH Key** nếu ưu tiên).

#### **C. Cấu hình GitHub (Node `githubApi`)**
- **Tham số cần điền:**
  - **Token**: Token Personal Access Token của GitHub (có quyền `repo`).
  - **Repository**: Chọn repository private đã tạo.

#### **D. Cấu hình Form Upload (Node `Upload Restore File`)**
- **Tham số cần điền:**
  - **Basic Auth**: Cấu hình username/password để bảo mật form.
  - **HTTPS**: Đảm bảo form chỉ hoạt động trên HTTPS (không HTTP).

#### **E. Cấu hình Credentials (Node `N8N_ENCRYPTION_KEY`)**
- **Nếu đã cấu hình mã hóa cho credentials:**
  - Thêm `N8N_ENCRYPTION_KEY` vào **Environment Variables** của container Docker.
  - **Không bao giờ chia sẻ key này!**

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow với **Schedule Trigger** (hoặc kích hoạt manual).
   - Kiểm tra log để đảm bảo backup được tạo thành công.
2. **Bật Active workflow**:
   - Sau khi cấu hình xong, các sếp có thể **bật workflow** và đặt lịch trình sao lưu (vd: hàng ngày lúc 2 giờ sáng).

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa sao lưu**
- **Sử dụng SSH Key** thay vì mật khẩu để tăng bảo mật.
- **Tạo branch riêng** cho mỗi phiên bản backup (vd: `backup-2024-05-01`).
- **Lưu trữ backup ngoài GitHub** (vd: AWS S3, Google Drive) để có bản sao dự phòng.

### **2. Khôi phục linh hoạt**
- **Khôi phục từng workflow/credentials riêng lẻ** (đơn giản hơn khôi phục toàn bộ).
- **So sánh phiên bản** trước khi khôi phục để tránh xung đột.
- **Kích hoạt workflow sau khi khôi phục** (do n8n sẽ deactivate workflow sau khi import).

### **3. Bảo mật nâng cao**
- **Khóa form upload** với CAPTCHA hoặc IP whitelist.
- **Xóa credentials cũ** sau khi khôi phục thành công.
- **Monitor log** để phát hiện bất kỳ hoạt động nghi ngờ nào.

### **4. Tích hợp với Slack/Telegram**
- **Gửi thông báo** khi backup thành công/lỗi qua Slack/Telegram.
- **Tự động khôi phục** khi phát hiện lỗi hệ thống (vd: sử dụng **n8n Webhook** + **Monitoring Tool**).

---

## 📌 **Kết luận**

Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa **sao lưu và khôi phục n8n Docker** một cách an toàn và hiệu quả. Với **GitHub private repo** và **SSH**, dữ liệu của bạn được bảo vệ tuyệt đối, đồng thời có thể khôi phục lại trạng thái cũ chỉ trong vài phút khi cần.

**🚀 Hãy áp dụng ngay để bảo vệ hệ thống tự động hóa của mình!**
- **Bắt đầu với một backup hàng ngày** để tránh mất mát dữ liệu.
- **Test restore trên staging** trước khi áp dụng vào production.
- **Cập nhật thường xuyên** để đảm bảo workflow luôn hoạt động ổn định.

---
:::success[Hành động tiếp theo]
1. **Cài đặt VPS** để self-host n8n (nếu chưa có).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Cấu hình workflow** theo hướng dẫn trên.

3. **Bật backup tự động** và yên tâm với hệ thống an toàn!
:::

---
**💡 Cần hỗ trợ thêm?**
- **Hỏi đáp trên [Community n8n](https://community.n8n.io/)**.
- **Liên hệ tác giả** (Hồ Đình Huy) qua [LinkedIn](https://www.linkedin.com/in/hodinhhuy/) hoặc email.