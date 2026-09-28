---
title: "📧 Tự động lưu trữ chi tiết email Gmail vào MySQL - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động lưu trữ thông tin email Gmail vào MySQL để quản lý ticket hiệu quả hơn. Giải pháp tự động hóa 100% không cần code."
slug: "tu-dong-luu-tru-email-gmail-vao-mysql"
tags: [n8n, automation, no-code, mysql, gmail]
keywords: [n8n workflow, tự động hóa email, lưu trữ email, mysql, gmail]
---

# 📧 Tự động lưu trữ chi tiết email Gmail vào MySQL - Workflow n8n hoàn chỉnh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu trữ toàn bộ thông tin email vào MySQL trong vòng 1 phút sau khi nhận
- Quản lý ticket hiệu quả hơn với dữ liệu được cấu trúc rõ ràng
- Tiết kiệm thời gian xử lý thủ công cho các bộ phận CSKH
- Dễ dàng tích hợp với các hệ thống báo cáo khác
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập API
- Cơ sở dữ liệu MySQL đã cài đặt và cấu hình
- Bảng dữ liệu với cấu trúc sau:
  - messageId (Gmail message ID)
  - threadId
  - snippet
  - sender_name (nullable)
  - sender_email
  - recipient_name (nullable)
  - recipient_email
  - subject (nullable)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/6302`
4. Nhấn "OK" để bắt đầu quá trình import

Hoặc bạn có thể:
1. Truy cập link gốc workflow: [https://n8n.io/workflows/6302](https://n8n.io/workflows/6302)
2. Nhấn nút "Copy JSON" ở góc trên bên phải
3. Trong n8n Editor, nhấn vào nút "Import from JSON" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Receive Email" (gmailTrigger)**
   - Cấu hình credentials cho Gmail OAuth2
   - Chọn các trường thông tin cần theo dõi (recommended: "messageId", "threadId", "snippet", "sender", "recipient", "subject")

2. **Node "Get Client Name and Email" (code)**
   - Không cần cấu hình gì thêm, node này sẽ tự động trích xuất thông tin từ email nhận được
   - Nếu cần tùy chỉnh thêm thông tin trích xuất, bạn có thể chỉnh sửa đoạn code JavaScript trong node này

3. **Node "Insert New Client in MySQL" (mySql)**
   - Cấu hình credentials cho MySQL
   - Chọn database và bảng chứa dữ liệu email
   - Đảm bảo các trường dữ liệu trong bảng MySQL khớp với cấu trúc sau:
     - messageId (Gmail message ID)
     - threadId
     - snippet
     - sender_name (nullable)
     - sender_email
     - recipient_name (nullable)
     - recipient_email
     - subject (nullable)
   - Chọn operation là "upsert" để cập nhật dữ liệu nếu đã tồn tại

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn vào nút "Activate" ở góc trên bên phải của workflow
2. Để kiểm tra hoạt động, bạn có thể gửi một email thử nghiệm đến tài khoản Gmail đã cấu hình
3. Sau 1-2 phút, kiểm tra bảng MySQL để xác nhận dữ liệu đã được lưu trữ đúng cách

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu trữ các tệp đính kèm từ email
- Tích hợp với Slack để thông báo khi có email mới
- Thiết lập báo cáo định kỳ về các email quan trọng
- Kết hợp với hệ thống CRM để tự động tạo ticket từ email
- Thêm bộ lọc để chỉ lưu trữ các email từ các địa chỉ cụ thể

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để tự động hóa việc lưu trữ thông tin email vào MySQL, giúp các bộ phận CSKH quản lý ticket hiệu quả hơn. Với việc tự động hóa toàn bộ quá trình này, các sếp có thể tập trung vào các công việc quan trọng hơn thay vì phải xử lý thủ công các email hàng ngày.