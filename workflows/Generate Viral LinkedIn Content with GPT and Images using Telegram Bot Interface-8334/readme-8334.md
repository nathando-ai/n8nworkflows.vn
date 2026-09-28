---
title: "🚀 Tạo nội dung LinkedIn viral kèm ảnh AI tự động qua Telegram Bot với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình sáng tạo bài viết LinkedIn viral và tạo ảnh minh họa bằng AI thông qua giao diện chat Telegram."
slug: "tao-noi-dung-linkedin-viral-kem-anh-ai-qua-telegram-bot"
tags: [n8n, automation, telegram, openai, ai-agent, content-creation]
keywords: [n8n workflow, tao bai viet linkedin, telegram bot ai, generate ai images, tu dong hoa content]
---

# 🚀 Tạo nội dung LinkedIn viral kèm ảnh AI tự động qua Telegram Bot

Viết nội dung LinkedIn thu hút hàng ngàn lượt tương tác (viral) tốn rất nhiều thời gian từ khâu nghiên cứu xu hướng, lên kịch bản, viết copy đến việc tìm kiếm hoặc thiết kế hình ảnh minh họa phù hợp. Việc làm thủ công này không chỉ mệt mỏi mà còn khó duy trì đều đặn. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Chỉ bằng một tin nhắn yêu cầu qua Telegram Bot, hệ thống sẽ tự động sử dụng AI thông minh để phân tích, viết bài chuẩn viral và tạo ảnh minh họa độc đáo trả về trực tiếp cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Biến một ý tưởng sơ khai thành bài đăng LinkedIn hoàn chỉnh chỉ trong vài giây.
- **Chất lượng viral cao:** Sử dụng các mô hình AI thông minh (OpenAI) kết hợp công cụ tìm kiếm (Tavily) để phân tích xu hướng và tối ưu hóa cấu trúc bài viết.
- **Hình ảnh minh họa tự động:** Tự động tạo và gửi ảnh đi kèm bài viết cực kỳ bắt mắt.
- **Tiện lợi tối đa:** Điều khiển và nhận kết quả mọi lúc mọi nơi ngay trên ứng dụng Telegram quen thuộc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot Token:** Tạo bot mới thông qua `@BotFather` trên Telegram.
- **OpenAI API Key:** Để chạy các AI Agent và LLM.
- **Tavily API Key:** Dành cho công cụ nghiên cứu dữ liệu web (Tavily Tool).
- **RapidAPI Key:** Dùng cho dịch vụ tạo ảnh AI trong workflow (`generate_img`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã JSON từ hệ thống.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (ba chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình kỹ các node sau:
- **Telegram Trigger** & các node **Telegram** (`Send a photo message`, `Send a text message`): Kết nối với credentials `telegramApi` chứa Bot Token của các sếp.
- **OpenAI Chat Model**: Nhập credentials `openAiApi` và kiểm tra lại model được chọn (ví dụ: `gpt-5-nano` hoặc các model tương đương).
- **tavily**: Thêm credentials `tavilyApi` để cho phép AI tìm kiếm thông tin ngoài internet khi cần nghiên cứu nội dung.
- **generate_img** & **download_img** (HTTP Request nodes): Đảm bảo các API endpoint và key của RapidAPI tạo ảnh được cấu hình chính xác theo hướng dẫn của nhà cung cấp dịch vụ ảnh.
- **AI Agents & Parsers** (`expert_algo`, `Community Manager`, `Structured Output Parser`...): Kiểm tra lại các system prompt nếu muốn tùy chỉnh văn phong bài viết LinkedIn theo cá tính riêng của thương hiệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn yêu cầu nội dung tới Telegram Bot của các sếp để kiểm tra kết quả trả về.
- Nếu mọi thứ hoạt động hoàn hảo, hãy gạt công tắc **Active** ở góc trên bên phải để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử bài viết:** Kết nối thêm node Google Sheets hoặc Notion sau bước tạo nội dung để lưu lại toàn bộ các bài viết đã tạo nhằm dễ dàng quản lý lịch đăng.
- **Đa kênh mạng xã hội:** Mở rộng workflow bằng cách gửi nội dung vừa tạo sang các kênh khác như Twitter (X), Facebook Page hoặc Slack.
- **Kiểm duyệt trước khi đăng:** Thêm bước hỏi ý kiến trên Telegram (Interactive buttons) để các sếp chọn "Duyệt" hoặc "Sửa lại" trước khi bot xuất bản bài viết.

### 📌 Kết luận
Tự động hóa sáng tạo nội dung chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và AI. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc và làm chủ các nền tảng mạng xã hội nhé các sếp!