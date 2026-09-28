---
title: "📊 Theo dõi xếp hạng từ khóa hàng tuần với Google SERP, Serper API và Google Sheets"
description: "Tự động hóa theo dõi xếp hạng từ khóa hàng tuần bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả SEO"
slug: "theo-doi-xep-hang-tu-khoa-hang-tuan-voi-google-serp-serper-api-va-google-sheets"
tags: [n8n, automation, no-code, seo, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi xếp hạng từ khóa, seo, google sheets]
---

# 📊 Theo dõi xếp hạng từ khóa hàng tuần với Google SERP, Serper API và Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi xếp hạng từ khóa hàng tuần bằng tay. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, tiết kiệm thời gian quý giá và giảm thiểu lỗi con người.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** theo dõi xếp hạng từ khóa hàng tuần
- Dữ liệu xếp hạng được cập nhật **tự động hàng tuần** vào Google Sheets
- Giảm thiểu lỗi con người trong quá trình theo dõi thủ công
- Có thể **tự động hóa báo cáo** hàng tuần cho bộ phận Marketing
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Service Account (để truy cập Google Sheets)
- Google Sheet chứa danh sách từ khóa cần theo dõi (ít nhất các cột: `Keyword`, `Target Page`, `Sr.no`)
- API Key của Serper (đăng ký tại [serper.dev](https://serper.dev))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8225](https://n8n.io/workflows/8225)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Targeted Keywords"**:
   - Thay thế `your-google-sheet-id` bằng ID của Google Sheet chứa từ khóa
   - Thay thế `your-sheet-name` bằng tên sheet chứa từ khóa
   - Chọn Google Service Account credentials đã được thiết lập trong n8n

2. **Node "Keyword Searching on Google"**:
   - Thêm Serper API key vào credentials của n8n (tên credentials: `serperApiKey`)

3. **Node "Extracting Ranking & URL"**:
   - (Tùy chọn) Cập nhật biến `HARDCODED_DOMAIN` nếu cần theo dõi domain khác

4. **Node "Update Rank and URLs (Google Sheet)"**:
   - Thay thế `your-google-sheet-id` bằng ID của Google Sheet chứa kết quả
   - Thay thế `your-sheet-name` bằng tên sheet chứa kết quả
   - Chọn Google Service Account credentials đã được thiết lập trong n8n

5. **Node "Run Every Monday"**:
   - (Tùy chọn) Điều chỉnh biểu thức CRON nếu cần chạy vào thời gian khác

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử với dữ liệu mẫu
2. Sau khi kiểm tra kết quả, click vào nút "Active workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo hàng tuần cho bộ phận Marketing
- Kết hợp với Slack/Telegram để thông báo khi từ khóa đạt được xếp hạng mong muốn
- Lưu log các thay đổi xếp hạng để phân tích xu hướng
- Tự động hóa báo cáo định kỳ với Google Data Studio

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc theo dõi xếp hạng từ khóa hàng tuần. Bằng cách tự động hóa toàn bộ quy trình này, các sếp có thể tập trung vào các chiến lược quan trọng hơn và nâng cao hiệu quả SEO cho doanh nghiệp. Hãy thử ngay và trải nghiệm sự khác biệt!