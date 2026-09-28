---
title: "🚀 Tự động hóa tài chính: Lấy dữ liệu QuickBooks hàng tuần vào Google BigQuery"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình ETL hàng tuần từ QuickBooks sang Google BigQuery, giúp các sếp tiết kiệm thời gian và nâng cao khả năng phân tích tài chính"
slug: "tu-dong-hoa-quickbooks-google-bigquery"
tags: [n8n, automation, no-code, quickbooks, google-bigquery]
keywords: [n8n workflow, tự động hóa tài chính, quickbooks bigquery, etl pipeline]
---

# 🚀 Tự động hóa tài chính: Lấy dữ liệu QuickBooks hàng tuần vào Google BigQuery

[Các sếp đang gặp khó khăn khi phải thủ công xuất dữ liệu tài chính từ QuickBooks sang Google BigQuery hàng tuần. Quy trình này tốn thời gian, dễ gây lỗi và không thể tự động hóa theo nhu cầu cá nhân của doanh nghiệp. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình ETL (Extract, Transform, Load) hàng tuần một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quy trình hàng tuần, giảm thiểu công việc thủ công
- **Dữ liệu chính xác**: Xử lý và phân loại dữ liệu theo logic kinh doanh của doanh nghiệp
- **Lịch sử đầy đủ**: Lưu trữ dữ liệu lịch sử trong BigQuery cho phân tích dài hạn
- **Tự động hóa liên tục**: Chạy tự động mỗi thứ Hai hàng tuần mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản QuickBooks Online với quyền truy cập API
- Dự án Google Cloud với Google BigQuery đã kích hoạt
- Bảng BigQuery đã tạo với schema phù hợp
- Credentials cho cả QuickBooks và Google BigQuery trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6493](https://n8n.io/workflows/6493)
2. Click vào nút "Download Workflow"
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Start: Weekly on Monday"**:
   - Kiểm tra lịch trình chạy (mặc định là mỗi thứ Hai hàng tuần)
   - Có thể điều chỉnh thời gian chạy nếu cần

2. **Node "1. Get Last Week's Transactions"**:
   - Thêm credentials QuickBooks OAuth2
   - Kiểm tra tham số "resource" đã được đặt là "transaction"

3. **Node "2. Clean & Classify Transactions"**:
   - **BẮT BUỘC**: Chỉnh sửa JavaScript trong node này
   - Cập nhật các mảng sau để phù hợp với biểu đồ tài khoản của doanh nghiệp:
     ```javascript
     const internalTransferAccounts = ['123', '456']; // Thay bằng mã tài khoản chuyển nội bộ của bạn
     const expenseCategories = ['789', '101']; // Thay bằng mã danh mục chi phí của bạn
     const incomeCategories = ['112', '113']; // Thay bằng mã danh mục thu nhập của bạn
     ```
   - Có thể thêm logic phân loại tùy chỉnh cho các trường hợp đặc biệt

4. **Node "4. Load Data to BigQuery"**:
   - Thêm credentials Google BigQuery OAuth2
   - Chọn đúng Google Cloud project
   - Kiểm tra và điều chỉnh câu truy vấn SQL nếu cần:
     ```sql
     INSERT INTO `your-project.quickbooks.transactions`
     (transaction_id, date, account_id, amount, description, type)
     VALUES
     {{ $node["2. Clean & Classify Transactions"].json.transactionData }}
     ```

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong bảng BigQuery
3. Nếu mọi thứ ổn, click vào "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack**: Thêm node gửi thông báo khi workflow hoàn thành
- **Lưu log**: Thêm node ghi log vào Google Sheets hoặc cơ sở dữ liệu
- **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo hàng tuần qua email
- **Xử lý lỗi**: Thêm node xử lý lỗi và gửi cảnh báo khi có vấn đề

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quy trình ETL tài chính hàng tuần từ QuickBooks sang Google BigQuery. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian, đảm bảo dữ liệu chính xác và có sẵn dữ liệu lịch sử đầy đủ cho phân tích dài hạn. Hãy thử ngay và nâng cao khả năng phân tích tài chính của doanh nghiệp!