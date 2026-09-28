---
title: "📈 Theo dõi giá dầu thô WTI từ Oilprice.com và gửi cảnh báo Telegram"
description: "Workflow n8n tự động hóa theo dõi giá dầu thô WTI từ trang Oilprice.com và gửi cảnh báo Telegram ngay khi giá thay đổi đáng kể. Giúp nhà đầu tư và quản lý hàng hóa theo dõi thị trường dầu thô một cách hiệu quả."
slug: "theo-doi-gia-dau-tho-wti-tu-oilprice-com-va-gui-canh-bao-telegram"
tags: [n8n, automation, no-code, dầu thô, giao dịch tiền tệ]
keywords: [n8n workflow, tự động hóa, theo dõi giá dầu thô, cảnh báo Telegram, WTI]
---

# 📈 Theo dõi giá dầu thô WTI từ Oilprice.com và gửi cảnh báo Telegram

[Các sếp đang làm việc trong lĩnh vực giao dịch tiền tệ, quản lý hàng hóa hay đầu tư dầu thô chắc hẳn đã gặp khó khăn khi phải theo dõi giá dầu thô WTI hàng ngày từ nhiều nguồn khác nhau. Việc thủ công này tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa quy trình theo dõi giá dầu thô WTI từ trang Oilprice.com và gửi cảnh báo Telegram ngay khi giá thay đổi đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi giá dầu thô WTI hàng ngày.
- Chính xác: Dữ liệu được lấy từ nguồn uy tín như Oilprice.com.
- Cá nhân hóa: Nhận cảnh báo Telegram ngay khi giá thay đổi đáng kể.
- Hoạt động liên tục: Workflow chạy tự động theo lịch trình đã đặt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram đã được tạo.
- API key của Telegram.
- Trang web Oilprice.com để lấy dữ liệu giá dầu thô WTI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [n8n.io/workflows/15947](https://n8n.io/workflows/15947).
2. Nhấp vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import from File" và chọn file JSON đã tải về.

Hoặc, các sếp có thể copy/paste JSON của workflow vào n8n Editor bằng cách:

1. Truy cập vào trang [n8n.io/workflows/15947](https://n8n.io/workflows/15947).
2. Nhấp vào nút "Copy JSON" để sao chép JSON của workflow.
3. Trong n8n Editor, nhấp vào nút "Import from Clipboard" và dán JSON đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "When Market Hour Starts"**: Cấu hình lịch trình để workflow chạy tự động vào giờ thị trường mở cửa.
- **Node "Fetch WTI Crude Prices"**: Đảm bảo URL để lấy dữ liệu giá dầu thô WTI từ trang Oilprice.com là chính xác.
- **Node "Extract WTI Futures Data"**: Kiểm tra và chỉnh sửa mã JavaScript để xử lý dữ liệu theo nhu cầu của các sếp.
- **Node "Send Telegram Alert"**: Cấu hình credentials của Telegram để gửi cảnh báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu theo dõi giá dầu thô WTI và gửi cảnh báo Telegram.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tùy chỉnh mã JavaScript trong node "Extract WTI Futures Data" để phân tích dữ liệu theo cách khác nhau.
- Kết hợp với các công cụ khác như Slack để nhận cảnh báo.
- Lưu log dữ liệu để theo dõi lịch sử giá dầu thô WTI.
- Gửi báo cáo định kỳ về giá dầu thô WTI qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi giá dầu thô WTI từ trang Oilprice.com và gửi cảnh báo Telegram ngay khi giá thay đổi đáng kể. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian và theo dõi thị trường dầu thô một cách hiệu quả hơn. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của các sếp!