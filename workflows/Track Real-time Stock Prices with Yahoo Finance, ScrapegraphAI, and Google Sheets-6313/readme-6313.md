---
title: "📈 Theo dõi giá cổ phiếu thời gian thực với Yahoo Finance, ScrapegraphAI và Google Sheets"
description: "Tự động hóa việc theo dõi giá cổ phiếu thời gian thực bằng n8n, kết hợp Yahoo Finance, ScrapegraphAI và Google Sheets để lưu trữ và phân tích dữ liệu"
slug: "theo-doi-gia-co-phieu-thoi-gian-thuc-yahoo-finance-scrapegraphai-google-sheets"
tags: [n8n, automation, no-code, crypto trading, ai summarization]
keywords: [n8n workflow, tự động hóa, theo dõi giá cổ phiếu, Yahoo Finance, ScrapegraphAI, Google Sheets]
---

# 📈 Theo dõi giá cổ phiếu thời gian thực với Yahoo Finance, ScrapegraphAI và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư khi phải theo dõi giá cổ phiếu thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Theo dõi giá cổ phiếu thời gian thực một cách tự động và chính xác
- Lưu trữ dữ liệu lịch sử giá cổ phiếu trong Google Sheets
- Phân tích dữ liệu dễ dàng với các công cụ của Google Sheets
- Nhận thông báo giá cổ phiếu theo lịch trình đã đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để sử dụng Google Sheets
- API Key từ ScrapegraphAI
- Tài khoản Yahoo Finance để truy cập dữ liệu giá cổ phiếu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/6313](https://n8n.io/workflows/6313)
2. Nhấp vào nút "Import" để thêm workflow vào n8n của bạn
3. Hoặc copy/paste JSON workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger Node**:
   - Cấu hình thời gian kích hoạt workflow theo lịch trình của bạn
   - Có thể chọn thời gian cố định hoặc theo lịch trình định kỳ

2. **ScrapegraphAI Node**:
   - Thêm credentials cho ScrapegraphAI
   - Cấu hình URL của trang web bạn muốn scrape (ví dụ: trang Yahoo Finance)
   - Nhập hướng dẫn để scrape dữ liệu (ví dụ: "Extract stock prices from this page")

3. **Code Node**:
   - Kiểm tra và chỉnh sửa mã JavaScript nếu cần thiết để xử lý dữ liệu đầu ra từ ScrapegraphAI
   - Đảm bảo dữ liệu được định dạng đúng để lưu vào Google Sheets

4. **Google Sheets Node**:
   - Thêm credentials cho Google Sheets
   - Chọn spreadsheet và worksheet mục tiêu
   - Cấu hình các trường dữ liệu để lưu vào Google Sheets
   - Đặt operation thành "Append" để thêm dữ liệu mới vào hàng mới

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Bật Active workflow để bắt đầu theo dõi giá cổ phiếu thời gian thực

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo giá cổ phiếu thời gian thực
- Lưu log hoạt động của workflow để theo dõi lịch sử thực thi
- Gửi báo cáo giá cổ phiếu định kỳ qua email
- Kết hợp với các công cụ phân tích dữ liệu khác để tạo báo cáo chi tiết

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn chỉnh để theo dõi giá cổ phiếu thời gian thực và lưu trữ dữ liệu vào Google Sheets. Với các sếp, việc áp dụng workflow này sẽ tiết kiệm thời gian đáng kể và giúp bạn đưa ra quyết định đầu tư thông minh hơn. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!