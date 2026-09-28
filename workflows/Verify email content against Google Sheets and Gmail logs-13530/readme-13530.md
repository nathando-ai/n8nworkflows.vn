---
title: "🚀 Tự động hóa kiểm tra nội dung email với Google Sheets và Gmail"
description: "Hướng dẫn tự động so sánh nội dung email với dữ liệu mẫu trong Google Sheets để đảm bảo chất lượng nội dung email marketing"
slug: "tu-dong-hoa-kiem-tra-noi-dung-email-voi-google-sheets-va-gmail"
tags: [n8n, automation, no-code, email-marketing, google-sheets]
keywords: [n8n workflow, tự động hóa email, kiểm tra nội dung email, google sheets, email marketing]
---

# 🚀 Tự động hóa kiểm tra nội dung email với Google Sheets và Gmail

[Các sếp marketing] thường gặp khó khăn khi phải kiểm tra thủ công nội dung email trước khi gửi. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình kiểm tra nội dung email bằng cách so sánh với dữ liệu mẫu trong Google Sheets, giúp đảm bảo chất lượng nội dung email marketing một cách hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian kiểm tra nội dung email từ 70% đến 90%
- Đảm bảo tính nhất quán và chính xác của nội dung email
- Giảm thiểu lỗi do kiểm tra thủ công
- Tự động hóa toàn bộ quá trình kiểm tra nội dung email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để truy cập Google Sheets và Gmail)
- Dữ liệu mẫu nội dung email trong Google Sheets
- Quyền truy cập vào email marketing của công ty
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/13530](https://n8n.io/workflows/13530)
2. Click vào nút "Import" để tải xuống file JSON của workflow
3. Trong n8n Editor, click vào nút "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get many messages"**:
   - Chọn credentials "gmailOAuth2" đã được cấu hình
   - Đảm bảo tài khoản Gmail có quyền truy cập vào email marketing

2. **Node "Load Expected Content"**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được cấu hình
   - Cập nhật tham số "spreadsheetId" với ID của Google Sheets chứa dữ liệu mẫu nội dung email
   - Đảm bảo cột dữ liệu trong Google Sheets khớp với cấu trúc dữ liệu trong workflow

3. **Node "Log Content Checks to Excel"**:
   - Chọn credentials "googleSheetsOAuth2Api" đã được cấu hình
   - Cập nhật tham số "spreadsheetId" với ID của Google Sheets để lưu kết quả kiểm tra
   - Đảm bảo cột dữ liệu trong Google Sheets khớp với cấu trúc dữ liệu trong workflow

4. **Node "Extracting Preheader From HTML"**:
   - Cập nhật logic trích xuất nội dung HTML để phù hợp với cấu trúc email của công ty

5. **Node "Extract Actual Content and Results"**:
   - Cập nhật logic so sánh nội dung email với dữ liệu mẫu trong Google Sheets

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để kiểm tra workflow
2. Đảm bảo workflow chạy thành công và kết quả được lưu vào Google Sheets
3. Bật Active workflow để tự động hóa quá trình kiểm tra nội dung email

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có lỗi trong quá trình kiểm tra nội dung email
- Lưu log kiểm tra nội dung email để theo dõi lịch sử kiểm tra
- Gửi báo cáo kiểm tra nội dung email định kỳ qua email hoặc Slack

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa toàn bộ quá trình kiểm tra nội dung email, đảm bảo chất lượng nội dung email marketing một cách hiệu quả. Các sếp chỉ cần cấu hình các thông số cần thiết và kích hoạt workflow, hệ thống sẽ tự động thực hiện quá trình kiểm tra nội dung email và lưu kết quả vào Google Sheets.