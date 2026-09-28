---
title: "🚀 Tự động nhắc nhở hết hạn tên miền với Google Sheets, WHOIS, Telegram và Ollama AI"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra hạn sử dụng tên miền hàng ngày, phân tích dữ liệu WHOIS bằng AI Ollama và gửi cảnh báo qua Telegram."
slug: "tu-dong-nhac-nho-het-han-ten-mien-google-sheets-telegram-ollama-ai"
tags: [n8n, automation, no-code, devops, ai-summarization, google-sheets, telegram]
keywords: [n8n workflow, tự động hóa tên miền, kiểm tra whois, nhắc nhở hết hạn domain, ollama ai, telegram bot]
---

# 🚀 Tự động nhắc nhở hết hạn tên miền với Google Sheets, WHOIS, Telegram và Ollama AI

Các sếp đang quản lý bao nhiêu tên miền (domain) cho công việc kinh doanh? Việc bỏ quên hạn gia hạn một domain quan trọng có thể dẫn đến hậu quả mất thương hiệu, gián đoạn website hoặc bị kẻ xấu chiếm đoạt. Làm thủ công bằng cách ghi nhớ hay tra cứu từng cái một vừa mất thời gian lại rủi ro cao.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100%: Định kỳ quét danh sách domain từ Google Sheets, lấy thông tin WHOIS, sử dụng AI (Ollama) để trích xuất ngày hết hạn chính xác, tính toán số ngày còn lại và tự động bắn thông báo nhắc nhở qua Telegram nếu domain sắp hết hạn dưới 90 ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ tài sản số:** Không bao giờ bỏ lỡ lịch gia hạn domain nhờ hệ thống cảnh báo tự động trước 90 ngày.
- **Tiết kiệm thời gian tuyệt đối:** Thay vì kiểm tra thủ công hàng loạt trang web WHOIS, mọi thứ diễn ra hoàn toàn tự động mỗi 8:00 sáng.
- **Trích xuất thông minh:** Ứng dụng Ollama AI (Llama 3.1) để bóc tách dữ liệu ngày tháng từ mã HTML thô của WHOIS một cách chính xác.
- **Chống làm phiền (Anti-spam):** Tự động cập nhật cột `last_notified` vào Google Sheets để tránh việc gửi tin nhắn cảnh báo lặp lại mỗi ngày.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Google Sheets:** File Google Sheets chứa danh sách các domain cần theo dõi.
- **Telegram Bot:** Một Telegram Bot Token và Chat ID để nhận tin nhắn cảnh báo.
- **Ollama AI:** Local Ollama server đang chạy model `llama3.1:8b` (hoặc cấu hình lại sang OpenAI/Anthropic nếu thích).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc (ID: `12387`) trên n8n.io hoặc copy đoạn JSON tương ứng paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy cấu hình các node cốt lõi sau để hệ thống chạy mượt mà:

- **Cron (Daily 08:00):** Node này mặc định chạy lúc 8 giờ sáng mỗi ngày. Các sếp có thể thay đổi lịch trình nếu muốn quét vào khung giờ khác.
- **Google Sheets (Read Domains):** 
  - Kết nối `Google Sheets OAuth2 API`.
  - Điền Spreadsheet ID và chọn đúng Sheet Name chứa danh sách domain của các sếp.
- **Get raw data html from whois.com (HTTP Request):** Node này gọi dữ liệu HTML từ whois.com dựa trên domain được truyền vào từ Google Sheets qua vòng lặp `Split In Batches`.
- **Ollama Chat Model & Information Extractor:** 
  - Kết nối thông tin kết nối tới server Ollama.
  - Sử dụng model `llama3.1:8b` (hoặc model tương đương) để AI phân tích cú pháp HTML và trích xuất chính xác ngày hết hạn (`expired date`), chủ sở hữu (`domain owner`), và trạng thái domain.
- **Get Date & Time Diff:** Tính toán khoảng thời gian giữa ngày hiện tại và ngày hết hạn trích xuất được.
- **IF (Should Notify):** Kiểm tra điều kiện xem domain có sắp hết hạn trong vòng 90 ngày hay không.
- **Telegram (Send Reminder):** 
  - Cấu hình Telegram Credentials.
  - Điền Chat ID nhận thông báo và nội dung template tin nhắn cảnh báo.
- **Google Sheets (Update last_notified):** 
  - Chọn operation `update`.
  - Ghi lại mốc thời gian đã thông báo vào Google Sheets để các lần quét sau không bị spam tin nhắn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step-by-step) với một vài domain mẫu trong Google Sheets để đảm bảo dữ liệu trả về Telegram chính xác.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh phụ:** Ngoài Telegram, các sếp có thể nối thêm node Slack, Discord hoặc Email để gửi cảnh báo tới nhiều phòng ban cùng lúc (kỹ thuật, kế toán, ban quản trị).
- **Lưu Log lỗi:** Thêm một nhánh `Error Trigger` để nếu việc gọi WHOIS bị lỗi (do chặn IP hoặc mạng), hệ thống sẽ gửi thông báo vào một nhóm chat riêng để xử lý.
- **Mở rộng thời gian cảnh báo:** Có thể tinh chỉnh node `IF` để gửi nhiều mốc cảnh báo khác nhau: trước 90 ngày, 30 ngày, và 7 ngày.

### 📌 Kết luận
Hệ thống giám sát hạn dùng domain tự động này là một mảnh ghép DevOps không thể thiếu cho các agency, đội ngũ IT hoặc lập trình viên quản lý nhiều tài sản số. Hãy thiết lập ngay hôm nay để loại bỏ hoàn toàn rủi ro mất domain vì quên gia hạn các sếp nhé!