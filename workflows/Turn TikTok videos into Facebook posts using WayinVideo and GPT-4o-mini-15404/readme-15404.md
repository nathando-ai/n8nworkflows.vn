---
title: "🚀 Tự động chuyển đổi video TikTok thành bài đăng Facebook bằng WayinVideo và GPT-4o-mini"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi video TikTok thành bài đăng Facebook chuyên nghiệp với n8n, WayinVideo và GPT-4o-mini. Tiết kiệm thời gian và tăng hiệu quả nội dung."
slug: "tu-dong-chuyen-doi-video-tiktok-thanh-bai-dang-facebook"
tags: [n8n, automation, no-code, social-media, ai]
keywords: [n8n workflow, tự động hóa nội dung, video TikTok, Facebook, GPT-4o-mini, WayinVideo]
---

# 🚀 Tự động chuyển đổi video TikTok thành bài đăng Facebook bằng WayinVideo và GPT-4o-mini

[Các sếp] có biết không? Với lượng video TikTok ngày càng tăng, việc chuyển đổi nội dung sang các nền tảng khác đang trở thành một thách thức lớn. Bạn phải xem video, viết caption, chọn hashtag và đăng lên Facebook - quá nhiều công việc thủ công và dễ sai sót. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này trong vòng vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình từ 6 bước thành 1 workflow duy nhất
- **Nội dung chuyên nghiệp**: GPT-4o-mini tạo ra caption theo các quy tắc Facebook
- **Theo dõi hiệu quả**: Log tất cả bài đăng vào Google Sheets với Post ID và URL
- **Tăng tương tác**: Hashtag và CTA được tối ưu hóa cho Facebook
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo (API Key)
- Tài khoản OpenAI (API Key)
- Trang Facebook (Page ID và Access Token)
- Google Sheets (OAuth2 và Sheet ID)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15404](https://n8n.io/workflows/15404)
2. Click "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 2 & 4 (WayinVideo)**:
   - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API Key thực của bạn
   - Đảm bảo tài khoản WayinVideo có đủ credit

2. **Node 9 (OpenAI)**:
   - Kết nối credential OpenAI của bạn
   - Đảm bảo tài khoản có đủ credit cho GPT-4o-mini

3. **Node 11 (Facebook)**:
   - Thay thế `YOUR_FACEBOOK_PAGE_ID` trong URL
   - Thay thế `YOUR_FACEBOOK_PAGE_ACCESS_TOKEN` trong body
   - Đảm bảo token có quyền `pages_manage_posts`

4. **Node 12 (Google Sheets)**:
   - Kết nối credential Google Sheets OAuth2 của bạn
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet
   - Tạo tab "Facebook Posts" với các cột: Video URL, Video Title, Brand/Page, Facebook Caption, Hashtags, Character Count, Post ID, Post URL, Status, Posted On

#### 3. Kích hoạt ⚡️
1. Test run với URL video TikTok mẫu
2. Kiểm tra kết quả trên Facebook và Google Sheets
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi bài đăng thành công
2. **Lịch đăng bài**: Thêm node để lên lịch đăng bài theo thời gian cụ thể
3. **Phân tích hiệu quả**: Kết nối với Google Analytics để theo dõi lượt tương tác
4. **Nhiều nền tảng**: Sửa đổi workflow để hỗ trợ Instagram và LinkedIn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý nội dung. Bằng cách tự động hóa quy trình chuyển đổi video TikTok thành bài đăng Facebook, các sếp có thể tập trung vào việc tạo nội dung sáng tạo hơn. Hãy thử ngay và nâng cao hiệu quả nội dung của bạn!