```yaml
---
title: "🤖💬 Tự động hóa Chatbot AI với Google Gemini cho Text & Image trên Telegram"
description: "Hướng dẫn chi tiết cách tạo chatbot AI thông minh trên Telegram sử dụng Google Gemini, tự động xử lý cả văn bản và hình ảnh, hoàn toàn không cần code."
slug: "tao-chatbot-ai-google-gemini-telegram"
tags: [n8n, automation, no-code, ai, chatbot]
keywords: [n8n workflow, tự động hóa, chatbot, google gemini, telegram]
---
```

# 🤖💬 Tự động hóa Chatbot AI với Google Gemini cho Text & Image trên Telegram

[Các sếp] có biết không? Với công việc ngày càng bận rộn, việc phải trả lời từng tin nhắn một trên Telegram đang tốn rất nhiều thời gian quý giá. Đặc biệt khi phải xử lý cả văn bản lẫn hình ảnh, công việc này trở nên cực kỳ phức tạp và dễ gây lỗi.

Với workflow này, các sếp có thể tạo ngay một chatbot AI thông minh trên Telegram, tự động xử lý cả văn bản và hình ảnh, mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc trả lời tin nhắn
- Tự động xử lý cả văn bản và hình ảnh một cách thông minh
- Giao tiếp tự nhiên với người dùng nhờ khả năng nhớ lịch sử hội thoại
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tăng cường trải nghiệm khách hàng với AI thông minh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API Key từ Google Cloud Platform (Google Gemini API)
- Kiến thức cơ bản về cách tạo bot trên Telegram
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/4365](https://n8n.io/workflows/4365)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "userInput" (Telegram Trigger)**:
   - Chọn credentials "telegramApi"
   - Điền Bot Token của bạn
   - Chọn "onMessage" để kích hoạt khi có tin nhắn mới

2. **Node "GeminiModel" và "GeminiModel1" (Google Gemini)**:
   - Chọn credentials "googlePalmApi"
   - Điền Google API Key của bạn
   - Đảm bảo tài khoản Google của bạn đã kích hoạt Google Gemini API

3. **Node "sendImage" và "sendTextMessage" (Telegram)**:
   - Chọn credentials "telegramApi"
   - Đảm bảo bot của bạn có quyền gửi tin nhắn đến người dùng

4. **Node "imageGeneration" (HTTP Request)**:
   - Đảm bảo URL API của bạn đang hoạt động
   - Kiểm tra headers và body của request

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Telegram của bạn
3. Nếu mọi thứ hoạt động tốt, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" để nhận thông báo khi có lỗi xảy ra
- Kết nối với Google Sheets để lưu trữ lịch sử hội thoại
- Tích hợp với Google Drive để lưu trữ hình ảnh được tạo
- Thêm node "Email" để gửi báo cáo hàng ngày về hoạt động của chatbot
- Tùy chỉnh các prompt để phù hợp với ngành nghề của bạn

### 📌 Kết luận
Với workflow này, các sếp có thể tạo ngay một chatbot AI thông minh trên Telegram, tự động xử lý cả văn bản và hình ảnh, mà không cần viết một dòng code nào! Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.