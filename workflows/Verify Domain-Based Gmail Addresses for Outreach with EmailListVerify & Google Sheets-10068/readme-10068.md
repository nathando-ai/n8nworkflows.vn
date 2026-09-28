---
title: "🚀 Tự động tìm kiếm email Gmail từ tên miền cho chiến dịch liên hệ - n8n Workflow"
description: "Hướng dẫn tự động hóa tìm kiếm email Gmail từ tên miền để xây dựng liên kết (link building) với n8n Workflow. Tiết kiệm thời gian và tăng hiệu quả liên hệ."
slug: "tu-dong-tim-kiem-email-gmail-tu-ten-mien"
tags: [n8n, automation, no-code, link-building, email-verification]
keywords: [n8n workflow, tự động hóa, tìm kiếm email, liên hệ doanh nghiệp, xây dựng liên kết]
---

# 🚀 Tự động tìm kiếm email Gmail từ tên miền cho chiến dịch liên hệ

[Các sếp] có bao giờ gặp tình trạng mất thời gian tìm kiếm email liên hệ cho các trang web nhỏ không? Với workflow này, các sếp có thể tự động hóa quá trình này hoàn toàn, tiết kiệm thời gian và tăng hiệu quả liên hệ cho chiến dịch link building.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tìm kiếm email Gmail từ tên miền (ví dụ: domain@gmail.com)
- Kiểm tra tính hợp lệ của email thông qua API EmailListVerify
- Lưu kết quả vào Google Sheets để quản lý dễ dàng
- Tiết kiệm thời gian lên tới 90% so với làm thủ công
- Tăng hiệu quả liên hệ cho chiến dịch link building
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- API Key từ [EmailListVerify](https://app.emaillistverify.com/api?utm_source=n8n&utm_medium=referral&utm_campaign=GmaimFinder)
- Bản sao của [Google Sheets Template](https://docs.google.com/spreadsheets/d/1r4DZ4GnqKzivmIhRdv1D35fvS_Mg-VTKgbuZS-7H-HY/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/10068](https://n8n.io/workflows/10068)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get list of email extension"**:
   - Chọn credentials là "googleSheetsOAuth2Api"
   - Điền thông tin Spreadsheet ID và Sheet Name từ bản sao của template

2. **Node "Get list of domain"**:
   - Chọn credentials là "googleSheetsOAuth2Api"
   - Điền thông tin Spreadsheet ID và Sheet Name từ bản sao của template

3. **Node "Use EmailListVerify API to check if email is valid"**:
   - Chọn credentials là "httpQueryAuth"
   - Điền API Key từ EmailListVerify vào trường "API Key"
   - Đảm bảo URL API là `https://app.emaillistverify.com/api/verifyEmail`

4. **Node "Save results"**:
   - Chọn credentials là "googleSheetsOAuth2Api"
   - Điền thông tin Spreadsheet ID và Sheet Name từ bản sao của template

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử
2. Kiểm tra kết quả trên Google Sheets
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi tìm thấy email hợp lệ
- Kết hợp với workflow gửi email tự động để liên hệ ngay lập tức
- Tạo lịch trình chạy định kỳ để cập nhật danh sách email mới
- Thêm node lưu log để theo dõi quá trình thực thi

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình tìm kiếm email liên hệ. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các hoạt động quan trọng hơn trong chiến dịch link building. Hãy áp dụng ngay để tăng hiệu quả liên hệ và xây dựng mạng lưới liên kết mạnh mẽ hơn!