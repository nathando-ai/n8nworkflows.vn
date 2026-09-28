---
title: "🎙️ Tự động chuyển đổi âm thanh thành văn bản từ Cloud Storage với n8n"
description: "Hướng dẫn tự động hóa chuyển đổi âm thanh thành văn bản từ Google Drive/AWS S3 sang Google Sheets bằng n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-chuyen-doi-am-thanh-thanh-van-ban-voi-n8n"
tags: [n8n, automation, no-code, aws, google-drive]
keywords: [n8n workflow, tự động hóa âm thanh, chuyển đổi âm thanh, AWS Transcribe, Google Sheets]
---

# 🎙️ Tự động chuyển đổi âm thanh thành văn bản từ Cloud Storage với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải đối mặt với hàng loạt file âm thanh cần chuyển đổi thành văn bản để xử lý, phân tích hoặc lưu trữ. Việc làm thủ công này tốn thời gian, dễ gây lỗi và không hiệu quả. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ khi file âm thanh được tải lên Cloud Storage đến khi văn bản được lưu vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi âm thanh thành văn bản với độ chính xác cao
- Tiết kiệm thời gian xử lý hàng loạt file âm thanh
- Dữ liệu văn bản được lưu trữ và quản lý tập trung trong Google Sheets
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Giảm thiểu lỗi do làm việc thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AWS với dịch vụ Transcribe và S3
- Tài khoản Google với quyền truy cập Google Drive và Google Sheets
- File âm thanh đã được tải lên Google Drive hoặc AWS S3
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/1394)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Drive Trigger1**:
   - Chọn credentials Google Drive OAuth2 API
   - Cấu hình các tham số:
     - Folder ID: ID của thư mục chứa file âm thanh
     - File Type: Chọn "Audio" để chỉ theo dõi file âm thanh

2. **AWS S3 2**:
   - Chọn credentials AWS
   - Cấu hình các tham số:
     - Bucket Name: Tên bucket chứa file âm thanh
     - Prefix: (Tùy chọn) Thư mục con trong bucket

3. **AWS Transcribe 1**:
   - Chọn credentials AWS
   - Cấu hình các tham số:
     - Language Code: Chọn ngôn ngữ của file âm thanh
     - Media Format: Định dạng file âm thanh (mp3, wav, vv.)

4. **AWS Transcribe 2**:
   - Chọn credentials AWS
   - Cấu hình các tham số:
     - Operation: Chọn "get" để lấy kết quả chuyển đổi

5. **Google Sheets**:
   - Chọn credentials Google Sheets OAuth2 API
   - Cấu hình các tham số:
     - Spreadsheet ID: ID của Google Sheet nhận kết quả
     - Sheet Name: Tên sheet trong Google Sheet
     - Operation: Chọn "append" để thêm dữ liệu mới

#### 3. Kích hoạt ⚡️
1. Test run workflow với một file âm thanh mẫu
2. Kiểm tra kết quả trong Google Sheet đã chỉ định
3. Nếu mọi thứ hoạt động tốt, bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý hàng loạt file**: Workflow này có thể được mở rộng để xử lý hàng loạt file âm thanh cùng một lúc bằng cách sử dụng node "Loop Over Items"
2. **Thông báo kết quả**: Kết hợp với node Slack/Telegram để nhận thông báo khi quá trình chuyển đổi hoàn thành
3. **Lưu trữ log**: Thêm node để lưu log các file đã được xử lý để tránh xử lý trùng lặp
4. **Xử lý lỗi**: Thêm node xử lý lỗi để gửi thông báo khi có file không thể chuyển đổi

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình chuyển đổi âm thanh thành văn bản từ Cloud Storage, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để tối ưu hóa quy trình xử lý dữ liệu âm thanh của doanh nghiệp!