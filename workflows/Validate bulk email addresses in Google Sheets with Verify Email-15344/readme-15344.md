---
title: "📧 [Tự động hóa] Kiểm tra hàng loạt địa chỉ email trong Google Sheets với Verify Email"
description: "Hướng dẫn tự động hóa kiểm tra hàng loạt địa chỉ email trong Google Sheets bằng n8n và Verify Email API. Tiết kiệm thời gian và đảm bảo chất lượng dữ liệu email."
slug: "tu-dong-hoa-kiem-tra-email-google-sheets"
tags: [n8n, automation, no-code, email-validation, google-sheets]
keywords: [n8n workflow, tự động hóa email, kiểm tra email, google sheets, verify email]
---

# 📧 [Tự động hóa] Kiểm tra hàng loạt địa chỉ email trong Google Sheets với Verify Email

[Các sếp đang gặp khó khăn khi phải kiểm tra thủ công hàng loạt địa chỉ email trong Google Sheets. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này trong vòng vài phút, đảm bảo chất lượng dữ liệu email và tiết kiệm thời gian quý giá.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình kiểm tra hàng loạt địa chỉ email trong Google Sheets.
- **Đảm bảo chất lượng dữ liệu**: Lọc ra các địa chỉ email hợp lệ và không hợp lệ.
- **Tích hợp dễ dàng**: Kết nối với các công cụ khác như Slack, HubSpot, Airtable.
- **Hoạt động liên tục**: Chạy tự động theo lịch trình hoặc kích hoạt thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ [Verify Email](https://verify-email.app).
- Google Sheets API credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/15344`.
4. Nhấn "Import" để tải workflow vào n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Every Monday at 8am"**: Cấu hình thời gian chạy tự động hàng tuần.
- **Node "Read Emails from Sheets"**: Cấu hình Google Sheets API credentials và chỉ định Sheet ID, tên sheet, và phạm vi dữ liệu.
- **Node "Parse Email Data for Batches"**: Kiểm tra và chỉnh sửa mã JavaScript nếu cần xử lý dữ liệu theo định dạng khác.
- **Node "Process in Batches of 10"**: Điều chỉnh kích thước batch nếu cần.
- **Node "Post Email Batch to Verify API"**: Cấu hình HTTP Bearer Auth và HTTP Header Auth với API Key từ Verify Email.
- **Node "Parse Verification Results"**: Kiểm tra và chỉnh sửa mã JavaScript để xử lý kết quả trả về từ API.
- **Node "Update Results in Sheets"**: Cấu hình Google Sheets API credentials và chỉ định Sheet ID, tên sheet, và phạm vi dữ liệu để cập nhật kết quả.
- **Node "Webhook Trigger"**: Cấu hình URL webhook nếu cần kích hoạt workflow từ bên ngoài.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Node" để kiểm tra từng node.
2. Kiểm tra kết quả và đảm bảo dữ liệu được xử lý đúng.
3. Bật chế độ "Active" cho workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo khi workflow hoàn thành.
- **Lưu log**: Thêm node để lưu log các địa chỉ email đã kiểm tra.
- **Gửi báo cáo định kỳ**: Tạo báo cáo tổng hợp các địa chỉ email hợp lệ và không hợp lệ.
- **Kiểm tra định kỳ**: Cấu hình workflow để chạy định kỳ để kiểm tra danh sách email mới.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình kiểm tra hàng loạt địa chỉ email trong Google Sheets một cách hiệu quả. Với các bước cấu hình đơn giản và linh hoạt, các sếp có thể dễ dàng tích hợp và chạy workflow này trong môi trường sản xuất. Hãy áp dụng ngay để tiết kiệm thời gian và đảm bảo chất lượng dữ liệu email!