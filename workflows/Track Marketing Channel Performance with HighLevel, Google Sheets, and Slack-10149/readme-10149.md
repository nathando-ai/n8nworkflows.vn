---
title: "🚀 Theo dõi hiệu suất kênh tiếp thị với HighLevel, Google Sheets và Slack"
description: "Tự động hóa quy trình theo dõi hiệu suất kênh tiếp thị bằng n8n, tích hợp HighLevel CRM, Google Sheets và Slack để phân tích dữ liệu và gửi báo cáo tự động."
slug: "theo-doi-hieu-suat-kenh-tiep-thi-highlevel-google-sheets-slack"
tags: [n8n, automation, no-code, crm, analytics]
keywords: [n8n workflow, tự động hóa tiếp thị, phân tích dữ liệu, HighLevel, Google Sheets, Slack]
---

# 🚀 Theo dõi hiệu suất kênh tiếp thị với HighLevel, Google Sheets và Slack

[Các sếp] có biết rằng việc theo dõi hiệu suất kênh tiếp thị thủ công là một công việc tốn thời gian và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy dữ liệu đến phân tích và báo cáo chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình phân tích dữ liệu kênh tiếp thị
- **Chính xác**: Giảm thiểu lỗi do nhập liệu thủ công
- **Cá nhân hóa**: Phân tích chi tiết từng kênh tiếp thị
- **Hoạt động liên tục**: Nhận báo cáo tự động mỗi khi có dữ liệu mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HighLevel CRM
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Slack với quyền gửi tin nhắn
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10149](https://n8n.io/workflows/10149)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch All HighLevel Opportunities"**:
   - Đảm bảo đã thiết lập credentials cho HighLevel
   - Kiểm tra lại các tham số: operation và resource phải là "getAll" và "opportunity"

2. **Node "Log Won Deals to Sheets"**:
   - Thiết lập credentials cho Google Sheets
   - Chỉnh sửa ID của Google Sheet và tên của sheet cần ghi dữ liệu
   - Cấu hình các cột dữ liệu cần ghi (thường là: ID, Name, Status, Amount, Lead Source)

3. **Node "Calculate Lead Source Metrics"**:
   - Kiểm tra hàm tính toán trong node này để đảm bảo nó phù hợp với dữ liệu của các sếp
   - Có thể chỉnh sửa hàm để tính các chỉ số khác như tỷ lệ chuyển đổi, giá trị trung bình...

4. **Node "Send Analytics to Slack"**:
   - Thiết lập credentials cho Slack
   - Chỉnh sửa kênh Slack cần gửi tin nhắn
   - Tùy chỉnh nội dung tin nhắn để phù hợp với báo cáo của các sếp

5. **Node "Alert Non-Won Status to Slack"**:
   - Thiết lập credentials cho Slack
   - Chỉnh sửa kênh Slack cần gửi cảnh báo
   - Tùy chỉnh nội dung cảnh báo để phù hợp với yêu cầu của các sếp

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trên Google Sheets và Slack
3. Sau khi đảm bảo workflow hoạt động đúng, click vào nút "Active workflow" để bật chế độ tự động

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi cảnh báo qua các kênh khác
- **Lưu log**: Thêm node để lưu log hoạt động của workflow
- **Gửi báo cáo định kỳ**: Thiết lập lịch chạy workflow theo chu kỳ (hàng ngày, hàng tuần...)
- **Phân tích nâng cao**: Thêm các chỉ số phân tích phức tạp hơn như ROI, LTV...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình theo dõi hiệu suất kênh tiếp thị, từ lấy dữ liệu đến phân tích và báo cáo. Với việc tích hợp các công cụ phổ biến như HighLevel CRM, Google Sheets và Slack, các sếp có thể nhận được báo cáo chi tiết và chính xác mà không cần phải can thiệp thủ công. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!