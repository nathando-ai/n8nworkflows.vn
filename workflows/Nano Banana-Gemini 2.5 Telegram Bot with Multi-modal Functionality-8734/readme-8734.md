---
title: "🚀 Xây dựng Telegram Bot Đa phương thức thông minh với n8n, OpenAI và Gemini 2.5"
description: "Hướng dẫn chi tiết thiết lập workflow n8n tích hợp Telegram Bot đa phương thức (Text, Audio, Image, PDF) sử dụng OpenAI và Google Gemini 2.5."
slug: "huong-dan-telegram-bot-da-phuong-thuc-n8n-openai-gemini-2.5"
tags: [n8n, automation, telegram-bot, openai, google-gemini, ai-agent]
keywords: [n8n workflow, telegram bot ai, openai whisper, google gemini 2.5, multimodal bot, tự động hóa n8n]
---

# 🚀 Xây dựng Telegram Bot Đa phương thức thông minh với n8n, OpenAI và Gemini 2.5

Các sếp có bao giờ cảm thấy việc quản lý một con bot Telegram chỉ biết trả lời text đơn thuần là quá nhàm chán và thiếu chuyên nghiệp? Người dùng ngày nay muốn gửi ảnh để bot phân tích, gửi tin nhắn thoại (voice) để bot tự nghe - hiểu, hoặc thậm chí gửi cả tài liệu PDF để tra cứu, kèm theo tính năng tạo ảnh nghệ thuật theo yêu cầu.

Giải pháp thủ công hay việc thuê lập trình viên viết riêng một con bot tốn kém không còn là lựa chọn tối ưu. Với workflow n8n này, các sếp sẽ sở hữu ngay một **AI Telegram Bot đa phương thức (Multimodal AI Bot)** hoạt động 24/7 chỉ trong vài phút thiết lập mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý mượt mà các file nặng (ảnh, audio, PDF) mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa phương thức hoàn hảo**: Bot tiếp nhận và xử lý mượt mà 4 dạng dữ liệu: Văn bản (Text), Hình ảnh (Image), Giọng nói (Audio/Voice), và Tài liệu (PDF).
- **Trí tuệ nhân tạo kép (Dual-Model Agent)**: Kết hợp sức mạnh lập luận của GPT-5-mini và sự nhanh nhạy của Gemini-2.5-flash.
- **Tích hợp tạo ảnh chuyên sâu**: Tích hợp Nano Banana API (Gemini Image Generation) để tạo và gửi ảnh chất lượng cao trực tiếp qua Telegram chỉ với câu lệnh.
- **Bộ nhớ ngữ cảnh thông minh**: Duy trì lịch sử trò chuyện 10 tin nhắn gần nhất cho từng người dùng nhờ `Simple Memory`.
:::

### 📌 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI LÊN ĐỒ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted bản mới nhất hỗ trợ LangChain/Agents).
- **Telegram Bot Token** (Lấy từ `@BotFather`).
- **OpenAI API Key** (Dùng cho GPT-5-mini phân tích ngữ cảnh, Whisper transribe audio và phân tích hình ảnh).
- **Google AI Studio API Key** (Dùng cho Gemini-2.5-flash và Nano Banana Image API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Copy toàn bộ mã JSON của workflow mẫu từ nguồn cung cấp.
2. Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File/Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để bot hoạt động trơn tru, các sếp cần cấu hình chính xác các thông số quan trọng sau:

- **Telegram Trigger Node**: 
  - Chọn credential Telegram API đã tạo.
  - Bật tính năng tải file nhị phân (Binary Data) để bot có thể nhận ảnh, voice và tài liệu PDF.
- **Các HTTP Request Nodes (Get Image Url, Get File Url, Get Audio Url)**:
  - Cập nhật đúng đường dẫn API Telegram, thay thế `<YOUR_TOKEN>` bằng Token thật của bot: `https://api.telegram.org/bot<YOUR_TOKEN>/getFile`
- **Nano Banana API Node**:
  - Cấu hình credential dạng Header Auth với tên header `x-goog-api-key` và giá trị là khóa API từ Google AI Studio.
- **Generator Agent & Các Language Model Nodes (gpt-5-mini, gemini-2.5-flash)**:
  - Đảm bảo đã liên kết chính xác OpenAI API Key và Google Gemini API Key vào các node tương ứng.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách gửi tin nhắn văn bản, hình ảnh hoặc voice mẫu qua Telegram Bot.
- Kiểm tra dữ liệu luân chuyển qua các nhánh `Switch` và `Extract from File`.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để bot chính thức hoạt động 24/7.

### ✍️ Gợi ý nâng cao & Mở rộng
- **Lưu trữ lịch sử**: Kết nối thêm node Google Sheets hoặc PostgreSQL ngay sau `Telegram Trigger` để lưu lại toàn bộ câu hỏi và tương tác của khách hàng.
- **Giao tiếp đa nền tảng**: Mở rộng workflow để đồng thời đẩy thông báo quan trọng lên kênh Slack hoặc Microsoft Teams của công ty khi có khách hàng VIP tương tác.
- **Hệ thống phân quyền**: Thêm node `If` để kiểm tra `chat_id`, chỉ cho phép một nhóm người dùng nội bộ sử dụng các tính năng tạo ảnh AI tốn phí.

### 📌 Kết luận
Workflow tích hợp Telegram Bot đa phương thức với OpenAI và Gemini 2.5 này là giải pháp toàn diện giúp tự động hóa khâu chăm sóc khách hàng và sáng tạo nội dung. Hãy triển khai ngay lên VPS của các sếp để tối ưu hóa hiệu suất công việc ngay hôm nay!