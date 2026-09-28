---
title: "📧 [Tự động hóa] Kiểm tra và sửa lỗi email trong bảng Airtable với n8n"
description: "Hướng dẫn tự động hóa kiểm tra và sửa lỗi email trong bảng Airtable bằng n8n, tiết kiệm thời gian và giảm sai sót"
slug: "tu-dong-hoa-kiem-tra-email-airtable-n8n"
tags: [n8n, automation, no-code, airtable, email-validation]
keywords: [n8n workflow, tự động hóa, kiểm tra email, airtable, mailcheck]
---

# 📧 [Tự động hóa] Kiểm tra và sửa lỗi email trong bảng Airtable với n8n

[Các sếp đang làm việc với bảng Airtable chứa danh sách khách hàng, nhưng phải mất thời gian và công sức để kiểm tra từng email một. Workflow này sẽ tự động hóa quy trình này, giúp các sếp tiết kiệm thời gian và giảm sai sót khi làm việc với dữ liệu email.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động kiểm tra hàng nghìn email trong bảng Airtable một cách nhanh chóng
- Phát hiện và sửa lỗi email sai định dạng ngay lập tức
- Tiết kiệm thời gian đáng kể so với kiểm tra thủ công
- Giảm thiểu sai sót khi làm việc với dữ liệu email quan trọng
- Tự động cập nhật bảng Airtable với email đã được kiểm tra và sửa lỗi
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với bảng chứa email cần kiểm tra
- API Key của Airtable (để kết nối với n8n)
- API Key của Mailcheck (dịch vụ kiểm tra email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của các sếp
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn tùy chọn "From File" và tải lên file JSON của workflow
4. Hoặc, các sếp có thể copy nội dung JSON của workflow và dán vào ô "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính:

1. **Airtable (Node đầu tiên)**:
   - Cấu hình credentials: Chọn "airtableApi" đã được thiết lập trước đó
   - Tham số cần cấu hình:
     - Operation: Chọn "List"
     - Base ID: Nhập ID của cơ sở dữ liệu Airtable
     - Table Name: Nhập tên bảng chứa email
     - Fields: Chọn trường chứa email (thường là "Email")

2. **Mailcheck**:
   - Cấu hình credentials: Chọn "mailcheckApi" đã được thiết lập trước đó
   - Tham số cần cấu hình:
     - Email: Chọn trường email từ dữ liệu đầu vào

3. **Set**:
   - Không cần cấu hình credentials
   - Tham số cần cấu hình:
     - Key: Nhập "email"
     - Value: Chọn trường email đã được kiểm tra từ node Mailcheck

4. **Airtable1 (Node cuối cùng)**:
   - Cấu hình credentials: Chọn "airtableApi" đã được thiết lập trước đó
   - Tham số cần cấu hình:
     - Operation: Chọn "Update"
     - Base ID: Nhập ID của cơ sở dữ liệu Airtable
     - Table Name: Nhập tên bảng chứa email
     - Record ID: Chọn trường ID từ dữ liệu đầu vào
     - Fields: Chọn trường email đã được kiểm tra từ node Set

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình đầy đủ các node, các sếp cần thực hiện các bước sau:

1. Kiểm tra kết nối với Airtable và Mailcheck bằng cách nhấn nút "Execute Node" trên từng node
2. Sau khi tất cả các node đều hoạt động đúng, các sếp có thể kích hoạt workflow bằng cách nhấn nút "Activate" ở góc trên bên phải
3. Để kiểm tra workflow hoạt động đúng, các sếp có thể tạo một bản ghi mới trong bảng Airtable và xem kết quả sau khi workflow chạy

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với các dịch vụ khác như Slack hoặc Telegram để nhận thông báo khi có email bị lỗi
- Để tối ưu hóa, các sếp có thể chạy workflow này định kỳ (ví dụ: hàng ngày) bằng cách sử dụng node "Schedule Trigger"
- Các sếp có thể lưu log của quá trình kiểm tra email để theo dõi lịch sử thay đổi
- Workflow này có thể được mở rộng để kiểm tra nhiều loại dữ liệu khác trong bảng Airtable

### 📌 Kết luận
Workflow "Validate emails in a table using Mailcheck" giúp các sếp tự động hóa quá trình kiểm tra và sửa lỗi email trong bảng Airtable một cách hiệu quả. Bằng cách sử dụng công nghệ tự động hóa của n8n, các sếp có thể tiết kiệm thời gian đáng kể và giảm thiểu sai sót khi làm việc với dữ liệu email quan trọng. Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của các sếp!