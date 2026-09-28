---
title: "🚀 Tự động hóa khảo sát CSAT sau giao hàng với Gmail, Google Sheets và Typeform"
description: "Hướng dẫn tự động hóa quy trình khảo sát CSAT sau giao hàng 100% không cần code, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-hoa-khao-sat-csat-sau-giao-hang"
tags: [n8n, automation, no-code, customer-experience, google-sheets]
keywords: [n8n workflow, tự động hóa, khảo sát CSAT, trải nghiệm khách hàng, Google Sheets]
---

# 🚀 Tự động hóa khảo sát CSAT sau giao hàng với Gmail, Google Sheets và Typeform

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý thủ công các khảo sát CSAT sau giao hàng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý khảo sát thủ công
- Tăng độ chính xác dữ liệu khách hàng
- Tự động hóa quy trình khảo sát CSAT sau giao hàng
- Nhận phản hồi khách hàng ngay lập tức
- Phân loại và xử lý phản hồi khách hàng một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API
- Tài khoản Google Workspace với Google Sheets
- API Key của Typeform
- URL của Typeform survey
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/15237
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**Node "Incoming Delivery Webhook"**:
- Cấu hình webhook với path: `delivery-webhook` và method: `POST`
- Cập nhật URL webhook trong hệ thống gửi webhook (ví dụ: Shopify, WooCommerce)

**Node "Send Low CSAT Alert (Gmail)" và "Send Survey Email (Gmail)"**:
- Cấu hình credentials Gmail OAuth2
- Điền địa chỉ email người nhận cảnh báo

**Node "Fetch Sent Survey Records" và các node Google Sheets khác**:
- Cấu hình credentials Google Sheets OAuth2
- Điền ID của Google Sheet chứa dữ liệu khảo sát
- Đảm bảo cấu trúc cột phù hợp (order_id, email, csat_score, feedback)

**Node "CSAT Response Intake Webhook"**:
- Cấu hình webhook với path: `csat-response` và method: `POST`
- Cập nhật URL webhook trong Typeform

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu thông qua webhook
- Kiểm tra email khảo sát được gửi đến khách hàng
- Kiểm tra dữ liệu được lưu trong Google Sheets
- Kiểm tra xử lý phản hồi từ khách hàng

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo cảnh báo CSAT thấp
- Thêm bước gửi email cảm ơn cho khách hàng có CSAT cao
- Tích hợp với hệ thống CRM để cập nhật thông tin phản hồi khách hàng
- Thiết lập báo cáo định kỳ dựa trên dữ liệu CSAT

### 📌 Kết luận
Workflow này tạo ra một hệ thống tự động hoàn chỉnh để quản lý khảo sát CSAT sau giao hàng, từ việc gửi email khảo sát đến xử lý phản hồi và phân loại khách hàng. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và nhận được dữ liệu phản hồi khách hàng một cách nhanh chóng và chính xác.