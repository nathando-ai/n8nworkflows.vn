---
title: "🚀 Tự động nhận bản tin An ninh mạng hàng ngày qua Telegram, Slack với GPT-4"
description: "Xây dựng hệ thống Threat Intelligence tự động 100%: Thu thập tin tức từ GNews, NewsAPI, Reddit, xử lý trùng lặp, phân tích bằng GPT-4 và gửi báo cáo qua Telegram, Slack, Email."
slug: "tu-dong-nhan-ban-tin-an-ninh-mang-telegram-slack-gpt4"
tags: [n8n, automation, ai, security, openai, telegram, slack]
keywords: [n8n workflow, an ninh mạng, cybersecurity digest, openai gpt-4, telegram bot, slack automation, threat intelligence]
---

# 🚀 Tự động nhận bản tin An ninh mạng hàng ngày qua Telegram, Slack với GPT-4

Các đội ngũ An ninh mạng (SOC), IT Manager hay Quản trị viên hệ thống thường tốn rất nhiều thời gian mỗi ngày để tổng hợp tin tức bảo mật, lỗ hổng mới (CVE) và các cuộc tấn công từ nhiều nguồn khác nhau. Việc đọc thủ công dễ bỏ sót thông tin quan trọng.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa toàn bộ quy trình: thu thập đa nguồn, loại bỏ tin trùng lặp, dùng **GPT-4** để phân tích, đánh giá mức độ nguy hiểm và gửi bản tin tổng hợp (Digest) trực tiếp đến **Telegram, Slack, Email**, đồng thời lưu trữ vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Lấy tin tức, phân tích và gửi báo cáo theo lịch trình cố định mỗi ngày mà không cần chạm tay.
- **AI thông minh (GPT-4)**: Tự động phân loại (Lỗ hổng, Rò rỉ dữ liệu, Công cụ mới...) và đánh giá mức độ nghiêm trọng (Critical, High, Medium).
- **Lọc tin trùng lặp thông minh**: Sử dụng thuật toán xử lý dữ liệu để loại bỏ các bản tin giống nhau từ nhiều nguồn.
- **Đa kênh phân phối**: Gửi đồng thời tới Telegram, Slack, Email định dạng HTML và lưu trữ lịch sử vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Cloud hoặc Self-hosted)
- **OpenAI API Key** (Dùng cho GPT-4)
- **GNews API Key** (Có gói miễn phí)
- **NewsAPI Key** (Có gói miễn phí)
- **Telegram Bot Token** & Chat ID
- **Slack Workspace** (Webhook hoặc Bot Token)
- **Google Sheets** (Tài khoản Google OAuth2)
- **Email/Gmail Credentials** (Dành cho node gửi email báo cáo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow hoặc tải file JSON từ nguồn cung cấp.
- Trong n8n Editor, bấm vào menu **Add workflow** -> **Import from File** hoặc dán trực tiếp (Ctrl+V) vào giao diện.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Daily Schedule Trigger**: Cài đặt thời gian chạy định kỳ mỗi ngày (ví dụ: 8:00 sáng).
- **GNews API & NewsAPI**: Điền API Key tương ứng vào phần Header hoặc Parameters của node `httpRequest`.
- **OpenAI GPT-4**: Chọn credentials `openAiApi` và đảm bảo model được chọn là `gpt-4-turbo-preview` hoặc model tương đương.
- **Send to Telegram**: Kết nối `telegramApi`, cấu hình Chat ID nhận tin nhắn.
- **Send to Slack**: Kết nối tài khoản Slack và chọn channel nhận bản tin.
- **Archive to Google Sheets**: Chọn file Google Sheets và cấu hình mapping các cột dữ liệu (Tiêu đề, Tóm tắt, Mức độ nguy hiểm, Link).
- **Send a message (Gmail)**: Cấu hình tài khoản `gmailOAuth2` để gửi báo cáo dạng HTML cho ban quản trị.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm và kiểm tra dữ liệu đầu ra ở từng node (`Normalize Articles`, `AI Threat Analysis Agent`...).
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Webhook**: Kết nối thêm node Discord hoặc Microsoft Teams nếu đội ngũ của các sếp sử dụng các nền tảng này thay vì Slack/Telegram.
- **Lưu Log lỗi**: Tận dụng cơ chế xử lý lỗi sẵn có trong workflow để bắn một tin nhắn cảnh báo về kênh Telegram riêng nếu API nguồn bị lỗi (Timeout).
- **Tùy biến Prompt AI**: Tinh chỉnh prompt trong AI Agent để GPT-4 tập trung sâu hơn vào các chủ đề cụ thể như Ransomware, Cloud Security hoặc Zero-day exploits.

### 📌 Kết luận
Hệ thống **Cyber Threat Intelligence Digest** này sẽ giúp các sếp nắm bắt toàn bộ tình hình an ninh mạng thế giới mỗi sáng chỉ trong 1 phút đọc tin. Hãy import workflow ngay và tối ưu hóa quy trình bảo mật cho doanh nghiệp của mình nhé!