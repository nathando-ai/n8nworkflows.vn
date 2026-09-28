---
title: "🚀 Tự động hóa Nghiên cứu SERP với Scrape.do API & Google Sheets"
description: "Hướng dẫn tự động hóa nghiên cứu từ khóa trên Google với n8n, Scrape.do và Google Sheets - tiết kiệm thời gian và tăng hiệu quả SEO"
slug: "tu-dong-hoa-nghien-cuu-serp-voi-scrape-do-va-google-sheets"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa, nghiên cứu từ khóa, seo, scrape.do]
---

# 🚀 Tự động hóa Nghiên cứu SERP với Scrape.do API & Google Sheets

[Các sếp đang làm thủ công việc nghiên cứu từ khóa trên Google để tối ưu hóa SEO? Hãy để workflow này giúp các sếp tiết kiệm thời gian và tăng hiệu quả SEO với giải pháp tự động hóa hoàn toàn không cần code!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình nghiên cứu từ khóa
- **Chính xác cao**: Lấy dữ liệu trực tiếp từ Google Search
- **Cá nhân hóa**: Phân tích theo từ khóa và quốc gia cụ thể
- **Hoạt động liên tục**: Chạy tự động theo lịch trình hoặc khi cần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- API Key từ Scrape.do (đăng ký tại [dashboard.scrape.do](https://dashboard.scrape.do/))
- Google Sheet chứa danh sách từ khóa cần nghiên cứu (cấu trúc cột: 'Keyword' và 'Target Country')
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8917](https://n8n.io/workflows/8917)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Keywords from Sheet"**:
   - Chọn credentials là "googleSheetsOAuth2Api"
   - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của Google Sheet chứa từ khóa
   - Thay thế `YOUR_GOOGLE_SHEETS_CREDENTIAL_ID` bằng ID của credentials Google Sheets
   - Đảm bảo Google Sheet có cấu trúc cột: 'Keyword' và 'Target Country'

2. **Node "Fetch Google Search Results"**:
   - Thay thế `YOUR_SCRAPEDO_TOKEN` bằng API Key từ Scrape.do
   - Đảm bảo đã kích hoạt JavaScript rendering trong Scrape.do

3. **Node "Append Results to Sheet"**:
   - Đảm bảo Google Sheet có tab "Results" để lưu kết quả
   - Nếu chưa có, tạo tab mới với tên "Results" trong cùng Google Sheet

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheet
3. Bật chế độ "Active" để workflow chạy tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động để theo dõi lịch sử nghiên cứu
- Tự động gửi báo cáo định kỳ qua email với kết quả phân tích
- Kết hợp với các công cụ khác như Ahrefs hoặc SEMrush để phân tích sâu hơn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc nghiên cứu từ khóa SEO. Bằng cách tự động hóa toàn bộ quy trình từ lấy dữ liệu đến phân tích, các sếp có thể tập trung vào việc tối ưu hóa chiến lược SEO hiệu quả hơn. Hãy áp dụng ngay để nâng cao hiệu quả công việc!