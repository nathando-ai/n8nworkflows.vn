---
title: "🚀 Tự động hóa báo thức thông minh với Google Maps, Twilio SMS và iOS Shortcuts"
description: "Hướng dẫn tự động hóa báo thức thông minh dựa trên thời gian di chuyển thực tế từ Google Maps, gửi SMS qua Twilio và kích hoạt báo thức trên iPhone"
slug: "tu-dong-hoa-bao-thuc-thong-minh-google-maps-twilio-sms-ios-shortcuts"
tags: [n8n, automation, no-code, google-maps, twilio, ios-shortcuts]
keywords: [n8n workflow, tự động hóa báo thức, google maps traffic, twilio sms, ios shortcuts]
---

# 🚀 Tự động hóa báo thức thông minh với Google Maps, Twilio SMS và iOS Shortcuts

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi bị kẹt xe vào buổi sáng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần kiểm tra thời gian di chuyển mỗi sáng
- Chính xác: Dựa trên dữ liệu thời gian di chuyển thực tế từ Google Maps
- Cá nhân hóa: Thiết lập thời gian báo thức dựa trên lịch trình cá nhân
- Hoạt động liên tục: Tự động kiểm tra và gửi thông báo mỗi phút
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với Distance Matrix API đã kích hoạt
- Tài khoản Twilio với số điện thoại đã xác minh
- Google Sheets với bảng dữ liệu lịch trình (cấu trúc chi tiết bên dưới)
- iPhone (tùy chọn cho phần kích hoạt báo thức tự động)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13386](https://n8n.io/workflows/13386)
2. Click "Download" để tải file JSON workflow
3. Trong n8n Editor, click "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get date & status of alarm" và "Update alarm date & status"**:
   - Thiết lập Google Sheets OAuth2 credentials
   - Cấu hình Spreadsheet ID và Sheet Name chứa dữ liệu lịch trình
   - Đảm bảo bảng có cấu trúc: `Date` (YYYY-MM-DD) và `Status` (ini/end)

2. **Node "Get Latitude/Longitude of Origin Address" và "Get Latitude/Longitude of End Address"**:
   - Thiết lập Google Maps API key trong HTTP Request node
   - Cập nhật địa chỉ xuất phát và đích đến trong node "Define Origin and Destination addresses"

3. **Node "Send an SMS/MMS/WhatsApp message"**:
   - Thiết lập Twilio credentials
   - Cấu hình số điện thoại nhận thông báo (đã được xác minh trong Twilio)

4. **Node "Triggers at 7 AM till 8 AM every minute on weekdays"**:
   - Điều chỉnh thời gian kích hoạt phù hợp với lịch trình của các sếp

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để kiểm tra kết nối và cấu hình
2. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram: Thêm node gửi thông báo đến các kênh khác
2. Lưu log: Thêm node lưu lịch sử các lần gửi thông báo
3. Gửi báo cáo định kỳ: Thêm node gửi báo cáo tổng hợp hàng tuần
4. Kích hoạt báo thức nâng cao: Sử dụng iOS Shortcuts để kích hoạt cảnh báo hoặc chuyển sang chế độ Focus

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tránh bị kẹt xe vào buổi sáng bằng cách tự động hóa quá trình kiểm tra thời gian di chuyển và gửi thông báo báo thức thông minh. Hãy thử ngay và tận hưởng những buổi sáng hiệu quả hơn!