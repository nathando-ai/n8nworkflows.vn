---
title: "🎤 Tự động chuyển đổi tin nhắn âm thanh WhatsApp thành văn bản với Whisper AI qua Groq"
description: "Hướng dẫn tự động hóa chuyển đổi tin nhắn âm thanh WhatsApp thành văn bản sử dụng Whisper AI thông qua Groq, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-chuyen-doi-tin-nhan-am-thanh-whatsapp-thanh-van-ban-voi-whisper-ai-qua-groq"
tags: [n8n, automation, no-code, WhatsApp, AI]
keywords: [n8n workflow, tự động hóa, Whisper AI, Groq, chuyển đổi âm thanh thành văn bản]
---

# 🎤 Tự động chuyển đổi tin nhắn âm thanh WhatsApp thành văn bản với Whisper AI qua Groq

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi làm việc với khách hàng qua WhatsApp, các sếp thường gặp khó khăn khi phải nghe lại tin nhắn âm thanh để hiểu nội dung. Việc này tốn thời gian và có thể gây mất tập trung. Workflow này sẽ giúp các sếp tự động chuyển đổi tin nhắn âm thanh WhatsApp thành văn bản sử dụng công nghệ Whisper AI thông qua Groq, giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động chuyển đổi tin nhắn âm thanh thành văn bản, không cần phải nghe lại.
- Nâng cao hiệu quả làm việc: Hiểu rõ nội dung tin nhắn ngay lập tức, không phải chờ đợi.
- Tích hợp với các công cụ khác: Kết quả có thể được sử dụng để gửi email, lưu vào Google Sheets, hoặc gửi thông báo qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc Evolution API).
- API Key của Groq để sử dụng Whisper AI.
- Tài khoản n8n để import và cấu hình workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook1**: Cấu hình webhook để nhận tin nhắn từ WhatsApp. Các sếp cần cấu hình đường dẫn (path) và phương thức HTTP (httpMethod) để nhận tin nhắn. Ví dụ: `seucaminho/MESSAGES_UPSERT` với phương thức POST.

- **Edit Fields1**: Sử dụng node này để chỉnh sửa các trường dữ liệu đầu vào. Các sếp cần cấu hình các trường dữ liệu cần thiết để gửi đến Groq.

- **Switch1**: Sử dụng node này để kiểm tra xem tin nhắn có phải là tin nhắn âm thanh hay không. Nếu là tin nhắn âm thanh, workflow sẽ tiếp tục xử lý. Nếu không, workflow sẽ kết thúc.

- **Convert to File1**: Sử dụng node này để chuyển đổi dữ liệu âm thanh thành file nhị phân. Các sếp cần cấu hình tham số `operation` thành `toBinary` để chuyển đổi dữ liệu âm thanh thành file nhị phân.

- **HTTP Request1**: Sử dụng node này để gửi yêu cầu đến Groq để chuyển đổi tin nhắn âm thanh thành văn bản. Các sếp cần cấu hình URL của Groq và các tham số cần thiết để gửi yêu cầu.

- **Evolution API**: Sử dụng node này để kết nối với WhatsApp Business API (hoặc Evolution API). Các sếp cần cấu hình tài khoản và thông tin xác thực để kết nối với WhatsApp Business API.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram: Gửi thông báo khi có tin nhắn mới hoặc khi chuyển đổi thành công.
- Lưu log: Lưu lại lịch sử chuyển đổi để theo dõi và phân tích.
- Gửi báo cáo định kỳ: Gửi báo cáo định kỳ về số lượng tin nhắn đã chuyển đổi và thời gian trung bình để chuyển đổi.

### 📌 Kết luận
Workflow này giúp các sếp tự động chuyển đổi tin nhắn âm thanh WhatsApp thành văn bản sử dụng Whisper AI thông qua Groq, tiết kiệm thời gian và nâng cao hiệu quả làm việc. Các sếp chỉ cần import và cấu hình workflow, sau đó kích hoạt để bắt đầu sử dụng.