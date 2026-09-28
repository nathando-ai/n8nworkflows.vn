---
title: "🎙️ Tự động chuyển đổi tin nhắn thoại Telegram thành văn bản bằng Whisper & Gemini"
description: "Hướng dẫn tự động hóa chuyển đổi tin nhắn thoại Telegram thành văn bản sử dụng Whisper (OpenAI) và Gemini (Google) với cơ chế dự phòng. Giảm thiểu công việc thủ công, tăng hiệu quả làm việc."
slug: "tu-dong-chuyen-doi-tin-nhan-thoai-telegram-thanh-van-ban"
tags: [n8n, automation, no-code, telegram, ai]
keywords: [n8n workflow, tự động hóa, chuyển đổi âm thanh, whisper, gemini, telegram]
---

# 🎙️ Tự động chuyển đổi tin nhắn thoại Telegram thành văn bản bằng Whisper & Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải ngồi nghe và ghi chép lại tin nhắn thoại từ khách hàng, đồng nghiệp hay nhân viên trên Telegram? Việc này không chỉ tốn thời gian mà còn dễ gây lỗi do sự tập trung không đủ. Với workflow này, các sếp có thể tự động chuyển đổi tin nhắn thoại thành văn bản chỉ trong vài giây, giúp tiết kiệm thời gian và giảm thiểu sai sót.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi tin nhắn thoại thành văn bản với độ chính xác cao
- Tiết kiệm thời gian xử lý tin nhắn thoại lên đến 90%
- Hỗ trợ nhiều định dạng âm thanh (OGG, MP3, MP4, M4A)
- Cơ chế dự phòng tự động khi Whisper (OpenAI) gặp lỗi
- Gửi kết quả trực tiếp đến Telegram với phân đoạn văn bản dài
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và quyền truy cập vào bot
- API Key từ OpenAI (cho Whisper) và Google (cho Gemini)
- Các sếp cần có quyền truy cập vào các dịch vụ này để cấu hình credentials trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/9625](https://n8n.io/workflows/9625)
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger1**:
   - Cấu hình credentials "telegramApi" với thông tin bot của bạn
   - Đảm bảo bot có quyền truy cập vào các kênh/cuộc trò chuyện cần xử lý

2. **Get File GPT & Get File Gemini**:
   - Cấu hình credentials "telegramApi" giống như trên
   - Đảm bảo bot có quyền tải xuống các file âm thanh

3. **Transcription by OpenAi**:
   - Cấu hình credentials "openAiApi" với API Key của OpenAI
   - Chọn "transcribe" trong operation và "audio" trong resource

4. **Transcription by Gemini**:
   - Cấu hình credentials "googlePalmApi" với API Key của Google
   - Chọn "audio" trong resource

5. **MSG - Starting transcription. Please wait.**:
   - Cấu hình credentials "telegramApi" giống như trên
   - Tùy chỉnh nội dung thông báo nếu cần

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách gửi một tin nhắn thoại đến bot Telegram
2. Kiểm tra kết quả trong n8n Editor
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Teams để nhận thông báo khi có tin nhắn thoại mới
2. Lưu log các tin nhắn đã xử lý vào Google Sheets hoặc Notion
3. Tự động gửi báo cáo hàng ngày về số lượng tin nhắn đã xử lý
4. Thêm chức năng nhận dạng ngôn ngữ tự động trước khi chuyển đổi

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình chuyển đổi tin nhắn thoại thành văn bản, giảm thiểu công việc thủ công và tăng hiệu quả làm việc. Với cơ chế dự phòng tự động và hỗ trợ nhiều định dạng âm thanh, workflow này là giải pháp hoàn hảo cho các doanh nghiệp cần xử lý lượng lớn tin nhắn thoại hàng ngày. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao chất lượng công việc!