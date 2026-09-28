---
title: "🚀 Tự động đồng bộ danh bạ CRM với Rapidmail và Slack - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh bạ từ CentralStationCRM sang Rapidmail với xác nhận qua Slack, tiết kiệm thời gian và tối ưu quy trình làm việc"
slug: "tu-dong-dong-bo-danh-ba-crm-voi-rapidmail-slack"
tags: [n8n, automation, no-code, crm, email-marketing]
keywords: [n8n workflow, tự động hóa, crm, email marketing, rapidmail]
---

# 🚀 Tự động đồng bộ danh bạ CRM với Rapidmail và Slack - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý danh bạ thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ danh bạ mới từ CentralStationCRM hàng ngày
- Xác nhận qua Slack trước khi thêm người dùng vào danh sách email
- Tiết kiệm thời gian quản lý danh bạ thủ công
- Đảm bảo dữ liệu đồng bộ chính xác và liên tục
- Tối ưu quy trình marketing email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản CentralStationCRM với quyền truy cập API
- Tài khoản Slack với quyền gửi tin nhắn
- Tài khoản Rapidmail với quyền truy cập API
- API Key từ CentralStationCRM
- Thông tin xác thực cho Rapidmail (username và password)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản của bạn
2. Nhấn vào "Workflows" trong menu bên trái
3. Nhấn vào nút "+" để tạo workflow mới
4. Chọn "Import from URL" và nhập link: [https://n8n.io/workflows/6125](https://n8n.io/workflows/6125)
5. Hoặc copy nội dung JSON từ file workflow và paste vào editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Workflow triggers daily at 5PM** (scheduleTrigger):
   - Chỉnh sửa thời gian chạy workflow theo nhu cầu (mặc định 17:00 hàng ngày)
   - Thay đổi "Trigger Interval" và "Days between Triggers" nếu cần

2. **Get new people per day from CentralStationCRM** (httpRequest):
   - Tạo credentials mới với loại "HTTP Header Auth"
   - Đặt tên credentials là "X-apikey"
   - Nhập API Key từ CentralStationCRM vào trường "Value"
   - Chọn credentials này trong node

3. **ask in Slack: add "Newsletter" tag?** (slack):
   - Tạo credentials mới với loại "Slack OAuth2 API"
   - Nhập tên người dùng Slack (bắt đầu bằng @)
   - Tùy chỉnh nội dung tin nhắn nếu cần (đảm bảo không thay đổi JSON code)

4. **give person a "Newsletter" tag** (httpRequest):
   - Sử dụng cùng credentials "X-apikey" như node trước đó

5. **Write person to Rapidmail list** (httpRequest):
   - Tạo credentials mới với loại "HTTP Basic Auth"
   - Nhập username và password từ Rapidmail
   - Thay thế "ENTER-RAPIDMAIL-LIST-ID" trong JSON code bằng ID danh sách Rapidmail thực tế

#### 3. Kích hoạt ⚡️
- Nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu
- Kiểm tra kết quả trên Slack và Rapidmail
- Bật workflow bằng cách chuyển công tắc sang "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi workflow hoàn thành
- Tạo báo cáo hàng tuần về số lượng người dùng mới được thêm
- Kết hợp với workflow khác để tự động gửi email chào mừng
- Thiết lập cảnh báo khi có lỗi xảy ra trong quá trình chạy
- Tùy chỉnh nội dung tin nhắn Slack để phù hợp với quy trình làm việc của bạn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý danh bạ và đồng bộ dữ liệu với hệ thống email marketing. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và tối ưu hóa hiệu quả marketing. Hãy thử áp dụng ngay để trải nghiệm lợi ích của tự động hóa!