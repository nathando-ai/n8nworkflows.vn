---
title: "🎟️ Tự động hóa Phân phối & Kiểm tra Mã QR Coupon cho Lead Generation với SuiteCRM"
description: "Hướng dẫn tự động hóa phân phối mã QR coupon duy nhất và kiểm tra tính hợp lệ cho hệ thống lead generation bằng n8n và SuiteCRM"
slug: "tu-dong-hoa-phan-phoi-kiem-tra-ma-qr-coupon-voi-suitercrm"
tags: [n8n, automation, no-code, SuiteCRM, lead generation]
keywords: [n8n workflow, tự động hóa, SuiteCRM, lead generation, mã QR coupon]
---

# 🎟️ Tự động hóa Phân phối & Kiểm tra Mã QR Coupon cho Lead Generation với SuiteCRM

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý thủ công các mã coupon và kiểm tra tính hợp lệ. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân phối mã QR coupon duy nhất cho mỗi lead mới
- Kiểm tra tính hợp lệ của mã coupon khi quét QR
- Tiết kiệm thời gian quản lý thủ công
- Giảm thiểu rủi ro trùng lặp coupon
- Tích hợp liền mạch với SuiteCRM để quản lý lead
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets (để lưu trữ danh sách coupon và lead)
- Tài khoản SuiteCRM (để quản lý thông tin lead)
- Thông tin SMTP (để gửi email thông báo)
- API credentials cho Google Sheets và SuiteCRM
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2899](https://n8n.io/workflows/2899)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đặt path tùy chỉnh cho webhook (ví dụ: `/coupon-webhook`)
   - Lưu ý: Path mặc định là `bb832325-8c58-4717-b866-41f8a9714cf2`

2. **Node Token SuiteCRM**:
   - Cập nhật các thông tin sau:
     - `SUITECRMURL`: URL của SuiteCRM instance
     - `CLIENTSECRET`: Client secret của SuiteCRM
     - `CLIENTID`: Client ID của SuiteCRM

3. **Node Duplicate Lead?**:
   - Cấu hình Google Sheets credentials
   - Đặt tên sheet chứa danh sách lead (mặc định: `Lead`)

4. **Node Get Coupon**:
   - Cấu hình Google Sheets credentials
   - Đặt tên sheet chứa danh sách coupon (mặc định: `Coupon`)

5. **Node Send Email**:
   - Cấu hình SMTP credentials
   - Cập nhật địa chỉ email gửi và nhận

6. **Node Get QR**:
   - Cập nhật URL để tạo mã QR (nếu cần)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu thông qua webhook
2. Kiểm tra các node quan trọng:
   - Kiểm tra tính hợp lệ của coupon
   - Kiểm tra trùng lặp lead
   - Kiểm tra quá trình gửi email
3. Bật Active workflow sau khi kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để thông báo khi có lead mới
2. Thêm bước xác thực hai yếu tố cho quá trình kiểm tra coupon
3. Tích hợp với hệ thống CRM khác để đồng bộ dữ liệu
4. Thêm báo cáo định kỳ về số lượng coupon đã sử dụng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc quản lý coupon và lead generation. Bằng cách tự động hóa toàn bộ quy trình, các sếp có thể tiết kiệm thời gian, giảm thiểu lỗi và nâng cao trải nghiệm khách hàng. Hãy thử ngay và tối ưu hóa theo nhu cầu cụ thể của doanh nghiệp!