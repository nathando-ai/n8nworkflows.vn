---
title: "💳 Tự động theo dõi giao dịch thẻ tín dụng HDFC với Google Sheets & Telegram"
description: "Workflow n8n giúp tự động hóa việc theo dõi giao dịch thẻ tín dụng HDFC, lưu trữ dữ liệu vào Google Sheets và nhận thông báo Telegram tức thì."
slug: "tu-dong-theo-doi-giao-dich-the-tin-dung-hdfc-voi-google-sheets-va-telegram"
tags: [n8n, automation, no-code, finance, google-sheets]
keywords: [n8n workflow, tự động hóa tài chính, theo dõi giao dịch thẻ tín dụng, Google Sheets, Telegram]
---

# 💳 Tự động theo dõi giao dịch thẻ tín dụng HDFC với Google Sheets & Telegram

[Các sếp tài chính và quản lý ngân hàng đang gặp khó khăn khi phải theo dõi thủ công các giao dịch thẻ tín dụng HDFC. Việc này tốn thời gian, dễ bỏ sót và không thể tự động hóa. Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ nhận email giao dịch đến lưu trữ và thông báo tức thì.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng nghìn giao dịch mỗi ngày mà không cần can thiệp.
- **Chính xác 100%**: Dữ liệu được trích xuất và lưu trữ tự động từ email giao dịch.
- **Thông báo tức thì**: Nhận thông báo Telegram ngay khi có giao dịch mới.
- **Dễ quản lý**: Tất cả dữ liệu được lưu trữ trong Google Sheets với lịch sử đầy đủ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận email giao dịch thẻ tín dụng HDFC.
- Tài khoản Telegram và Bot Telegram để nhận thông báo.
- Google Sheets API đã được kích hoạt và credentials đã được thiết lập trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4128](https://n8n.io/workflows/4128).
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Gmail Trigger**: Cấu hình credentials Gmail OAuth2 và chọn hộp thư nhận email giao dịch.
- **Google Sheets**: Cấu hình credentials Google Sheets OAuth2 và chỉ định tên sheet và phạm vi dữ liệu.
- **Telegram**: Cấu hình credentials Telegram API và chỉ định chat ID để nhận thông báo.
- **Code Nodes**: Các node "Extract the required data from mail" và "map used articls ids" cần được kiểm tra và chỉnh sửa nếu cấu trúc email giao dịch thay đổi.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. Bật Active workflow để bắt đầu theo dõi giao dịch thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo cùng lúc với Telegram.
- **Lưu log giao dịch**: Thêm node Google Sheets để lưu trữ lịch sử giao dịch đầy đủ.
- **Báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp hàng tuần/tháng qua email.

### 📌 Kết luận
Workflow này giúp các sếp tài chính tự động hóa toàn bộ quy trình theo dõi giao dịch thẻ tín dụng HDFC, tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!