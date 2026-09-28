---
title: "🚀 Tự động hóa lọc lead Form.io với ZeroBounce và đồng bộ Pipedrive - Workflow n8n"
description: "Hướng dẫn tự động hóa lọc lead từ Form.io với ZeroBounce (xác thực email và AI Scoring) và đồng bộ Pipedrive. Tiết kiệm thời gian và tăng chất lượng lead."
slug: "tu-dong-hoa-loc-lead-formio-zerobounce-pipedrive"
tags: [n8n, automation, no-code, lead-generation, crm]
keywords: [n8n workflow, tự động hóa lead, xác thực email, AI scoring, Pipedrive]
---

# 🚀 Tự động hóa lọc lead Form.io với ZeroBounce và đồng bộ Pipedrive

[Các sếp đang gặp khó khăn khi xử lý hàng loạt lead từ Form.io thủ công. Workflow này giúp tự động hóa toàn bộ quy trình từ xác thực email đến đồng bộ Pipedrive, giảm thiểu rác và tăng chất lượng lead.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **✨ Zero-Waste Sync:** Chỉ các lead "Valid" hoặc "High-Scoring" mới được đồng bộ vào CRM.
- **🛡️ Credit Safety:** Kiểm tra tín dụng trước khi gọi API để tránh lỗi.
- **📊 Detailed Suppressions:** Mỗi lead bị loại đều được ghi lại lý do cụ thể (Email thiếu, Invalid, Low Score, hoặc không đủ tín dụng).
- **🔄 Tự động hóa hoàn toàn:** Tiết kiệm thời gian xử lý thủ công hàng loạt lead.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Form.io:** Kết nối qua credentials để nhận sự kiện "Form Submission".
- **ZeroBounce:** Kết nối qua API Key. [Tạo API Key tại đây](https://www.zerobounce.net/members/API).
- **Pipedrive:** Kết nối qua API Key để tạo/cập nhật người dùng cho lead chất lượng cao.
- **Google Sheets:** Kết nối qua OAuth2 để thêm/cập nhật dữ liệu vào bảng tính. Hoặc có thể thay thế bằng các node lưu trữ dữ liệu khác như n8n Data Table hoặc Microsoft Excel. Các bảng tính có thể được tạo với các cột sau:
  - *Accepted* columns:
    `Email,Name,Accepted At,Accepted Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`
  - *Rejected* columns:
    `Email,Name,Rejected At,Rejected Reason,ZB Status,ZB Sub Status,ZB Free Email,ZB Did You Mean,ZB Account,ZB Domain,ZB Domain Age Days,ZB SMTP Provider,ZB MX Found,ZB MX Record,ZB Score`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13008](https://n8n.io/workflows/13008)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Form.io Trigger**: Cần cấu hình credentials cho Form.io và chọn form cần theo dõi.
- **ZeroBounce**: Cần tạo và cấu hình API Key từ [ZeroBounce](https://www.zerobounce.net/members/API).
- **Pipedrive**: Cần cấu hình API Key và chọn organization.
- **Google Sheets**:
  - Cấu hình credentials OAuth2.
  - Chỉnh sửa các tham số:
    - Spreadsheet ID: ID của Google Sheet cần lưu trữ dữ liệu.
    - Worksheet Name: Tên của worksheet (ví dụ: "Accepted" hoặc "Rejected").
    - Column Names: Đảm bảo các cột trong Google Sheet khớp với định dạng yêu cầu.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Execute Node" để kiểm tra workflow với dữ liệu mẫu.
2. Kiểm tra kết quả ở các node cuối cùng (Add to Accepted, Add to Rejected).
3. Nếu mọi thứ hoạt động tốt, click vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có lead mới được đồng bộ hoặc bị loại.
- **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu để theo dõi hiệu suất workflow.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo hàng tuần về số lượng lead được xử lý, tỷ lệ chuyển đổi và các chỉ số quan trọng khác.
- **Tích hợp với các công cụ khác**: Có thể kết hợp với các công cụ như Mailchimp để tự động gửi email chào mừng cho lead chất lượng cao.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình lọc lead từ Form.io, từ xác thực email đến đồng bộ Pipedrive, giảm thiểu rác và tăng chất lượng lead. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian và tập trung vào các hoạt động quan trọng hơn trong quá trình chăm sóc khách hàng.