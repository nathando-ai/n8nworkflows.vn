---
title: "🚀 Tự động hóa Microsoft OneDrive với n8n - Giải phóng sức lao động"
description: "Workflow n8n này giúp tự động hóa 14 thao tác quan trọng trên OneDrive: từ upload/download đến chia sẻ và quản lý thư mục. Tiết kiệm thời gian và giảm lỗi thủ công."
slug: "tu-dong-hoa-microsoft-onedrive-voi-n8n"
tags: [n8n, automation, no-code, Microsoft OneDrive, cloud storage]
keywords: [n8n workflow, tự động hóa OneDrive, quản lý file tự động, n8n Microsoft OneDrive]
---

# 🚀 Tự động hóa Microsoft OneDrive với n8n - Giải phóng sức lao động

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 14 thao tác quan trọng trên OneDrive
- Tiết kiệm thời gian đáng kể cho các tác vụ quản lý file
- Giảm thiểu lỗi thủ công
- Tích hợp dễ dàng với các hệ thống khác
- Hoạt động liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft 365 với quyền truy cập OneDrive
- API Key từ Microsoft Graph API
- Quyền truy cập vào tài nguyên OneDrive cần quản lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5179)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Microsoft OneDrive Tool MCP Server** (Node đầu tiên):
   - Cấu hình credentials với API Key từ Microsoft Graph API
   - Điền thông tin xác thực tài khoản Microsoft 365

2. Các node Microsoft OneDrive Tool khác:
   - **Copy a file**: Cấu hình đường dẫn nguồn và đích
   - **Delete a file**: Xác nhận quyền xóa file
   - **Download a file**: Thiết lập vị trí lưu file tải về
   - **Get a file**: Cấu hình ID hoặc tên file cần lấy
   - **Rename a file**: Điền tên mới cho file
   - **Search a file**: Thiết lập tiêu chí tìm kiếm
   - **Share a file**: Cấu hình quyền chia sẻ và người nhận
   - **Upload a file**: Thiết lập vị trí upload và file nguồn
   - **Create a folder**: Điền tên và vị trí thư mục mới
   - **Delete a folder**: Xác nhận quyền xóa thư mục
   - **Get items in a folder**: Cấu hình ID thư mục cần lấy danh sách
   - **Rename a folder**: Điền tên mới cho thư mục
   - **Search a folder**: Thiết lập tiêu chí tìm kiếm
   - **Share a folder**: Cấu hình quyền chia sẻ và người nhận

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với các file/thư mục thử nghiệm
- Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi các thao tác hoàn thành
- Lưu log các hoạt động quan trọng vào Google Sheets hoặc Notion
- Tạo báo cáo định kỳ về các thay đổi trong OneDrive
- Kết nối với các hệ thống khác như Google Drive để đồng bộ dữ liệu

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quản lý file trên Microsoft OneDrive. Với 14 thao tác quan trọng được tự động hóa, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu lỗi thủ công. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!