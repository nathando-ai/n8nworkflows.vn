---
title: "📧 [Tự động hóa] Gửi email cá nhân hóa từ Google Sheets qua SMTP - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động gửi email cá nhân hóa từ Google Sheets qua SMTP với workflow n8n. Tiết kiệm thời gian, tránh spam và theo dõi kết quả gửi email."
slug: "tu-dong-hoa-gui-email-ca-nhan-hoa-tu-google-sheets-qua-smtp"
tags: [n8n, automation, no-code, email-marketing, google-sheets]
keywords: [n8n workflow, tự động hóa email, gửi email cá nhân hóa, google sheets automation, smtp email]
---

# 📧 [Tự động hóa] Gửi email cá nhân hóa từ Google Sheets qua SMTP - Workflow n8n hoàn chỉnh

[Các sếp đang gặp khó khăn khi phải gửi hàng trăm email cá nhân hóa một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi email và cập nhật trạng thái, giúp tiết kiệm thời gian đáng kể và giảm thiểu lỗi.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi gửi hàng trăm email cá nhân hóa
- Giảm thiểu lỗi khi gửi email thủ công
- Theo dõi trạng thái gửi email trong Google Sheets
- Tránh gửi trùng lặp email cho cùng một người nhận
- Tùy chỉnh nội dung email theo từng cá nhân
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản SMTP (khuyến nghị sử dụng SendGrid, Webmail hoặc SMTP của hosting)
- Google Sheets đã chuẩn bị với các cột: Email, Name, Status, Email Sent
- Nội dung email mẫu đã chuẩn bị sẵn sàng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/12982
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Start email automation** (scheduleTrigger):
   - Cấu hình thời gian gửi email theo lịch trình mong muốn

2. **Fetch contacts from Google Sheets** (googleSheets):
   - Chọn credentials Google Sheets OAuth2 API
   - Điền thông tin Spreadsheet ID và Sheet Name
   - Đảm bảo các cột trong Google Sheets khớp với cấu hình: Email, Name, Status, Email Sent

3. **Check no-show status** (if):
   - Cấu hình điều kiện lọc (ví dụ: Status != "No-show")

4. **Check if email already sent** (if):
   - Cấu hình điều kiện lọc (ví dụ: Email Sent != "Yes")

5. **Prepare email content** (set):
   - Cấu hình nội dung email với các biến động như {{ $node["Fetch contacts from Google Sheets"].json["Name"] }}
   - Đảm bảo các biến động được đặt trong dấu ngoặc kép kép

6. **Send email via SMTP** (emailSend):
   - Chọn credentials SMTP
   - Cấu hình From Email, Subject và Body của email
   - Đảm bảo sử dụng SMTP của dịch vụ chuyên nghiệp (không phải Gmail, Yahoo, Outlook)

7. **Mark email as sent in sheet** (googleSheets):
   - Đảm bảo cấu hình update đúng Spreadsheet ID, Sheet Name và phạm vi cập nhật
   - Cập nhật giá trị Email Sent thành "Yes" sau khi gửi email thành công

#### 3. Kích hoạt ⚡️
1. Test run workflow với 2-3 email thử nghiệm
2. Kiểm tra:
   - Nội dung email cá nhân hóa
   - Email không bị gửi vào thư mục spam
   - Google Sheets được cập nhật trạng thái Email Sent
   - Workflow không gửi trùng lặp email
3. Sau khi kiểm tra thành công, kích hoạt workflow bằng cách nhấn "Active"

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
2. Thêm node lưu log gửi email để theo dõi hiệu suất
3. Tự động gửi báo cáo hàng tuần về số lượng email đã gửi
4. Tích hợp với CRM để cập nhật trạng thái lead sau khi gửi email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gửi email cá nhân hóa từ Google Sheets qua SMTP, tiết kiệm thời gian đáng kể và giảm thiểu lỗi. Hãy thử nghiệm với 2-3 email trước khi kích hoạt toàn bộ workflow để đảm bảo mọi thứ hoạt động như mong đợi.