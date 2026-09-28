---
title: "🚀 Trợ lý AI cá nhân trên Telegram: Quản lý Lịch & Gmail tự động bằng Claude AI"
description: "Hướng dẫn xây dựng trợ lý AI toàn năng trên Telegram tích hợp Claude Haiku, OpenAI Whisper, Google Calendar và Gmail giúp xử lý tin nhắn, giọng nói, hình ảnh tự động."
slug: "tro-ly-ai-telegram-quan-ly-lich-gmail-claude-ai"
tags: [n8n, automation, no-code, telegram, ai-agent, google-calendar, gmail]
keywords: [n8n workflow, trợ lý ai telegram, claude ai n8n, quản lý lịch gmail tự động, openrouter n8n]
---

# 🚀 Xây dựng Trợ lý AI trên Telegram quản lý Google Calendar & Gmail cực thông minh với Claude AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục chuyển đổi giữa ứng dụng Telegram, mở Google Calendar để lên lịch hẹn, rồi lại nhảy sang Gmail để đọc và trả lời thư công việc? Việc quản lý thủ công này không chỉ tốn thời gian mà còn dễ bỏ sót các thông tin quan trọng.

Giải pháp ở đây là gì? Hãy để **n8n** thay các sếp làm điều đó! Workflow tuyệt vời này sẽ biến Telegram của các sếp thành một trung tâm điều khiển thông minh tích hợp **Claude AI**, cho phép nhắn tin văn bản, gửi ghi âm giọng nói (voice note), hoặc tải lên hình ảnh để trợ lý tự động xử lý và thao tác trực tiếp với **Google Calendar** và **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa dạng kênh đầu vào:** Nhận và hiểu lệnh bằng cả **văn bản**, **giọng nói** (audio) và **hình ảnh** (ảnh chụp màn hình, tài liệu...).
- **Tự động hóa lịch trình:** Tạo, đọc, cập nhật, xóa sự kiện hoặc kiểm tra lịch trống trên Google Calendar chỉ qua một câu lệnh chát đơn giản.
- **Quản lý email chuyên nghiệp:** Gửi, tìm kiếm, đọc, trả lời và xóa email trực tiếp trong Gmail mà không cần mở hòm thư.
- **Hoạt động 24/7 thông minh:** Trợ lý sử dụng mô hình Claude Haiku qua OpenRouter kết hợp bộ nhớ ngữ cảnh 30 tin nhắn giúp trò chuyện tự nhiên và chuẩn xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Telegram Bot Token**: Tạo bot thông qua [@BotFather](https://t.me/BotFather).
- **OpenAI API Key**: Dùng cho node Whisper (chuyển giọng nói thành văn bản) và GPT-4o (phân tích hình ảnh).
- **OpenRouter API Key**: Chạy mô hình ngôn ngữ Claude Haiku (`anthropic/claude-haiku-4.5`).
- **Google Calendar OAuth2**: Tài khoản Google kết nối để quản lý lịch.
- **Gmail OAuth2**: Tài khoản Google kết nối để đọc/gửi email.
- **Telegram User ID**: Số ID Telegram cá nhân của các sếp để bảo mật bot (chỉ cho phép chính chủ sử dụng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở giao diện n8n của các sếp, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 27 nodes được thiết kế tỉ mỉ, các sếp cần chú ý cấu hình các điểm cốt lõi sau:

- **Node `Telegram Trigger` & các node Telegram (`Get Audio`, `Telegram2`, `Send a text message...`)**: Kết nối với credential `telegramApi` chứa Bot Token của các sếp.
- **Node `If` (Bảo mật)**: **CỰC KỲ QUAN TRỌNG!** Hãy thay thế giá trị mẫu trong node này bằng **Telegram numeric User ID** của chính các sếp. Điều này giúp ngăn chặn người lạ sử dụng bot cá nhân của các sếp.
- **Node `OpenAI` & `Analyze image`**: Cấu hình credential `openAiApi` để hệ thống có khả năng phiên âm audio (Whisper) và phân tích ảnh (GPT-4o).
- **Node `OpenRouter Chat Model1`**: Chọn mô hình `anthropic/claude-haiku-4.5` và kết nối credential `openRouterApi`.
- **Các node Google Calendar (`createEvent`, `GetManyEvents`, `GetEvent`, `DeleteEvent`, `Availability`, `UpdateEvent`)**: Kết nối toàn bộ với credential `googleCalendarOAuth2Api` và cấu hình đúng Calendar ID (thường là `primary` nếu dùng lịch chính).
- **Các node Gmail (`sendMessage`, `getEmails`, `getEmail`, `replyEmail`, `deleteEmail`)**: Kết nối toàn bộ với credential `gmailOAuth2` để cấp quyền đọc/gửi email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn hoặc một file ghi âm tới bot Telegram của các sếp để kiểm tra kết quả.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để trợ lý hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Telegram channel khác để gửi bản tóm tắt công việc mỗi tối.
- **Lưu log công việc:** Thêm node Google Sheets để ghi lại tất cả các yêu cầu mà trợ lý đã thực hiện nhằm dễ dàng tra cứu về sau.
- **Tùy biến Prompt cho AI:** Các sếp có thể chỉnh sửa System Prompt trong node `MainAgent` để dạy bot cách xưng hô (ví dụ: xưng hô "sếp - tôi", nói chuyện hài hước hoặc trang trọng tùy thích).

### 📌 Kết luận
Với workflow n8n kết hợp Telegram và Claude AI này, các sếp đã sở hữu ngay một "thư ký riêng" thực thụ, giúp tiết kiệm hàng giờ đồng hồ mỗi ngày cho việc quản lý lịch hẹn và email. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của mình nhé!