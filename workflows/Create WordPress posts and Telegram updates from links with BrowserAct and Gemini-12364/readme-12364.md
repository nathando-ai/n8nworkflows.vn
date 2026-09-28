---
title: "🚀 Tự động tạo bài viết WordPress và cập nhật Telegram từ Link bằng BrowserAct và Gemini"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động hóa n8n: Cào dữ liệu bài viết bằng BrowserAct, xử lý thông minh với Gemini, tạo ảnh độc quyền và xuất bản đồng thời lên WordPress và Telegram."
slug: "tao-wordpress-post-telegram-tu-link-browseract-gemini"
tags: [n8n, automation, wordpress, telegram, gemini, ai-agent, browseract]
keywords: [n8n workflow, tự động hóa wordpress, browseract n8n, gemini ai content, auto post telegram]
---

# 🚀 Tự động tạo bài viết WordPress và cập nhật Telegram từ Link với BrowserAct & Gemini

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công đi copy bài viết từ các trang tin, viết lại chuẩn SEO, thiết kế ảnh đại diện, sau đó lại loay hoay đăng lên website rồi chia sẻ lên Telegram? Quá nhiều thao tác lặp đi lặp lại khiến tốn hàng giờ đồng hồ mỗi ngày!

Giải pháp đây rồi! Workflow n8n siêu cấp này sẽ giúp các sếp tự động hóa 100% quy trình: **Gửi link vào Telegram Bot ➡️ AI tự động cào nội dung, viết lại bài chuẩn SEO ➡️ Tạo ảnh minh họa độc quyền ➡️ Đăng lên WordPress ➡️ Gửi thông báo kèm ảnh và link về Telegram**. Tất cả diễn ra chỉ trong vài giây mà không cần đụng một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến việc tổng hợp tin tức, viết bài và đăng mạng xã hội thành một cú click gửi link qua Telegram.
- **Nội dung chuẩn SEO & Độc quyền:** AI (Gemini & OpenRouter) hỗ trợ viết lại bài viết mạch lạc, chia cấu trúc HTML chuyên nghiệp.
- **Tự động hóa đa kênh:** Đăng bài lên WordPress website và phát sóng (broadcast) ngay lập tức lên kênh Telegram cá nhân hoặc cộng đồng.
- **Hoạt động 24/7:** Bot Telegram luôn sẵn sàng nhận yêu cầu bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **BrowserAct Account & API Key:** Nền tảng cào dữ liệu web (cần lưu sẵn template *Telegram and WordPress Post Architect*).
- **Telegram Bot Token:** Tạo qua `@BotFather`.
- **WordPress Site:** Tài khoản quản trị và cài đặt ứng dụng mật khẩu (Application Passwords) để n8n gọi API.
- **OpenRouter API Key & Google Gemini (Google Palm) API Key:** Dành cho các LangChain Agent xử lý ngôn ngữ và tạo ảnh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n hoặc copy toàn bộ JSON workflow, sau đó vào giao diện n8n Editor chọn **Import from JSON** để dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong các node:
- **User Sends Message to Bot (`telegramTrigger`):** Kết nối với Credentials của Telegram Bot của sếp để nhận tin nhắn gửi link.
- **Extract Data from Target Site (`BrowserAct`):** Nhập BrowserAct API Key và đảm bảo đã thiết lập template *Telegram and WordPress Post Architect* trên nền tảng BrowserAct.
- **OpenRouter & Google Gemini Nodes (`OpenRouter`, `Generate an image`, `Analyze Input & Generate Article`, v.v.):** Điền API Key tương ứng để các Agent AI có "năng lượng" hoạt động phân tích và viết bài.
- **Publish Post via WordPress & Upload Image To Wordpress (`wordpress` & `httpRequest`):** 
  - Kết nối Credentials tài khoản WordPress.
  - ⚠️ **LƯU Ý QUAN TRỌNG:** Các sếp phải tìm và thay thế đường dẫn mặc định `YourWordPressAddress.com` thành tên miền website thật của các sếp (ví dụ: `your-actual-site.com`).
- **Send a photo And caption (`telegram`):** Cấu hình Chat ID của kênh hoặc nhóm Telegram muốn nhận thông báo tự động.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một đường băng tin tức bất kỳ vào Telegram Bot của các sếp để test luồng chạy.
- Kiểm tra kết quả trên WordPress Draft/Publish và Telegram Bot.
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** góc trên cùng bên phải để workflow trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable vào sau bước xử lý bài viết để lưu lại lịch sử các link đã xử lý.
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord để đội ngũ nội dung cùng nhận được thông báo khi có bài viết mới xuất bản.
- **Kiểm duyệt trước khi đăng:** Thay vì publish trực tiếp lên WordPress, cấu hình node WordPress ở trạng thái `Draft` (Bản nháp) để các sếp review lại nội dung trước khi bấm xuất bản chính thức.

### 📌 Kết luận
Workflow "Create WordPress posts and Telegram updates from links with BrowserAct and Gemini" là một cỗ máy tự động hóa hoàn hảo cho các nhà sáng tạo nội dung, marketer và chủ website. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc và để AI gánh vác các công việc thủ công nặng nhọc thay cho các sếp!