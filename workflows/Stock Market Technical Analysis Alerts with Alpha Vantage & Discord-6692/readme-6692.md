---
title: "📈 Tự động phân tích thị trường chứng khoán với Alpha Vantage & Discord - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động theo dõi tín hiệu Golden Cross và Death Cross cho cổ phiếu bằng n8n, tiết kiệm thời gian và tối ưu hóa chiến lược giao dịch"
slug: "tu-dong-phan-tich-thi-truong-chung-khoan-voi-alpha-vantage-discord"
tags: [n8n, automation, crypto trading, stock market, discord]
keywords: [n8n workflow, tự động hóa thị trường chứng khoán, phân tích kỹ thuật, Golden Cross, Death Cross]
---

# 📈 Tự động phân tích thị trường chứng khoán với Alpha Vantage & Discord - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư khi phải theo dõi thủ công các chỉ số kỹ thuật. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi 4 cổ phiếu hàng ngày (NVDA, JPM, PG, SPY)
- Nhận cảnh báo ngay lập tức khi có tín hiệu Golden Cross (📈) hoặc Death Cross (📉)
- Lưu trữ lịch sử giá đóng cửa để phân tích dài hạn
- Nhận thông báo trên Discord với định dạng dễ đọc
- Tiết kiệm thời gian lên tới 80% so với phương pháp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Alpha Vantage (API Key)
- Tài khoản Discord (Webhook URL)
- Cơ sở dữ liệu PostgreSQL (hoặc sử dụng dịch vụ như Supabase)
- Danh sách mã cổ phiếu cần theo dõi (mặc định: NVDA, JPM, PG, SPY)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6692](https://n8n.io/workflows/6692)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger - Daily Close**:
   - Thiết lập lịch chạy hàng ngày lúc 17:00 (UTC+7) để phân tích dữ liệu đóng cửa
   - Đảm bảo thời gian này phù hợp với thị trường chứng khoán của bạn

2. **Compute 60/120 SMAs**:
   - Node này tính toán các giá trị SMA 60 và 120 ngày
   - Không cần cấu hình thêm, chỉ cần đảm bảo dữ liệu đầu vào đúng

3. **Fetch Daily History**:
   - Cấu hình credentials cho Alpha Vantage
   - Đảm bảo API Key hợp lệ và có quyền truy cập vào dữ liệu lịch sử

4. **Insert rows in a table**:
   - Cấu hình kết nối PostgreSQL
   - Tạo bảng "stock_data" với các cột: ticker, date, close_price, sma_60, sma_120

5. **HTTP Request** (Discord Webhook):
   - Thay thế URL Webhook bằng URL của kênh Discord của bạn
   - Kiểm tra định dạng thông báo để đảm bảo hiển thị đúng trên Discord

6. **Set - Ticker List**:
   - Chỉnh sửa danh sách mã cổ phiếu theo nhu cầu của bạn
   - Mặc định: ["NVDA", "JPM", "PG", "SPY"]

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra logic
2. Kích hoạt workflow bằng cách nhấn "Activate"
3. Kiểm tra kênh Discord để xác nhận nhận được thông báo test

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm các mã cổ phiếu theo ngành hoặc theo danh mục đầu tư của bạn
2. Kết hợp với các chỉ số kỹ thuật khác như RSI, MACD để tăng độ chính xác
3. Thiết lập cảnh báo cho các mức giá cụ thể thay vì chỉ dựa trên SMA
4. Tích hợp với các dịch vụ khác như Telegram hoặc Slack để đa kênh thông báo

### 📌 Kết luận
Workflow này giúp các nhà đầu tư tiết kiệm thời gian quý giá trong việc theo dõi thị trường chứng khoán. Bằng cách tự động hóa phân tích kỹ thuật và thông báo, bạn có thể tập trung vào các quyết định đầu tư quan trọng hơn. Hãy thử ngay và nâng cấp chiến lược giao dịch của bạn!