---
title: "🚀 Tự động đồng bộ danh sách email mới từ Google Sheets sang MailerLite tránh trùng lặp"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ danh sách email mới từ Google Sheets sang MailerLite mà không bị trùng lặp, tiết kiệm thời gian và giảm thiểu lỗi thủ công"
slug: "tu-dong-dong-bo-danh-sach-email-moi-tu-google-sheets-sang-mailerlite-tranh-trung-lap"
tags: [n8n, automation, no-code, email-marketing, google-sheets]
keywords: [n8n workflow, tự động hóa email, đồng bộ danh sách, MailerLite, Google Sheets]
---

# 🚀 Tự động đồng bộ danh sách email mới từ Google Sheets sang MailerLite tránh trùng lặp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi quản lý danh sách email cho chiến dịch marketing, các sếp thường phải đối mặt với những thách thức như:
- 🕒 Tốn thời gian nhập liệu thủ công giữa Google Sheets và MailerLite
- 📉 Rủi ro trùng lặp email trong danh sách
- 🔄 Khó khăn trong việc duy trì đồng bộ dữ liệu giữa các hệ thống
- 📉 Giảm hiệu quả chiến dịch do dữ liệu không chính xác

Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🕒 Tiết kiệm 20-30 phút mỗi ngày cho công việc nhập liệu thủ công
- 📉 Giảm 100% rủi ro trùng lặp email trong danh sách
- 🔄 Dữ liệu luôn đồng bộ giữa Google Sheets và MailerLite
- 📈 Tăng hiệu quả chiến dịch marketing nhờ dữ liệu chính xác
- ⚡ Tự động hóa liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản MailerLite với quyền truy cập API
- Google Sheet đã chuẩn bị với các cột dữ liệu: Email, first_name, last_name, Company, Country, group_id
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/7681)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Start Workflow" (manualTrigger)**
   - Không cần cấu hình gì, chỉ cần kích hoạt workflow khi cần

2. **Node "Get row(s) in sheet" (googleSheets)**
   - Cấu hình credentials: Chọn Google Sheets OAuth2 API đã được thiết lập
   - Tham số cần điền:
     - Spreadsheet ID: ID của Google Sheet chứa danh sách email
     - Range: Phạm vi dữ liệu cần lấy (ví dụ: "Sheet1!A2:F")
     - Output Format: Chọn "Object" để dữ liệu dễ xử lý

3. **Node "Get a Subscriber" (mailerLite)**
   - Cấu hình credentials: Chọn MailerLite API đã được thiết lập
   - Tham số cần điền:
     - Email: Chọn từ dữ liệu đầu ra của node trước đó ({{$node["Get row(s) in sheet"].json[0].Email}})
     - Fields: Chọn "email" để kiểm tra sự tồn tại của email

4. **Node "Create Subscriber & Assign to Group" (httpRequest)**
   - Cấu hình credentials: Chọn MailerLite API đã được thiết lập
   - Tham số cần điền:
     - URL: `https://connect.mailerlite.com/api/subscribers`
     - Method: POST
     - Headers:
       ```json
       {
         "Content-Type": "application/json",
         "Authorization": "Bearer {{credentials.mailerLiteApi.apiKey}}"
       }
       ```
     - Body:
       ```json
       {
         "email": "{{$node["Get row(s) in sheet"].json[0].Email}}",
         "fields": {
           "first_name": "{{$node["Get row(s) in sheet"].json[0].first_name}}",
           "last_name": "{{$node["Get row(s) in sheet"].json[0].last_name}}",
           "company": "{{$node["Get row(s) in sheet"].json[0].Company}}",
           "country": "{{$node["Get row(s) in sheet"].json[0].Country}}"
         },
         "groups": ["{{$node["Get row(s) in sheet"].json[0].group_id}}"]
       }
       ```

5. **Node "End workflow" (noOp)**
   - Node này chỉ để kết thúc workflow cho các email đã tồn tại
   - Không cần cấu hình gì

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Để test workflow, click vào nút "Execute Workflow" và theo dõi kết quả
3. Kiểm tra danh sách email trong MailerLite để xác nhận dữ liệu đã được đồng bộ chính xác

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa định kỳ**: Thiết lập workflow chạy tự động mỗi ngày bằng cách sử dụng node "Schedule Trigger" thay vì "Manual Trigger"
2. **Xử lý lỗi**: Thêm node "Error Trigger" để nhận thông báo khi có lỗi xảy ra trong quá trình đồng bộ
3. **Báo cáo kết quả**: Kết nối với Slack hoặc Email để nhận báo cáo sau mỗi lần đồng bộ
4. **Xử lý dữ liệu phức tạp**: Sử dụng node "Function" để xử lý dữ liệu phức tạp trước khi gửi sang MailerLite

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình đồng bộ danh sách email từ Google Sheets sang MailerLite, giảm thiểu rủi ro trùng lặp và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để nâng cao hiệu quả quản lý danh sách email của doanh nghiệp! 🚀