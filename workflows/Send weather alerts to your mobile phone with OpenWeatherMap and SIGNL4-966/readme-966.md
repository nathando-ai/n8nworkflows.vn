---
title: "🌦️ Tự động cảnh báo thời tiết qua điện thoại với OpenWeatherMap và SIGNL4"
description: "Hướng dẫn tự động hóa cảnh báo thời tiết theo thời gian thực đến điện thoại của bạn bằng n8n, OpenWeatherMap và SIGNL4 - giải pháp không cần code cho doanh nghiệp"
slug: "tu-dong-cao-bao-thoi-tiet-dien-thoai-openweathermap-signl4"
tags: [n8n, automation, no-code, weather, alerting]
keywords: [n8n workflow, tự động hóa thời tiết, cảnh báo thời tiết, OpenWeatherMap, SIGNL4]
---

# 🌦️ Tự động cảnh báo thời tiết đến điện thoại của bạn với OpenWeatherMap và SIGNL4

[Các sếp đang làm việc từ xa hay quản lý đội ngũ di động thường gặp khó khăn khi phải theo dõi thời tiết hàng ngày. Với workflow này, các sếp có thể tự động nhận cảnh báo thời tiết theo thời gian thực ngay trên điện thoại thông minh, giúp đảm bảo an toàn và hiệu quả công việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận cảnh báo thời tiết theo thời gian thực ngay trên điện thoại
- Tiết kiệm thời gian theo dõi thời tiết thủ công
- Đảm bảo an toàn cho đội ngũ làm việc ngoài trời
- Nhận thông báo khi có điều kiện thời tiết nguy hiểm
- Tích hợp dễ dàng với hệ thống cảnh báo hiện có
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenWeatherMap API (để lấy dữ liệu thời tiết)
- Tài khoản SIGNL4 (để gửi cảnh báo đến điện thoại)
- Địa chỉ email hoặc số điện thoại đã đăng ký với SIGNL4
- Thiết bị di động đã cài đặt ứng dụng SIGNL4
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/966)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Schedule Trigger**:
   - Thiết lập lịch chạy workflow (ví dụ: mỗi ngày lúc 7:00 AM)
   - Chọn múi giờ phù hợp với khu vực của bạn

2. **Node OpenWeatherMap**:
   - Thêm credentials OpenWeatherMap API
   - Nhập tên thành phố hoặc tọa độ GPS để lấy dữ liệu thời tiết
   - Chọn đơn vị đo lường (Celsius/Fahrenheit)

3. **Node If**:
   - Thiết lập điều kiện cảnh báo (ví dụ: nhiệt độ dưới 0°C hoặc trên 35°C)
   - Cấu hình thông báo phù hợp với từng điều kiện thời tiết

4. **Node SIGNL4**:
   - Thêm credentials SIGNL4 API
   - Nhập địa chỉ email hoặc số điện thoại đã đăng ký với SIGNL4
   - Tùy chỉnh nội dung cảnh báo (có thể bao gồm thông tin thời tiết chi tiết)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi cảnh báo đến Slack hoặc Teams cùng lúc
- Tích hợp với hệ thống quản lý nhân sự để gửi cảnh báo đến các nhân viên cụ thể
- Thiết lập cảnh báo đa cấp (ví dụ: cảnh báo cấp 1 cho nhiệt độ cực đoan, cấp 2 cho mưa lớn)
- Lưu lịch sử cảnh báo vào Google Sheets hoặc cơ sở dữ liệu để phân tích
- Tự động gửi báo cáo thời tiết hàng tuần đến email của các sếp

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn chỉnh cho việc theo dõi thời tiết và cảnh báo đến điện thoại thông minh. Với việc tích hợp OpenWeatherMap và SIGNL4, các sếp có thể dễ dàng triển khai hệ thống cảnh báo thời tiết theo thời gian thực mà không cần viết code. Hãy thử ngay để nâng cao hiệu suất làm việc và đảm bảo an toàn cho đội ngũ của bạn!