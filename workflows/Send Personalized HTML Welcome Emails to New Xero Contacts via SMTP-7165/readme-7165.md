```yaml
---
title: "🚀 Tự động gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero qua SMTP"
description: "Hướng dẫn tự động hóa gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero thông qua SMTP trong n8n. Tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-gui-email-chao-mung-ca-nhan-hoa-tu-xero-qua-smtp"
tags: [n8n, automation, no-code, xero, email]
keywords: [n8n workflow, tự động hóa email, xero integration, email cá nhân hóa]
---
```

# 🚀 Tự động gửi email chào mừng cá nhân hóa cho khách hàng mới từ Xero qua SMTP

[Các sếp đang làm thủ công việc gửi email chào mừng cho khách hàng mới? Hãy dừng lại và tự động hóa ngay với workflow này! Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể và nâng cao trải nghiệm khách hàng bằng cách gửi email chào mừng cá nhân hóa ngay khi có khách hàng mới được thêm vào Xero.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc gửi email chào mừng thủ công.
- Nâng cao trải nghiệm khách hàng với nội dung email cá nhân hóa.
- Tự động hóa toàn bộ quy trình từ khi có khách hàng mới đến khi gửi email.
- Giảm thiểu lỗi do thủ công và đảm bảo tính nhất quán trong nội dung email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Xero với quyền truy cập API.
- Thông tin SMTP để gửi email (SMTP server, port, username, password).
- Biết cách tạo và cấu hình webhook trong Xero.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và nhập URL sau: [https://n8n.io/workflows/7165](https://n8n.io/workflows/7165)
3. Hoặc các sếp có thể tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "New Contact in Xero" (Webhook)**:
   - Cấu hình webhook trong Xero để kích hoạt workflow khi có khách hàng mới.
   - Đảm bảo webhook được kích hoạt và các sếp có quyền truy cập vào Xero API.

2. **Node "Is it a NEW Contact?" (If)**:
   - Cấu hình điều kiện để kiểm tra xem khách hàng mới có phải là khách hàng mới thực sự hay không.
   - Có thể thêm các điều kiện bổ sung như kiểm tra trạng thái khách hàng, loại khách hàng, v.v.

3. **Node "Fetch Full Contact Details from Xero" (Xero)**:
   - Cấu hình credentials cho Xero để truy cập API.
   - Chọn các trường thông tin cần lấy từ Xero (ví dụ: tên, email, địa chỉ, v.v.).

4. **Node "Build Personalized HTML Email" (Code)**:
   - Viết mã JavaScript để tạo nội dung email cá nhân hóa.
   - Sử dụng các biến từ dữ liệu khách hàng để cá nhân hóa email (ví dụ: tên khách hàng, sản phẩm quan tâm, v.v.).

5. **Node "Send Personalized Welcome Email" (Email Send)**:
   - Cấu hình credentials cho SMTP để gửi email.
   - Điền các thông tin cần thiết như chủ đề email, nội dung email, v.v.

#### 3. Kích hoạt ⚡️
1. Các sếp nên test workflow với dữ liệu mẫu trước khi kích hoạt.
2. Sau khi test thành công, các sếp có thể kích hoạt workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm node để lưu log gửi email để theo dõi hiệu suất và phân tích dữ liệu.
- Kết hợp với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo khi có lỗi xảy ra.
- Tự động hóa thêm các quy trình khác như gửi email nhắc nhở, cập nhật thông tin khách hàng, v.v.

### 📌 Kết luận
[Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể và nâng cao trải nghiệm khách hàng bằng cách tự động gửi email chào mừng cá nhân hóa ngay khi có khách hàng mới được thêm vào Xero. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp!]