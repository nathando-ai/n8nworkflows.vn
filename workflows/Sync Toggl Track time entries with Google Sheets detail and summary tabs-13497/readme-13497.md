---
title: "📊 Tự động đồng bộ dữ liệu Toggl Track với Google Sheets chi tiết và tóm tắt hàng tháng"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ dữ liệu thời gian làm việc từ Toggl Track sang Google Sheets với hai bảng chi tiết và tóm tắt hàng tháng"
slug: "tu-dong-dong-bo-toggl-track-google-sheets"
tags: [n8n, automation, no-code, toggl, google-sheets, time-tracking]
keywords: [n8n workflow, tự động hóa, quản lý thời gian, toggl, google sheets]
---

# 📊 Tự động đồng bộ dữ liệu Toggl Track với Google Sheets chi tiết và tóm tắt hàng tháng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường phải tốn nhiều thời gian để thủ công đồng bộ dữ liệu thời gian làm việc từ Toggl Track sang Google Sheets. Quá trình này bao gồm nhiều bước thủ công, dễ gây lỗi và không thể thực hiện tự động. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách dễ dàng và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đồng bộ dữ liệu thủ công
- Dữ liệu được cập nhật tự động hàng ngày với độ chính xác cao
- Dễ dàng theo dõi và phân tích thời gian làm việc thông qua Google Sheets
- Tự động tạo và quản lý các bảng chi tiết và tóm tắt hàng tháng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Toggl Track với quyền truy cập API
- Tài khoản Google với quyền truy cập Google Sheets API
- API Key và Credentials cho cả hai dịch vụ trên
- ID của hai Google Sheets (chi tiết và tóm tắt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp
2. Nhấp vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: https://n8n.io/workflows/13497
4. Nhấp vào nút "Import" để hoàn tất quá trình import

Hoặc các sếp cũng có thể tải xuống file JSON từ link trên và import thủ công qua nút "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần thực hiện các bước cấu hình sau:

1. **Cấu hình Toggl HTTP Basic Auth**:
   - Tạo một credential mới với loại "HTTP Basic Auth"
   - Nhập API Key của Toggl Track vào trường "Username"
   - Để trường "Password" trống
   - Lưu credential với tên phù hợp (ví dụ: "Toggl API")

2. **Cấu hình Google Sheets OAuth2**:
   - Tạo một credential mới với loại "Google Sheets OAuth2 API"
   - Nhập Client ID và Client Secret từ Google Cloud Console
   - Lưu credential với tên phù hợp (ví dụ: "Google Sheets API")

3. **Cấu hình node "Set Date Range"**:
   - Thiết lập giá trị cho biến `start_date` theo định dạng YYYY-MM-DD
   - Ví dụ: `2023-01-01`

4. **Cấu hình node "Process Data"**:
   - Thiết lập giá trị cho biến `PROJECT_NAME` với tên dự án cần theo dõi
   - Thiết lập giá trị cho biến `TIMEZONE` với múi giờ phù hợp (ví dụ: "Asia/Ho_Chi_Minh")

5. **Thay thế các placeholder**:
   - Thay thế `YOUR_DETAIL_SPREADSHEET_ID` bằng ID của Google Sheet chi tiết
   - Thay thế `YOUR_SUMMARY_SPREADSHEET_ID` bằng ID của Google Sheet tóm tắt

#### 3. Kích hoạt ⚡️
Sau khi hoàn thành các bước cấu hình, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Nhấp vào nút "Execute Workflow" để kiểm tra dữ liệu mẫu
2. Kiểm tra kết quả trên các node cuối cùng để đảm bảo dữ liệu được đồng bộ đúng cách
3. Nếu mọi thứ hoạt động tốt, nhấp vào nút "Activate" để kích hoạt workflow
4. Thiết lập lịch chạy tự động (nếu cần) thông qua tính năng "Schedule" của n8n

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo khi đồng bộ dữ liệu hoàn tất
- Để lưu log hoạt động, các sếp có thể thêm node "Write to File" sau các node cuối cùng
- Để gửi báo cáo định kỳ, các sếp có thể thêm node "Email" hoặc "Google Drive" để lưu trữ các file báo cáo
- Các sếp có thể mở rộng workflow này để đồng bộ dữ liệu với các hệ thống khác như Jira, Asana, hoặc các công cụ phân tích dữ liệu khác

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ dữ liệu thời gian làm việc từ Toggl Track sang Google Sheets một cách dễ dàng và chính xác. Với các bước cấu hình đơn giản và kết quả đáng tin cậy, workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể và nâng cao hiệu quả quản lý thời gian làm việc. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm việc của các sếp!