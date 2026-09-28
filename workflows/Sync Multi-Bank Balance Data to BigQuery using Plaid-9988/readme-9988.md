```yaml
---
title: "💰 Tự động đồng bộ dữ liệu số dư ngân hàng đa ngân hàng lên BigQuery với Plaid"
description: "Hướng dẫn tự động hóa việc lấy số dư từ 4 ngân hàng (RBC, Amex, Wise, PayPal) thông qua Plaid và tải lên Google BigQuery để phân tích tài chính"
slug: "tu-dong-dong-bo-du-lieu-ngan-hang-plaid-bigquery"
tags: [n8n, automation, finance, plaid, bigquery]
keywords: [tự động hóa tài chính, plaid api, bigquery analytics, đồng bộ số dư ngân hàng]
---
```

# 💰 Tự động đồng bộ dữ liệu số dư ngân hàng đa ngân hàng lên BigQuery với Plaid

[Các sếp tài chính và kế toán thường phải làm việc thủ công để lấy số dư từ nhiều ngân hàng khác nhau, sau đó nhập vào hệ thống phân tích. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng 15 phút, giảm thiểu lỗi và tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lấy số dư từ 4 ngân hàng chính (RBC, Amex, Wise, PayPal) hàng tuần
- Đồng bộ dữ liệu với hệ thống kế toán QuickBooks Online
- Tạo báo cáo tài chính tự động trong Google BigQuery
- Giảm thời gian xử lý từ 2-3 giờ xuống còn 15 phút
- Dữ liệu được lưu trữ và phân tích một cách chính xác và liên tục
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Plaid Developer với API keys cho các ngân hàng mục tiêu
- Tài khoản Google Cloud với quyền truy cập vào Google BigQuery
- Bảng BigQuery đã được tạo với schema phù hợp
- Biết cách tạo và quản lý credentials trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9988](https://n8n.io/workflows/9988)
2. Click "Download" để tải file JSON workflow
3. Trong n8n Editor, click "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình lịch chạy (ví dụ: mỗi thứ Hai lúc 8h sáng)
   - Đặt timezone phù hợp với múi giờ của các sếp

2. **Plaid API Nodes (4 nodes)**:
   - Tạo credentials Plaid trong n8n với client_id và secret
   - Thay thế các tham số trong URL Plaid API:
     - `client_id={{$credentials.plaid.clientId}}`
     - `secret={{$credentials.plaid.secret}}`
     - `access_token` cho từng ngân hàng (RBC, Amex, Wise, PayPal)

3. **Mapping Nodes (4 nodes)**:
   - Chỉnh sửa mã JavaScript trong các node "Map [Ngân hàng] Accounts to QBO"
   - Đảm bảo ánh xạ đúng giữa tên tài khoản Plaid và tên tài khoản QBO

4. **Google BigQuery Node**:
   - Tạo credentials Google BigQuery trong n8n
   - Cấu hình tham số:
     - Project ID
     - Dataset ID
     - Table ID (bảng lưu trữ dữ liệu tài khoản)
     - Query: `INSERT INTO [project_id].[dataset_id].[table_id] VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,