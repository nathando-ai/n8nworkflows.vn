---
title: "🚀 Tạo giọng đọc AI Text-to-Speech tự động từ văn bản với ElevenLabs và n8n Webhook"
description: "Hướng dẫn xây dựng API endpoint chuyển đổi văn bản thành giọng nói (Text-to-Speech) tự động bằng ElevenLabs API thông qua n8n Webhook, giúp tiết kiệm thời gian làm video."
slug: "tao-giong-doc-text-to-speech-elevenlabs-n8n"
tags: [n8n, automation, no-code, elevenlabs, ai, text-to-speech, api]
keywords: [n8n workflow, elevenlabs api, text to speech n8n, tao giong noi ai, tu dong hoa n8n]
---

# 🚀 Tạo giọng đọc AI Text-to-Speech tự động từ văn bản với ElevenLabs và n8n

Các sếp có đang gặp khó khăn khi phải chuyển đổi thủ công hàng loạt văn bản thành giọng đọc (Voiceover) cho video, podcast hay các ứng dụng âm thanh? Việc copy từng đoạn text vào trang web của ElevenLabs vừa tốn thời gian, vừa nhàm chán và khó tích hợp vào hệ thống tự động hóa của doanh nghiệp.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tạo ra một **API Endpoint riêng** để tự động hóa hoàn toàn quá trình chuyển đổi Text-to-Speech thông qua ElevenLabs API. Chỉ cần gửi một POST Request chứa nội dung văn bản và Voice ID, hệ thống sẽ trả về file âm thanh ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file âm thanh mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo API Endpoint riêng:** Dễ dàng tích hợp với các hệ thống CRM, phần mềm làm video tự động, hoặc chatbot.
- **Tự động hóa 100%:** Không cần thao tác thủ công trên giao diện ElevenLabs, tiết kiệm hàng giờ đồng hồ mỗi tuần.
- **Linh hoạt lựa chọn giọng đọc:** Tùy chỉnh `voice_id` linh hoạt theo từng yêu cầu thông qua tham số truyền vào.
- **Hoạt động 24/7:** Xử lý request mọi lúc mọi nơi với độ ổn định cao trên n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản ElevenLabs:** Đã đăng ký và lấy được **API Key**.
- **Kiến thức cơ bản:** Biết cách gửi POST Request (thông qua Postman, cURL, hoặc các hệ thống khác).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Webhook`**: 
  - Đóng vai trò là điểm nhận request (API Endpoint).
  - Đường dẫn mặc định (Path): `generate-voice`, phương thức HTTP: `POST`. Các sếp sẽ gửi dữ liệu đến URL này.
- **Node `If params correct`**: 
  - Kiểm tra xem các tham số truyền vào (`voice_id` và `text`) có đầy đủ hay không trước khi gọi API ElevenLabs.
- **Node `Generate voice` (HTTP Request)**: 
  - Đây là node quan trọng nhất gọi đến ElevenLabs API.
  - Các sếp cần tạo **Custom Credentials** trong n8n với cấu trúc JSON sau để xác thực:
    ```json
    {
      "headers": {
        "xi-api-key": "your-elevenlabs-api-key"
      }
    }
    ```
    *(Thay thế `"your-elevenlabs-api-key"` bằng API Key thực tế của các sếp trên ElevenLabs).*
- **Node `Respond to Webhook` & `Error`**: 
  - Trả về kết quả file âm thanh thành công cho người gọi hoặc trả về thông báo lỗi nếu tham số không hợp lệ.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và dùng Postman/cURL gửi một POST Request mẫu kèm `voice_id` và `text` để test thử.
- Khi mọi thứ chạy trơn tru, hãy gạt công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Google Sheets/Airtable:** Lưu lại lịch sử các đoạn text đã chuyển đổi kèm link file audio.
- **Tích hợp Telegram/Slack Bot:** Cho phép người dùng gửi tin nhắn dạng chữ vào nhóm chat, bot sẽ gọi webhook này và trả lại file voice ngay trong đoạn chat.
- **Mở rộng làm video tự động:** Kết hợp workflow này với các công cụ tạo video AI khác để tự động sản xuất video TikTok/YouTube Shorts hàng loạt.

### 📌 Kết luận
Workflow tạo giọng đọc AI với ElevenLabs và n8n là một công cụ cực kỳ mạnh mẽ giúp tối ưu hóa quy trình sản xuất nội dung âm thanh và video. Hãy triển khai ngay hôm nay để giải phóng sức lao động và tăng tốc công việc của các sếp nhé!