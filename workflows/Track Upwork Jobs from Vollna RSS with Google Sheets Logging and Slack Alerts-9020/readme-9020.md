---
title: "🚀 Theo dõi công việc Upwork từ RSS Vollna với Google Sheets và cảnh báo Slack"
description: "Tự động hóa theo dõi công việc Upwork mới từ RSS Vollna, lưu trữ vào Google Sheets và gửi cảnh báo Slack - tiết kiệm thời gian và tránh bỏ lỡ cơ hội"
slug: "theo-doi-cong-viec-upwork-tu-rss-vollna-voi-google-sheets-va-slack"
tags: [n8n, automation, no-code, Upwork, Google Sheets, Slack]
keywords: [n8n workflow, tự động hóa công việc Upwork, theo dõi RSS, cảnh báo Slack, lưu trữ dữ liệu]
---

# 🚀 Theo dõi công việc Upwork từ RSS Vollna với Google Sheets và cảnh báo Slack

[Các sếp đang làm việc thủ công theo dõi công việc Upwork mới từ RSS Vollna? Hãy để n8n làm việc cho các sếp! Workflow này sẽ tự động hóa toàn bộ quy trình theo dõi, lọc, lưu trữ và thông báo công việc mới một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động theo dõi công việc mới mỗi 3 phút
- Tránh bỏ lỡ cơ hội: Nhận cảnh báo ngay khi có công việc mới phù hợp
- Dữ liệu được tổ chức: Lưu trữ thông tin chi tiết vào Google Sheets
- Hoạt động liên tục: Chạy 24/7 mà không cần can thiệp
- Thông báo đa kênh: Cảnh báo qua Slack và email (tùy chọn)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- Tài khoản Slack với quyền gửi tin nhắn vào kênh
- Tài khoản Gmail (tùy chọn cho email xác nhận)
- URL feed RSS của Upwork (hoặc Vollna)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9020](https://n8n.io/workflows/9020)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, chọn "Import from JSON" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Đặt thời gian chạy (mặc định mỗi 3 phút)
   - Kiểm tra lịch trình để đảm bảo không bị giới hạn API

2. **RSS Read**:
   - Thay đổi URL feed thành URL RSS của Upwork hoặc Vollna
   - Đảm bảo feed có định dạng chuẩn RSS

3. **Google Sheets**:
   - Tạo một Google Sheet mới và chia sẻ với tài khoản dịch vụ của bạn
   - Cấu hình node "Append row in sheet" với:
     - Spreadsheet ID: ID của Google Sheet của bạn
     - Sheet Name: Tên sheet cần ghi dữ liệu
     - Các cột dữ liệu: Title, Budget, Link, Posted, Date, Job Description, Skills, Categories

4. **Slack**:
   - Tạo một kênh Slack mới (ví dụ: #n8n-jobs)
   - Cấu hình node "Send a message" với:
     - Channel: Tên kênh Slack (ví dụ: #n8n-jobs)
     - Message: Tùy chỉnh nội dung thông báo

5. **Gmail (tùy chọn)**:
   - Cấu hình node "Send a message1" với:
     - To: Địa chỉ email nhận thông báo
     - Subject: Tiêu đề email
     - Body: Nội dung email

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối
2. Kích hoạt workflow bằng cách nhấn "Activate"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm bộ lọc nâng cao trong node "Check for foreign characters" để lọc theo từ khóa cụ thể
- Tạo một bảng điều khiển Google Data Studio để theo dõi số liệu công việc
- Kết nối với các công cụ phân tích khác như Google Analytics để theo dõi hiệu suất
- Thiết lập cảnh báo cho các công việc có mức giá cao hoặc các kỹ năng đặc biệt
- Tích hợp với các công cụ quản lý dự án để tự động tạo task khi có công việc mới

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi công việc Upwork mới. Bằng cách tự động hóa toàn bộ quy trình từ theo dõi đến thông báo, các sếp có thể tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!