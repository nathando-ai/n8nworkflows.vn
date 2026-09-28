---
title: "🚀 Tự động hóa Telegram lên Google Drive với AI Gemini: Upload Video & Theo dõi Tệp"
description: "Hướng dẫn chi tiết cách tự động tải video từ Telegram lên Google Drive, quản lý tên tệp và theo dõi bằng Google Sheets cùng trợ lý AI Gemini"
slug: "tu-dong-hoa-telegram-google-drive-voi-ai-gemini"
tags: [n8n, automation, no-code, google-drive, telegram, ai]
keywords: [n8n workflow, tự động hóa, google drive, telegram, ai gemini]
---

# 🚀 Tự động hóa Telegram lên Google Drive với AI Gemini: Upload Video & Theo dõi Tệp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tải video từ Telegram lên Google Drive trong vài giây
- Quản lý tên tệp một cách thông minh với logic động
- Theo dõi hoạt động với Google Sheets
- Trợ lý AI Gemini hỗ trợ trả lời tin nhắn
- Tiết kiệm thời gian và giảm lỗi thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram với bot đã tạo
- Google Drive và Google Sheets đã kích hoạt API
- API key cho Google Gemini
- Tài khoản n8n đã cài đặt các credentials: telegramApi, googleDriveOAuth2Api, googleSheetsOAuth2Api, googlePalmApi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger**:
   - Cấu hình credentials: telegramApi
   - Đảm bảo bot đã được kích hoạt và có quyền truy cập vào kênh/nhóm

2. **Google Drive Nodes**:
   - Cấu hình credentials: googleDriveOAuth2Api
   - Chọn thư mục đích trong Google Drive để lưu video

3. **Google Sheets Nodes**:
   - Cấu hình credentials: googleSheetsOAuth2Api
   - Tạo bảng tính mới hoặc sử dụng mẫu có sẵn
   - Đảm bảo có các cột: File name, Drive link, File size, Duration, Upload timestamp, Last update timestamp

4. **Google Gemini AI**:
   - Cấu hình credentials: googlePalmApi
   - Nhập API key cho Google Gemini
   - Cấu hình Simple Memory1 với window size phù hợp (ví dụ: 5)

5. **Code Node**:
   - Chỉnh sửa logic trong Code1 để phù hợp với định dạng tên tệp mong muốn
   - Ví dụ: `{{$node["Telegram Trigger"].json["message"]["video"]["file_name"]}}_processed`

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi có video mới
- Thêm chức năng phân loại video theo chủ đề
- Tích hợp với Google Calendar để theo dõi tiến độ xử lý
- Mở rộng hệ thống nhớ của AI để xử lý các yêu cầu phức tạp hơn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ nhận video đến lưu trữ và quản lý, đồng thời tích hợp AI để hỗ trợ trả lời tin nhắn. Với việc tự động hóa, các sếp có thể tập trung vào công việc quan trọng hơn và giảm thiểu lỗi thủ công. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!