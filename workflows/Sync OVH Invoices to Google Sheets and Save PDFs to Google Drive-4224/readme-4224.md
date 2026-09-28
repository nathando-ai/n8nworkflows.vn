---
title: "📄 Tự động hóa hóa đơn OVH: Lưu vào Google Sheets & Google Drive"
description: "Hướng dẫn chi tiết cách tự động đồng bộ hóa đơn OVH sang Google Sheets và lưu PDF vào Google Drive theo năm. Tiết kiệm thời gian và quản lý tài chính hiệu quả."
slug: "tu-dong-hoa-hoa-don-ovh-google-sheets-drive"
tags: [n8n, automation, no-code, google-sheets, google-drive, finance]
keywords: [n8n workflow, tự động hóa hóa đơn, OVH, Google Sheets, Google Drive]
---

# 📄 Tự động hóa hóa đơn OVH: Lưu vào Google Sheets & Google Drive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ hóa đơn từ OVH sang Google Sheets trong vòng 1 phút mỗi ngày.
- Lưu trữ PDF hóa đơn theo năm trong Google Drive để quản lý dễ dàng.
- Tiết kiệm thời gian và tránh lỗi thủ công khi xử lý hàng loạt hóa đơn.
- Tự động tạo thư mục theo năm để tổ chức hóa đơn một cách có hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OVH với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets và Google Drive.
- Google Sheet mẫu đã được sao chép từ [template này](https://docs.google.com/spreadsheets/d/1NDQVUayKCUktwhDfgdyueW15JPeQZl_oExO_4O5GV-I/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4224](https://n8n.io/workflows/4224) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy/paste nội dung JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Query Latest OVH Invoices"**:
   - Cấu hình credentials cho HTTP Header Auth với token OVH.
   - Điều chỉnh tham số thời gian truy vấn trong phần "Query String Parameters" để lấy hóa đơn trong khoảng thời gian mong muốn.

2. **Node "Get Invoice Data"**:
   - Cấu hình credentials cho HTTP Header Auth với token OVH.
   - Đảm bảo URL API đúng với endpoint của OVH.

3. **Node "Record in OVH Sheet"**:
   - Cấu hình credentials cho Google Sheets OAuth2 API.
   - Điền thông tin Spreadsheet ID từ Google Sheet mẫu đã sao chép.
   - Đảm bảo tên sheet và cột dữ liệu phù hợp với template.

4. **Node "Safe File" và "Create Folder"**:
   - Cấu hình credentials cho Google Drive OAuth2 API.
   - Đảm bảo thư mục gốc trong Google Drive có quyền truy cập đầy đủ.

5. **Node "Check for FY Folder ID"**:
   - Cấu hình credentials cho Google Drive OAuth2 API.
   - Đảm bảo tên thư mục theo năm được cấu hình đúng.

#### 3. Kích hoạt ⚡️
1. Nhấn "Test workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn "Activate workflow" để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy workflow hàng ngày để tự động cập nhật hóa đơn mới.
- Kết hợp với Slack/Telegram để nhận thông báo khi có hóa đơn mới.
- Lưu log hoạt động của workflow để theo dõi và giải quyết vấn đề nếu có.
- Tạo báo cáo định kỳ từ dữ liệu trong Google Sheets để phân tích tài chính.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và tránh lỗi thủ công khi xử lý hàng loạt hóa đơn từ OVH. Bằng cách tự động đồng bộ hóa đơn sang Google Sheets và lưu trữ PDF vào Google Drive theo năm, các sếp có thể quản lý tài chính một cách hiệu quả và có hệ thống. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!