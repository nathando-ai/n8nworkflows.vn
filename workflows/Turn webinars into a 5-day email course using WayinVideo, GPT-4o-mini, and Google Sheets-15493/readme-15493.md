```yaml
---
title: "🚀 Tự động chuyển đổi webinar thành khóa học email 5 ngày bằng WayinVideo + GPT-4o-mini + Google Sheets"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi webinar thành khóa học email 5 ngày sử dụng n8n, WayinVideo, GPT-4o-mini và Google Sheets. Tiết kiệm thời gian và nâng cao hiệu quả marketing."
slug: "tu-dong-chuyen-doi-webinar-thanh-khoa-hoc-email-5-ngay"
tags: [n8n, automation, no-code, wayinvideo, google-sheets, gpt-4o-mini, content-creation]
keywords: [n8n workflow, tự động hóa webinar, khóa học email, wayinvideo, gpt-4o-mini, google sheets]
---
```

# 🚀 Tự động chuyển đổi webinar thành khóa học email 5 ngày bằng WayinVideo + GPT-4o-mini + Google Sheets

[Các sếp] có biết rằng việc chuyển đổi webinar thành khóa học email 5 ngày là một công việc tốn thời gian và công sức không nhỏ? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, giúp tiết kiệm thời gian quý giá và nâng cao hiệu quả marketing.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình chuyển đổi từ 2-3 ngày xuống còn vài phút.
- Nâng cao hiệu quả: Tạo ra nội dung chất lượng cao với sự hỗ trợ của AI.
- Cá nhân hóa: Tùy chỉnh nội dung email phù hợp với đối tượng mục tiêu.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WayinVideo với API key.
- Tài khoản OpenAI với API key.
- Tài khoản Google với quyền truy cập Google Sheets.
- Google Sheet có sẵn với tên tab "Drip Email Course" và các cột: Webinar Title, Course Name, Day Number, Email Subject, Preview Text, Email Body, Key Takeaway, CTA Text, CTA URL Placeholder, Word Count, Clip Title, Clip Score, Clip Timestamp, Webinar URL, Generated On, Status.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link: [https://n8n.io/workflows/15493](https://n8n.io/workflows/15493).
3. Hoặc tải file JSON về và import từ local.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node 2. WayinVideo — Submit AI Clipping**: Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API key của WayinVideo.
- **Node 4. WayinVideo — Get Clip Results**: Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng API key của WayinVideo.
- **Node 9. OpenAI — GPT-4o-mini Model**: Kết nối với OpenAI credential của các sếp.
- **Node 11. Google Sheets — Save Email Course**: Kết nối với Google Sheets OAuth2 credential và thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test run với dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheet để đảm bảo dữ liệu được lưu đúng.
3. Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi workflow hoàn thành.
- Lưu log các lần chạy để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về hiệu quả của khóa học email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình chuyển đổi webinar thành khóa học email 5 ngày một cách nhanh chóng và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả marketing!