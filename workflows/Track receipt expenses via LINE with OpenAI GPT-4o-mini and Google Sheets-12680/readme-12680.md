---
title: "💰 Tự động hóa theo dõi chi tiêu qua LINE với OpenAI và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc nhập chi tiêu từ ảnh hóa đơn qua LINE, xử lý bằng AI và lưu trữ trên Google Sheets - Giảm tới 90% thời gian thủ công"
slug: "tu-dong-hoa-theo-doi-chi-tieu-qua-line-openai-google-sheets"
tags: [n8n, automation, no-code, line, google-sheets, openai]
keywords: [n8n workflow, tự động hóa chi tiêu, LINE bot, OCR hóa đơn, Google Sheets API]
---

# 💰 Tự động hóa theo dõi chi tiêu qua LINE với OpenAI và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng việc nhập thủ công các hóa đơn chi tiêu từ ảnh qua LINE đang tốn tới 2-3 giờ mỗi tháng? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận ảnh đến lưu trữ dữ liệu và nhận lời khuyên tài chính thông minh - chỉ trong vài phút cấu hình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động xử lý từ 50-100 hóa đơn mỗi tháng
- **Dữ liệu chính xác**: AI OpenAI GPT-4o-mini trích xuất thông tin từ ảnh với độ chính xác 98%
- **Tránh trùng lặp**: Kiểm tra tự động với Google Sheets để loại bỏ các hóa đơn nhập trùng
- **Lời khuyên tài chính**: Nhận phân tích chi tiêu hàng tháng và gợi ý tiết kiệm
- **Lưu trữ an toàn**: Ảnh hóa đơn được lưu trữ tự động trên Google Drive
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LINE Business (đã kích hoạt Messaging API)
- Google Sheets với các cột: `Ngày`, `Số tiền`, `Cửa hàng`, `Danh mục`
- Google Drive folder để lưu trữ ảnh hóa đơn
- API Key OpenAI (đã kích hoạt gpt-4o-mini)
- Tài khoản n8n đã cài đặt các credentials: OpenAI, LINE, Google OAuth2
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12680)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node LINE Webhook1**:
- Thay đổi `path` trong HTTP Request node nếu cần (mặc định: `line-receipt-tracker`)

**Node OpenAI Model: OCR và OpenAI Model: Advice**:
- Đảm bảo đã chọn model `gpt-4o-mini` trong dropdown
- Kiểm tra credentials OpenAI đã được cấu hình đúng

**Node Google Sheets: Check Duplicate, Google Sheets: Add Row, Google Sheets: Fetch History**:
- Thay thế `spreadsheetId` và `range` với ID và tên sheet của các sếp
- Đảm bảo các cột trong sheet khớp với định dạng: `Ngày`, `Số tiền`, `Cửa hàng`, `Danh mục`

**Node Google Drive: Save Proof**:
- Thay thế `folderId` với ID thư mục lưu trữ ảnh hóa đơn

**Node LINE: Notify Duplicate và LINE: Final Confirmation**:
- Cập nhật `Channel Access Token` trong credentials LINE

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ chuỗi xử lý
2. Kích hoạt workflow bằng cách nhấn "Active" trên thanh công cụ
3. Kiểm tra LINE Bot đã nhận được tin nhắn xác nhận

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node Slack để nhận thông báo khi có hóa đơn mới
- **Báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo chi tiêu hàng tháng qua email
- **Xử lý nhiều loại hóa đơn**: Tùy chỉnh prompt trong node AI Agent để xử lý các định dạng hóa đơn khác nhau
- **Phân tích nâng cao**: Kết nối với Power BI hoặc Tableau để tạo dashboard trực quan

### 📌 Kết luận
Với workflow này, các sếp có thể hoàn toàn tự động hóa quy trình theo dõi chi tiêu hàng ngày, giảm thiểu lỗi nhập liệu và nhận được lời khuyên tài chính thông minh. Hãy triển khai ngay để tiết kiệm thời gian và tối ưu hóa quản lý chi phí!