---
title: "🚀 Tự động đồng bộ dữ liệu Salesforce Leads & Opportunities vào PostgreSQL - Hỗ trợ Backfill & ETL Tăng dần"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu từ Salesforce vào PostgreSQL với tính năng backfill lịch sử và ETL tăng dần, giúp tiết kiệm thời gian và đảm bảo dữ liệu chính xác."
slug: "tu-dong-dong-bo-salesforce-postgresql-backfill-etl-tang-dan"
tags: [n8n, automation, no-code, salesforce, postgresql, crm, etl]
keywords: [n8n workflow, tự động hóa, salesforce, postgresql, etl, crm]
---

# 🚀 Tự động đồng bộ dữ liệu Salesforce Leads & Opportunities vào PostgreSQL - Hỗ trợ Backfill & ETL Tăng dần

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý thủ công dữ liệu từ Salesforce sang PostgreSQL. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ dữ liệu từ Salesforce sang PostgreSQL với 2 chế độ: backfill lịch sử và ETL tăng dần.
- Tiết kiệm thời gian xử lý thủ công dữ liệu.
- Đảm bảo dữ liệu đồng bộ chính xác và liên tục.
- Hỗ trợ xử lý dữ liệu theo lô (batch processing) để tránh quá tải hệ thống.
- Tích hợp sẵn các tính năng xử lý số điện thoại, loại bỏ trùng lặp và chuẩn hóa dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Salesforce với quyền truy cập vào các đối tượng Lead và Opportunity.
- Tài khoản PostgreSQL với quyền tạo bảng và chèn dữ liệu.
- API keys hoặc credentials cho Salesforce và PostgreSQL.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/14993](https://n8n.io/workflows/14993).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Fetch Opportunity Records**: Cấu hình node này để lấy dữ liệu từ Salesforce Opportunity. Cần cung cấp các trường dữ liệu cần thiết từ Salesforce Object Manager → Opportunity → Fields & Relationships.

- **Fetch Lead Records**: Cấu hình node này để lấy dữ liệu từ Salesforce Lead. Cần cung cấp các trường dữ liệu cần thiết từ Salesforce Object Manager → Lead → Fields & Relationships.

- **Upsert Rows into Postgres**: Cấu hình node này để chèn dữ liệu vào PostgreSQL. Cần cung cấp thông tin kết nối PostgreSQL và tên bảng đích.

- **Set Historical Date Range**: Cấu hình node này để thiết lập khoảng thời gian lịch sử cho backfill. Cần cung cấp `start_date` và `end_date`.

- **Schedule Trigger (Incremental)**: Cấu hình node này để thiết lập lịch chạy tự động cho ETL tăng dần. Cần cung cấp khoảng thời gian chạy (ví dụ: hàng ngày).

- **Manual Trigger (Historical Backfill)**: Cấu hình node này để chạy backfill lịch sử. Cần cung cấp `start_date` và `end_date`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy thành công hoặc gặp lỗi.
- Lưu log chạy workflow để theo dõi lịch sử và hiệu suất.
- Gửi báo cáo định kỳ về dữ liệu đã đồng bộ để giám sát quá trình ETL.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ dữ liệu từ Salesforce sang PostgreSQL một cách hiệu quả và chính xác. Với tính năng backfill lịch sử và ETL tăng dần, dữ liệu sẽ luôn được cập nhật liên tục và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!