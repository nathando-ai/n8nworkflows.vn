---
title: "📦 Tự động hóa xử lý tin nhắn EDI với Gmail và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa xử lý tin nhắn EDI từ email đến Google Sheets, tiết kiệm thời gian và giảm lỗi thủ công cho các sếp quản lý chuỗi cung ứng."
slug: "tu-dong-hoa-xu-ly-tin-nhan-edi-voi-gmail-va-google-sheets"
tags: [n8n, automation, no-code, supply-chain, logistics]
keywords: [n8n workflow, tự động hóa EDI, xử lý email tự động, quản lý đơn hàng]
---

# 📦 Tự động hóa xử lý tin nhắn EDI với Gmail và Google Sheets

[Các sếp quản lý chuỗi cung ứng thường phải xử lý hàng loạt tin nhắn EDI hàng ngày. Việc này tốn thời gian, dễ gây lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ nhận email EDI đến lưu trữ dữ liệu vào Google Sheets, đảm bảo dữ liệu chính xác và cập nhật liên tục.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý hàng loạt tin nhắn EDI hàng ngày
- Giảm thiểu lỗi thủ công trong quá trình xử lý dữ liệu
- Dữ liệu được lưu trữ tự động vào Google Sheets, dễ dàng truy cập và quản lý
- Hệ thống hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Dữ liệu được phân loại tự động thành các loại đơn hàng khác nhau (trả hàng, xuất hàng)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail API credentials để nhận và xử lý email
- Tài khoản Google Sheets API credentials để lưu trữ dữ liệu
- Một Google Sheet đã được tạo sẵn với hai sheet: "Return Orders" và "Outbound Orders"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: https://n8n.io/workflows/3221
3. Hoặc tải file JSON về và import từ local

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Email Trigger** (gmailTrigger node):
   - Cấu hình Gmail API credentials
   - Đảm bảo email được gửi đến có tiêu đề chứa từ "EDI"

2. **Get Email** (gmail node):
   - Cấu hình Gmail API credentials
   - Đảm bảo node này được kết nối với Email Trigger node

3. **Return Orders** và **Outbound Orders** (googleSheets nodes):
   - Cấu hình Google Sheets API credentials
   - Chọn Google Sheet file và sheet tương ứng (Return Orders hoặc Outbound Orders)
   - Đảm bảo các cột trong sheet đã được tạo sẵn để ánh xạ dữ liệu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách gửi email EDI mẫu đến tài khoản Gmail của bạn
2. Kiểm tra dữ liệu được lưu trữ đúng vào Google Sheets
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo khi có đơn hàng mới được xử lý
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng của workflow
3. **Xử lý lỗi tự động**: Thêm node để xử lý các trường hợp lỗi trong quá trình xử lý
4. **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng ngày về các đơn hàng đã xử lý

### 📌 Kết luận
Workflow này giúp các sếp quản lý chuỗi cung ứng tự động hóa toàn bộ quy trình xử lý tin nhắn EDI từ email đến lưu trữ dữ liệu vào Google Sheets. Với việc giảm thiểu công việc thủ công, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn và đảm bảo dữ liệu luôn được cập nhật và chính xác. Hãy áp dụng ngay để nâng cao hiệu quả quản lý chuỗi cung ứng của bạn!