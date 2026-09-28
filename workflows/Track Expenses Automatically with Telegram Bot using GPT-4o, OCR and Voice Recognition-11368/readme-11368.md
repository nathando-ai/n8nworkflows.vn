---
title: "💰 Tự động theo dõi chi tiêu bằng Telegram Bot với GPT-4o, OCR và nhận dạng giọng nói"
description: "Hướng dẫn chi tiết cách tự động hóa việc theo dõi chi tiêu cá nhân bằng Telegram Bot kết hợp trí tuệ nhân tạo, OCR và nhận dạng giọng nói. Tiết kiệm thời gian và nâng cao hiệu quả quản lý tài chính."
slug: "tu-dong-theo-doi-chi-tieu-voi-telegram-bot-gpt-4o-ocr-nhan-dang-giong-noi"
tags: [n8n, automation, no-code, telegram, ai, ocr, voice-recognition]
keywords: [n8n workflow, tự động hóa, telegram bot, theo dõi chi tiêu, trí tuệ nhân tạo, ocr, nhận dạng giọng nói]
---

# 💰 Tự động theo dõi chi tiêu bằng Telegram Bot với GPT-4o, OCR và nhận dạng giọng nói

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi chi tiêu
- Tiết kiệm thời gian lên đến 80% so với phương pháp thủ công
- Nhận dạng chính xác thông tin từ hóa đơn, ảnh và giọng nói
- Quản lý chi tiêu theo danh mục và thời gian một cách hiệu quả
- Nhận báo cáo chi tiêu định kỳ thông qua Telegram
- Bảo mật thông tin cá nhân với hệ thống xác thực người dùng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và quyền tạo bot
- API Key từ OpenRouter để sử dụng GPT-4o và Claude Sonnet 4.5
- Tài khoản Ainoflow để lưu trữ dữ liệu
- Các node cần cấu hình:
  - Telegram: 8 nodes (Trigger, WelcomeMessage, GetAudioFile, GetAttachedFile, GetAttachedPhoto, ReplyText, NotAuthorizedMessage, DeleteProcessing)
  - OpenRouter: 2 nodes (Gpt4o, Sonnet45)
  - Ainoflow: 12 nodes (GetAppSettings, SaveAppSettings, SaveExecutionState, TranscribeAudio, ExtractFileText, ExtractImageText, GetExecutionState, ForEachCategory, ForEachCategoryItem, DeleteItem, JsonStorageMcp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11368)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Telegram**:
   - Tạo bot Telegram theo hướng dẫn [tại đây](https://blog.n8n.io/create-telegram-bot/)
   - Cấu hình credentials cho tất cả các node Telegram (8 nodes) với thông tin bot vừa tạo

2. **Cấu hình OpenRouter**:
   - Tạo API Key theo hướng dẫn [tại đây](https://docs.n8n.io/integrations/builtin/credentials/openrouter/)
   - Cấu hình credentials cho node Gpt4o và Sonnet45 với API Key vừa tạo

3. **Cấu hình Ainoflow**:
   - Đăng ký tài khoản và tạo API Key tại [Ainoflow](https://www.ainoflow.io/signup)
   - Cấu hình credentials cho tất cả các node Ainoflow (12 nodes) với API Key vừa tạo

4. **Cấu hình các node quan trọng**:
   - **Trigger**: Cấu hình để nhận tin nhắn từ Telegram
   - **GetAppSettings**: Cấu hình để lấy cài đặt ứng dụng
   - **SaveAppSettings**: Cấu hình để lưu cài đặt ứng dụng
   - **TranscribeAudio**: Cấu hình để chuyển đổi giọng nói thành văn bản
   - **ExtractFileText**: Cấu hình để trích xuất văn bản từ file
   - **ExtractImageText**: Cấu hình để trích xuất văn bản từ ảnh
   - **AIAgent**: Cấu hình để xử lý logic chính của ứng dụng
   - **ExpenseAssistant**: Cấu hình để xử lý logic về chi tiêu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng
2. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack hoặc Discord để nhận thông báo chi tiêu
2. Lưu log các giao dịch để phục vụ mục đích kiểm toán
3. Gửi báo cáo chi tiêu định kỳ (tuần, tháng) qua email
4. Tích hợp với các ứng dụng tài chính khác như QuickBooks hoặc Xero

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa theo dõi chi tiêu cá nhân thông qua Telegram Bot. Với sự kết hợp của trí tuệ nhân tạo, OCR và nhận dạng giọng nói, nó giúp tiết kiệm thời gian đáng kể và nâng cao hiệu quả quản lý tài chính. Các sếp hãy áp dụng ngay để nâng cao hiệu suất làm việc và quản lý tài chính cá nhân một cách hiệu quả hơn!