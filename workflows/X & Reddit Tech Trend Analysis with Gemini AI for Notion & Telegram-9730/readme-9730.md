---
title: "🚀 Tự động hóa phân tích xu hướng công nghệ từ Reddit & X (Twitter) với Gemini AI cho Notion & Telegram"
description: "Workflow n8n tự động thu thập xu hướng công nghệ từ Reddit và X (Twitter), phân tích bằng AI Gemini và gửi báo cáo tự động vào Notion và Telegram. Tiết kiệm 80% thời gian theo dõi thị trường."
slug: "tu-dong-hoa-phan-tich-xu-huong-cong-nghe-reddit-x-gemini-notion-telegram"
tags: [n8n, automation, no-code, ai, social-media]
keywords: [n8n workflow, tự động hóa, phân tích xu hướng, Reddit, X (Twitter), Gemini AI, Notion, Telegram]
---

# 🚀 Tự động hóa phân tích xu hướng công nghệ từ Reddit & X (Twitter) với Gemini AI cho Notion & Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ cảm thấy mệt mỏi khi phải theo dõi xu hướng công nghệ hàng ngày trên Reddit và X (Twitter)? Khi phải thu thập thông tin từ nhiều subreddit khác nhau, lọc những nội dung quan trọng và tổng hợp lại thành báo cáo? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài phút!

Workflow này sẽ tự động:
1. Thu thập bài viết từ các subreddit công nghệ hàng đầu
2. Phân tích nội dung bằng AI Gemini để tìm ra xu hướng quan trọng
3. Tạo báo cáo tự động trong Notion
4. Gửi thông báo qua Telegram

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** theo dõi thị trường công nghệ hàng ngày
- Nhận báo cáo **tự động hóa** với nội dung chính xác và chi tiết
- **Cá nhân hóa** báo cáo theo nhu cầu của từng doanh nghiệp
- **Hoạt động liên tục** 24/7 mà không cần can thiệp
- **Tăng cường quyết định** với dữ liệu thị trường cập nhật liên tục
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **Google Cloud** để sử dụng Google Gemini API
- Tài khoản **Reddit Developer** để truy cập API
- Tài khoản **Twitter Developer** để truy cập API
- Tài khoản **Notion** để lưu trữ báo cáo
- Tài khoản **Telegram** để nhận thông báo
- **API Keys** cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/9730)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình thời gian chạy workflow (ví dụ: hàng ngày lúc 8h sáng)

2. **Node "Google Gemini Chat Model4" và "Google Gemini Chat Model5"**:
   - Tạo credentials cho Google Cloud
   - Nhập API Key và cấu hình model (ví dụ: gemini-pro)

3. **Node "Get many posts in Reddit" (các node Reddit)**:
   - Tạo credentials cho Reddit Developer
   - Nhập Client ID, Client Secret và User Agent
   - Cấu hình các subreddit cần theo dõi (ví dụ: technology, AI, programming)

4. **Node "Search Tweets in X"**:
   - Tạo credentials cho Twitter Developer
   - Nhập API Key, API Secret Key, Access Token và Access Token Secret
   - Cấu hình các từ khóa tìm kiếm (ví dụ: #AI, #MachineLearning)

5. **Node "Create a page" và "Append a block" (Notion)**:
   - Tạo credentials cho Notion
   - Nhập Internal Integration Token
   - Cấu hình Database ID và các trường cần lưu (ví dụ: Title, Content, Date)

6. **Node "Send a text message1" (Telegram)**:
   - Tạo credentials cho Telegram Bot
   - Nhập Bot Token và Chat ID

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Sau khi test thành công, workflow sẽ chạy tự động theo lịch trình đã cài đặt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh báo cáo**: Thay đổi prompt trong node AI Agent để phù hợp với nhu cầu phân tích cụ thể của doanh nghiệp
2. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo cùng lúc với Telegram
3. **Lưu log hoạt động**: Thêm node để lưu log các bài viết đã phân tích vào Google Sheets
4. **Gửi báo cáo định kỳ**: Cấu hình lịch trình gửi báo cáo hàng tuần/tháng qua email

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi thị trường công nghệ. Với khả năng tự động hóa mạnh mẽ và tích hợp AI Gemini, các sếp có thể nhận được báo cáo chất lượng cao mà không cần phải can thiệp trực tiếp. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!