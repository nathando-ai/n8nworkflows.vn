---
title: "🚀 Tự động gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero qua SMTP"
description: "Hướng dẫn tự động hóa gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero thông qua SMTP mà không cần lập trình"
slug: "tu-dong-gui-email-chao-mung-ca-nhan-hoa-tu-xero-qua-smtp"
tags: [n8n, automation, no-code, xero, email]
keywords: [n8n workflow, tự động hóa, xero, email cá nhân hóa, smtp]
---

# 🚀 Tự động gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero qua SMTP

[Các sếp đang làm thủ công việc gửi email chào mừng cho khách hàng mới từ Xero? Bạn đang mất thời gian quý giá để tạo và gửi từng email một? Hãy để workflow này giúp bạn tự động hóa quy trình này hoàn toàn mà không cần viết một dòng code nào!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc tạo và gửi email chào mừng
- Đảm bảo email được gửi đến đúng người nhận với nội dung cá nhân hóa
- Tự động hóa hoàn toàn quy trình mà không cần can thiệp thủ công
- Giữ được tính chuyên nghiệp và cá nhân hóa trong giao tiếp với khách hàng
- Hoạt động liên tục 24/7 mà không cần giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Xero với quyền truy cập API
- Thông tin SMTP để gửi email (server, port, username, password)
- Template email HTML sẵn sàng cho việc cá nhân hóa
- Kiến thức cơ bản về cách sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **New Contact in Xero (Webhook)**:
  - Cấu hình webhook để nhận thông báo khi có khách hàng mới trong Xero
  - Đảm bảo webhook được kích hoạt và có thể nhận dữ liệu từ Xero

- **Is it a NEW Contact? (If)**:
  - Cấu hình điều kiện để kiểm tra xem liên hệ mới có phải là khách hàng mới hay không
  - Có thể thêm các điều kiện bổ sung như kiểm tra trạng thái hoặc loại liên hệ

- **Fetch Full Contact Details from Xero (Xero)**:
  - Cấu hình kết nối Xero và chọn operation là "Get Contact"
  - Đảm bảo có quyền truy cập đầy đủ vào thông tin khách hàng trong Xero

- **Build Personalized HTML Email (Code)**:
  - Viết mã JavaScript để tạo nội dung email cá nhân hóa
  - Sử dụng các biến từ dữ liệu khách hàng để cá nhân hóa email
  - Đảm bảo mã được viết đúng cú pháp và không có lỗi

- **Send Personalized Welcome Email (Email Send)**:
  - Cấu hình thông tin SMTP để gửi email
  - Điền địa chỉ email người gửi và chủ đề email
  - Sử dụng output từ node "Build Personalized HTML Email" làm nội dung email

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các email đã gửi để theo dõi và kiểm tra lại sau này
- Kết hợp với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo khi có lỗi xảy ra
- Tạo nhiều template email khác nhau cho các loại khách hàng khác nhau
- Thêm chức năng theo dõi mở email và nhấp chuột để đánh giá hiệu quả của chiến dịch

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc gửi email chào mừng cho khách hàng mới từ Xero. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong kinh doanh. Hãy áp dụng ngay để nâng cao hiệu quả giao tiếp với khách hàng!