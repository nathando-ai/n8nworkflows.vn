---
title: "🚀 Theo dõi giá Crypto, danh sách mới & giao dịch với CoinGecko, Telegram & Google Sheets"
description: "Tự động hóa theo dõi giá Bitcoin, thông báo danh sách mới và ghi log giao dịch Binance - giải pháp toàn diện cho nhà đầu tư crypto"
slug: "theo-doi-gia-crypto-voi-coingecko-telegram-google-sheets"
tags: [n8n, automation, no-code, crypto, trading]
keywords: [n8n workflow, tự động hóa, theo dõi giá crypto, CoinGecko, Telegram, Google Sheets]
---

# 🚀 Theo dõi giá Crypto, danh sách mới & giao dịch với CoinGecko, Telegram & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư crypto khi phải theo dõi thủ công giá Bitcoin, danh sách mới và giao dịch Binance. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Theo dõi giá Bitcoin theo thời gian thực
- Nhận thông báo tức thời khi có danh sách mới
- Ghi log giao dịch Binance tự động
- Tiết kiệm thời gian và giảm lỗi thủ công
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và token bot
- Tài khoản Google và Google Sheets API credentials
- API Key từ CoinGecko
- API Key từ Binance (tùy chọn cho phần giao dịch)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6473](https://n8n.io/workflows/6473)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "1. Cron (Price Monitor Trigger)"**:
   - Thiết lập lịch chạy (ví dụ: mỗi 5 phút)
   - Đảm bảo thời gian UTC phù hợp với múi giờ của bạn

2. **Node "2. HTTP Request (Check BTC Price)"**:
   - Thêm API Key từ CoinGecko vào URL request
   - Ví dụ: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies=usd&x_cg_demo_api_key=YOUR_API_KEY`

3. **Node "3. If (Price > $50k)"**:
   - Điều chỉnh giá ngưỡng theo nhu cầu của bạn
   - Có thể thay đổi điều kiện so sánh (> < =)

4. **Node "4. Telegram (Send Alert)"**:
   - Thêm Telegram credentials
   - Cấu hình chat ID để nhận thông báo

5. **Node "1. RSS Feed (New Listing Trigger)"**:
   - Đảm bảo URL feed CoinGecko mới nhất
   - Có thể thay đổi thời gian kiểm tra (ví dụ: mỗi giờ)

6. **Node "2. Telegram (Listing Notif)"**:
   - Cấu hình tương tự như node gửi cảnh báo giá

7. **Node "1. Cron (Transaction Logger Trigger)"**:
   - Thiết lập lịch chạy phù hợp (ví dụ: mỗi 15 phút)

8. **Node "2. HTTP Request (Get Binance Trades)"**:
   - Thêm API Key từ Binance (nếu cần)
   - Cấu hình symbol và số lượng giao dịch cần lấy

9. **Node "3. Function (Format Data)"**:
   - Kiểm tra và điều chỉnh hàm JavaScript nếu cần
   - Đảm bảo định dạng dữ liệu đầu ra phù hợp với Google Sheets

10. **Node "4. Google Sheets (Log Transactions)"**:
    - Thêm Google Sheets credentials
    - Cấu hình Spreadsheet ID và tên sheet chính xác
    - Đảm bảo quyền truy cập đủ cho tài khoản n8n

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Telegram và Google Sheets
3. Sau khi xác nhận hoạt động đúng, nhấn "Activate" để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email để nhận báo cáo hàng ngày
- Kết hợp với các chỉ số kỹ thuật để tạo tín hiệu giao dịch
- Tạo bản sao lưu tự động cho Google Sheets
- Thêm cảnh báo khi giá xuống dưới mức hỗ trợ
- Kết nối với các sàn giao dịch khác như Kraken hoặc Huobi

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi thị trường crypto, giúp các nhà đầu tư tiết kiệm thời gian và giảm thiểu lỗi thủ công. Với cấu hình đơn giản và khả năng tùy chỉnh cao, nó phù hợp cho cả nhà đầu tư cá nhân và tổ chức quản lý quỹ. Hãy thử ngay và nâng cấp chiến lược giao dịch của bạn với tự động hóa!