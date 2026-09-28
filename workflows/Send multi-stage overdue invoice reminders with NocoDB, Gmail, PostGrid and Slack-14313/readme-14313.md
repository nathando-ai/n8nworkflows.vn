---
title: "📄 Tự động hóa nhắc nhở hóa đơn quá hạn với NocoDB, Gmail, PostGrid và Slack"
description: "Hướng dẫn tự động hóa quy trình nhắc nhở hóa đơn quá hạn với n8n, tiết kiệm thời gian và tăng hiệu quả quản lý tài chính"
slug: "tu-dong-hoa-nhac-nho-hoa-don-qua-han"
tags: [n8n, automation, no-code, nocodb, postgrid, gmail, slack]
keywords: [n8n workflow, tự động hóa hóa đơn, nhắc nhở quá hạn, nocodb, postgrid, gmail, slack]
---

# 📄 Tự động hóa nhắc nhở hóa đơn quá hạn với NocoDB, Gmail, PostGrid và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý hóa đơn quá hạn thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động nhắc nhở hóa đơn sắp đến hạn và quá hạn qua email và thư truyền thống
- Tiết kiệm thời gian quản lý hóa đơn thủ công
- Theo dõi quá trình nhắc nhở qua Slack
- Tăng hiệu quả thu hồi nợ và giảm thiệt hại tài chính
- Hệ thống hóa dữ liệu hóa đơn và khách hàng trong NocoDB
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản NocoDB với API token
- Tài khoản Gmail với quyền truy cập OAuth2
- Tài khoản Slack với quyền gửi tin nhắn
- API key từ PostGrid
- Dữ liệu hóa đơn và thông tin khách hàng đã được nhập vào NocoDB
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14313](https://n8n.io/workflows/14313)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Config** node:
   - Cấu hình các khoảng thời gian gửi nhắc nhở khác nhau (nhắc nhở thông thường, cảnh báo, thông báo pháp lý)
   - Chọn phương thức gửi (email, thư, hoặc cả hai)

2. **NocoDB Config** node:
   - Cấu hình kết nối đến NocoDB của bạn
   - Đảm bảo bảng "Clients" và "Invoices" đã được tạo

3. **Your Company Details** node:
   - Nhập đầy đủ thông tin công ty (tên, địa chỉ, email, số điện thoại)
   - Thông tin này sẽ được sử dụng trong các mẫu email và thư

4. **Send Letter using PostGrid API** node:
   - Tạo credentials "Custom Auth" với cấu trúc:
     ```json
     {
       "headers": {
         "x-api-key": "<Your API Key>"
       }
     }
     ```

5. **Send an Email** node:
   - Cấu hình credentials Gmail OAuth2
   - Đảm bảo tài khoản Gmail có quyền gửi email

6. **Send a message** node:
   - Cấu hình credentials Slack OAuth2
   - Chọn kênh Slack để nhận thông báo

#### 3. Kích hoạt ⚡️
1. Kiểm tra dữ liệu mẫu bằng cách chạy từng node từ đầu đến cuối
2. Sau khi xác nhận hoạt động đúng, bật "Active" cho workflow
3. Đảm bảo workflow được chạy hàng ngày (được cấu hình trong node "Run daily")

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các hóa đơn đã xử lý vào bảng riêng trong NocoDB
- Kết hợp với Telegram để nhận thông báo thay thế cho Slack
- Tạo báo cáo hàng tuần về tình hình thu hồi nợ
- Tích hợp với hệ thống kế toán để tự động cập nhật trạng thái thanh toán
- Thêm chức năng gửi SMS nhắc nhở cho khách hàng quan trọng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình nhắc nhở hóa đơn, giảm thiểu công việc thủ công và tăng hiệu quả quản lý tài chính. Bằng cách kết hợp NocoDB, Gmail, PostGrid và Slack, hệ thống cung cấp giải pháp toàn diện cho việc theo dõi và thu hồi nợ một cách hiệu quả. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý hóa đơn của doanh nghiệp!