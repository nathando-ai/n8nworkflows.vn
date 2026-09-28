---
title: "🚀 Theo dõi các sản phẩm mới trên Product Hunt và xác thực website trong Google Sheets"
description: "Tự động hóa việc theo dõi các sản phẩm mới được đăng trên Product Hunt hàng ngày và xác thực website của chúng trong Google Sheets, tiết kiệm thời gian và đảm bảo dữ liệu chính xác."
slug: "theo-doi-san-pham-moi-product-hunt-google-sheets"
tags: [n8n, automation, no-code, Product Hunt, Google Sheets]
keywords: [n8n workflow, tự động hóa, Product Hunt, Google Sheets, theo dõi sản phẩm]
---

# 🚀 Theo dõi các sản phẩm mới trên Product Hunt và xác thực website trong Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc theo dõi các sản phẩm mới hàng ngày.
- Dữ liệu chính xác: Xác thực website của các sản phẩm mới.
- Cá nhân hóa: Lưu trữ thông tin sản phẩm trong Google Sheets của bạn.
- Hoạt động liên tục: Workflow chạy tự động mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Product Hunt và token API.
- Tài khoản Google và quyền truy cập vào Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3588](https://n8n.io/workflows/3588).
2. Nhấn vào nút "Import" và chọn "Import from URL".
3. Dán URL của workflow vào ô nhập liệu và nhấn "OK".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger1**: Cấu hình thời gian chạy hàng ngày.
2. **Fetches today’s Product Hunt posts via API**: Cấu hình credentials cho Product Hunt.
3. **Appends all details**: Cấu hình credentials cho Google Sheets và chỉ định tên sheet và phạm vi dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có sản phẩm mới.
- Lưu log các sản phẩm đã được theo dõi.
- Gửi báo cáo định kỳ về các sản phẩm mới.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và đảm bảo dữ liệu chính xác khi theo dõi các sản phẩm mới trên Product Hunt. Hãy áp dụng ngay để tối ưu hóa quá trình làm việc của bạn!