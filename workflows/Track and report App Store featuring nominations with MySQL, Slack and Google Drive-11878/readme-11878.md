---
title: "🚀 Tự động hóa theo dõi và báo cáo đề cử App Store với MySQL, Slack và Google Drive"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình theo dõi và báo cáo đề cử ứng dụng trên App Store bằng n8n, MySQL, Slack và Google Drive"
slug: "tu-dong-hoa-theo-doi-de-cuu-app-store"
tags: [n8n, automation, no-code, app-store, mysql, slack, google-drive]
keywords: [n8n workflow, tự động hóa, app store, đề cử ứng dụng, báo cáo tự động]
---

# 🚀 Tự động hóa theo dõi và báo cáo đề cử App Store với MySQL, Slack và Google Drive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi theo dõi thủ công đề cử ứng dụng trên App Store. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian theo dõi thủ công
- Dữ liệu đề cử ứng dụng được lưu trữ và cập nhật tự động trong MySQL
- Báo cáo tự động được chia sẻ qua Slack và Google Drive
- Theo dõi trạng thái đề cử một cách dễ dàng
- Hoạt động liên tục theo lịch trình hàng tuần
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apple Developer với quyền truy cập App Store Connect API
- MySQL database đã được thiết lập
- (Tùy chọn) Tài khoản Google Drive và Slack để chia sẻ báo cáo tự động
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11878)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **JWT Auth** (Node: "App Store Connect API authentication")
   - Chọn credentials "jwtAuth"
   - Cấu hình các tham số:
     - Issuer ID: ID nhà phát hành từ Apple Developer
     - Key ID: ID khóa từ Apple Developer
     - Private Key: Khóa riêng từ Apple Developer

2. **MySQL Nodes** (Nodes: "Store applications in MySQL", "Store nominations in MySQL", "Generate the report with a query")
   - Chọn credentials "mySql"
   - Cấu hình kết nối MySQL với thông tin server, database, username và password
   - Đảm bảo các bảng `applications` và `nominations` đã được tạo với cấu trúc như trong ghi chú

3. **Google Drive** (Node: "Upload file")
   - Chọn credentials "googleApi"
   - Chọn thư mục đích trong Google Drive để lưu báo cáo

4. **Slack** (Node: "Upload a file")
   - Chọn credentials "slackApi"
   - Chọn kênh Slack để chia sẻ báo cáo

5. **Schedule Trigger** (Node: "Weekly Trigger")
   - Cấu hình lịch chạy hàng tuần (ví dụ: mỗi thứ Hai lúc 9:00 AM)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách kích hoạt workflow thủ công
2. Kiểm tra dữ liệu trong MySQL và báo cáo được tạo
3. Bật Active workflow để chạy theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để thông báo khi có đề cử mới được chấp nhận
- Tạo báo cáo định kỳ hàng tháng với dữ liệu tổng hợp
- Kết hợp với workflow khác để tự động gửi email báo cáo
- Thêm node để lưu log hoạt động của workflow

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và công sức trong việc theo dõi và báo cáo đề cử ứng dụng trên App Store. Bằng cách tự động hóa toàn bộ quá trình, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quản lý ứng dụng. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!