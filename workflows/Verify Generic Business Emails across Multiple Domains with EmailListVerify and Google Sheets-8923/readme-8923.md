---
title: "🚀 Tự động kiểm tra email doanh nghiệp chung với EmailListVerify và Google Sheets"
description: "Hướng dẫn tự động hóa kiểm tra email chung (contact@, sales@...) trên nhiều domain bằng n8n, tiết kiệm thời gian và tăng hiệu quả tìm kiếm email doanh nghiệp."
slug: "tu-dong-kiem-tra-email-doanh-nghiep-chung"
tags: [n8n, automation, no-code, email-verification, google-sheets]
keywords: [n8n workflow, tự động hóa email, kiểm tra email, EmailListVerify, Google Sheets]
---

# 🚀 Tự động kiểm tra email doanh nghiệp chung với EmailListVerify và Google Sheets

[Bạn là người quản lý marketing, sales hay tuyển dụng?] Bạn có bao giờ phải tìm kiếm email doanh nghiệp chung như contact@, sales@ hay info@ cho hàng trăm domain không? Việc này thường tốn thời gian và công sức, đặc biệt khi phải kiểm tra từng email một. Với workflow này, bạn có thể tự động hóa toàn bộ quy trình này trong vài phút, tiết kiệm hàng giờ làm việc mỗi tháng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình kiểm tra email từ 30-60 phút xuống còn vài giây.
- **Chính xác cao**: Sử dụng API EmailListVerify để xác thực email thực sự hoạt động.
- **Quản lý tập trung**: Tất cả kết quả được lưu trong Google Sheets, dễ dàng theo dõi và chia sẻ.
- **Tùy chỉnh linh hoạt**: Có thể kiểm tra nhiều domain và nhiều pattern email khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets.
- API Key từ [EmailListVerify](https://app.emaillistverify.com/api?utm_source=n8n&utm_medium=referral&utm_campaign=genericEmailFinder).
- Một bản sao của [Google Sheets template](https://docs.google.com/spreadsheets/d/11JW2e9w00bZO_ORe0FNaK_u5tnchI8ZOwcq8qN1toZw/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8923](https://n8n.io/workflows/8923) và tải file JSON về máy.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get list of domain"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Cập nhật "Spreadsheet ID" và "Sheet Name" trỏ đến sheet "[Input] domain" trong bản sao của bạn.

2. **Node "Get list of email root"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Cập nhật "Spreadsheet ID" và "Sheet Name" trỏ đến sheet "[Input] pattern" trong bản sao của bạn.

3. **Node "Use EmailListVerify API to check if email is valid"**:
   - Chọn credentials là "httpQueryAuth".
   - Thêm API Key của bạn vào query parameters với key là "key".
   - Thêm header "Content-Type" với giá trị "application/json".

4. **Node "Save results"**:
   - Chọn credentials là "googleSheetsOAuth2Api".
   - Cập nhật "Spreadsheet ID" và "Sheet Name" trỏ đến sheet "[Output] results" trong bản sao của bạn.

#### 3. Kích hoạt ⚡️
1. Nhấn vào node "When clicking ‘Execute workflow’" và chọn "Manual Trigger".
2. Nhấn "Execute Node" để chạy thử với dữ liệu mẫu.
3. Sau khi kiểm tra kết quả, nhấn "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo kết quả qua Slack hoặc Telegram.
- **Lịch chạy tự động**: Sử dụng node "Schedule Trigger" để chạy workflow định kỳ hàng ngày.
- **Xử lý lỗi**: Thêm node "Error Trigger" để xử lý các trường hợp lỗi và gửi cảnh báo.
- **Báo cáo định kỳ**: Tạo một workflow phụ để tổng hợp kết quả hàng tuần và gửi email báo cáo.

### 📌 Kết luận
Workflow này giúp các sếp marketing, sales và tuyển dụng tiết kiệm thời gian và công sức trong việc tìm kiếm email doanh nghiệp chung. Với việc tự động hóa toàn bộ quy trình, bạn có thể tập trung vào các công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!