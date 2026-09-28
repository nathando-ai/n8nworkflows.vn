---
title: "📅 Tự động hóa lịch hẹn Calendly với Google Sheets & Thông báo Slack"
description: "Hướng dẫn chi tiết cách tự động theo dõi và ghi lại lịch hẹn Calendly vào Google Sheets cùng thông báo Slack tức thì khi có thay đổi"
slug: "tu-dong-hoa-lich-hen-calendly-voi-google-sheets-slack"
tags: [n8n, automation, no-code, calendly, google-sheets, slack]
keywords: [n8n workflow, tự động hóa lịch hẹn, Calendly, Google Sheets, Slack]
---

# 📅 Tự động hóa lịch hẹn Calendly với Google Sheets & Thông báo Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động ghi lại tất cả lịch hẹn mới vào Google Sheets ngay khi được đặt
- Nhận thông báo Slack tức thì khi có thay đổi lịch hẹn
- Phân loại và xử lý các loại sự kiện khác nhau (đặt lịch, hủy lịch, thay đổi)
- Tiết kiệm thời gian quản lý lịch hẹn thủ công
- Giảm thiểu lỗi do quên ghi chép
- Theo dõi hiệu suất lịch hẹn một cách chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Calendly với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền tạo ứng dụng
- Biết cách tạo và cấu hình webhook trong Calendly
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [https://n8n.io/workflows/11247](https://n8n.io/workflows/11247)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node Calendly Webhook Trigger1:**
- Cần cấu hình credentials Calendly OAuth2
- Đảm bảo webhook được kích hoạt trong tài khoản Calendly của bạn
- Chọn các loại sự kiện cần theo dõi: invitee.created và invitee.canceled

**Node Log to Bookings Sheet1 và Log to Cancellations Sheet:**
- Cần cấu hình credentials Google Sheets OAuth2
- Tạo Google Sheet với 2 tab: "Bookings" và "Cancellations"
- Đảm bảo tài khoản n8n có quyền ghi vào Google Sheet này
- Cấu hình các cột dữ liệu cần ghi (email, tên, thời gian, liên kết...)

**Node Slack Booking Notification và Slack Cancellation Alert:**
- Cần cấu hình credentials Slack API
- Tạo kênh Slack để nhận thông báo
- Cấu hình thông điệp Slack với các biến động như tên, email, thời gian...

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test với một lịch hẹn mới hoặc hủy lịch để kiểm tra hoạt động
3. Kiểm tra Google Sheets và kênh Slack để xác nhận dữ liệu được ghi và thông báo được gửi

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi email thông báo khi có thay đổi lịch hẹn
- Tạo báo cáo hàng tuần tự động từ dữ liệu trong Google Sheets
- Thêm chức năng nhắc nhở trước khi cuộc hẹn diễn ra
- Kết nối với các hệ thống CRM khác để cập nhật thông tin khách hàng
- Thêm chức năng phân loại ưu tiên cho các lịch hẹn quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình quản lý lịch hẹn Calendly, từ ghi nhận đến thông báo, giúp tiết kiệm thời gian và giảm thiểu lỗi. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!