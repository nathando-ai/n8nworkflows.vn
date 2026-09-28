---
title: "🚀 Tự động hóa dữ liệu từ Webflow sang Google Sheets + Thông báo WhatsApp"
description: "Hướng dẫn tự động lưu dữ liệu form Webflow vào Google Sheets và gửi thông báo qua WhatsApp ngay khi có lead mới"
slug: "tu-dong-hoa-du-lieu-webflow-sang-google-sheets-whatsapp"
tags: [n8n, automation, no-code, webflow, google-sheets, whatsapp]
keywords: [n8n workflow, tự động hóa, webflow, google sheets, whatsapp]
---

# 🚀 Tự động hóa dữ liệu từ Webflow sang Google Sheets + Thông báo WhatsApp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu dữ liệu form Webflow vào Google Sheets ngay khi có lead mới
- Gửi thông báo xác nhận qua email và WhatsApp tự động
- Xử lý hàng loạt lead một cách hiệu quả
- Tiết kiệm thời gian và công sức cho đội ngũ marketing
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Webflow với quyền truy cập API
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Tài khoản Rapiwa (dịch vụ gửi tin nhắn WhatsApp)
- Tài khoản Gmail để gửi email thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15349)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán JSON đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webflow Trigger**:
   - Cấu hình credentials cho Webflow
   - Chọn site và form cần theo dõi
   - Đảm bảo Webhook URL đã được cấu hình đúng trong Webflow

2. **Google Sheet**:
   - Cấu hình credentials cho Google Sheets
   - Chọn spreadsheet và worksheet đích
   - Đảm bảo có quyền chỉnh sửa trên sheet này

3. **Rapiwa (WhatsApp)**:
   - Cấu hình credentials cho Rapiwa
   - Điền số điện thoại WhatsApp cần gửi thông báo
   - Tùy chỉnh nội dung tin nhắn trong node "Rapiwa (Send WhatsApp Confirmation Message)"

4. **Gmail**:
   - Cấu hình credentials cho Gmail
   - Điền địa chỉ email nhận thông báo
   - Tùy chỉnh nội dung email trong node "Send a confirmation email message"

5. **Code Node**:
   - Kiểm tra và chỉnh sửa mã JavaScript trong node "Code (Clean response data)" nếu cần
   - Đảm bảo mã xử lý dữ liệu đầu vào phù hợp với cấu trúc dữ liệu của bạn

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kích hoạt workflow sau khi đã kiểm tra và xác nhận hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log hoạt động của workflow
- Kết hợp với các dịch vụ khác như Slack để nhận thông báo
- Tạo báo cáo tự động từ dữ liệu trong Google Sheets
- Thiết lập lịch gửi báo cáo định kỳ cho quản lý

### 📌 Kết luận
Workflow này giúp tự động hóa toàn bộ quá trình xử lý lead từ Webflow, từ lưu trữ dữ liệu đến thông báo. Với việc tích hợp Google Sheets và WhatsApp, các sếp có thể theo dõi và phản hồi khách hàng một cách nhanh chóng và hiệu quả. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!