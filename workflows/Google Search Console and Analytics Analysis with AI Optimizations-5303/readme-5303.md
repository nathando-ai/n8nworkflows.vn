---
title: "🚀 Phân tích Google Search Console & Analytics tự động bằng AI với n8n"
description: "Tự động trích xuất dữ liệu từ sitemap, kết hợp Google Search Console, Google Analytics và OpenAI để phân tích SEO thông minh và gửi báo cáo chi tiết qua email."
slug: "phan-tich-seo-google-search-console-analytics-ai-n8n"
tags: [n8n, automation, seo, google-search-console, google-analytics, openai, ai-agent]
keywords: [n8n workflow, phân tích seo ai, google search console n8n, google analytics automation, tự động hóa seo, openai seo report]
---

# 🚀 Phân tích Google Search Console & Analytics tự động bằng AI với n8n

Các sếp làm SEO hay quản trị website chắc chắn đã quen thuộc với việc mất hàng giờ đồng hồ mò mẫm trong Google Search Console (GSC) và Google Analytics (GA4) để tổng hợp số liệu, tìm từ khóa rớt hạng hay trang web cần tối ưu. Công việc thủ công này vừa tẻ nhạt, vừa dễ bỏ sót cơ hội vàng.

Đã đến lúc "lên đời" quy trình làm việc với workflow n8n cực kỳ mạnh mẽ: **Google Search Console and Analytics Analysis with AI Optimizations**. Workflow này sẽ tự động hóa từ A-Z: quét sitemap website, thu thập dữ liệu GSC & GA4, đưa qua AI Agent (OpenAI) để phân tích chuyên sâu, và tự động gửi bảng báo cáo HTML đẹp mắt thẳng vào hộp thư của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần copy-paste thủ công số liệu từ nhiều nền tảng.
- **Phân tích chuẩn chuyên gia SEO:** Tận dụng AI Agent kết hợp OpenAI để đánh giá sâu sắc hiệu suất từng trang.
- **Báo cáo trực quan:** Nhận ngay email tổng hợp dưới dạng bảng HTML chuyên nghiệp ngay trong hộp thư.
- **Chạy định động liên tục:** Có thể cấu hình lịch chạy hàng tuần/hàng tháng để theo dõi sát sao sức khỏe website.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản Google:** Đã kết nối Google Search Console và Google Analytics (GA4).
- **OpenAI API Key:** Để sử dụng mô hình AI phân tích dữ liệu.
- **SMTP Server:** (Gmail, SendGrid, Resend, v.v.) để gửi email báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes được sắp xếp logic. Các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Node `Globals - CHANGE ME!` (Set):** Đây là nơi quan trọng nhất để thiết lập thông số website của các sếp:
  - `sitemap_url`: Đường dẫn sitemap XML của website (ví dụ: `https://example.com/sitemap.xml`).
  - `search_console_selector`: Định dạng theo cú pháp GSC (ví dụ: `sc-domain:example.com` hoặc dạng URL tùy cách cài đặt).
  - `analysis_start_date` & `analysis_end_date`: Khoảng thời gian phân tích dữ liệu (mặc định 30 ngày gần nhất).
  - `analytics_selector_id`: ID của Google Analytics (là dãy số nguyên dài nằm sau chữ `p` trên URL GA4 của sếp, ví dụ: `p123456789`).
  - `report_receiver`: Địa chỉ email nhận báo cáo hoàn thiện.
- **Node `OpenAI Chat Model` & `SEO analyst` (Agent):** Chọn credentials OpenAI và chọn model (workflow mặc định dùng `o4-mini`, các sếp có thể đổi sang `gpt-4o` nếu muốn).
- **Node `Get Page GSC Status`, `Get Page GSC Stats`, `Get Google Analytics Data`:** Kết nối tài khoản Google OAuth2 của các sếp để cấp quyền đọc dữ liệu GSC và GA4.
- **Node `Send Email with Full report`:** Cấu hình credentials SMTP để gửi email.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** để chạy thử nghiệm xem dữ liệu từ sitemap có được lọc, AI có phân tích và email có gửi đi thành công không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** để workflow tự động hóa hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo nhanh qua chat ngay sau khi email báo cáo hoàn tất để team kịp thời nắm bắt.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets ở cuối luồng để lưu trữ lại các đánh giá của AI theo thời gian, giúp dễ dàng so sánh hiệu quả SEO qua các tháng.
- **Chạy tự động định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để chạy báo cáo tự động mỗi thứ Hai hàng tuần.

### 📌 Kết luận
Với workflow n8n này, việc audit SEO và theo dõi hiệu suất website không còn là cơn ác mộng tốn thời gian nữa. Hãy thiết lập ngay hôm nay để để AI làm việc vất vả thay cho các sếp!