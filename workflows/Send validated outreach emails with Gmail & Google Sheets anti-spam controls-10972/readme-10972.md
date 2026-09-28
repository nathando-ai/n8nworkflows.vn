---
title: "📧 Tự động hóa gửi email chào hàng với kiểm soát chống spam bằng Gmail & Google Sheets"
description: "Hướng dẫn chi tiết cách tự động gửi email chào hàng với kiểm soát chống spam bằng n8n, kết hợp Gmail và Google Sheets để tối ưu hóa quá trình chăm sóc khách hàng tiềm năng."
slug: "tu-dong-hoa-gui-email-chao-hang-voi-gmail-google-sheets"
tags: [n8n, automation, no-code, email-marketing, lead-nurturing]
keywords: [n8n workflow, tự động hóa email, chống spam, Google Sheets, Gmail]
---

# 📧 Tự động hóa gửi email chào hàng với kiểm soát chống spam bằng Gmail & Google Sheets

[Các sếp] có biết rằng việc gửi email chào hàng thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ lấy danh sách liên hệ đến gửi email và cập nhật trạng thái, đồng thời bảo vệ danh tiếng email của doanh nghiệp bằng các kiểm soát chống spam tiên tiến.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình gửi email, giảm thiểu công việc thủ công.
- **Chính xác cao**: Kiểm soát chống spam và xác thực email trước khi gửi.
- **Cá nhân hóa**: Tạo nội dung email cá nhân hóa cho từng khách hàng tiềm năng.
- **Hoạt động liên tục**: Gửi email theo lịch trình tự động, bao gồm cả kiểm soát số lượng email hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets và Gmail.
- API Key cho Google Sheets và Gmail (sẽ được hướng dẫn trong phần cấu hình).
- Danh sách liên hệ trong Google Sheets với các trường thông tin: Name, EMAIL, Opening, Body, Closing, Signature.
- File đính kèm (nếu có) trong Google Drive.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10972](https://n8n.io/workflows/10972)
2. Click vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get Contacts with Emails" (Code)**
   - Chỉnh sửa đoạn code để lấy dữ liệu từ Google Sheets của các sếp.
   - Đảm bảo các trường dữ liệu (Name, EMAIL, Opening, Body, Closing, Signature) được ánh xạ đúng.

2. **Node "Download file" (Google Drive)**
   - Cấu hình credentials cho Google Drive.
   - Điền ID của file đính kèm trong Google Drive vào trường "File ID".

3. **Node "EMAILS SHEET" (Google Sheets)**
   - Cấu hình credentials cho Google Sheets.
   - Điền ID của Google Sheet chứa danh sách liên hệ vào trường "Spreadsheet ID".
   - Điền tên sheet chứa danh sách liên hệ vào trường "Sheet Name".

4. **Node "SEND INITIAL EMAIL" (Gmail)**
   - Cấu hình credentials cho Gmail.
   - Đảm bảo email gửi đi có cấu trúc đúng với các biến động như trong phần GMAIL PAYLOAD của ghi chú.

5. **Node "INITIAL EMAIL SHEET" (Google Sheets)**
   - Cấu hình credentials cho Google Sheets.
   - Điền ID của Google Sheet chứa danh sách liên hệ vào trường "Spreadsheet ID".
   - Điền tên sheet chứa danh sách liên hệ vào trường "Sheet Name".

6. **Node "UPDATE EMAIL SHEET" (Google Sheets)**
   - Cấu hình credentials cho Google Sheets.
   - Điền ID của Google Sheet chứa danh sách liên hệ vào trường "Spreadsheet ID".
   - Điền tên sheet chứa danh sách liên hệ vào trường "Sheet Name".

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow và theo dõi quá trình gửi email.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để thông báo khi có email gửi thành công hoặc thất bại.
- **Lưu log**: Thêm node để lưu log các email đã gửi vào Google Sheets hoặc cơ sở dữ liệu khác.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về số lượng email đã gửi mỗi ngày.
- **Tích hợp với CRM**: Kết nối với các hệ thống CRM như HubSpot, Salesforce để cập nhật trạng thái liên hệ sau khi gửi email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình gửi email chào hàng, đồng thời bảo vệ danh tiếng email của doanh nghiệp bằng các kiểm soát chống spam tiên tiến. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, tăng chính xác và cá nhân hóa trong quá trình chăm sóc khách hàng tiềm năng.