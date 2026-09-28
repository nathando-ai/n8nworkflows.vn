---
title: "🤖 Discord Message Proxy: Tự động hóa phản hồi AI khi được nhắc đến"
description: "Workflow n8n tự động xử lý tin nhắn Discord khi bot được nhắc đến, kết hợp với AI để trả lời thông minh và chính xác."
slug: "discord-message-proxy-ai-actions"
tags: [n8n, automation, discord, no-code, ai]
keywords: [n8n workflow, tự động hóa discord, bot discord, ai discord, xử lý tin nhắn]
---

# 🤖 Discord Message Proxy: Tự động hóa phản hồi AI khi được nhắc đến

[Các sếp đang mệt mỏi với việc phải theo dõi và trả lời tin nhắn Discord thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình khi bot được nhắc đến, kết hợp với AI để trả lời thông minh và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động xử lý tin nhắn khi bot được nhắc đến.
- Chính xác: Lọc và xử lý tin nhắn một cách thông minh.
- Cá nhân hóa: AI có thể trả lời theo ngữ cảnh và yêu cầu cụ thể.
- Hoạt động liên tục: Workflow chạy 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Discord với quyền quản trị.
- API key của dịch vụ AI (nếu sử dụng).
- Credentials cho Discord trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này từ file JSON hoặc copy/paste JSON vào n8n Editor. Để làm điều này, các sếp cần:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from File" hoặc "Import from Clipboard".
3. Dán nội dung JSON của workflow vào và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lại các node quan trọng sau:

- **Schedule Trigger**: Cấu hình thời gian kiểm tra tin nhắn (ví dụ: mỗi 5 phút).
- **Discord1**: Cấu hình credentials cho Discord.
- **Get All Servers' Channels**: Đảm bảo bot có quyền truy cập vào tất cả các kênh cần theo dõi.
- **Set Values**: Cấu hình các giá trị cần thiết cho quá trình xử lý.
- **Filter (Remove empty)**: Lọc bỏ các tin nhắn trống.
- **Get last message**: Lấy tin nhắn mới nhất.
- **Filter (Remove Old)**: Lọc bỏ các tin nhắn cũ.
- **Filter (Messages with mentions)**: Lọc các tin nhắn có nhắc đến người dùng.
- **Filter (Authorized User)**: Lọc các tin nhắn từ người dùng được ủy quyền.
- **Filter (Messages mentioning bot)**: Lọc các tin nhắn nhắc đến bot.
- **HTTP Request**: Cấu hình API endpoint của dịch vụ AI.
- **Clean Message**: Sử dụng code để làm sạch tin nhắn trước khi gửi đến AI.
- **Remove Duplicates**: Loại bỏ các tin nhắn trùng lặp.
- **It**: Cấu hình để gửi phản hồi từ AI trở lại kênh Discord.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần:
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có tin nhắn mới.
- Lưu log các tin nhắn đã xử lý để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng tin nhắn đã xử lý và thời gian phản hồi trung bình.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình xử lý tin nhắn Discord khi bot được nhắc đến, kết hợp với AI để trả lời thông minh và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!