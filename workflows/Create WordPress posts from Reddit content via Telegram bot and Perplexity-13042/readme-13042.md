---
title: "🚀 Tự động tạo bài viết WordPress từ Reddit bằng Telegram Bot và AI Perplexity"
description: "Xây dựng hệ thống tự động hóa nội dung hoàn chỉnh với n8n: quét bài viết Reddit hot, gửi ý tưởng qua Telegram để duyệt, dùng Perplexity nghiên cứu chuyên sâu và tự động xuất bản bài viết chuẩn SEO lên WordPress."
slug: "tu-dong-tao-bai-viet-wordpress-tu-reddit-telegram-perplexity"
tags: [n8n, automation, wordpress, reddit, telegram, perplexity, ai-agent]
keywords: [n8n workflow, tự động hóa wordpress, ai viết bài tự động, reddit to wordpress, perplexity api, telegram bot n8n]
---

# 🚀 Tự động tạo bài viết WordPress từ Reddit bằng Telegram Bot và AI Perplexity

Việc lên ý tưởng nội dung, nghiên cứu chuyên sâu và viết bài đăng blog hàng ngày ngốn rất nhiều thời gian của các nhà sáng tạo nội dung và doanh nghiệp. Nếu các sếp đang tìm giải pháp tự động hóa toàn bộ quy trình này mà vẫn giữ được quyền kiểm soát chất lượng nội dung, thì đây chính là "vũ khí tối thượng".

Workflow n8n này sẽ tự động quét các bài viết mới từ Reddit theo ngách (niche) của các sếp, dùng AI tạo ý tưởng và gửi thẳng qua Telegram Bot. Khi các sếp bấm nút phê duyệt, hệ thống sẽ tự động dùng **Perplexity API** để nghiên cứu chuyên sâu, kết hợp **Google Gemini** viết bài chuẩn SEO và xuất bản trực tiếp lên **WordPress** mà không cần đụng tay vào một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa từ khâu tìm kiếm ý tưởng, nghiên cứu, viết bài cho đến đăng blog.
- **Kiểm soát nội dung chặt chẽ:** Ý tưởng bài viết được gửi qua Telegram để các sếp duyệt trước khi AI tiến hành viết.
- **Nội dung chất lượng cao & chuẩn SEO:** Kết hợp dữ liệu nóng từ Reddit, thông tin nghiên cứu real-time từ Perplexity Sonar Pro và tư duy ngôn ngữ từ Google Gemini.
- **Hoạt động 24/7:** Chạy tự động theo lịch trình (Schedule Trigger) hoặc tương tác trực tiếp qua Telegram Webhook.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Reddit API:** Tài khoản Reddit có quyền truy cập API.
- **Telegram Bot:** Một Bot Telegram (tạo qua BotFather) để nhận ý tưởng và gửi phản hồi.
- **Perplexity API Key:** Dùng để nghiên cứu thông tin bài viết chuyên sâu.
- **Google Gemini API (Google Palm API):** Dùng cho các AI Agent và LLM Chain.
- **WordPress Website:** Đã bật REST API hoặc ứng dụng mật khẩu (Application Passwords) để n8n có thể tạo bài viết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Tạo 2 Data Tables trong n8n:**
  1. *Reddit Article Ideas*: Các cột gồm `post_id`, `topic`, `status`.
  2. *Reddit Approved Topics*: Các cột gồm `post_id`, `topic`, `status`, `title`, `url`.
- **Cấu hình SubReddits (`Get Reddit Posts`):** Thêm ít nhất 10-15 subreddits phù hợp với ngách nội dung của sếp.
- **Cấu hình Telegram Bot (`Telegram Webhook` & `Send Article Ideas to User`):** Thêm Telegram Chat ID cá nhân/nhóm và API Credentials của bot.
- **Cấu hình Perplexity (`Research about Approved Topic`):** Chọn model `sonar-pro` và điền Perplexity API credentials.
- **Cấu hình AI & Prompt (`Generate Article Idea`, `Content Generation`, `Title Generation`, `Slug Generation`):** 
  - Kết nối Google Gemini Chat Model.
  - Tùy chỉnh thông tin về Tác giả và Văn phong viết bài trong prompt để nội dung giống người thật viết nhất.
- **Cấu hình WordPress (`WP Post Creation`):** Nhập URL website WordPress và thông tin tài khoản API (Application Passwords), thiết lập trạng thái bài viết mặc định (Draft hoặc Publish).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách kích hoạt thủ công node `Periodic Check for Reddit Posts` để kiểm tra luồng nhận ý tưởng qua Telegram.
- Bấm nút **Active** góc trên cùng bên phải để bật workflow chạy hoàn toàn tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể kết hợp node Slack hoặc Discord để đội ngũ cùng tham gia duyệt bài viết.
- **Lưu trữ backup:** Thêm một node Google Sheets hoặc Airtable để lưu lại lịch sử các bài viết đã xuất bản nhằm phục vụ việc phân tích dữ liệu sau này.
- **Tự động chia sẻ mạng xã hội:** Nối tiếp sau node `WP Post Creation`, thêm các bước tự động đăng URL bài viết mới lên Twitter/X, LinkedIn hoặc Facebook Page.

### 📌 Kết luận
Workflow tự động hóa kết hợp Reddit, Telegram, Perplexity và WordPress này là giải pháp toàn diện giúp các sếp xây dựng hệ thống content marketing "tự vận hành". Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất sản xuất nội dung cho doanh nghiệp của mình!