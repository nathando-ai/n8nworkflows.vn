---
title: "🚀 Tự động gửi email với trích dẫn và joke lập trình hàng ngày"
description: "Hướng dẫn tự động hóa gửi email hàng ngày với trích dẫn cảm hứng và joke lập trình bằng n8n, tiết kiệm thời gian và nâng cao tinh thần làm việc"
slug: "tu-dong-gui-email-trich-dan-joke-lap-trinh-hang-ngay"
tags: [n8n, automation, no-code, email, gmail]
keywords: [n8n workflow, tự động hóa email, trích dẫn cảm hứng, joke lập trình]
---

# 🚀 Tự động gửi email với trích dẫn và joke lập trình hàng ngày

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi email hàng ngày mà không cần can thiệp thủ công
- Nâng cao tinh thần làm việc: Nhận được trích dẫn cảm hứng và joke lập trình hàng ngày
- Cá nhân hóa nội dung: Email được tùy chỉnh với thông tin cá nhân của từng người nhận
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API (cần bật Gmail API trong Google Cloud Console)
- API key hoặc OAuth credentials để kết nối với Gmail
- Danh sách email người nhận (có thể lưu trong Google Sheets hoặc file CSV)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Click vào "Import from URL" trong menu Workflows
3. Dán link sau vào ô nhập: `https://n8n.io/workflows/9373`
4. Click "Import" để hoàn tất

Hoặc bạn có thể:
1. Truy cập link gốc: [Workflow trên n8n.io](https://n8n.io/workflows/9373)
2. Click vào nút "Copy JSON" để sao chép cấu hình
3. Trong n8n Editor, click "Import from JSON" và dán nội dung đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule me here" (Schedule Trigger)**:
   - Double-click vào node này
   - Thiết lập thời gian gửi email hàng ngày (ví dụ: 8:00 AM mỗi ngày)
   - Click "Update" để lưu thay đổi

2. **Node "Connect your Gmail" (Gmail)**:
   - Click vào node này
   - Trong phần "Credentials", chọn hoặc tạo mới Gmail OAuth2 credentials
   - Đảm bảo tài khoản Gmail đã được ủy quyền đầy đủ
   - Trong phần "Options", thiết lập:
     - To: Địa chỉ email người nhận (hoặc sử dụng biến nếu có nhiều người nhận)
     - Subject: Tiêu đề email (ví dụ: "Trích dẫn và joke hàng ngày")
     - Body: Nội dung email (có thể sử dụng các biến từ các node trước đó)

3. **Node "Get quote" và "Programming joke" (HTTP Request)**:
   - Các node này đã được cấu hình sẵn để lấy trích dẫn và joke từ các API công khai
   - Không cần thay đổi gì nếu muốn sử dụng các nguồn dữ liệu mặc định

4. **Node "Results" và "Map the fields" (Set)**:
   - Các node này được sử dụng để định dạng và kết hợp dữ liệu từ các node trước đó
   - Có thể chỉnh sửa các trường dữ liệu nếu muốn thay đổi định dạng email

#### 3. Kích hoạt ⚡️
1. Để test workflow:
   - Click vào node "Schedule me here"
   - Click "Execute workflow" để chạy thử
   - Kiểm tra email của bạn để xem kết quả

2. Để kích hoạt workflow:
   - Đảm bảo tất cả các node đã được cấu hình đúng
   - Click vào node "Schedule me here"
   - Click "Activate" để bật workflow
   - Workflow sẽ tự động chạy theo lịch trình đã thiết lập

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung email**:
   - Thêm các trường dữ liệu khác vào email (ví dụ: thời tiết, tin tức hàng ngày)
   - Sử dụng các node khác như Google Sheets để lưu trữ và quản lý danh sách email

2. **Thêm thông báo Slack/Teams**:
   - Kết nối với Slack hoặc Microsoft Teams để nhận thông báo khi email được gửi
   - Sử dụng node "Slack" hoặc "Microsoft Teams" để gửi thông báo

3. **Lưu log hoạt động**:
   - Thêm node "Google Sheets" để lưu log các email đã gửi
   - Giúp theo dõi lịch sử gửi email và quản lý dữ liệu

4. **Tự động hóa nâng cao**:
   - Kết nối với các dịch vụ khác như Trello, Asana để tạo task từ các trích dẫn/joke
   - Sử dụng node "Webhook" để tích hợp với các hệ thống khác

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc gửi email hàng ngày với nội dung động và cá nhân hóa. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào công việc quan trọng hơn và nâng cao tinh thần làm việc cho đội nhóm. Hãy thử áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!