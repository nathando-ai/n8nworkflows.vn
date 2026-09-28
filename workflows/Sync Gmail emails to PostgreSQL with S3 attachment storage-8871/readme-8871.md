---
title: "📧 Tự động lưu trữ Email Gmail vào PostgreSQL cùng lưu trữ đính kèm S3"
description: "Hướng dẫn tự động hóa lưu trữ email Gmail vào PostgreSQL với lưu trữ đính kèm trên S3/MinIO, giải pháp hoàn chỉnh cho lưu trữ và phân tích dữ liệu email doanh nghiệp"
slug: "tu-dong-luu-tru-email-gmail-postgresql-s3"
tags: [n8n, automation, no-code, gmail, postgresql, s3, minio, email, data-storage]
keywords: [n8n workflow, tự động hóa email, lưu trữ email, postgresql, s3, minio, quản lý email, dữ liệu doanh nghiệp]
---

# 📧 Tự động lưu trữ Email Gmail vào PostgreSQL cùng lưu trữ đính kèm S3

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý email thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lưu trữ hoàn chỉnh**: Tự động lưu trữ toàn bộ email Gmail vào PostgreSQL với cấu trúc dữ liệu linh hoạt
- **Quản lý đính kèm**: Tự động xử lý và lưu trữ đính kèm email lên S3/MinIO
- **Tìm kiếm và phân tích**: Dữ liệu email có thể tìm kiếm và phân tích dễ dàng
- **Tích hợp hệ thống**: Kết nối liền mạch với các hệ thống khác trong doanh nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API
- PostgreSQL database với quyền tạo bảng và chèn dữ liệu
- Tài khoản S3/MinIO với quyền tạo bucket và tải lên
- Google Cloud Console project với Gmail API đã kích hoạt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8871](https://n8n.io/workflows/8871)
2. Nhấn nút "Import" để tải về file JSON workflow
3. Trong n8n Editor, nhấn "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Gmail OAuth2 Credential**:
   - Tạo mới credential trong n8n Editor
   - Điền thông tin từ Google Cloud Console
   - Đảm bảo đã kích hoạt scope `gmail.readonly`

2. **PostgreSQL Credential**:
   - Tạo credential với thông tin kết nối PostgreSQL
   - Chạy script tạo bảng messages (xem phần Database Schema bên dưới)

3. **S3 Credential**:
   - Tạo credential với thông tin kết nối S3/MinIO
   - Tạo bucket `gmail-attachments` với quyền tải lên

4. **Cấu hình các node quan trọng**:
   - **Get Individual Message**: Đảm bảo `downloadAttachments: true` và `simple: false`
   - **Get Many Sent/Inbox**: Cập nhật query để lấy email từ thời điểm mong muốn
   - **Email to PostgreSQL Transform**: Cập nhật `authenticatedUserEmail` với email của bạn
   - **Upload to Storage**: Cập nhật cấu hình bucket và path nếu cần

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các credential
2. Chạy test với một email mẫu để đảm bảo dữ liệu được xử lý đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc email**: Cập nhật các query trong Get Many nodes để chỉ lấy email quan trọng
- **Xử lý đính kèm**: Thêm bộ lọc để chỉ xử lý các loại đính kèm quan trọng
- **Báo cáo**: Kết nối với các dịch vụ báo cáo để theo dõi lượng email được xử lý
- **Tích hợp Slack**: Thêm node để thông báo khi có email mới được xử lý
- **Lịch sử thay đổi**: Thêm trường `updated_at` để theo dõi lịch sử thay đổi email

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động lưu trữ và quản lý email Gmail, giúp các sếp tiết kiệm thời gian và nguồn lực trong việc quản lý dữ liệu quan trọng. Với khả năng tích hợp linh hoạt và cấu trúc dữ liệu linh hoạt, workflow này đáp ứng nhu cầu lưu trữ và phân tích email của các doanh nghiệp hiện đại.