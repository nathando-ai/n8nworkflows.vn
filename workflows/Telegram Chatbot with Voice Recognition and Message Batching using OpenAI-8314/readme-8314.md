---
title: "🤖 Tự động hóa Chatbot Telegram với Nhận dạng giọng nói và Gộp tin nhắn bằng OpenAI"
description: "Hướng dẫn chi tiết cách tự động hóa chatbot Telegram với khả năng nhận dạng giọng nói và gộp tin nhắn bằng OpenAI, giúp tiết kiệm thời gian và nâng cao trải nghiệm người dùng."
slug: "tu-dong-hoa-chatbot-telegram-voi-nhan-dang-giong-noi-va-gop-tin-nhan-bang-openai"
tags: [n8n, automation, no-code, telegram, openai]
keywords: [n8n workflow, tự động hóa, chatbot telegram, nhận dạng giọng nói, gộp tin nhắn]
---

# 🤖 Tự động hóa Chatbot Telegram với Nhận dạng giọng nói và Gộp tin nhắn bằng OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý tin nhắn thủ công.
- Tự động chuyển đổi giọng nói thành văn bản với độ chính xác cao.
- Gộp tin nhắn từ cùng một người dùng trong khoảng thời gian ngắn để tránh spam.
- Tích hợp trí tuệ nhân tạo để trả lời tự động và thông minh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot được tạo từ @BotFather.
- API key từ OpenAI để sử dụng dịch vụ Whisper cho nhận dạng giọng nói.
- Google Sheets với hai bảng dữ liệu: Message Retention và Message Checkup.
- Tài khoản Google với quyền truy cập vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/8314).
2. Nhấn vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Tạo một bot mới trên Telegram bằng cách nhắn tin với @BotFather và sử dụng lệnh `/newbot`.
   - Sao chép token của bot.
   - Trong n8n, vào mục **Credentials** → **Telegram API** → điền token vừa sao chép.
   - Chọn node **Telegram Trigger** và nhấn **Execute Node** một lần để đăng ký webhook.

2. **Google Sheets**:
   - Tạo hai bảng dữ liệu trên Google Sheets:
     - **Message Retention**: Ba cột `date`, `user_id`, `message`.
     - **Message Checkup**: Ba cột `user_id`, `is_waiting`, `last_updated`.
   - Chia sẻ cả hai bảng với email của service account từ Google Sheets credential trong n8n với quyền **Editor**.

3. **OpenAI API**:
   - Đăng ký tài khoản OpenAI và lấy API key.
   - Trong n8n, vào mục **Credentials** → **OpenAI API** → điền API key.

4. **Cấu hình các node quan trọng**:
   - **Get Audio File**: Chọn credential là **Telegram API**.
   - **Transcribe a recording**: Chọn credential là **OpenAI API**.
   - **Append row in sheet** và **Get row(s) in sheet**: Chọn credential là **Google Sheets OAuth2 API**.
   - **OpenAI Chat Model**: Chọn model là `gpt-5-mini` hoặc model khác phù hợp.
   - **AI Agent**: Cấu hình system prompt và user text để trả lời tin nhắn từ người dùng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo các node hoạt động đúng.
- Bật **Active workflow** để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để thông báo khi có tin nhắn mới.
- Lưu log các tin nhắn vào Google Sheets để theo dõi lịch sử.
- Gửi báo cáo định kỳ về số lượng tin nhắn đã xử lý và thời gian trung bình phản hồi.

### 📌 Kết luận
Workflow này giúp tự động hóa chatbot Telegram với khả năng nhận dạng giọng nói và gộp tin nhắn, tiết kiệm thời gian và nâng cao trải nghiệm người dùng. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!