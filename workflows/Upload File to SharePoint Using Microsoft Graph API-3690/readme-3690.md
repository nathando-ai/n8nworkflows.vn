---
title: "🚀 Tự động Upload File lên SharePoint bằng Microsoft Graph API - Hướng dẫn chi tiết cho n8n"
description: "Hướng dẫn tự động hóa upload file lên SharePoint bằng Microsoft Graph API trong n8n. Giải pháp hoàn hảo cho các sếp quản lý tài liệu, tự động hóa quy trình làm việc và tiết kiệm thời gian."
slug: "tu-dong-upload-file-len-sharepoint-bang-microsoft-graph-api"
tags: [n8n, automation, no-code, sharepoint, microsoft-graph-api]
keywords: [n8n workflow, tự động hóa, sharepoint, microsoft graph api, upload file]
---

# 🚀 Tự động Upload File lên SharePoint bằng Microsoft Graph API - Hướng dẫn chi tiết cho n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa quy trình upload file lên SharePoint
- Tiết kiệm thời gian và công sức cho các sếp quản lý tài liệu
- Đảm bảo tính chính xác và nhất quán trong quá trình upload
- Tích hợp dễ dàng với các hệ thống khác thông qua API
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập SharePoint
- Application user đã được tạo (theo hướng dẫn [tại đây](https://learn.microsoft.com/en-us/power-platform/admin/manage-application-users))
- Các quyền sau đã được thiết lập:
  - Sites.ReadWrite.All - để truy cập SharePoint site
  - Files.ReadWrite.All - để thực hiện upload file
- Thông tin xác thực bao gồm:
  - TENANT_ID
  - CLIENT_ID
  - CLIENT_SECRET
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/3690](https://n8n.io/workflows/3690)
3. Hoặc bạn có thể tải file JSON về và import thủ công qua nút "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Authentication** (Node HTTP Request):
   - Thiết lập các tham số xác thực:
     - TENANT_ID: ID của tenant Microsoft 365 của bạn
     - CLIENT_ID: ID của ứng dụng đã đăng ký
     - CLIENT_SECRET: Secret của ứng dụng đã đăng ký
   - Đảm bảo các quyền đã được cấp theo hướng dẫn trong phần Yêu cầu cần thiết

2. **Set config (sensitive data)** (Node Set):
   - Thiết lập các thông tin nhạy cảm như TENANT_ID, CLIENT_ID, CLIENT_SECRET
   - Lưu ý: Trong môi trường sản xuất, hãy sử dụng các phương pháp an toàn hơn như credentials, secure vault để lưu trữ thông tin này

3. **Set destination** (Node Set):
   - Thiết lập các tham số đích:
     - TARGET_FOLDER: Đường dẫn thư mục đích trên SharePoint (ví dụ: `/uploads/pictures from n8n`)
     - FILE_NAME: Tên file muốn upload (ví dụ: `example.jpg`)

4. **Upload photo** (Node HTTP Request):
   - Cấu hình request để upload file lên SharePoint
   - Đảm bảo file nguồn đã được thiết lập đúng trong node trước đó

5. **Get photo (for testing purposes)** (Node HTTP Request):
   - Node này dùng để kiểm tra file đã được upload thành công
   - Có thể bỏ qua nếu không cần kiểm tra

#### 3. Kích hoạt ⚡️
- Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Sau khi kiểm tra thành công, bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các dịch vụ khác như Slack/Telegram để nhận thông báo khi upload thành công
- Lưu log các hoạt động upload để theo dõi và kiểm tra
- Tự động hóa quá trình upload định kỳ từ các nguồn dữ liệu khác nhau
- Tích hợp với các hệ thống quản lý tài liệu khác để tạo luồng công việc liên tục

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn hảo cho việc upload file lên SharePoint thông qua Microsoft Graph API. Với các sếp quản lý tài liệu, đây là công cụ không thể thiếu để tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả mà tự động hóa mang lại!