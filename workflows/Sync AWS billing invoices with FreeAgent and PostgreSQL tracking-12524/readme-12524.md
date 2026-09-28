```yaml
---
title: "💰 Tự động đồng bộ hóa hóa đơn AWS với FreeAgent và PostgreSQL"
description: "Hướng dẫn tự động hóa quy trình đồng bộ hóa hóa đơn AWS với FreeAgent và theo dõi bằng PostgreSQL, tiết kiệm thời gian và tránh trùng lặp hóa đơn"
slug: "tu-dong-dong-bo-hoa-don-aws-voi-freeagent-postgresql"
tags: [n8n, automation, aws, freeagent, postgres]
keywords: [n8n workflow, tự động hóa hóa đơn, aws invoicing, freeagent api, postgres tracking]
---
# 💰 Tự động đồng bộ hóa hóa đơn AWS với FreeAgent và PostgreSQL

[Các sếp] có biết không? Mỗi tháng phải xử lý hàng chục hóa đơn AWS thủ công là một công việc nhàm chán và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy hóa đơn đến ghi sổ và thanh toán, giảm thiểu rủi ro nhân viên và tiết kiệm thời gian quý giá.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công cho mỗi hóa đơn
- **Tránh trùng lặp**: Kiểm tra và bỏ qua hóa đơn đã xử lý trước đó
- **Theo dõi minh bạch**: Lưu trữ đầy đủ thông tin hóa đơn trong PostgreSQL
- **Tiết kiệm thời gian**: Xử lý hàng chục hóa đơn trong vài phút thay vì vài giờ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản AWS với quyền `invoicing:ListInvoiceSummaries`
- Tài khoản FreeAgent với quyền tạo hóa đơn và thanh toán
- PostgreSQL database đã cài đặt và chạy
- Thông tin liên kết (URL) của nhà cung cấp, danh mục và tài khoản ngân hàng trong FreeAgent
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12524](https://n8n.io/workflows/12524)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán URL workflow vào ô nhập liệu và nhấn "OK"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Generate AWS Signature"**:
   - Thay thế `accessKeyId` và `secretAccessKey` bằng thông tin IAM của các sếp
   - Đảm bảo IAM user có quyền `invoicing:ListInvoiceSummaries`

2. **Node "Calculate Last Month Date Range"**:
   - Cập nhật giá trị `account_id` với AWS Account ID của các sếp

3. **Node "Create FreeAgent Bill"**:
   - Tạo credentials OAuth2 cho FreeAgent trong n8n
   - Cập nhật URL `contact` với ID nhà cung cấp trong FreeAgent
   - Cập nhật URL `category` với ID danh mục chi phí trong FreeAgent

4. **Node "Prepare Payment"**:
   - Cập nhật URL `bank_account` với tài khoản ngân hàng của các sếp trong FreeAgent

5. **Node "Check If Already Processed" và "Record In PostgreSQL"**:
   - Tạo credentials PostgreSQL trong n8n
   - Chạy câu lệnh SQL sau để tạo bảng theo dõi:
     ```sql
     CREATE TABLE aws_invoices_processed (
       id SERIAL PRIMARY KEY,
       aws_invoice_id VARCHAR(255) UNIQUE,
       freeagent_invoice_url VARCHAR(500),
       billing_period VARCHAR(7),
       amount DECIMAL(10,2),
       currency VARCHAR(3),
       created_at TIMESTAMP DEFAULT NOW()
     );
     ```

#### 3. Kích hoạt ⚡️
1. Thiết lập node "Trigger Monthly" để chạy vào ngày 3 và 4 hàng tháng
2. Thực hiện test run với dữ liệu mẫu
3. Kích hoạt workflow sau khi xác nhận hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email báo cáo sau khi hoàn thành xử lý hóa đơn
- Kết hợp với Slack để thông báo khi có hóa đơn mới
- Tạo bản sao lưu tự động của bảng PostgreSQL hàng tuần
- Thiết lập cảnh báo khi có hóa đơn vượt ngưỡng chi phí

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xử lý hóa đơn AWS, giảm thiểu rủi ro và tiết kiệm thời gian đáng kể. Bằng cách kết hợp AWS, FreeAgent và PostgreSQL, các sếp có thể duy trì hệ thống tài chính minh bạch và hiệu quả. Hãy áp dụng ngay để trải nghiệm sự khác biệt!