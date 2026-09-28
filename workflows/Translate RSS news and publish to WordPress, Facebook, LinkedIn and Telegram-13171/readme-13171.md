---
title: "🚀 Tự động hóa dịch tin tức RSS và đăng lên WordPress, Facebook, LinkedIn và Telegram"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình dịch tin tức từ RSS và đăng lên các nền tảng xã hội với n8n. Tiết kiệm thời gian và nâng cao hiệu quả truyền thông."
slug: "tu-dong-hoa-dich-tin-tuc-rss-va-dang-len-wordpress-facebook-linkedin-telegram"
tags: [n8n, automation, no-code, content creation, social media]
keywords: [n8n workflow, tự động hóa, dịch tin tức, đăng bài xã hội, WordPress, Facebook, LinkedIn, Telegram]
---

# 🚀 Tự động hóa dịch tin tức RSS và đăng lên WordPress, Facebook, LinkedIn và Telegram

[Các sếp] có biết không? Với việc đọc tin tức hàng ngày, các sếp thường phải tốn nhiều thời gian để dịch và đăng lên nhiều nền tảng khác nhau. Hãy để n8n làm việc này thay các sếp nhé!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian dịch và đăng tin tức lên nhiều nền tảng
- Tự động hóa quy trình dịch tin tức từ RSS sang nhiều ngôn ngữ
- Đăng bài đồng bộ lên WordPress, Facebook, LinkedIn và Telegram
- Tăng cường hiệu quả truyền thông với nội dung được cá nhân hóa
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WordPress với quyền đăng bài
- Tài khoản Facebook với quyền đăng bài
- Tài khoản LinkedIn với quyền đăng bài
- Tài khoản Telegram với quyền gửi tin nhắn
- API key Google Translate
- URL của RSS feed bạn muốn theo dõi
- Hình ảnh watermark (nếu muốn thêm)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13171](https://n8n.io/workflows/13171)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger (hourly)**: Cấu hình thời gian chạy workflow theo nhu cầu của bạn
2. **RSS News Sites Urls**: Thay đổi URL của RSS feed bạn muốn theo dõi
3. **Sets Translate Language Code**: Thay đổi mã ngôn ngữ đích (ví dụ: "vi" cho tiếng Việt)
4. **WordPress Credentials**: Cấu hình thông tin đăng nhập WordPress của bạn
5. **Facebook Graph API Credentials**: Cấu hình thông tin đăng nhập Facebook
6. **LinkedIn Credentials**: Cấu hình thông tin đăng nhập LinkedIn
7. **Telegram Credentials**: Cấu hình thông tin đăng nhập Telegram
8. **Google Translate API Key**: Thêm API key Google Translate của bạn
9. **Edit Image (Add Watermark)**: Cấu hình hình ảnh watermark nếu muốn sử dụng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, click vào nút "Activate" để kích hoạt workflow
2. Test run với một bài viết mẫu để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi thông báo qua Discord hoặc Microsoft Teams để theo dõi quá trình chạy workflow
2. Tùy chỉnh nội dung bài viết trước khi đăng bằng node "Code (Prepare Post)"
3. Thêm node lưu log hoạt động vào Google Sheets để theo dõi hiệu suất workflow
4. Kết hợp với workflow khác để tự động hóa thêm các tác vụ liên quan đến nội dung

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc dịch và đăng tin tức lên nhiều nền tảng. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các công việc quan trọng hơn và nâng cao hiệu quả truyền thông của mình. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!