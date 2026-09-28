---
title: "🚀 Giám sát tính toàn vẹn tệp tin từ xa với SSH và Slack Alerts tự động trên n8n"
description: "Tự động hóa kiểm tra mã hash (checksum) tệp tin quan trọng trên VPS/Server qua SSH, phát hiện sớm sự thay đổi trái phép và cảnh báo ngay lập tức qua Slack."
slug: "giam-sat-toan-ven-tep-tin-ssh-slack-n8n"
tags: [n8n, automation, secops, ssh, slack, devops]
keywords: [n8n workflow, giám sát file server, kiểm tra integrity file, cảnh báo slack ssh, bảo mật server tự động]
---

# 🚀 Giám sát tính toàn vẹn tệp tin từ xa với SSH và Slack Alerts tự động trên n8n

Là một quản trị viên hệ thống hoặc developer, bạn có chắc chắn rằng các file cấu hình quan trọng trên server (`/etc/passwd`, file cấu hình Nginx, env,...) chưa bao giờ bị chỉnh sửa trái phép? Việc kiểm tra thủ công bằng tay là cực kỳ tẻ nhạt, dễ bỏ sót và gần như bất khả thi nếu quản lý nhiều server cùng lúc. Nếu server bị xâm nhập, kẻ tấn công thường sẽ thay đổi các tệp tin hệ thống làm bước đệm.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp chủ động bảo vệ cơ sở hạ tầng, tự động kết nối vào server qua SSH để kiểm tra mã băm (checksum) định kỳ và bắn cảnh báo ngay lập tức vào Slack khi phát hiện bất thường.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm sự cố (Early Detection):** Nhận diện ngay lập tức khi file hệ thống hoặc mã nguồn bị thay đổi trái phép.
- **Tự động hóa hoàn toàn:** Chạy ngầm định kỳ 24/7 mà không cần sự can thiệp thủ công của con người.
- **Cảnh báo tức thì:** Gửi thông tin chi tiết (file nào bị đổi, checksum cũ vs checksum mới) trực tiếp vào kênh Slack của đội ngũ DevOps/IT.
- **Tiết kiệm thời gian:** Thay vì kiểm tra log hay chạy lệnh thủ công mỗi ngày, hệ thống sẽ tự lo việc đó.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **SSH Access:** Thông tin truy cập SSH vào Server/VPS mục tiêu (Hostname, Port, User, SSH Private Key hoặc Password). Người dùng SSH cần có quyền chạy lệnh `sha256sum`.
- **Slack Workspace:** Đã tạo Slack App hoặc Bot và có quyền gửi tin nhắn vào kênh thông báo (kèm Channel ID).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON gốc.
- Trong giao diện n8n, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow hoạt động mượt mà:

- **Scheduled Check (`cron`):** Tùy chỉnh lịch chạy mong muốn (Ví dụ: Chạy lúc 3 giờ sáng mỗi ngày hoặc chạy mỗi vài tiếng).
- **List Files & Checksums (`code`):** Node này chứa danh sách các file cần giám sát và mã checksum chuẩn ban đầu. Các sếp cần chỉnh sửa mảng `filesToCheck` trỏ đến đúng đường dẫn file thực tế trên server và điền giá trị SHA256 chuẩn đã lấy trước đó.
- **Get Remote File Checksum (`ssh`):** 
  - Chọn **SSH Credentials** đã chuẩn bị.
  - Đảm bảo câu lệnh thực thi (thường dùng `sha256sum /path/to/file`) khớp với đường dẫn cấu hình.
- **Send Alert (`slack`):**
  - Chọn **Slack API Credentials**.
  - Thay thế `YOUR_SECURITY_ALERT_CHANNEL_ID` bằng ID kênh Slack thực tế nhận cảnh báo (Ví dụ: `#secops-alerts`).

#### 3. Kích hoạt ⚡️
- **Test Run:** Nhấp vào nút **Execute Workflow** để chạy thử nghiệm thủ công và kiểm tra kết quả trả về ở node `Checksums Match?`.
- **Active:** Sau khi test thành công, gạt công tắc sang **Active** để n8n tự động vận hành ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống giám sát bảo mật tối ưu hơn, các sếp có thể mở rộng workflow:
- **Tích hợp thêm Telegram/Discord:** Ngoài Slack, có thể duplicate nhánh cảnh báo sang Telegram Bot để đa dạng hóa kênh nhận tin.
- **Lưu lịch sử kiểm tra:** Đẩy log kết quả kiểm tra thành công hoặc thất bại vào Google Sheets / Notion để làm báo cáo kiểm toán (Audit Log) hàng tuần.
- **Tự động hóa phản ứng (Auto-remediation):** Ở nhánh phát hiện lỗi, thay vì chỉ bắn tin nhắn, có thể cấu hình thêm lệnh SSH tự động khôi phục file gốc từ bản backup trên Git.

### 📌 Kết luận
Bảo mật hệ thống không bao giờ là thừa, đặc biệt là với các hệ thống chạy dịch vụ cho khách hàng. Với workflow n8n giám sát file integrity này, các sếp sẽ có thêm một lớp phòng thủ tự động, nhẹ nhàng nhưng cực kỳ hiệu quả. Triển khai ngay hôm nay để yên tâm ngủ ngon giấc nhé!