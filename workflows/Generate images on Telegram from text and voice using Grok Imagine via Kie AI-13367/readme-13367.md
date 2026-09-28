---
title: "🚀 Tạo bot Telegram tạo ảnh bằng giọng nói và văn bản sử dụng Grok Imagine qua Kie AI"
description: "Hướng dẫn xây dựng trợ lý AI trên Telegram kết hợp Grok 4.1 Fast, Kie AI và Whisper để tạo hoặc biến hóa hình ảnh từ văn bản và tin nhắn thoại một cách tự động."
slug: "tao-bot-telegram-tao-anh-grok-imagine-kie-ai"
tags: [n8n, automation, telegram-bot, ai-image-generator, openrouter, kie-ai]
keywords: [n8n workflow, telegram bot ai, grok imagine, kie ai, text to image telegram, whisper transcription]
---

# 🚀 Tạo bot Telegram tạo ảnh bằng giọng nói và văn bản sử dụng Grok Imagine qua Kie AI

Các sếp có bao giờ cảm thấy việc mở các ứng dụng tạo ảnh phức tạp trên web tốn quá nhiều thời gian khi đang di chuyển? Việc phải gõ prompt dài dòng trên điện thoại đôi khi cũng gây bất tiện. 

Giải pháp hoàn hảo ở đây là xây dựng ngay một **AI Telegram Bot** riêng cho mình! Workflow n8n này sẽ giúp các sếp tạo và chỉnh sửa ảnh trực tiếp qua Telegram chỉ bằng cách nhắn tin văn bản hoặc gửi... tin nhắn thoại. Hệ thống thông minh này sử dụng mô hình **Grok 4.1 Fast** qua OpenRouter, kết hợp cùng **Kie AI API** và **OpenAI Whisper** để xử lý đa phương thức (Text, Voice, Image) một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa phương thức (Multi-modal):** Ra lệnh tạo ảnh bằng văn bản, gửi tin nhắn thoại (âm thanh tự chuyển thành prompt) hoặc gửi kèm ảnh gốc để AI biến hóa (Image-to-Image).
- **Tự động hóa thông minh:** Sử dụng AI Agent (Grok 4.1 Fast) để tự động phân tích ý định người dùng, tối ưu hóa câu lệnh (prompt) trước khi gọi API tạo ảnh.
- **Xử lý bất đồng bộ (Asynchronous):** Ứng dụng các node `Wait` và `Polling` để không bị nghẽn mạng hay timeout khi đợi AI render ảnh dung lượng lớn.
- **Bảo mật quyền truy cập:** Tích hợp bộ lọc Telegram ID giúp giới hạn chỉ những người dùng được phép mới có thể sử dụng bot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token:** Tạo qua [@BotFather](https://t.me/BotFather) trên Telegram.
- **OpenRouter API Key:** Để sử dụng mô hình **Grok 4.1 Fast** (`lmChatOpenRouter`).
- **Kie AI API Key:** Đăng ký miễn phí tại [Kie AI](https://kie.ai?ref=188b79f5cb949c9e875357ac098e1ff5) để lấy Bearer Token gọi model tạo ảnh (`httpRequest`).
- **OpenAI API Key:** Dùng cho tính năng chuyển đổi giọng nói thành văn bản bằng Whisper (`Transcribe recording`).
- **FTP Server / BunnyCDN:** Cấu hình FTP (ví dụ: [BunnyCDN](https://bunny.net?ref=0pfu5rh4tp)) để lưu trữ tạm các hình ảnh người dùng gửi lên và lấy Public URL cho AI xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc copy trực tiếp mã nguồn, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để bot chạy trơn tru, các sếp cần cấu hình chính xác các điểm sau trên canvas:

- **Node `Get Message` (Telegram Trigger):** Kết nối với Telegram API Credentials của bot do các sếp vừa tạo.
- **Node `Code` (STEP 1 - Telegram and switch):** Điền chính xác **Telegram User ID** của các sếp vào phần phân quyền để tránh người lạ lạm dụng bot.
- **Node `Transcribe recording` (OpenAI):** Cấu hình OpenAI API credentials để bot có thể nghe hiểu và dịch tin nhắn thoại.
- **Node `Upload image` (FTP):** Điền thông tin máy chủ FTP hoặc BunnyCDN của các sếp để lưu ảnh người dùng tải lên, tạo đường dẫn công khai cho công cụ Image-to-Image.
- **Node `Run text to image1` & `Run image to image1` (HTTP Request):** Cấu hình `httpBearerAuth` bằng **Kie AI API Key** lấy từ [Kie AI](https://kie.ai?ref=188b79f5cb949c9e875357ac098e1ff5).
- **Node `Grok 4.1 Fast` (LM Chat OpenRouter):** Thêm OpenRouter API credentials và chọn đúng model `x-ai/grok-4.1-fast`.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và thử gửi một tin nhắn văn bản hoặc voice chat cho bot trên Telegram để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để bật bot chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng tính năng:** Kết hợp thêm các node gửi thông báo về Google Sheets hoặc cơ sở dữ liệu để lưu lại lịch sử tạo ảnh của người dùng.
- **Tích hợp thêm kênh:** Dễ dàng nhân bản luồng chat này sang các nền tảng nhắn tin khác như Slack, Discord hoặc Zalo OA bằng cách thay thế Trigger node tương ứng.
- **Tối ưu Prompt:** Tùy chỉnh System Prompt bên trong **Grok Imagine Agent** để định hình phong cách nghệ thuật mặc định cho hình ảnh sinh ra (anime, photorealistic, 3D render...).

### 📌 Kết luận
Một trợ lý tạo ảnh cá nhân hóa ngay trên ứng dụng chat quen thuộc sẽ giúp công việc sáng tạo nội dung của các sếp trở nên thú vị và nhanh chóng hơn bao giờ hết. Hãy áp dụng ngay workflow này và làm chủ công nghệ AI tự động hóa!