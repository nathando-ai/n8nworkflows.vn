---
title: "🚀 Sao lưu Credentials n8n tự động lên Google Drive qua SSH & Docker"
description: "Giải pháp tự động sao lưu toàn bộ credentials của n8n lên Google Drive, giảm thiểu rủi ro mất dữ liệu và tiết kiệm thời gian quản trị."
slug: "sao-luu-credentials-n8n-tro-voi-google-drive"
tags: [n8n, automation, no-code, devops, backup]
keywords: [n8n workflow, tự động hóa, sao lưu credentials, Google Drive, Docker]
---

# 🚀 Sao lưu Credentials n8n tự động lên Google Drive qua SSH & Docker

Bạn đang quản lý một hệ thống n8n chạy trong Docker và lo lắng về việc mất dữ liệu credentials khi có sự cố? Việc sao lưu thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Workflow này giúp bạn **sao lưu toàn bộ credentials** của n8n lên Google Drive một cách tự động, 100% không cần code, chỉ cần cấu hình một vài biến và chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thao tác thủ công, chỉ một lần cấu hình.
- **Độ chính xác cao**: Tự động lấy file credentials, tránh sai sót khi copy‑paste.
- **Bảo mật**: Credentials được lưu trữ an toàn trong Google Drive, có thể thiết lập quyền truy cập.
- **Tự động liên tục**: Đặt lịch chạy hàng ngày/tuần, hoặc kích hoạt thủ công khi cần.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive** có quyền ghi vào thư mục mục tiêu.
- **SSH credentials** (host, port, username, private key hoặc password) để kết nối tới máy chủ chứa container n8n.
- **Docker container name hoặc ID** của container n8n đang chạy.
- **Node credentials** cho các node trong workflow:
  - `SSH` node: chọn hoặc tạo credential mới.
  - `Google Drive` node: chọn hoặc tạo credential mới.
- **File JSON** chứa credentials của n8n sẽ được tạo bởi lệnh Docker:  
  `/home/node/.n8n-files/credentials.json` (hoặc đường dẫn tùy chỉnh).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
- Tải file JSON workflow từ [đây](https://n8n.io/workflows/11842) hoặc copy nội dung JSON vào editor n8n.
- Mở **n8n Editor**, chọn **Import** → **Upload JSON** → chọn file.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên node | Cấu hình cần thiết |
|------|----------|---------------------|
| **Variables** | `Variables` | Đặt 3 biến: `Backup Folder`, `Docker Container name`, `Docker - n8n credentials files`. |
| **SSH** | `Execute a command` | Chọn credential SSH, nhập lệnh:  
`docker exec -u node [Docker Container name] mkdir -p /home/node/.n8n-files && docker exec -u node [Docker Container name] n8n export:credentials --all --decrypted --output=[Docker - n8n credentials files]` |
| **Read File** | `Read File` | Đường dẫn file: `[Docker - n8n credentials files]`. |
| **Google Drive Upload File** | `Google Drive Upload File` | Chọn credential Google Drive, thư mục: `Backup Folder`, file name: `credentials-{{ $now.format('YYYY-MM-DD_HH-mm-ss') }}.json`. |
| **Schedule Trigger** | `Schedule Trigger` | Thiết lập lịch (ví dụ: `0 2 * * *` để chạy lúc 02:00 mỗi ngày). |
| **Manual Trigger** | `On clicking 'execute'` | Kích hoạt khi cần sao lưu ngay. |
| **Sticky Note** | `Sticky Note` | Ghi chú nội dung workflow (không ảnh hưởng tới thực thi). |

> **Lưu ý**: Đảm bảo biến `Docker Container name` và `Docker - n8n credentials files` khớp với cấu hình Docker của bạn. Nếu bạn thay đổi đường dẫn xuất file, cập nhật biến tương ứng.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn **Execute Workflow** trong editor, xem log từng node. Đảm bảo lệnh Docker chạy thành công và file được tải lên Google Drive.
2. **Bật Active**: Khi mọi thứ ổn, bật toggle **Active** ở góc trên bên phải. Workflow sẽ chạy theo lịch hoặc khi trigger thủ công.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo qua Slack**: Thêm node `Slack` sau `Google Drive Upload File` để thông báo khi sao lưu thành công.
- **Lưu log vào Google Sheets**: Sử dụng node `Google Sheets` để ghi lại thời gian, tên file, trạng thái.
- **Tự động xóa file cũ**: Thêm node `Execute a command` để chạy `find /home/node/.n8n-files -mtime +7 -delete` và giữ file chỉ trong 7 ngày.
- **Sử dụng Telegram**: Thêm node `Telegram` để nhận tin nhắn khi có lỗi.

## 📌 Kết luận
Workflow này giúp các sếp **đảm bảo an toàn dữ liệu** một cách nhanh chóng, dễ dàng và không tốn công sức. Hãy thử ngay, tùy chỉnh theo nhu cầu và chia sẻ cho đồng nghiệp! Nếu gặp bất kỳ khó khăn nào, bạn có thể liên hệ với tác giả: **alex@elitiv.com**.

---