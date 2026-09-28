---
title: "📈 Tự động theo dõi giá cổ phiếu với ScrapeGraphAI, Yahoo Finance & Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi giá cổ phiếu bằng n8n, kết hợp ScrapeGraphAI và Google Sheets để lưu trữ dữ liệu lịch sử"
slug: "tu-dong-theo-doi-gia-co-phieu-voi-scrapegraphai-yahoo-finance-google-sheets"
tags: [n8n, automation, no-code, stock-market, google-sheets]
keywords: [n8n workflow, tự động hóa giá cổ phiếu, ScrapeGraphAI, Yahoo Finance, Google Sheets]
---

# 📈 Tự động theo dõi giá cổ phiếu với ScrapeGraphAI, Yahoo Finance & Google Sheets

[Các sếp đang làm việc với dữ liệu cổ phiếu thủ công? Bạn mệt mỏi với việc phải kiểm tra giá cổ phiếu hàng ngày trên Yahoo Finance và sao chép dữ liệu vào Google Sheets? Hãy để n8n giúp các sếp tự động hóa quy trình này trong vài phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải kiểm tra giá cổ phiếu hàng ngày
- Dữ liệu chính xác: Lấy dữ liệu trực tiếp từ Yahoo Finance
- Dễ dàng theo dõi: Dữ liệu được lưu trữ trong Google Sheets
- Tự động hóa hoàn toàn: Không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets
- API key từ ScrapeGraphAI
- Tài khoản Yahoo Finance (nếu cần truy cập dữ liệu riêng tư)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/6726)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy workflow (ví dụ: hàng ngày lúc 9h sáng)
   - Có thể thay đổi thành bất kỳ trigger nào khác phù hợp

2. **Yahoo Finance Stock Scraper**:
   - Cấu hình credentials cho ScrapeGraphAI
   - Nhập URL của trang Yahoo Finance cần scrape (ví dụ: `https://finance.yahoo.com/quote/AAPL`)
   - Nhập instruction: "Extract stock price, change percentage, and volume from this page"

3. **Stock Data Formatter**:
   - Node này đã được cấu hình sẵn, không cần chỉnh sửa
   - Nó sẽ định dạng dữ liệu để phù hợp với Google Sheets

4. **Google Sheets Stock Logger**:
   - Cấu hình credentials cho Google Sheets
   - Chọn spreadsheet và worksheet đích
   - Đảm bảo operation được đặt là "Append" để thêm dữ liệu mới vào hàng cuối cùng

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra Google Sheets để đảm bảo dữ liệu được lưu trữ đúng cách
3. Bật Active workflow để chạy tự động theo lịch trình đã cấu hình

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo khi giá cổ phiếu vượt ngưỡng nhất định
- Kết hợp với Slack/Telegram để nhận thông báo tức thì
- Lưu trữ dữ liệu lịch sử trong nhiều tháng/năm
- Tự động tạo báo cáo định kỳ từ dữ liệu trong Google Sheets

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi giá cổ phiếu hàng ngày. Dữ liệu được lưu trữ trong Google Sheets giúp dễ dàng phân tích và tạo báo cáo. Hãy áp dụng ngay để tự động hóa quy trình theo dõi cổ phiếu của các sếp!