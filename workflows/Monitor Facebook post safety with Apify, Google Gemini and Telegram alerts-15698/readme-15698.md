---
title: "🚀 Giám sát an toàn bài viết Facebook tự động với Apify, Google Gemini và Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động quét bài viết Facebook qua Apify, phân tích độ an toàn bằng AI Gemini và gửi cảnh báo trực quan qua Telegram."
slug: "giam-sat-an-toan-facebook-apify-gemini-telegram"
tags: [n8n, automation, ai-agent, facebook-monitor, google-gemini, telegram]
keywords: [n8n workflow, giám sát facebook tự động, apify facebook scraper, google gemini ai, telegram bot automation]
---

# 🚀 Giám sát an toàn bài viết Facebook tự động với Apify, Google Gemini và Telegram

Việc theo dõi thủ công các bài viết và bình luận trên trang Facebook của doanh nghiệp để phát hiện các nội dung nhạy cảm, độc hại hoặc rủi ro truyền thông là một công việc tốn rất nhiều thời gian. Nếu bỏ lỡ, doanh nghiệp có thể đối mặt với khủng hoảng truyền thông bất cứ lúc nào. 

Workflow n8n này do tác giả **Nguyễn Thiệu Toàn (Jay Nguyen)** xây dựng sẽ giải quyết triệt để bài toán trên bằng một hệ thống kép thông minh: vừa tự động quét - phân tích an toàn bài viết nhờ AI, vừa tích hợp Trợ lý ảo AI Chatbot trực tiếp trên Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét bài viết mới trên Facebook theo lịch trình định sẵn mà không cần thao tác thủ công.
- **Phân tích thông minh bằng AI:** Google Gemini đánh giá ngữ cảnh, hình ảnh và phản ứng của người dùng để phát hiện nội dung độc hại (toxic) hoặc rủi ro an toàn.
- **Cảnh báo tức thì:** Gửi báo cáo chi tiết, trực quan kèm emoji qua Telegram ngay khi phát hiện vấn đề.
- **Trợ lý ảo đa năng:** Tích hợp AI Agent trên Telegram với bộ nhớ MongoDB dài hạn, hỗ trợ tra cứu thông tin và xử lý câu hỏi linh hoạt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Self-hosted hoặc Cloud).
- Tài khoản và API Key từ **Apify** (cho Apify Facebook Scraper).
- Tài khoản **Google Gemini (Google AI / Vertex AI)** để kích hoạt các mô hình ngôn ngữ lớn (LLM).
- **Telegram Bot Token** (tạo qua `@BotFather`) và ID Admin cá nhân.
- Cơ sở dữ liệu **MongoDB** để lưu trữ bộ nhớ trò chuyện cho AI Chatbot.
- Tài khoản **SerpAPI** (nếu muốn AI chatbot có khả năng tìm kiếm thông tin web mở rộng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ thư viện n8n hoặc copy trực tiếp mã nguồn, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Set Context (Chat) & Set Context (Scraper):** Mở node này để cập nhật các biến quan trọng như Link trang Facebook mục tiêu (`Target Facebook Page URL`), Telegram Admin ID và giới hạn số lượng bài viết quét mỗi lần (`Scraper post limits`).
- **Telegram Trigger & Send Telegram Reply / Send Notification:** Kết nối tài khoản `telegramApi` với Bot Token của các sếp.
- **Google Gemini Chat Model & Google Gemini Chat Model1:** Thêm thông tin xác thực Google Gemini API Key.
- **Apify Facebook Scraper:** Điền thông tin xác thực `apifyApi` để trích xuất dữ liệu bài viết chuẩn xác.
- **MongoDB Chat Memory / MongoDB Chat Memory 1:** Cấu hình kết nối MongoDB để AI ghi nhớ lịch sử trò chuyện dài hạn.
- **Data Table Upsert & If row does not exist:** Đảm bảo n8n Data Table đã được tạo và chọn đúng trong node Upsert để hệ thống lọc bỏ các bài viết trùng lặp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một vài bài viết mẫu để kiểm tra luồng dữ liệu qua các node xử lý hình ảnh và AI Safety Analysis.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, bật công tắc **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Telegram, các sếp có thể nối thêm node Slack hoặc Discord ở cuối luồng để đồng bộ cảnh báo an toàn vào group chung của đội ngũ vận hành.
- **Lưu lịch sử báo cáo:** Kết nối thêm Google Sheets hoặc Airtable sau bước `Safety Analysis Agent` để lưu trữ toàn bộ lịch sử kiểm duyệt phục vụ việc làm báo cáo định kỳ.
- **Tinh chỉnh Prompt:** Tùy chỉnh system prompt trong AI Safety Agent để siết chặt hoặc nới lỏng các tiêu chuẩn kiểm duyệt nội dung phù hợp với đặc thù riêng của doanh nghiệp.

### 📌 Kết luận
Workflow giám sát an toàn Facebook kết hợp giữa Apify, Google Gemini và Telegram là một giải pháp tự động hóa cực kỳ mạnh mẽ, giúp bảo vệ hình ảnh thương hiệu và tiết kiệm hàng giờ kiểm duyệt thủ công mỗi ngày. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!