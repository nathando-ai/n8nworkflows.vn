---
title: "🤖 Trợ lý AI Telegram kết hợp Gmail, Google Calendar & Google Sheets"
description: "Tự động hóa hoàn toàn các tác vụ quản lý email, lịch và dữ liệu với trợ lý AI thông minh trên Telegram"
slug: "tro-ly-ai-telegram-gmail-google-calendar-google-sheets"
tags: [n8n, automation, no-code, telegram, ai, google-workspace]
keywords: [n8n workflow, tự động hóa, trợ lý ai, telegram, google workspace]
---

# 🤖 Trợ lý AI Telegram kết hợp Gmail, Google Calendar & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn các tác vụ quản lý email, lịch và dữ liệu
- Tiết kiệm thời gian đáng kể cho các công việc lặp lại
- Tích hợp thông minh giữa các dịch vụ Google Workspace
- Hỗ trợ nhớ lịch sử hội thoại cho trải nghiệm người dùng tốt hơn
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot API key
- Tài khoản Google Workspace (Gmail, Google Calendar, Google Sheets)
- API key cho Google Gemini (để sử dụng AI)
- MCP Tools (nếu sử dụng tính năng MCP)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4902](https://n8n.io/workflows/4902)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Chọn credentials cho Telegram
   - Điền ID của bot Telegram vào trường "Bot ID"
   - Điền tên của bot Telegram vào trường "Bot Name"

2. **Google Gemini Chat Model**:
   - Chọn credentials cho Google Gemini
   - Điền API key của Google Gemini vào trường "API Key"

3. **Gmail nodes (Gmail, Gmail1, Gmail2)**:
   - Chọn credentials cho Gmail
   - Điền email của bạn vào trường "Email"

4. **Google Calendar nodes (Google Calendar, Google Calendar1, Google Calendar2)**:
   - Chọn credentials cho Google Calendar
   - Điền email của bạn vào trường "Email"

5. **Google Sheets node (contact data)**:
   - Chọn credentials cho Google Sheets
   - Điền ID của Google Sheet vào trường "Spreadsheet ID"
   - Điền tên của sheet vào trường "Sheet Name"

6. **AI Agent**:
   - Điền prompt cho AI agent vào trường "Prompt"
   - Cấu hình các công cụ (tools) mà AI agent có thể sử dụng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách gửi tin nhắn đến bot Telegram của bạn
3. Kiểm tra kết quả trong các dịch vụ Google Workspace tương ứng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp thêm Slack**: Thêm node Slack để nhận thông báo từ workflow
2. **Lưu log hoạt động**: Thêm node Google Sheets để lưu log các hoạt động của workflow
3. **Gửi báo cáo định kỳ**: Sử dụng node Gmail để gửi báo cáo định kỳ về hoạt động của workflow
4. **Tích hợp với các dịch vụ khác**: Kết nối với các dịch vụ khác như Notion, Trello, hoặc các API tùy chỉnh

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa các tác vụ quản lý email, lịch và dữ liệu thông qua trợ lý AI trên Telegram. Với các tính năng tích hợp thông minh và khả năng nhớ lịch sử hội thoại, workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể và nâng cao hiệu suất làm việc.