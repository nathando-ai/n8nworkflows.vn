---
title: "🚀 Tự động tạo ảnh AI bằng Gemini & Đăng bài lên Facebook, Instagram, X kèm Phê duyệt qua Telegram"
description: "Xây dựng Bot Telegram thông minh giúp biến ý tưởng văn bản/giọng nói thành hình ảnh AI bằng Gemini, kiểm duyệt qua Telegram và tự động đăng đa nền tảng qua Blotato."
slug: "tu-dong-tao-anh-ai-gemini-dang-facebook-instagram-x-telegram"
tags: [n8n, automation, ai-agent, gemini, telegram, social-media]
keywords: [n8n workflow, tạo ảnh ai gemini, tự động đăng facebook instagram x, bot telegram ai, blotato n8n]
---

# 🚀 Biến Telegram thành trạm kiểm soát nội dung & Tạo ảnh AI đăng mạng xã hội tự động

Các sếp có bao giờ cảm thấy mệt mỏi khi phải nghĩ ý tưởng, viết bài, tạo hình ảnh rồi lại thủ công đăng lên từng mạng xã hội (Facebook, Instagram, X)? Quy trình này ngốn rất nhiều thời gian và dễ làm giảm cảm hứng sáng tạo.

Với workflow n8n cực đỉnh này, các sếp chỉ cần gửi một tin nhắn văn bản hoặc **tin nhắn thoại (voice note)** qua Telegram, hệ thống AI sẽ tự động lo từ A-Z: từ việc viết nội dung, tạo ảnh bằng Google Gemini, cho đến khâu kiểm duyệt và tự động đăng bài lên đa nền tảng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh chuyển đổi qua lại giữa nhiều ứng dụng để thiết kế và đăng bài.
- **Ra lệnh bằng giọng nói:** Gửi voice note trực tiếp trên Telegram, AI tự động chuyển thành văn bản và hiểu ý bạn.
- **Kiểm soát tuyệt đối:** Hình ảnh và nội dung bài viết sẽ được gửi qua Telegram để sếp "duyệt" trước khi lên sóng.
- **Đăng đa nền tự động:** Tự động phát hành bài viết lên Facebook, Instagram, X (Twitter) cùng lúc thông qua Blotato và gửi link xác nhận chính xác.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Telegram Bot Token:** Tạo bot qua `@BotFather` để nhận/gửi tin nhắn và duyệt nội dung.
- **OpenAI API Key:** Dùng cho tính năng Speech-to-Text (Whisper) và AI Agent xử lý ngôn ngữ.
- **Google Gemini API Key:** Sử dụng model Gemini để tạo hình ảnh chất lượng cao từ prompt.
- **Google Drive & Google Sheets OAuth2:** Lưu trữ hình ảnh và ghi lại lịch sử prompt, nội dung bài đăng.
- **Tài khoản Blotato:** Kết nối các trang mạng xã hội (Facebook, Instagram, X) tại [Blotato](https://blotato.com/?ref=feras) và lấy API key.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy trực tiếp và dán (Paste) vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Listen for incoming events (Telegram Trigger):** Kết nối với Telegram Credentials của sếp để bot lắng nghe tin nhắn đến.
- **AI Agent & OpenAI Chat Model:** Cấu hình OpenAI API, sau đó tinh chỉnh System Prompt bên trong AI Agent để định hình văn phong, phong cách thương hiệu và cách AI tạo prompt ảnh phù hợp.
- **Generate an image (Google Gemini):** Điền Google Palm/Gemini API key và đảm bảo prompt lấy dữ liệu chính xác từ node `Parse AI Output`.
- **Upload image1 & Download image from Drive (Google Drive):** Kết nối tài khoản Google Drive để tự động lưu trữ ảnh vừa tạo làm kho lưu trữ riêng.
- **Save Prompt & Post-Text (Google Sheets):** Trỏ tới file Google Sheet chuẩn bị sẵn để lưu lại lịch sử bài viết.
- **Các node Blotato (Upload media1, Create FB post, Create instagram Post, Create x post...):** Kết nối Blotato API để hệ thống tiến hành đẩy hình ảnh và nội dung lên các nền tảng mạng xã hội một cách trơn tru.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn hoặc voice note cho bot Telegram của sếp để test toàn bộ luồng.
- Sau khi kiểm tra mọi thứ chạy ổn định, hãy gạt công tắc sang **Active** để bật chế độ tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nền tảng:** Có thể tích hợp thêm LinkedIn hoặc TikTok thông qua các node hỗ trợ của Blotato.
- **Lưu log lỗi:** Thiết lập thêm node gửi thông báo qua Telegram hoặc Slack riêng cho đội ngũ kỹ thuật nếu gặp lỗi API từ mạng xã hội.
- **Tạo lịch trình định kỳ:** Kết hợp thêm node Cron (Schedule) để yêu cầu AI tự động tạo ý tưởng hàng ngày mà không cần đợi sếp ra lệnh thủ công.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho các nhà sáng tạo nội dung, marketer hay chủ doanh nghiệp muốn tối ưu hóa quy trình sản xuất nội dung hình ảnh trên mạng xã hội với sự hỗ trợ đắc lực từ AI. Hãy cài đặt ngay hôm nay để giải phóng thời gian và bứt phá tương tác!