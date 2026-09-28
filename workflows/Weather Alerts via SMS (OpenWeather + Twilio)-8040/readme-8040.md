---
title: "🌦️ Tự động cảnh báo thời tiết qua SMS với n8n (OpenWeather + Twilio)"
description: "Hướng dẫn tự động hóa cảnh báo thời tiết qua SMS với n8n, kết hợp OpenWeather và Twilio. Nhận thông báo kịp thời về mưa, tuyết và nhiệt độ cực đoan."
slug: "tu-dong-canh-bao-thoi-tiet-qua-sms-voi-n8n"
tags: [n8n, automation, no-code, openweather, twilio]
keywords: [n8n workflow, tự động hóa thời tiết, cảnh báo thời tiết, openweather, twilio]
---

# 🌦️ Tự động cảnh báo thời tiết qua SMS với n8n (OpenWeather + Twilio)

[Các sếp] có bao giờ phải dậy sớm để xem thời tiết trước khi ra đường không? Hay phải liên tục kiểm tra ứng dụng thời tiết để biết có mưa không? Với workflow này, các sếp sẽ nhận được cảnh báo thời tiết kịp thời qua SMS, giúp tiết kiệm thời gian và tránh những bất ngờ không mong muốn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận cảnh báo thời tiết kịp thời qua SMS
- Tiết kiệm thời gian kiểm tra thời tiết hàng ngày
- Tránh những bất ngờ không mong muốn
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenWeather API (miễn phí)
- Tài khoản Twilio (bao gồm số điện thoại và credit)
- Số điện thoại nhận cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8040](https://n8n.io/workflows/8040)
2. Click vào nút "Import" để tải xuống file JSON
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Check Every 6 Hours" (cron)**
   - Đảm bảo node này đang hoạt động (Active)

2. **Node "Get Current Weather" (httpRequest)**
   - Cập nhật API key của OpenWeather
   - Thay đổi thành tọa độ hoặc tên thành phố của các sếp

3. **Node "Get Weather Forecast" (httpRequest)**
   - Cập nhật API key của OpenWeather
   - Thay đổi thành tọa độ hoặc tên thành phố của các sếp

4. **Node "Send Weather SMS" (twilio)**
   - Thêm credentials Twilio vào n8n
   - Cập nhật số điện thoại nhận cảnh báo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu nhận cảnh báo thời tiết

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack hoặc Telegram để nhận cảnh báo thời tiết
- Lưu log cảnh báo vào Google Sheets hoặc Notion
- Gửi báo cáo thời tiết định kỳ qua email

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận được cảnh báo thời tiết kịp thời qua SMS. Với việc tự động hóa cảnh báo thời tiết, các sếp có thể tập trung vào những việc quan trọng hơn. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!