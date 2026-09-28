---
title: "🚨 Tự động cảnh báo lỗi theo mức độ nghiêm trọng qua Telegram, Email và Google Sheets"
description: "Hướng dẫn tự động hóa cảnh báo lỗi theo mức độ nghiêm trọng trong n8n, giúp giảm thời gian phản hồi và nâng cao hiệu quả giám sát hệ thống."
slug: "tu-dong-canh-bao-loi-theo-muc-do-nghiem-trong-n8n"
tags: [n8n, automation, devops, google-sheets, telegram]
keywords: [n8n workflow, tự động hóa lỗi, cảnh báo lỗi, devops, google sheets]
---

# 🚨 Tự động cảnh báo lỗi theo mức độ nghiêm trọng qua Telegram, Email và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý hệ thống gặp lỗi. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại lỗi theo mức độ nghiêm trọng (Critical, High, Normal)
- Gửi cảnh báo qua Telegram và Email ngay lập tức
- Lưu log lỗi quan trọng vào Google Sheets cho việc kiểm tra sau
- Giảm thời gian phản hồi và nâng cao hiệu quả giám sát hệ thống
- Tránh bị mất cảnh báo quan trọng trong luồng thông báo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và API key
- Tài khoản Gmail và API key
- Google Sheets với Sheet ID và tên sheet
- Chat ID của Telegram channel/group để nhận cảnh báo
- Email nhận cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [Workflow này trên n8n.io](https://n8n.io/workflows/12890)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Send Alert" (Telegram)**: Cấu hình credentials "telegramApi" và điền Chat ID của Telegram channel/group nhận cảnh báo
- **Node "Send an Email" (Gmail)**: Cấu hình credentials "gmailApi" và điền địa chỉ email nhận cảnh báo
- **Node "Add Logs to Sheet" (Google Sheets)**:
  - Cấu hình credentials "googleSheetsApi"
  - Điền Sheet ID và tên sheet để lưu log
  - Đảm bảo tài khoản Google có quyền chỉnh sửa sheet này
- **Node "Error Trigger"**: Đảm bảo workflow này được kích hoạt (Active) để bắt lỗi từ các workflow khác

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để kiểm tra định dạng cảnh báo
2. Bật Active workflow
3. Trong các workflow khác, chọn workflow này làm Error Workflow để bắt lỗi

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận cảnh báo cùng với Telegram
- Tạo báo cáo hàng ngày từ Google Sheets để theo dõi xu hướng lỗi
- Tích hợp với các hệ thống giám sát khác như Prometheus để nâng cao khả năng phát hiện lỗi
- Thiết lập các quy tắc cảnh báo nâng cao trong node "Classify Error & Context" để phân loại lỗi một cách chính xác hơn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc giám sát và cảnh báo lỗi trong hệ thống n8n. Bằng cách tự động phân loại và gửi cảnh báo theo mức độ nghiêm trọng, các sếp có thể giảm thời gian phản hồi và nâng cao hiệu quả quản lý hệ thống. Hãy áp dụng ngay để nâng cao khả năng giám sát và bảo trì hệ thống của bạn!