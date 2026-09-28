---
title: "🚀 Tự động gửi email cá nhân hóa từ Google Sheets đến khách hàng tiềm năng bằng SendGrid"
description: "Hướng dẫn chi tiết cách tự động hóa gửi email cá nhân hóa từ Google Sheets đến khách hàng tiềm năng sử dụng SendGrid. Tiết kiệm thời gian và nâng cao hiệu quả chăm sóc khách hàng."
slug: "tu-dong-gui-email-ca-nhan-hoa-tu-google-sheets-den-khach-hang-tiem-nang-bang-sendgrid"
tags: [n8n, automation, no-code, email-marketing, sendgrid]
keywords: [n8n workflow, tự động hóa email, email cá nhân hóa, sendgrid, google sheets]
---

# 🚀 Tự động gửi email cá nhân hóa từ Google Sheets đến khách hàng tiềm năng bằng SendGrid

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức trong việc gửi email thủ công
- Gửi email cá nhân hóa với nội dung phù hợp cho từng khách hàng
- Tăng hiệu quả chăm sóc khách hàng tiềm năng
- Tự động hóa quy trình marketing qua email
- Theo dõi và quản lý khách hàng tiềm năng một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt
- Tài khoản SendGrid với API key và domain đã được xác thực
- Google Sheets với 2 tab: "Leads" và "Email Template"
- Dữ liệu khách hàng tiềm năng đã được nhập vào tab "Leads"
- Các mẫu email đã được chuẩn bị sẵn trong tab "Email Template"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **When clicking ‘Execute workflow’**: Node này sẽ kích hoạt workflow khi bạn nhấn nút "Execute workflow" trong n8n Editor.
- **Loop Over Items**: Node này sẽ lặp qua từng khách hàng tiềm năng trong danh sách.
- **Merge**: Node này sẽ hợp nhất dữ liệu từ các node trước đó.
- **Wait**: Node này sẽ tạo độ trễ giữa các lần gửi email để tránh bị chặn bởi dịch vụ email.
- **Parse Email Template from DB**: Node này sẽ lấy mẫu email từ Google Sheets. Các sếp cần cấu hình:
  - Chọn credentials là "googleSheetsOAuth2Api"
  - Chọn Spreadsheet ID và Sheet Name là "Email Template"
- **Pick a random template**: Node này sẽ chọn ngẫu nhiên một mẫu email từ danh sách mẫu đã có.
- **Limit**: Node này sẽ giới hạn số lượng email được gửi trong một lần chạy workflow.
- **Get row(s) in sheet**: Node này sẽ lấy dữ liệu khách hàng tiềm năng từ Google Sheets. Các sếp cần cấu hình:
  - Chọn credentials là "googleSheetsOAuth2Api"
  - Chọn Spreadsheet ID và Sheet Name là "Leads"
- **Send an email**: Node này sẽ gửi email đến khách hàng tiềm năng. Các sếp cần cấu hình:
  - Chọn credentials là "sendGridApi"
  - Điền các thông tin cần thiết như From, To, Subject, và Body
- **Fix Variables**: Node này sẽ sửa các biến trong mẫu email để phù hợp với từng khách hàng.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công hoặc thất bại.
- Lưu log các email đã gửi vào Google Sheets để theo dõi và quản lý.
- Gửi báo cáo định kỳ về hiệu quả của chiến dịch email marketing.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn chỉnh để gửi email cá nhân hóa đến khách hàng tiềm năng từ Google Sheets sử dụng SendGrid. Với workflow này, các sếp có thể tiết kiệm thời gian và công sức trong việc gửi email thủ công, đồng thời tăng hiệu quả chăm sóc khách hàng tiềm năng.