---
title: "🚀 Tự động giám sát Email, Lọc Spam & Trả lời thông minh bằng Ollama AI & Telegram"
description: "Xây dựng hệ thống tự động hóa xử lý email đến qua IMAP, lọc spam thông minh, sử dụng Ollama AI tạo nội dung phản hồi tự động và thông báo qua Telegram."
slug: "tu-dong-giam-sat-email-ollama-ai-telegram"
tags: [n8n, automation, ai, ollama, telegram, email-automation, local-llm]
keywords: [n8n workflow, tự động hóa email, ollama ai, telegram notification, imap smtp automation]
---

# 🚀 Tự động giám sát Email, Lọc Spam & Trả lời thông minh bằng Ollama AI & Telegram

Các sếp có đang mệt mỏi vì mỗi ngày phải kiểm tra hàng chục, hàng trăm email đến, trong đó có cả tá thư rác, newsletter hay email thông báo tự động? Việc đọc thủ công, phân loại và soạn email phản hồi tốn rất nhiều thời gian và năng lượng quý báu.

Giải pháp ở đây chính là workflow n8n tự động hóa toàn diện này! Hệ thống sẽ thay các sếp "gác cổng" hộp thư 24/7: tự động đọc email qua IMAP, gửi cảnh báo tức thì qua Telegram, lọc bỏ email rác/no-reply, dùng **Ollama AI (Local LLM)** để tự động viết câu trả lời cá nhân hóa, gửi phản hồi qua SMTP và báo cáo lại kết quả hoàn chỉnh qua Telegram. Hoàn toàn tự động và bảo mật dữ liệu nhờ chạy AI cục bộ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian xử lý email:** Tự động hóa hoàn toàn quy trình đọc, phân loại và trả lời email cơ bản.
- **Không bỏ lỡ khách hàng quan trọng:** Nhận thông báo tức thì qua Telegram ngay khi có email mới với đầy đủ tiêu đề, người gửi.
- **Phản hồi thông minh, cá nhân hóa:** AI phân tích nội dung email, tóm tắt chủ đề chính và viết lời cảm ơn lịch sự, chuyên nghiệp.
- **Bảo mật tuyệt đối:** Sử dụng Ollama chạy local (hoặc qua API nội bộ), đảm bảo dữ liệu email không bị lộ ra các dịch vụ AI bên thứ ba.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Hệ thống n8n** (Self-hosted hoặc Cloud).
2. **IMAP Credential**: Thông tin kết nối hộp thư đến (Host, Port SSL, Email, App-specific Password).
3. **SMTP Credential**: Thông tin máy chủ gửi email (ví dụ: Postfix, Gmail SMTP, SendGrid...).
4. **Telegram Bot Token**: Tạo bot thông qua `@BotFather` và lấy `Chat ID`.
5. **Ollama API & Model**: Cài đặt Ollama (local hoặc server riêng) và tải model `llama3.1` (chạy lệnh `ollama pull llama3.1`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu `...` ở góc trên bên phải -> Chọn **Import from JSON** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Check Incoming Emails - IMAP**: Điền thông tin kết nối IMAP của hộp thư (Host, Port `993`, bật SSL/TLS, Username và mật khẩu ứng dụng).
- **Send Notification from Incoming Email (Telegram)**: Kết nối tài khoản Telegram API, cập nhật chính xác `Chat ID` của các sếp (ví dụ: `-1234567890123`) để nhận thông báo email mới.
- **Dedicate Filtering As No-Response (IF Node)**: Kiểm tra logic lọc spam. Mặc định hệ thống sẽ chặn các địa chỉ chứa `noreply`, `no-reply` hoặc tiêu đề chứa `newsletter`. Các sếp có thể tùy chỉnh thêm điều kiện lọc tùy theo nhu cầu thực tế.
- **Ollama Model & Basic LLM Chain**: Chọn credential kết nối Ollama API, cấu hình model là `llama3.1`. Đảm bảo Ollama server đang chạy và đã tải model.
- **Send Auto-Response in SMTP**: Điền thông tin SMTP để gửi email phản hồi tự động. Nhớ cập nhật địa chỉ email gửi đi (`fromEmail`) chính xác là của các sếp.
- **Send Notification from Response (Telegram)**: Cấu hình lại Chat ID Telegram để nhận thông báo xác nhận khi AI đã gửi email phản hồi thành công.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài email mẫu để kiểm tra luồng chạy từ IMAP -> Lọc Spam -> Ollama AI -> SMTP -> Telegram.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử vào Google Sheets / Airtable:** Thêm một node lưu trữ dữ liệu email đến và phản hồi của AI để tiện theo dõi, thống kê khách hàng về sau.
- **Tích hợp thêm Slack/Discord:** Ngoài Telegram, các sếp có thể bắn webhook thông báo vào kênh chung của đội ngũ CSKH/Sales để mọi người cùng nắm bắt.
- **Tinh chỉnh Prompt cho AI:** Tùy biến system prompt trong `Basic LLM Chain` để AI nói chuyện theo đúng văn phong thương hiệu (lịch sự, hài hước, trang trọng...).

### 📌 Kết luận
Workflow "Monitor Emails & Send AI-Powerful Auto-Replies" là một mảnh ghép hoàn hảo giúp tối ưu hóa quy trình CSKH và quản lý hộp thư cá nhân/doanh nghiệp. Triển khai ngay hôm nay để giải phóng thời gian của các sếp khỏi những công việc lặp đi lặp lại!