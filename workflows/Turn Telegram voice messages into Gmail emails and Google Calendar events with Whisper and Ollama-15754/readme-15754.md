---
title: "🚀 Chuyển đổi tin nhắn thoại Telegram thành email Gmail và sự kiện Google Calendar với Whisper và Ollama"
description: "Hướng dẫn tự động hóa chuyển đổi tin nhắn thoại Telegram thành email và sự kiện lịch với AI, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "chuyen-doi-tin-nhan-thoai-telegram-thanh-email-va-su-kien-lich"
tags: [n8n, automation, no-code, telegram, gmail, google-calendar, ai, ollama]
keywords: [n8n workflow, tự động hóa, telegram, gmail, google calendar, whisper, ollama]
---

# 🚀 Chuyển đổi tin nhắn thoại Telegram thành email Gmail và sự kiện Google Calendar với Whisper và Ollama

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi tin nhắn thoại thành email và sự kiện lịch
- Tiết kiệm thời gian xử lý thông tin thủ công
- Tăng tính chuyên nghiệp trong giao tiếp và quản lý lịch
- Hỗ trợ nhiều loại yêu cầu thông qua giao tiếp tự nhiên
- Tích hợp hệ thống phê duyệt để đảm bảo chất lượng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram với bot đã cấu hình
- Tài khoản Gmail với quyền truy cập API
- Tài khoản Google Calendar với quyền truy cập API
- Ollama API key (phi3:mini model)
- Whisper API key (hoặc dịch vụ chuyển đổi giọng nói thành văn bản khác)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15754](https://n8n.io/workflows/15754)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** (Node đầu tiên):
   - Cấu hình credentials cho Telegram API
   - Đảm bảo bot Telegram đã được cấu hình đúng

2. **Wisper API** (Node chuyển đổi giọng nói thành văn bản):
   - Cấu hình endpoint và API key cho dịch vụ Whisper
   - Hoặc thay thế bằng dịch vụ chuyển đổi giọng nói thành văn bản khác

3. **Ollama Chat Model** (Các node sử dụng AI):
   - Cấu hình credentials cho Ollama API
   - Đảm bảo đã cài đặt model phi3:mini
   - Kiểm tra các tham số cấu hình model

4. **Gmail** (Node gửi email):
   - Cấu hình credentials cho Gmail OAuth2
   - Đảm bảo tài khoản Gmail có quyền gửi email

5. **Google Calendar** (Node tạo sự kiện):
   - Cấu hình credentials cho Google Calendar OAuth2
   - Đảm bảo tài khoản có quyền tạo sự kiện

6. **Code in JavaScript** (Các node xử lý dữ liệu):
   - Kiểm tra và cập nhật các hàm xử lý dữ liệu nếu cần
   - Đảm bảo các hàm JSON parser hoạt động đúng

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra từng node
2. Kiểm tra các điểm phân nhánh (If nodes) để đảm bảo logic điều kiện đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Microsoft Teams để nhận thông báo
- Thêm node lưu log để theo dõi hoạt động của workflow
- Cấu hình gửi báo cáo định kỳ về hoạt động của workflow
- Tích hợp với các dịch vụ khác như Notion hoặc Trello để quản lý công việc
- Sử dụng các model Ollama khác để tối ưu hóa hiệu suất

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa việc chuyển đổi tin nhắn thoại thành email và sự kiện lịch, giúp tiết kiệm thời gian và nâng cao hiệu suất làm việc. Bằng cách tích hợp các công nghệ AI như Whisper và Ollama, workflow này không chỉ đơn giản là chuyển đổi thông tin mà còn có khả năng hiểu và xử lý các yêu cầu phức tạp thông qua giao tiếp tự nhiên. Hãy áp dụng ngay để trải nghiệm sự thay đổi đáng kể trong cách làm việc của bạn!