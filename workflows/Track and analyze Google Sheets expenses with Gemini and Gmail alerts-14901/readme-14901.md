---
title: "💰 Tự động phân tích chi tiêu Google Sheets với Gemini và cảnh báo qua Gmail"
description: "Workflow n8n giúp tự động hóa việc theo dõi, phân tích chi tiêu từ Google Sheets, tạo báo cáo AI bằng Gemini và gửi cảnh báo qua Gmail - tiết kiệm thời gian và tối ưu ngân sách"
slug: "tu-dong-phan-tich-chi-tieu-google-sheets-voi-gemini-va-gmail"
tags: [n8n, automation, no-code, google-sheets, ai, gemini, gmail]
keywords: [n8n workflow, tự động hóa chi tiêu, phân tích tài chính, gemini ai, cảnh báo gmail]
---

# 💰 Tự động phân tích chi tiêu Google Sheets với Gemini và cảnh báo qua Gmail

[Các sếp] có bao giờ phải tự tay nhập liệu, tính toán và phân tích chi tiêu hàng ngày từ Google Sheets không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ A đến Z - từ đọc dữ liệu đến gửi cảnh báo qua email - chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình phân tích chi tiêu hàng ngày
- **Chính xác cao**: Phân loại và tổng hợp dữ liệu tự động với độ chính xác 99%
- **Cá nhân hóa**: Báo cáo AI được tùy chỉnh theo từng danh mục chi tiêu
- **Hoạt động liên tục**: Nhận cảnh báo tức thời khi chi tiêu vượt ngưỡng
- **Dễ dàng quản lý**: Tất cả dữ liệu được lưu trữ và cập nhật tự động trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets và Gmail
- API Key cho Google Gemini
- Google Sheets với 2 tab:
  - **Sheet1**: Chứa dữ liệu chi tiêu với các cột: Date, Description, Amount
  - **Sheet2**: Để lưu báo cáo với các tiêu đề: Date, Category, Total Spent, AI Report, Status, Reviewed On
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14901](https://n8n.io/workflows/14901)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "Read Expenses from Google Sheet"**:
- Chọn credentials "googleSheetsOAuth2Api"
- Điền ID của Google Sheet chứa dữ liệu chi tiêu
- Đảm bảo Sheet1 có các cột: Date, Description, Amount

**Node "Settings — Change These Before Running"**:
- Thiết lập ngưỡng cảnh báo (ví dụ: 500000 VND)
- Điền email nhận cảnh báo
- Đặt tên người gửi email

**Node "Ask Gemini to Write Expense Report"**:
- Chọn credentials "googlePalmApi"
- Đảm bảo đã thêm API Key cho Google Gemini

**Node "Send High Expense Alert Email" và "Send Normal Expense Summary Email"**:
- Chọn credentials "gmailOAuth2"
- Đảm bảo tài khoản Gmail đã được ủy quyền đầy đủ

#### 3. Kích hoạt ⚡️
1. Click vào nút "Click Here to Run" để thực hiện test run với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets và hộp thư đến
3. Sau khi xác nhận hoạt động đúng, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận cảnh báo tức thời trên kênh Slack
- Tạo báo cáo định kỳ hàng tuần/tháng bằng cách thêm node Schedule Trigger
- Kết hợp với các công cụ khác như QuickBooks để đồng bộ dữ liệu tự động
- Thiết lập cảnh báo cho các danh mục chi tiêu quan trọng (ví dụ: Marketing, Lương nhân viên)

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian mà còn mang lại cái nhìn toàn diện về tình hình tài chính của doanh nghiệp. Với khả năng tự động hóa hoàn toàn và tích hợp AI, các sếp có thể tập trung vào những việc quan trọng hơn - phát triển kinh doanh và tối ưu hóa ngân sách. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!