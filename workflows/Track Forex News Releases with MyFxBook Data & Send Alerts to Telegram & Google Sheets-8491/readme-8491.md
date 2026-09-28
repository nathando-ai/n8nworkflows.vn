---
title: "🚀 Theo dõi tin tức Forex từ Forex Factory và gửi cảnh báo qua Telegram & Google Sheets"
description: "Tự động hóa việc theo dõi tin tức Forex từ Forex Factory, phân tích dữ liệu và gửi cảnh báo qua Telegram và Google Sheets để hỗ trợ giao dịch tiền tệ."
slug: "theo-doi-tin-tuc-forex-voi-myfxbook-va-gui-canh-bao-qua-telegram-va-google-sheets"
tags: [n8n, automation, no-code, forex, trading, crypto]
keywords: [n8n workflow, tự động hóa, forex trading, crypto, tiền tệ]
---

# 🚀 Theo dõi tin tức Forex từ Forex Factory và gửi cảnh báo qua Telegram & Google Sheets

[Các sếp giao dịch Forex và Crypto thường gặp khó khăn khi phải theo dõi thủ công tin tức từ Forex Factory, phân tích dữ liệu và gửi cảnh báo đến các nền tảng khác. Workflow này giúp tự động hóa toàn bộ quy trình này, tiết kiệm thời gian và giảm thiểu lỗi con người.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi có tin tức mới.
- **Cảnh báo tức thời**: Nhận thông báo qua Telegram ngay khi có tin tức quan trọng.
- **Dữ liệu chính xác**: Lấy dữ liệu từ Forex Factory và MyFxBook để phân tích.
- **Lưu trữ dữ liệu**: Ghi lại tất cả thông tin vào Google Sheets cho phân tích sau này.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar và Google Sheets.
- API key từ Airtop.
- Telegram Bot API token và Chat ID.
- Tài khoản MyFxBook.
- Kích hoạt Google Drive API trong Google Cloud Console.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8491](https://n8n.io/workflows/8491).
2. Nhấn nút **Download** để tải file JSON.
3. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Calendar Trigger**: Cấu hình tài khoản Google Calendar của bạn.
- **Airtop**: Nhập API key của bạn.
- **Telegram**: Cấu hình Bot API token và Chat ID.
- **Google Sheets**: Tạo một Google Sheets mới và nhập ID của nó vào các node `Input to Sheets` và `Input to Sheets2`.
- **MyFxBook**: Cấu hình tài khoản MyFxBook của bạn.

#### 3. Kích hoạt ⚡️
- **Test run**: Chạy workflow với dữ liệu mẫu để kiểm tra.
- **Bật Active workflow**: Sau khi kiểm tra, bật workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với MetaTrader 4**: Sử dụng thông báo Telegram để mở vị thế giao dịch.
- **Phân tích dữ liệu**: Sử dụng Google Sheets để phân tích dữ liệu lịch sử.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo qua email hoặc Telegram hàng ngày.
- **Kết hợp với Slack**: Thêm node Slack để nhận cảnh báo trên Slack.

### 📌 Kết luận
Workflow này giúp các sếp giao dịch Forex và Crypto tự động hóa việc theo dõi tin tức, phân tích dữ liệu và gửi cảnh báo. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian và giảm thiểu lỗi con người, từ đó tăng hiệu quả giao dịch.