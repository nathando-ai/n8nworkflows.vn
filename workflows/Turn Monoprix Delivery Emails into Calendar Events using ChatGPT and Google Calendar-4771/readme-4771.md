---
title: "🚀 Tự động hóa lịch hẹn giao hàng Monoprix bằng ChatGPT và Google Calendar"
description: "Hướng dẫn tự động hóa việc thêm lịch hẹn giao hàng Monoprix vào Google Calendar từ email thông báo bằng n8n, ChatGPT và Google Calendar"
slug: "tu-dong-hoa-lich-hen-giao-hang-monoprix-bang-chatgpt-va-google-calendar"
tags: [n8n, automation, no-code, google-calendar, chatgpt]
keywords: [n8n workflow, tự động hóa, google calendar, chatgpt, email]
---

# 🚀 Tự động hóa lịch hẹn giao hàng Monoprix bằng ChatGPT và Google Calendar

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc thêm lịch hẹn giao hàng vào Google Calendar từ email thông báo.
- Chính xác: Sử dụng ChatGPT để trích xuất thông tin chính xác từ email.
- Cá nhân hóa: Tùy chỉnh nội dung lịch hẹn theo nhu cầu cá nhân.
- Hoạt động liên tục: Workflow hoạt động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận email thông báo giao hàng.
- Tài khoản OpenAI để sử dụng ChatGPT.
- Tài khoản Google Calendar để thêm lịch hẹn.
- API keys cho các dịch vụ trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Pull email from Gmail**: Cấu hình credentials cho Gmail và chọn email và chủ đề để theo dõi.
- **Extract key info**: Sử dụng node này để trích xuất thông tin từ email.
- **OpenAI Chat Model**: Cấu hình credentials cho OpenAI và chọn model (gpt-4o-mini).
- **Set GCal fields**: Cấu hình các trường cho Google Calendar.
- **Update Calendar**: Cấu hình credentials cho Google Calendar và chọn lịch để cập nhật.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi lịch hẹn được thêm vào.
- Lưu log các email đã xử lý để tránh xử lý trùng lặp.
- Gửi báo cáo định kỳ về các lịch hẹn đã được thêm vào.

### 📌 Kết luận
Workflow này giúp tự động hóa việc thêm lịch hẹn giao hàng Monoprix vào Google Calendar từ email thông báo, tiết kiệm thời gian và giảm thiểu lỗi. Các sếp có thể tùy chỉnh nội dung lịch hẹn và kết hợp với các dịch vụ khác để nâng cao hiệu quả.