---
title: "🚀 Tự động đồng bộ dữ liệu công ty từ Google Sheets sang Salesforce với hệ thống phòng tránh trùng lặp thông minh"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu công ty từ Google Sheets sang Salesforce với hệ thống phòng tránh trùng lặp thông minh, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-du-lieu-cong-ty-tu-google-sheets-sang-salesforce"
tags: [n8n, automation, no-code, salesforce, google-sheets]
keywords: [n8n workflow, tự động hóa, salesforce, google sheets, đồng bộ dữ liệu]
---

# 🚀 Tự động đồng bộ dữ liệu công ty từ Google Sheets sang Salesforce với hệ thống phòng tránh trùng lặp thông minh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải nhập liệu thủ công giữa Google Sheets và Salesforce. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nhập liệu thủ công (từ 15-45 giây/cong ty)
- Giảm lỗi nhập liệu do thủ công
- Đồng bộ dữ liệu liên tục giữa Google Sheets và Salesforce
- Phòng tránh trùng lặp dữ liệu thông minh
- Quản lý liên hệ công ty một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets chứa dữ liệu công ty (Tên công ty, Email, Điện thoại, Ngành nghề, v.v.)
- Credentials Google Sheets API (Xác thực OAuth 2.0 đã cấu hình trong n8n)
- Quyền truy cập API Salesforce (Connected App với quyền tạo/đọc tài khoản và liên hệ)
- Kiến thức về ánh xạ trường Salesforce (hiểu biết về các trường bắt buộc và tùy chọn cho Tài khoản/Liên hệ)
- Instance n8n (cloud hoặc self-hosted với HTTPS)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9053)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from file" và chọn file JSON vừa tải về

Hoặc bạn có thể copy/paste JSON workflow vào n8n Editor bằng cách:
1. Click vào "Import from JSON" trong n8n Editor
2. Dán nội dung JSON workflow vào hộp thoại xuất hiện

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get row(s) in sheet"**:
   - Chọn credentials Google Sheets OAuth 2.0 đã cấu hình
   - Điền thông tin Sheet ID và tên sheet chứa dữ liệu công ty
   - Cấu hình các cột dữ liệu cần lấy (Company Name, Email, Phone, Industry, v.v.)

2. **Node "Search Salesforce accounts"**:
   - Chọn credentials Salesforce đã cấu hình
   - Đảm bảo trường tìm kiếm (SOQL query) được cấu hình đúng để tìm kiếm tài khoản hiện có

3. **Node "Create Salesforce account"**:
   - Kiểm tra và cấu hình các trường bắt buộc cho Tài khoản Salesforce
   - Đảm bảo ánh xạ dữ liệu từ Google Sheets sang các trường Salesforce chính xác

4. **Node "Create Salesforce contact"**:
   - Cấu hình các trường bắt buộc cho Liên hệ Salesforce
   - Đảm bảo ánh xạ dữ liệu liên hệ từ Google Sheets sang các trường Salesforce chính xác

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chuẩn bị 1-2 dòng dữ liệu mẫu trong Google Sheets
   - Chạy workflow với dữ liệu mẫu và kiểm tra kết quả trong Salesforce
2. Bật Active workflow:
   - Sau khi test thành công, click vào nút "Active" để kích hoạt workflow
   - Cấu hình lịch chạy (nếu cần) trong phần "Settings" của workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý dữ liệu lớn**:
   - Thêm node "Delay" giữa các bước để tránh vượt quá giới hạn API
   - Xử lý dữ liệu theo batch (25-50 công ty/lần chạy)

2. **Báo cáo và theo dõi**:
   - Thêm node gửi email báo cáo kết quả sau mỗi lần chạy
   - Cấu hình gửi thông báo Slack/Teams khi có lỗi xảy ra

3. **Tích hợp thêm dữ liệu**:
   - Kết nối với các nguồn dữ liệu khác (LinkedIn, CRM khác) để bổ sung thông tin công ty
   - Thêm bước xử lý dữ liệu trước khi đồng bộ (xử lý tên công ty, chuẩn hóa số điện thoại...)

4. **Backup dữ liệu**:
   - Thêm bước backup dữ liệu Salesforce trước khi thực hiện các thay đổi lớn
   - Lưu trữ bản sao dữ liệu Google Sheets trước khi chạy workflow

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc đồng bộ dữ liệu công ty giữa Google Sheets và Salesforce với hệ thống phòng tránh trùng lặp thông minh. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian đáng kể, giảm lỗi nhập liệu và duy trì dữ liệu đồng bộ liên tục giữa hai hệ thống quan trọng này. Hãy thử nghiệm với dữ liệu mẫu trước khi triển khai đầy đủ và theo dõi kết quả để tối ưu hóa quy trình của bạn.