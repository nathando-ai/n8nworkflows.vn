---
title: "🚨 Tự động ghi log lỗi và cảnh báo với Google Sheets & Gmail"
description: "Hướng dẫn chi tiết cách tự động ghi log lỗi vào Google Sheets và gửi cảnh báo qua Gmail khi workflow n8n gặp sự cố"
slug: "tu-dong-ghi-log-loi-va-canh-bao-voi-google-sheets-gmail"
tags: [n8n, automation, no-code, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa, ghi log lỗi, cảnh báo lỗi, google sheets, gmail]
---

# 🚨 Tự động ghi log lỗi và cảnh báo với Google Sheets & Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý lỗi workflow thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động ghi log lỗi vào Google Sheets với đầy đủ thông tin chi tiết
- Nhận cảnh báo tức thì qua email khi workflow gặp sự cố
- Tiết kiệm thời gian quản lý lỗi thủ công
- Dễ dàng theo dõi và phân tích lỗi qua Google Sheets
- Có thể tùy chỉnh nội dung cảnh báo theo nhu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets và Gmail
- Google Sheets OAuth2 API Credential
- Gmail OAuth2 Credential
- Bản sao của [Google Sheets template](https://docs.google.com/spreadsheets/d/11-vLBAKolEvaL0qQDjckHmvC1S6_hxHbgSP8CLyngSs/edit?gid=0#gid=0)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7876
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Error Trigger**:
   - Node này sẽ tự động kích hoạt khi bất kỳ workflow nào trong n8n của bạn gặp lỗi
   - Không cần cấu hình thêm

2. **Google Sheets - Create Error Log**:
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Cập nhật **Spreadsheet ID** của bạn (tìm trong URL của Google Sheets)
   - Đảm bảo bảng tính của bạn có cấu trúc giống như template
   - Tham số `operation` đã được thiết lập là `append` (thêm dữ liệu mới)

3. **Gmail - Send Notification**:
   - Chọn credentials: `gmailOAuth2`
   - Cập nhật địa chỉ email nhận cảnh báo (thay thế `n8n_log_template@yopmail.com`)
   - Tùy chỉnh tiêu đề và nội dung email theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra Google Sheets để xác nhận dữ liệu đã được ghi đúng
3. Kiểm tra hộp thư email để xác nhận nhận được cảnh báo
4. Sau khi test thành công, nhấn "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận cảnh báo cùng lúc với email
- Tạo một workflow phụ để gửi báo cáo hàng ngày về các lỗi đã xảy ra
- Thiết lập các quy tắc lọc trong Google Sheets để phân loại lỗi theo mức độ nghiêm trọng
- Kết hợp với các công cụ giám sát khác như UptimeRobot để có cái nhìn toàn diện về hệ thống

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình ghi log lỗi và cảnh báo, giảm thiểu thời gian phản hồi khi hệ thống gặp sự cố. Bằng cách tích hợp Google Sheets và Gmail, bạn có thể dễ dàng theo dõi và quản lý lỗi một cách hiệu quả. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!