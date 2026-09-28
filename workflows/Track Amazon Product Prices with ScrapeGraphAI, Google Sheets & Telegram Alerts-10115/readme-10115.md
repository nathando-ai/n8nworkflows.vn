---
title: "🛒 Theo dõi giá sản phẩm Amazon tự động với ScrapeGraphAI, Google Sheets & Telegram Alerts"
description: "Hướng dẫn tự động hóa theo dõi giá sản phẩm Amazon, cập nhật Google Sheets và nhận thông báo Telegram khi giá giảm"
slug: "theo-doi-gia-amazon-tu-dong"
tags: [n8n, automation, no-code, amazon, google-sheets, telegram]
keywords: [n8n workflow, tự động hóa giá sản phẩm, theo dõi giá Amazon, ScrapeGraphAI, Google Sheets, Telegram]
---

# 🛒 Theo dõi giá sản phẩm Amazon tự động với ScrapeGraphAI, Google Sheets & Telegram Alerts

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Theo dõi giá sản phẩm Amazon tự động hàng ngày
- Cập nhật giá thấp nhất vào Google Sheets
- Nhận thông báo Telegram ngay khi giá giảm dưới ngưỡng đặt
- Tiết kiệm thời gian và công sức thủ công
- Dễ dàng quản lý danh sách sản phẩm theo dõi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ScrapeGraphAI (đăng ký miễn phí tại [ScrapeGraphAI](https://dashboard.scrapegraphai.com/?via=n3witalia))
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Telegram và ID Telegram của bạn
- Google Sheets mẫu đã được sao chép từ [đây](https://docs.google.com/spreadsheets/d/1_FBegOUXt3657og_ScfuiLCERWHtxDWn14799HkVrUo/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link workflow: https://n8n.io/workflows/10115
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Scrape Amazon Product Price node**:
   - Thêm credentials cho ScrapeGraphAI
   - Điền API Key từ tài khoản ScrapeGraphAI của bạn

2. **Get products node**:
   - Thêm credentials cho Google Sheets OAuth2
   - Điền ID của Google Sheet đã sao chép
   - Đảm bảo Sheet có tên là "Products"

3. **Update price node**:
   - Sử dụng cùng credentials với node Get products
   - Đảm bảo Sheet có tên là "Products"

4. **Send alert node**:
   - Thêm credentials cho Telegram API
   - Điền ID Telegram của bạn (có thể lấy từ @userinfobot)

#### 3. Kích hoạt ⚡️
1. Thiết lập lịch chạy (Schedule Trigger) theo nhu cầu của bạn
2. Test run dữ liệu mẫu
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm nhiều hơn 1 kênh thông báo (ví dụ: Slack, Email)
- Thiết lập cảnh báo giá tăng đột biến
- Kết hợp với workflow khác để tự động đặt hàng khi giá giảm
- Thêm cột "Last Updated" để theo dõi thời gian cập nhật giá
- Thiết lập cảnh báo khi sản phẩm hết hàng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi giá sản phẩm Amazon. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các hoạt động quan trọng hơn trong kinh doanh. Hãy thử ngay và nâng cao hiệu quả quản lý sản phẩm của bạn!