---
title: "🚀 Tự động hóa kiểm tra email tiềm năng với Hunter.io và Google Sheets"
description: "Hướng dẫn tự động hóa kiểm tra email tiềm năng từ Google Sheets sử dụng Hunter.io, tiết kiệm thời gian và tăng độ chính xác cho chiến dịch marketing"
slug: "tu-dong-hoa-kiem-tra-email-tiem-nang-hunter-google-sheets"
tags: [n8n, automation, no-code, hunter.io, google-sheets]
keywords: [n8n workflow, tự động hóa, kiểm tra email, hunter.io, google sheets]
---

# 🚀 Tự động hóa kiểm tra email tiềm năng với Hunter.io và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình kiểm tra email thủ công
- Tăng độ chính xác của danh sách email tiềm năng lên tới 96%
- Tự động hóa toàn bộ quy trình kiểm tra email hàng ngày
- Dễ dàng tích hợp với các hệ thống marketing hiện tại
- Nhận được báo cáo chi tiết về trạng thái của từng email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- API Key từ Hunter.io (đăng ký tại [hunter.io](https://hunter.io/))
- Google Sheet chứa danh sách email cần kiểm tra (Sheet1)
- Google Sheet để lưu kết quả kiểm tra (Email Verifier → Sheet1)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6992](https://n8n.io/workflows/6992)
2. Nhấn nút "Download" để tải file JSON workflow
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **📥 Fetch Emails from Source Sheet (Node Google Sheets đầu tiên)**
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Điền tham số:
     - Spreadsheet ID: ID của Google Sheet chứa danh sách email cần kiểm tra
     - Sheet Name: `Sheet1`
     - Range: `A:D` (hoặc phạm vi chứa dữ liệu của bạn)

2. **🕵️‍♂️ Hunter.io Email Verifier (Node HTTP Request)**
   - Chọn credentials: `hunterIoApi` (hoặc tạo mới nếu chưa có)
   - Điền tham số:
     - URL: `https://api.hunter.io/v2/email-verifier`
     - Method: `GET`
     - Query Parameters:
       - `email`: `{{$node["📥 Fetch Emails from Source Sheet"].json["Email"]}}`
       - `api_key`: `{{$credentials.hunterIoApi.apiKey}}`

3. **📤 Write Results to Output Sheet (Node Google Sheets cuối cùng)**
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Điền tham số:
     - Spreadsheet ID: ID của Google Sheet để lưu kết quả
     - Sheet Name: `Email Verifier → Sheet1`
     - Operation: `appendOrUpdate`
     - Match Key: `Email`

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Node" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy hàng ngày theo lịch trình được thiết lập

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo kết quả kiểm tra hàng ngày
- Kết hợp với Slack để nhận thông báo khi có email không hợp lệ
- Tự động loại bỏ các email không hợp lệ khỏi danh sách gửi email marketing
- Thiết lập cảnh báo khi tỷ lệ email hợp lệ dưới ngưỡng mong muốn
- Tích hợp với các hệ thống CRM khác để cập nhật trạng thái email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình kiểm tra email tiềm năng, tiết kiệm thời gian đáng kể và tăng độ chính xác cho chiến dịch marketing. Với việc tích hợp Hunter.io và Google Sheets, các sếp có thể dễ dàng quản lý và theo dõi trạng thái của từng email trong danh sách tiềm năng.