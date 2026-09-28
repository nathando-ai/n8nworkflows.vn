---
title: "🔄 Tự động đồng bộ dữ liệu giữa Excel/Google Sheets và PostgreSQL - Workflow n8n"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu hai chiều giữa bảng tính Excel/Google Sheets và cơ sở dữ liệu PostgreSQL bằng workflow n8n. Tiết kiệm thời gian và giảm thiểu lỗi khi làm việc với dữ liệu."
slug: "tu-dong-dong-bo-excel-postgresql-n8n"
tags: [n8n, automation, no-code, excel, postgresql]
keywords: [n8n workflow, tự động hóa, đồng bộ dữ liệu, excel, postgresql]
---

# 🔄 Tự động đồng bộ dữ liệu giữa Excel/Google Sheets và PostgreSQL

[Các sếp đang gặp khó khăn khi phải chuyển đổi dữ liệu giữa bảng tính Excel/Google Sheets và cơ sở dữ liệu PostgreSQL một cách thủ công. Việc này tốn thời gian, dễ gây lỗi và không thể đảm bảo tính nhất quán dữ liệu. Workflow này sẽ giúp các sếp tự động hóa quy trình này 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ dữ liệu hai chiều giữa Excel/Google Sheets và PostgreSQL
- Tiết kiệm thời gian đáng kể khi chuyển đổi dữ liệu thủ công
- Giảm thiểu lỗi do nhập liệu sai
- Đảm bảo tính nhất quán dữ liệu giữa hai nguồn
- Có thể chạy theo lịch trình hoặc kích hoạt thủ công
- Dễ dàng mở rộng để đồng bộ dữ liệu từ PostgreSQL về Excel
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft Excel/Google Sheets với quyền truy cập vào bảng tính cần đồng bộ
- Cơ sở dữ liệu PostgreSQL với bảng đã được tạo sẵn
- Credentials cho Microsoft Excel/Google Sheets và PostgreSQL trong n8n
- Cột dữ liệu trong bảng Excel/Google Sheets và bảng PostgreSQL phải có tên giống nhau để tự động ánh xạ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: `https://n8n.io/workflows/8457`
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/8457) và import vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Table" (Microsoft Excel)**:
   - Chọn credentials cho Microsoft Excel/Google Sheets
   - Điền ID của bảng tính Excel/Google Sheets
   - Điền tên của bảng (sheet) trong file Excel/Google Sheets
   - Đảm bảo cột dữ liệu trong bảng Excel/Google Sheets và bảng PostgreSQL có tên giống nhau

2. **Node "Upsert Table" (Postgres)**:
   - Chọn credentials cho PostgreSQL
   - Điền tên của bảng trong PostgreSQL
   - Điền tên của cột khóa chính (primary key) trong bảng PostgreSQL
   - Đảm bảo cột dữ liệu trong bảng Excel/Google Sheets và bảng PostgreSQL có tên giống nhau

3. **Node "Sanitize Date" (Code)**:
   - Kiểm tra và điều chỉnh đoạn mã xử lý dữ liệu nếu cần thiết
   - Đảm bảo định dạng ngày tháng được xử lý đúng theo yêu cầu

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối và cấu hình của các node
2. Chạy workflow một lần để kiểm tra dữ liệu đầu ra
3. Bật chế độ Active cho workflow để chạy tự động theo lịch trình hoặc kích hoạt thủ công

### ✍️ Mẹo & gợi ý nâng cao
1. **Đồng bộ dữ liệu từ PostgreSQL về Excel**:
   - Thêm node "Get Table" (Postgres) để lấy dữ liệu từ PostgreSQL
   - Thêm node "Update Table" (Microsoft Excel) để cập nhật dữ liệu vào bảng Excel/Google Sheets

2. **Thiết lập lịch trình đồng bộ tự động**:
   - Sử dụng node "Schedule Trigger" để đặt lịch chạy workflow theo định kỳ

3. **Gửi thông báo khi đồng bộ hoàn thành**:
   - Thêm node "Send Email" hoặc "Send Slack Message" để nhận thông báo khi đồng bộ dữ liệu hoàn thành

4. **Xử lý lỗi và ghi log**:
   - Thêm node "Error Trigger" để xử lý lỗi khi đồng bộ dữ liệu
   - Thêm node "Write to File" hoặc "Send to Database" để ghi log hoạt động của workflow

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ dữ liệu hai chiều giữa Excel/Google Sheets và PostgreSQL một cách dễ dàng và hiệu quả. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian đáng kể, giảm thiểu lỗi và đảm bảo tính nhất quán dữ liệu. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!