---
title: "🚀 Tự Động Hóa Backup Rsync Bằng Mật Khẩu + Hệ Thống Cảnh Báo Telegram & SMS (N8N)"
description: "Giải pháp tự động hóa backup dữ liệu giữa các server SSH bằng rsync, tự động cài đặt phụ thuộc, kiểm tra và gửi báo cáo trạng thái qua Telegram/SMS. Phù hợp cho doanh nghiệp cần bảo mật cao và tự động hóa 24/7."
slug: "tuy-dong-hoa-backup-rsync-ssh-password-notification"
tags: [n8n, automation, backup, ssh, rsync, telegram, sms, server, no-code]
keywords: [tự động hóa backup rsync n8n, backup server ssh bằng mật khẩu, cảnh báo telegram sms n8n, tự động hóa dữ liệu doanh nghiệp, backup tự động 24/7]
---

# 🚀 **Tự Động Hóa Backup Rsync Bằng Mật Khẩu + Hệ Thống Cảnh Báo Telegram & SMS**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm thời gian** bằng việc tự động hóa backup dữ liệu giữa các server SSH.
- **Đảm bảo bảo mật** với xác thực bằng mật khẩu (không cần SSH keys).
- **Nhận báo cáo trạng thái** ngay lập tức qua Telegram và SMS khi backup thành công/thất bại.
- **Không cần cài đặt thủ công** các phụ thuộc (sshpass, rsync) – workflow tự động kiểm tra và cài đặt.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Backup tự động 24/7** giữa các server, không phụ thuộc vào nhân viên.
- **Bảo mật cao** với xác thực bằng mật khẩu (không cần SSH keys).
- **Cảnh báo tức thời** khi backup thành công/thất bại qua Telegram và SMS.
- **Không cần can thiệp thủ công** – workflow tự động cài đặt phụ thuộc (sshpass, rsync) nếu thiếu.
- **Dữ liệu đồng bộ hóa chính xác** với tùy chọn `--delete` (xóa file thừa trên máy đích).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **Thông tin Server (Source & Target)**
| Thông tin          | Source Server               | Target Server               |
|--------------------|----------------------------|----------------------------|
| Host               | `source_host`               | `target_host`               |
| Port               | `source_port` (thường 22)  | `target_port` (thường 22)  |
| Username           | `source_user`               | `target_user`               |
| Mật khẩu          | `source_password`           | `target_password`           |
| Thư mục nguồn    | `source_folder`             | `target_folder`             |

### **Thông tin Rsync**
- **Tùy chọn mặc định:** `-avz --delete` (archive, verbose, compress, mirror).
- **Thư mục nguồn/target** phải tồn tại trên cả hai server.

### **Thông tin Cảnh Báo**
| Thông tin               | Giá trị cần thay thế                     |
|-------------------------|------------------------------------------|
| Telegram Bot Token      | `YOUR-TELEGRAM-BOT-TOKEN`                |
| Telegram Channel ID     | `YOUR-TELEGRAM-CHANNEL-ID`               |
| Số điện thoại (SMS)    | `+36301234567` (đổi thành số của bạn)   |
| API Key TextBelt        | `YOUR-TEXTBELT-API-KEY`                  |

### **Hệ điều hành hỗ trợ**
- Ubuntu, Debian, RHEL, CentOS, Alpine.

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/9873) hoặc copy toàn bộ JSON từ canvas.
- **Bước 2:** Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.
- **Bước 3:** Workflow sẽ hiển thị với **14 node** như mô tả dưới đây.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow bao gồm **14 node** với logic phân nhánh và kiểm tra. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: Manual Trigger**
- **Chức năng:** Khởi động workflow thủ công (hoặc kết hợp với `Schedule Trigger`).
- **Lưu ý:** Nếu muốn chạy tự động, **bật `Schedule Trigger`** (node 14) với lịch trình mong muốn (ví dụ: hàng ngày 2 giờ sáng).

