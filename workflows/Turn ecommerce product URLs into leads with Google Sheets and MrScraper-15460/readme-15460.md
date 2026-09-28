---
title: "🚀 Tự động hóa chuyển đổi URL sản phẩm thành lead với Google Sheets và MrScraper"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình chuyển đổi URL sản phẩm thành lead chất lượng cao bằng n8n, Google Sheets và MrScraper. Tiết kiệm thời gian và nâng cao hiệu quả marketing."
slug: "tu-dong-hoa-chuyen-doi-url-san-pham-thanh-lead"
tags: [n8n, automation, no-code, marketing, lead-generation]
keywords: [n8n workflow, tự động hóa marketing, lead generation, Google Sheets, MrScraper]
---

# 🚀 Tự động hóa chuyển đổi URL sản phẩm thành lead với Google Sheets và MrScraper

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình từ 30-50% thời gian làm việc thủ công.
- Tăng độ chính xác: Giảm sai sót do nhập liệu thủ công.
- Cá nhân hóa: Thu thập thông tin chi tiết về sản phẩm và nhà cung cấp.
- Hoạt động liên tục: Chạy 24/7 mà không cần can thiệp.
- Tích hợp hoàn hảo: Kết nối liền mạch với các công cụ marketing hiện có.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace với quyền truy cập Google Sheets.
- API key từ MrScraper và SERP API.
- Tài khoản n8n đã được cài đặt và cấu hình.
- 2 Google Sheets đã được tạo (chi tiết bên dưới).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n Community](https://n8n.io/workflows/15460) và tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải.
3. Hoặc copy toàn bộ nội dung JSON và dán vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Google Sheets**:
   - Tạo 2 Google Sheets: Product URL Queue và Leads Output.
   - Thêm các cột yêu cầu vào mỗi sheet (chi tiết trong phần Setup).
   - Thêm Google Sheets OAuth2 credential vào n8n và kết nối với các node Google Sheets.

2. **Cấu hình MrScraper**:
   - Thêm MrScraper API credential vào n8n.
   - Thay thế các placeholder trong các node MrScraper (YOUR_MRSCRAPER_API_TOKEN).
   - Tạo các scraper cần thiết (Product Detail, Contact URL Finder, Contact Detail).

3. **Cấu hình SERP API**:
   - Thêm thông tin API endpoint và token vào node HTTP Request.
   - Thay thế placeholder YOUR_SERP_API_TOKEN.

4. **Thay thế các placeholder khác**:
   - YOUR_PRODUCT_URL_SHEET_ID
   - YOUR_LEADS_SHEET_ID
   - YOUR_WORKFLOW_ID
   - YOUR_N8N_API_KEY

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ bên ngoài.
2. Chạy workflow với 1-3 URL sản phẩm mẫu để kiểm tra.
3. Sau khi xác nhận hoạt động ổn định, kích hoạt workflow chính thức.

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu hóa batch size**: Giảm batch size nếu gặp giới hạn API.
2. **Tùy chỉnh bộ lọc URL công ty**: Chỉnh sửa danh sách blacklist và trọng số trong node Filter Legit Company Profile Url.
3. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành.
4. **Lưu log hoạt động**: Thêm node ghi log các hoạt động quan trọng vào Google Sheets.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình chuyển đổi URL sản phẩm thành lead chất lượng cao. Bằng cách kết hợp Google Sheets, MrScraper và SERP API, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu quả marketing. Hãy thử nghiệm với một số URL sản phẩm mẫu trước khi triển khai quy mô lớn.