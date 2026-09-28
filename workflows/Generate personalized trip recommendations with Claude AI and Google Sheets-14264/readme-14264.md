---
title: "🚀 Tạo gợi ý chuyến đi cá nhân hóa tự động bằng Claude AI và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống gợi ý du lịch thông minh tự động 100% bằng n8n, Claude AI và Google Sheets, giúp cá nhân hóa trải nghiệm khách hàng và tối ưu hiệu suất."
slug: "tao-goi-y-chuyen-di-ca-nhan-hoa-claude-ai-google-sheets"
tags: [n8n, automation, ai-agent, claude-ai, google-sheets, travel-tech]
keywords: [n8n workflow, claude ai n8n, google sheets automation, goi y du lich ai, ai agent n8n]
keywords: [n8n workflow, tự động hóa, ai agent, claude ai, google sheets, gợi ý du lịch]
---

# 🚀 Tạo gợi ý chuyến đi cá nhân hóa tự động bằng Claude AI và Google Sheets

Việc lên kế hoạch du lịch hoặc tư vấn lịch trình thủ công cho hàng trăm khách hàng mỗi ngày tiêu tốn rất nhiều thời gian, nhân lực và thiếu đi sự cá nhân hóa sâu sắc. Các doanh nghiệp lữ hành hoặc nhà sáng tạo nội dung thường gặp khó khăn trong việc phân tích dữ liệu lịch sử của khách hàng kết hợp với xu hướng thời tiết, giá vé để đưa ra gợi ý chính xác.

Workflow n8n này chính là giải pháp tự động hóa toàn diện giúp giải quyết bài toán trên. Hệ thống sẽ tự động tiếp nhận yêu cầu qua Webhook hoặc lịch trình định kỳ, phân tích lịch sử du lịch từ Google Sheets, sử dụng sức mạnh siêu việt của **Claude AI (Anthropic)** để tạo ra các gợi ý chuyến đi độc đáo, kết hợp dữ liệu thời tiết thời gian thực và gửi trực tiếp qua email cho khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cá nhân hóa 100%:** Claude AI phân tích sâu sắc sở thích, ngân sách, phong cách du lịch và lịch sử của từng khách hàng để đưa ra gợi ý không trùng lặp.
- **Tự động hóa toàn trình:** Từ khâu nhận request, tra cứu dữ liệu Google Sheets, gọi AI, làm giàu dữ liệu (weather/API) đến lưu log và gửi email tự động.
- **Vận hành linh hoạt:** Hỗ trợ cả 2 chế độ: Xử lý theo thời gian thực (qua Webhook khi khách điền form) và Chạy batch tự động hàng ngày/hàng tuần cho toàn bộ danh sách khách hàng active.
- **Tiết kiệm 90% thời gian:** Loại bỏ hoàn toàn các tác vụ tra cứu thủ công và viết email chăm sóc khách hàng truyền thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **Anthropic API Key:** Để kết nối với mô hình Claude AI (Claude Sonnet).
- **Google Sheets Credentials:** Tài khoản Google API / OAuth2 để đọc/ghi dữ liệu từ Google Sheets.
- **SMTP Server / Email Account:** Để gửi email cá nhân hóa (Gmail, SendGrid, SMTP riêng...).
- **Weather API (Tùy chọn):** Dùng cho node làm giàu dữ liệu thời tiết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, sau đó trong giao diện n8n Editor, chọn **Import from File** hoặc copy toàn bộ mã JSON và dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:
- **Google Sheets (các node `Fetch User Travel History`, `Fetch User Profile Data`, `Store Recommendation Record`, `Fetch All Active Users`, `Log Analytics to Sheet`):** Chuẩn bị sẵn một Google Sheet với 4 tabs cơ bản: `user_profiles`, `trip_history`, `recommendations`, và `analytics`. Sau đó kết nối tài khoản Google API và trỏ đúng ID của Sheet vào các node này.
- **Claude Sonnet 4 Model & Claude AI Trip Recommendation Engine:** Chọn Credentials của Anthropic API. Kiểm tra lại tham số mô hình (`claude-sonnet-4-20250514`) và tinh chỉnh prompt trong Agent nếu muốn điều chỉnh văn phong gợi ý của AI.
- **Send Personalized Email & Send Weekly Trend Report:** Cấu hình thông tin kết nối SMTP hoặc dịch vụ gửi email để hệ thống có thể bắn email tự động đến `userEmail`.
- **Receive Trip Suggestion Request (Webhook):** Lấy URL Webhook để tích hợp vào Landing Page, Form đăng ký hoặc ứng dụng của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng dữ liệu mẫu (Sample Payload) qua Webhook để kiểm tra luồng từ đầu đến cuối.
- Kiểm tra kết quả trả về ở Google Sheets và Email cá nhân.
- Gạt công tắc sang **Active** để đưa workflow vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot Telegram/Slack:** Thay vì chỉ gửi email, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn thông báo ngay lập tức về cho bộ phận Sales hoặc cố vấn du lịch khi có khách hàng yêu cầu gợi ý mới.
- **Lưu trữ Log thông minh:** Tận dụng node `Log Analytics to Sheet` để thống kê số lượng request theo ngày, giúp phân tích xu hướng dịch chuyển của khách hàng.
- **Mở rộng API vé máy bay/khách sạn:** Kết nối thêm các API bên thứ ba qua node `Enrich with Weather Data (Optional)` để tự động đính kèm giá vé máy bay hoặc khách sạn thực tế vào gợi ý của AI.

### 📌 Kết luận
Workflow "Generate personalized trip recommendations with Claude AI and Google Sheets" là một cỗ máy tự động hóa hoàn hảo, ứng dụng AI thế hệ mới vào ngành dịch vụ lữ hành. Hãy triển khai ngay hôm nay trên hạ tầng n8n của các sếp để nâng tầm trải nghiệm khách hàng và tối ưu hóa vận hành kinh doanh!