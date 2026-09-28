---
title: "🚀 Tự động theo dõi lịch hẹn demo với Google Calendar và Meta Conversion API"
description: "Hướng dẫn tự động hóa theo dõi lịch hẹn demo từ Google Calendar và gửi dữ liệu đến Meta Conversion API để tối ưu hóa quảng cáo và phân tích hiệu quả"
slug: "tu-dong-theo-doi-lich-hen-demo-google-calendar-meta-conversion-api"
tags: [n8n, automation, no-code, google-calendar, meta-ads]
keywords: [n8n workflow, tự động hóa, google calendar, meta conversion api, quảng cáo facebook]
---

# 🚀 Tự động theo dõi lịch hẹn demo với Google Calendar và Meta Conversion API

[Các sếp] có biết không? Khi các bạn phải theo dõi thủ công từng lịch hẹn demo từ Google Calendar và gửi dữ liệu đến Meta Conversion API để tối ưu hóa chiến dịch quảng cáo, thì không chỉ tốn thời gian mà còn dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình theo dõi lịch hẹn demo từ Google Calendar
- Tự động gửi dữ liệu đến Meta Conversion API để tối ưu hóa chiến dịch quảng cáo
- Giảm thiểu lỗi và tăng độ chính xác trong việc theo dõi và báo cáo dữ liệu
- Tiết kiệm thời gian cho các công việc thủ công
- Tăng cường khả năng phân tích hiệu quả của chiến dịch quảng cáo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar với quyền truy cập đầy đủ
- Tài khoản Meta Ads Manager với quyền truy cập API
- Facebook Pixel ID
- Facebook Access Token
- URL trang đích (landing page URL)
- Tên sự kiện demo để lọc (Event Name Filter)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6331](https://n8n.io/workflows/6331)
2. Nhấn nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Calendar Trigger**:
   - Chọn credentials "googleCalendarOAuth2Api"
   - Cấu hình các tham số cần thiết như Calendar ID, Event Name Filter

2. **HTTP Request - Meta Conversion API**:
   - Điền Facebook Pixel ID
   - Điền Facebook Access Token
   - Cấu hình Facebook API Version (mặc định: v22.0)
   - Điền Source URL (URL trang đích)

3. **Params**:
   - Cấu hình các tham số bổ sung nếu cần gửi thêm dữ liệu đến Meta Conversion API

4. **Config**:
   - Cấu hình các tham số chung cho workflow

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn nút "Test Workflow" để kiểm tra dữ liệu mẫu
2. Nếu kết quả đúng, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Để gửi thêm thuộc tính (properties) đến Meta Conversion API, các sếp có thể tham khảo [Meta Payload Helper](https://developers.facebook.com/docs/marketing-api/conversions-api/payload-helper/)
- Kết hợp với Slack/Telegram để nhận thông báo khi có lịch hẹn mới
- Lưu log dữ liệu để phân tích hiệu quả chiến dịch quảng cáo
- Gửi báo cáo định kỳ về hiệu quả của chiến dịch quảng cáo

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi lịch hẹn demo từ Google Calendar và gửi dữ liệu đến Meta Conversion API. Với việc tự động hóa, các sếp có thể tiết kiệm thời gian, giảm thiểu lỗi và tối ưu hóa hiệu quả chiến dịch quảng cáo một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của các sếp!