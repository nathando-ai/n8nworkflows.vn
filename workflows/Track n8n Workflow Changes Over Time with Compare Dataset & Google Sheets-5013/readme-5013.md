---
title: "🚀 Theo dõi thay đổi workflow n8n qua thời gian với Compare Dataset & Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi thay đổi workflow n8n hàng ngày, phát hiện sự khác biệt giữa các phiên bản và lưu kết quả vào Google Sheets"
slug: "theo-doi-thay-doi-workflow-n8n-qua-thoi-gian"
tags: [n8n, automation, no-code, google-sheets, workflow-management]
keywords: [n8n workflow, tự động hóa, theo dõi thay đổi, quản lý workflow, n8n automation]
---

# 🚀 Theo dõi thay đổi workflow n8n qua thời gian với Compare Dataset & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải theo dõi thủ công các thay đổi trong workflow n8n, đặc biệt khi làm việc trong môi trường nhiều người. Việc này tốn thời gian và dễ gây lỗi, đặc biệt khi cần phải kiểm tra hàng ngày. Workflow này sẽ giúp các sếp tự động hóa quá trình này, phát hiện sự khác biệt giữa các phiên bản workflow và lưu kết quả vào Google Sheets một cách tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình theo dõi thay đổi hàng ngày
- Chính xác: Phát hiện chính xác các thay đổi trong nodes và connections
- Cá nhân hóa: Theo dõi chỉ những workflow quan trọng với bạn
- Hoạt động liên tục: Chạy tự động mà không cần can thiệp
- Tích hợp: Lưu kết quả vào Google Sheets dễ dàng theo dõi và chia sẻ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n API (để truy cập danh sách workflow)
- Tài khoản Google Service Account (để truy cập Google Sheets API)
- Google Sheet đã tạo trước đó (có thể xem mẫu tại [đây](https://docs.google.com/spreadsheets/d/1dOHSfeE0W_qPyEWj5Zz0JBJm8Vrf_cWp-02OBrA_ZYc/edit?usp=sharing))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Click vào "Templates" ở menu trái
3. Click vào "Import from URL" và nhập URL: https://n8n.io/workflows/5013
4. Hoặc copy nội dung JSON từ [đây](https://n8n.io/workflows/5013) và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Schedule Trigger**:
   - Cấu hình thời gian chạy (mặc định là hàng ngày)
   - Thiết lập timezone phù hợp

2. **n8n API Credentials**:
   - Tạo mới credential cho n8n API
   - Nhập URL của n8n instance (ví dụ: http://localhost:5678)
   - Nhập API Key (có thể tạo mới trong n8n Settings > Credentials)

3. **Google Sheets Credentials**:
   - Tạo mới credential cho Google Sheets OAuth2 API
   - Cung cấp Service Account Email và Private Key từ Google Cloud Console
   - Thiết lập phạm vi (scopes) cần thiết: https://www.googleapis.com/auth/spreadsheets

4. **Get Row Node**:
   - Chỉnh sửa Spreadsheet ID (ID của Google Sheet bạn đã tạo)
   - Đặt tên Sheet Name (mặc định là "Sheet1")
   - Thiết lập Range (ví dụ: "A:D")

5. **Create New Entry Node**:
   - Cấu hình tương tự như Get Row Node
   - Đảm bảo Spreadsheet ID và Sheet Name trùng khớp

6. **Update Entry Node**:
   - Cấu hình tương tự như Get Row Node
   - Thiết lập Operation thành "Append or Update"

7. **Compare Datasets Nodes**:
   - Không cần cấu hình nhiều, chỉ cần đảm bảo các trường dữ liệu cần so sánh được truyền đúng

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chạy từng node một để kiểm tra dữ liệu đầu ra
   - Đặc biệt kiểm tra các node Compare Datasets để đảm bảo so sánh chính xác

2. Bật Active workflow:
   - Sau khi kiểm tra đầy đủ, bật workflow để chạy tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**:
   - Thêm node gửi thông báo vào Slack/Teams khi phát hiện thay đổi quan trọng
   - Có thể sử dụng node "Slack" hoặc "Microsoft Teams" để gửi thông báo

2. **Lưu log thay đổi**:
   - Thêm node lưu log thay đổi vào một Google Sheet khác để theo dõi lịch sử dài hạn

3. **Gửi báo cáo định kỳ**:
   - Thêm node gửi email báo cáo tổng hợp các thay đổi hàng tuần/tháng

4. **Theo dõi nhiều n8n instance**:
   - Sao chép workflow và cấu hình cho các n8n instance khác
   - Sử dụng cùng một Google Sheet để theo dõi tất cả các instance

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc theo dõi thay đổi workflow n8n một cách tự động và hiệu quả. Bằng cách tích hợp với Google Sheets, các sếp có thể dễ dàng xem và quản lý các thay đổi xảy ra trong hệ thống n8n của mình. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu rủi ro khi làm việc với nhiều workflow trong n8n!