---
title: "🚀 Tự động hóa Google Calendar và Đề xuất Lịch hẹn thông minh với Gemini AI, WhatsApp & Gmail"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động tạo lịch hẹn từ Google Sheet, đồng thời sử dụng AI Agent (Gemini) để tự động tìm kiếm khung giờ trống và gửi đề xuất chăm sóc khách hàng qua WhatsApp và Gmail."
slug: "tu-dong-hoa-google-calendar-gemini-ai-whatsapp-gmail"
tags: [n8n, automation, google-calendar, google-sheets, ai-agent, gemini, whatsapp]
keywords: [n8n workflow, tự động hóa google calendar, gemini ai n8n, chăm sóc khách hàng tự động, whatsapp automation]
---

# 🚀 Tự động hóa Google Calendar và Đề xuất Lịch hẹn thông minh với AI

Việc quản lý lịch hẹn, tạo sự kiện thủ công từ Google Sheets và chủ động nhắn tin follow-up (chăm sóc lại) khách hàng sau cuộc họp là một "cực hình" tốn rất nhiều thời gian cho các đội ngũ sales và chăm sóc khách hàng. Nếu quên hoặc trễ hẹn, doanh nghiệp có thể mất đi những khách hàng tiềm năng quý giá.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100% hai quy trình cốt lõi: **Tự động tạo sự kiện từ Google Sheet** và **Sử dụng AI (Gemini/OpenAI) thông minh để phân tích lịch sử, tìm lịch trống và gửi đề xuất tái hẹn qua WhatsApp & Email**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thủ công copy dữ liệu từ Sheet sang Calendar hay tự tính lịch hẹn tiếp theo.
- **AI thông minh đề xuất lịch:** AI Agent tự động check lịch trống trên Google Calendar và đề xuất thời gian phù hợp nhất cho khách.
- **Đa kênh tiếp cận (Omnichannel):** Khách hàng nhận được xác nhận và đề xuất lịch hẹn ngay lập tức qua **WhatsApp (Rapiwa)** và **Gmail**.
- **Chống trùng lặp (Idempotency):** Cơ chế thông minh giúp không bao giờ gửi tin nhắn spam hoặc trùng lặp cho cùng một sự kiện.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Calendar:** Tài khoản Google có lịch sẵn sàng cho việc tạo sự kiện và check availability.
- **Google Sheets:** File Google Sheet chứa dữ liệu danh sách cuộc họp cần tạo. 👉 [Tham khảo Mẫu Sheet tại đây](https://docs.google.com/spreadsheets/d/1DSRrIDvw-Q9NugRK3eT7GMa0kwe0QnGhdySnqq1_kJU/edit?usp=sharing).
- **Rapiwa Account:** Tài khoản và API Credentials để gửi tin nhắn WhatsApp.
- **Gmail Account:** OAuth2 Credentials để gửi email tự động.
- **Google Gemini (hoặc OpenAI) API:** Credentials để cấp quyền cho AI Agent xử lý logic tìm kiếm lịch.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc của template (`10270`), sau đó chọn **Import from File** hoặc copy toàn bộ JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau:

- **Get in sheet & Update status in sheet:** Kết nối tài khoản Google Sheets OAuth2. Điền chính xác **Document ID** và **Sheet Name** của sếp.
- **Create an event & Get Past Events:** Chọn đúng tài khoản Google Calendar OAuth2 và chọn đúng **Calendar ID** cần quản lý.
- **Date & Time & Code:** Giúp chuẩn hóa định dạng thời gian kết thúc sự kiện từ Google Sheet sang chuỗi UTC ISO 8601 chuẩn xác trước khi đẩy vào Google Calendar.
- **Meeting Agent (AI Agent) & OpenAI / Gemini:** Cấu hình credentials cho LLM. Kiểm tra kỹ **System Message** để AI hiểu rõ khung giờ làm việc, quy tắc tìm lịch trống phù hợp với doanh nghiệp.
- **Rapiwa / Rapiwa1 & Send a message / Send a message1:** Kết nối tài khoản Rapiwa API và Gmail OAuth2 để cấu hình số điện thoại nhận/gửi tin nhắn WhatsApp và Email chăm sóc khách hàng.
- **Mark as Seen:** Giữ nguyên cấu hình này để hệ thống tự động ghi nhận các sự kiện đã xử lý, tránh việc gửi tin nhắn trùng lặp trong các lần chạy sau.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test Step / Execute Node**) từng nhánh (Nhánh tạo lịch từ Sheet và Nhánh AI nhắc lịch hẹn cũ).
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7 theo lịch của **Schedule Trigger**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thêm một node Telegram hoặc Slack ở nhánh sau khi AI tìm được lịch hẹn để thông báo cho đội ngũ Sales nội bộ nắm tình hình.
- **Lưu Log vào Airtable/Database:** Thay vì chỉ cập nhật trạng thái trong Google Sheet, các sếp có thể log toàn bộ nội dung tin nhắn AI đề xuất vào Airtable để dễ dàng quản lý lịch sử tương tác.
- **Tùy chỉnh Prompt của AI:** Tinh chỉnh System Message của Meeting Agent để AI nói chuyện lịch sự hơn, phù hợp với văn phong thương hiệu (Tone of Voice) của công ty.

### 📌 Kết luận
Workflow tích hợp Google Calendar, Google Sheets, Gemini AI và WhatsApp/Gmail này là một "vũ khí" tối ưu hóa vận hành cực mạnh cho các doanh nghiệp dịch vụ, sales B2B hay coaching. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ của bạn!