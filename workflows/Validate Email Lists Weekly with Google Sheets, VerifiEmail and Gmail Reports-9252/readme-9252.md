---
title: "🚀 Tự động hóa kiểm tra danh sách email hàng tuần với Google Sheets, VerifiEmail và báo cáo Gmail"
description: "Giải pháp tự động hóa kiểm tra danh sách email hàng tuần giúp giảm tỷ lệ email không hợp lệ, cải thiện chất lượng gửi email và tuân thủ quy định GDPR/CAN-SPAM"
slug: "tu-dong-hoa-kiem-tra-danh-sach-email-hang-tuan"
tags: [n8n, automation, no-code, email-marketing, google-sheets]
keywords: [n8n workflow, tự động hóa email, kiểm tra email, VerifiEmail, Google Sheets]
---

# 🚀 Tự động hóa kiểm tra danh sách email hàng tuần với Google Sheets, VerifiEmail và báo cáo Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giảm tỷ lệ email không hợp lệ lên tới 15% và giữ tỷ lệ bounce dưới 2%
- Cải thiện uy tín người gửi với các nhà cung cấp dịch vụ email (ISP)
- Tăng ROI và tỷ lệ tương tác cho các chiến dịch email
- Sẵn sàng tuân thủ các quy định GDPR/CAN-SPAM
- Tiết kiệm thời gian đáng kể so với kiểm tra thủ công
- Nhận báo cáo chuyên nghiệp hàng tuần về sức khỏe danh sách email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets
- API key từ VerifiEmail (đăng ký tại [https://verifi.email](https://verifi.email))
- Tài khoản Gmail để gửi báo cáo
- Danh sách email trong Google Sheets với cấu trúc cột như sau:
  • row_number (tự động sinh bởi Sheets)
  • name
  • email
  • status (để trống - sẽ được tự động điền)
  • checked_at (để trống - sẽ được tự động điền)
  • notes (để trống - sẽ được tự động điền)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9252](https://n8n.io/workflows/9252)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Weekly Schedule (Friday 5PM)"**:
   - Đảm bảo lịch trình chạy đúng vào thứ Sáu lúc 17:00 (UTC)
   - Nếu cần thay đổi, chỉnh sửa biểu thức cron trong node này

2. **Node "Read Email List"**:
   - Chọn credential Google Sheets OAuth2 đã cấu hình
   - Điền thông tin Spreadsheet ID và tên Sheet chứa danh sách email
   - Đảm bảo các cột có tên chính xác như yêu cầu (row_number, name, email, status, checked_at, notes)

3. **Node "Validate Email Address"**:
   - Cấu hình credential VerifiEmail API
   - Đảm bảo API key còn hạn sử dụng và có đủ quota

4. **Node "Send Weekly Report"**:
   - Cấu hình credential Gmail OAuth2
   - Chỉnh sửa địa chỉ email nhận báo cáo (mặc định là marketing.manager@company.com)
   - Có thể thêm CC/BCC nếu cần gửi cho nhiều người

5. **Node "Calculate Statistics"**:
   - Kích hoạt tùy chọn "Execute Once" để xử lý tất cả email cùng lúc
   - Có thể điều chỉnh công thức tính điểm sức khỏe nếu cần

#### 3. Kích hoạt ⚡️
1. Thêm 3-5 email thử nghiệm vào Google Sheet
2. Nhấn nút "Execute Workflow" để kiểm tra toàn bộ quy trình
3. Kiểm tra:
   - Google Sheet có được cập nhật trạng thái email không
   - Báo cáo email có được gửi đến đúng địa chỉ không
4. Nếu tất cả đều hoạt động đúng, bật chế độ "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm thông báo Slack**:
   - Thêm node Slack sau node gửi email báo cáo
   - Cấu hình để gửi thông báo đến kênh #marketing

2. **Lưu trữ email không hợp lệ**:
   - Thêm node Google Sheets trên nhánh FALSE để lưu trữ email không hợp lệ
   - Tạo một tab mới "Invalid_Archive" trong Google Sheet

3. **Xuất dữ liệu đến CRM**:
   - Thêm node HTTP Request/Webhook để đẩy email đã xác thực đến HubSpot/Salesforce
   - Đồng bộ tự động danh sách email với hệ thống CRM

4. **Giới hạn tốc độ xử lý**:
   - Thêm node "Wait" sau node kiểm tra email
   - Đặt thời gian chờ 1-2 giây để tránh bị giới hạn API khi xử lý danh sách lớn

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa việc kiểm tra danh sách email hàng tuần, giúp các sếp marketing duy trì danh sách email sạch sẽ, cải thiện chất lượng gửi email và tuân thủ các quy định về bảo mật dữ liệu. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào các chiến dịch marketing quan trọng hơn.