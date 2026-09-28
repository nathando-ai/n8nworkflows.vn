---
title: "🚀 Tự động hóa Crawler Website: Chuyển đổi nội dung trang web thành Markdown sẵn sàng cho AI trong Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình thu thập và chuyển đổi nội dung website thành định dạng Markdown, lưu trữ trong Google Sheets để xây dựng cơ sở kiến thức cho AI hoặc lưu trữ nội dung công ty."
slug: "tu-dong-hoa-crawler-website-chuyen-doi-markdown-google-sheets"
tags: [n8n, automation, no-code, web-scraping, google-sheets]
keywords: [n8n workflow, tự động hóa website, chuyển đổi markdown, google sheets, ai knowledge base]
---

# 🚀 Tự động hóa Crawler Website: Chuyển đổi nội dung trang web thành Markdown sẵn sàng cho AI trong Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải thu thập và quản lý nội dung website thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để chuyển đổi nội dung website thành định dạng Markdown và lưu trữ trong Google Sheets.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian thu thập và quản lý nội dung website
- Chuyển đổi tự động nội dung website thành định dạng Markdown chuẩn
- Lưu trữ nội dung trong Google Sheets dễ dàng truy cập và quản lý
- Xây dựng cơ sở kiến thức cho AI hoặc lưu trữ nội dung công ty
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- Instance n8n đã được cài đặt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/9594](https://n8n.io/workflows/9594).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Set Website**: Cập nhật tham số `website_url` với URL của trang web bạn muốn thu thập nội dung.
- **Google Sheets OAuth2 API Setup**:
  1. Truy cập [console.cloud.google.com](https://console.cloud.google.com/) → APIs & Services → Credentials.
  2. Tạo OAuth client ID cho Web application.
  3. Thêm n8n redirect URI: `https://your-n8n-instance.com/rest/oauth2-credential/callback`.
  4. Thêm vào n8n dưới dạng Google Sheets OAuth2 API và cấp quyền truy cập Sheets.
- **Add Images to Sheet, Add Links to Sheet, Add Scraped Content to Sheet**: Cập nhật `documentId` và `sheetName` với ID và tên của Google Sheet của bạn. Đảm bảo sheet có các cột: Website, Links, Scraped Content, Images.

#### 3. Kích hoạt ⚡️
- Thử chạy workflow với dữ liệu mẫu.
- Bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi thu thập nội dung hoàn thành.
- Lưu log các lần thu thập nội dung để theo dõi lịch sử.
- Gửi báo cáo định kỳ về nội dung đã thu thập.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình thu thập và chuyển đổi nội dung website thành định dạng Markdown, lưu trữ trong Google Sheets để xây dựng cơ sở kiến thức cho AI hoặc lưu trữ nội dung công ty. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả quản lý nội dung!