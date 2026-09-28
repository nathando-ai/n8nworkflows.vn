---
title: "🚀 Theo dõi sự thay đổi danh mục đầu tư hàng hóa với Google Sheets, Gemini AI và cảnh báo qua Gmail"
description: "Tự động theo dõi danh mục đầu tư hàng hóa của bạn, phát hiện sự thay đổi so với mục tiêu và nhận cảnh báo qua email với thông báo AI thông minh"
slug: "theo-doi-danh-muc-dau-tu-hang-hoa-voi-google-sheets-gemini-ai-va-gmail"
tags: [n8n, automation, no-code, crypto, trading, ai]
keywords: [n8n workflow, tự động hóa, theo dõi đầu tư, cảnh báo đầu tư, Gemini AI]
---

# 🚀 Theo dõi sự thay đổi danh mục đầu tư hàng hóa với Google Sheets, Gemini AI và cảnh báo qua Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư khi phải theo dõi thủ công danh mục đầu tư hàng hóa và phát hiện sự thay đổi. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động theo dõi danh mục đầu tư hàng hóa hàng ngày
- Phát hiện sự thay đổi so với mục tiêu đầu tư
- Nhận cảnh báo thông minh qua email với thông báo AI
- Ghi lại lịch sử các lần kiểm tra và cảnh báo
- Tiết kiệm thời gian và giảm thiểu lỗi thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets và Gmail đã kích hoạt
- API Key cho Google Gemini
- Google Sheet chứa danh mục đầu tư của bạn
- Email nhận cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15333](https://n8n.io/workflows/15333)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Read Holdings"**: Cấu hình Google Sheets OAuth2 API và chỉ định đúng Spreadsheet ID và Sheet Name chứa danh mục đầu tư của bạn
- **Node "Workflow Settings"**: Cập nhật các thông số quan trọng:
  - `targetAllocation`: Mục tiêu phân bổ đầu tư cho từng loại hàng hóa
  - `allowedRange`: Phạm vi cho phép thay đổi so với mục tiêu
  - `alertEmail`: Địa chỉ email nhận cảnh báo
  - `currency`: Đơn vị tiền tệ sử dụng
  - `severityRules`: Quy tắc phân loại mức độ cảnh báo
- **Node "Generate Alert Message"**: Cấu hình Google Palm API với API Key hợp lệ
- **Node "Send Rebalance Email"**: Cấu hình Gmail OAuth2 và xác nhận địa chỉ email nhận cảnh báo
- **Node "Log Sent Alert"**: Cập nhật Spreadsheet ID và Sheet Name cho bảng ghi log cảnh báo
- **Node "Daily Portfolio Rebalance Check"**: Cấu hình lịch chạy hàng ngày (ví dụ: 9:00 AM mỗi ngày)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả và đảm bảo không có lỗi
3. Click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận cảnh báo cùng lúc với email
- Tích hợp với các dịch vụ khác như Telegram hoặc Discord
- Thiết lập cảnh báo định kỳ hàng tuần/tháng
- Tạo báo cáo tổng hợp từ dữ liệu log
- Kết nối với các sàn giao dịch để thực hiện tự động rebalance

### 📌 Kết luận
Workflow này giúp các nhà đầu tư hàng hóa tự động theo dõi danh mục đầu tư hàng ngày, phát hiện sự thay đổi so với mục tiêu và nhận cảnh báo thông minh qua email. Với việc tự động hóa quy trình này, bạn có thể tiết kiệm thời gian và giảm thiểu lỗi thủ công, đồng thời duy trì danh mục đầu tư của mình luôn trong phạm vi mục tiêu. Hãy thử ngay và nâng cao hiệu quả đầu tư của bạn!