#### **🔹 Node 2-7: Kiểm tra & Cài đặt phụ thuộc (sshpass, rsync)**
Workflow tự động kiểm tra và cài đặt `sshpass` trên **máy nguồn và máy đích** nếu thiếu. Các bước:
1. **Check Sshpass Local** (Node 3): Kiểm tra `sshpass` có cài trên máy chạy n8n không.
2. **Is Installed Local?** (Node 4): Nếu thiếu, cài đặt bằng `apt/yum/dnf/apk` (Node 5).
3. **Check Sshpass on Source** (Node 6): Kiểm tra `sshpass` trên **máy nguồn**.
4. **Is Installed on Source?** (Node 7): Nếu thiếu, cài đặt trên máy nguồn (Node 8).

#### **🔹 Node 9: Thực thi Rsync Backup**
- **Command:**
  ```bash
  sshpass -p "$source_password" rsync -avz --delete $source_user@$source_host:$source_folder/ $target_user@$target_host:$target_folder/
  ```
- **Lưu ý:**
  - **StrictHostKeyChecking=no** được tự động thêm trong command (không cần cấu hình).
  - **Exit code của rsync** quyết định workflow tiếp theo:
    - **Exit 0:** Backup thành công (Node 10).
    - **Exit khác:** Backup thất bại (Node 11).

#### **🔹 Node 10-11: Xử lý kết quả**
- **Backup Successful** (Node 10): Lưu thông tin thành công vào `Backup Successful`.
- **Backup Failed** (Node 11): Lưu thông tin thất bại (exit code, stderr) vào `Backup Failed`.

#### **🔹 Node 12: Gửi báo cáo Telegram & SMS**
- **Command:**
  ```bash
  # Telegram (gửi thông báo thành công/thất bại)
  curl -s -X POST "https://api.telegram.org/bot$TELEGRAM_BOT_TOKEN/sendMessage" -d "chat_id=$TELEGRAM_CHANNEL_ID&text=$MESSAGE"

  # SMS (gửi qua TextBelt)
  curl -s -X POST "https://textbelt.com/text" -d "phone=$PHONE_NUMBER&message=$MESSAGE&key=$TEXTBELT_API_KEY"
  ```
- **Lưu ý:**
  - Thay thế tất cả placeholder (`YOUR-TELEGRAM-BOT-TOKEN`, `+36301234567`, `YOUR-TEXTBELT-API-KEY`) bằng giá trị thực.
  - **Dữ liệu gửi:** Thời gian, máy nguồn/target, kết quả (thành công/thất bại), và log chi tiết.

#### **🔹 Node 14: Schedule Trigger (Tùy chọn)**
- **Chức năng:** Chạy workflow tự động theo lịch (ví dụ: hàng ngày).
- **Cấu hình:**
  - **Cron:** `0 2 * * *` (2 giờ sáng hàng ngày).
  - **Time Zone:** Chọn múi giờ phù hợp.

---
### **3. Kích hoạt ⚡️**
1. **Test Run:** Nhấn **Run Workflow** với dữ liệu mẫu (điền các biến như `source_password`, `target_password`).
2. **Kiểm tra:**
   - Nếu backup thành công, kiểm tra Telegram/SMS có nhận được thông báo không.
   - Nếu thất bại, xem log trong node `Backup Failed`.
3. **Bật Active:** Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CẢNH BÁO & MỆNH CHỮ]
- **Bảo mật:** Không chia sẻ mật khẩu trong code hoặc log. Sử dụng **n8n Credentials** để lưu trữ an toàn.
- **Log chi tiết:** Thêm node **Slack/Email** để gửi log chi tiết khi backup thất bại.
- **Backup nhiều thư mục:** Sử dụng wildcard (`*` hoặc `**`) trong `source_folder` để backup nhiều thư mục.
- **Lưu lịch sử:** Kết hợp với **Google Sheets** hoặc **Airtable** để lưu lịch sử backup.
- **Không dùng SSH keys:** Workflow này **không hỗ trợ SSH keys** (chỉ mật khẩu). Nếu cần, phải sửa node `executeCommand`.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa backup dữ liệu giữa các server SSH **một cách an toàn và hiệu quả**, không cần can thiệp thủ công. Với **cảnh báo tức thời** qua Telegram và SMS, các sếp sẽ luôn biết trạng thái backup và có thể xử lý kịp thời nếu có lỗi.

**🚀 Hành động ngay:**
1. **Import workflow** và cấu hình các biến.
2. **Test run** với dữ liệu mẫu.
3. **Bật Active** và để nó chạy tự động hàng ngày!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::