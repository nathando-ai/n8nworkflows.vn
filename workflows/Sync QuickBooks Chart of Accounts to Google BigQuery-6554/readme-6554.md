---
title: "🚀 Tự động đồng bộ dữ liệu tài khoản từ QuickBooks sang Google BigQuery hàng tuần"
description: "Hướng dẫn chi tiết cách tự động hóa việc đồng bộ dữ liệu tài khoản từ QuickBooks sang Google BigQuery hàng tuần để phân tích dữ liệu tài chính hiệu quả"
slug: "tu-dong-dong-bo-quickbooks-sang-bigquery"
tags: [n8n, automation, no-code, quickbooks, bigquery]
keywords: [n8n workflow, tự động hóa, quickbooks, bigquery, phân tích tài chính]
---

# 🚀 Tự động đồng bộ dữ liệu tài khoản từ QuickBooks sang Google BigQuery hàng tuần

[Các sếp đang gặp khó khăn khi phải thủ công xuất dữ liệu tài khoản từ QuickBooks sang Google BigQuery để phân tích dữ liệu tài chính. Workflow này giúp tự động hóa quy trình này hàng tuần, tiết kiệm thời gian và đảm bảo dữ liệu luôn được cập nhật mới nhất.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Dữ liệu tài khoản từ QuickBooks được tự động đồng bộ sang Google BigQuery hàng tuần
- Tiết kiệm thời gian thủ công xuất dữ liệu
- Dữ liệu được lưu trữ lịch sử để phân tích thay đổi qua thời gian
- Dễ dàng tích hợp với các công cụ phân tích dữ liệu khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản QuickBooks Online
- QuickBooks Company ID
- Dự án Google Cloud với BigQuery
- Bảng dữ liệu (table) trong BigQuery để lưu trữ dữ liệu tài khoản
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Node "Start: Weekly on Monday"**: Cấu hình lịch chạy hàng tuần vào thứ Hai.
- **Node "1. Get Updated Accounts from QuickBooks"**:
  - Thêm credentials QuickBooks OAuth2 API
  - Thay thế `{COMPANY_ID}` trong URL bằng QuickBooks Company ID thực tế của các sếp
  - Có thể sử dụng phím tắt `Ctrl + Alt + ?` trong QuickBooks để tìm Company ID
- **Node "2. Structure Account Data"**: Có thể tùy chỉnh để thêm hoặc biến đổi các trường dữ liệu theo nhu cầu
- **Node "3. Format Data for SQL"**: Có thể tùy chỉnh để định dạng dữ liệu theo cấu trúc bảng trong BigQuery
- **Node "4. Load Accounts to BigQuery"**:
  - Thêm credentials Google BigQuery OAuth2 API
  - Chọn đúng dự án Google Cloud
  - Đảm bảo tên dataset và bảng trong câu truy vấn SQL là chính xác

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi tần suất đồng bộ**: Điều chỉnh node lịch để chạy hàng ngày, hàng tháng, hoặc theo nhu cầu cụ thể
- **Đồng bộ dữ liệu ban đầu**: Tạm thời cập nhật truy vấn API để `select * from Account` để lấy toàn bộ dữ liệu ban đầu
- **Thêm trường dữ liệu**: Sửa đổi node "2. Structure Account Data" để bao gồm hoặc biến đổi các trường dữ liệu theo nhu cầu
- **Kết hợp với các công cụ khác**: Kết nối với Slack hoặc Email để thông báo khi đồng bộ hoàn thành

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc đồng bộ dữ liệu tài khoản từ QuickBooks sang Google BigQuery hàng tuần, tiết kiệm thời gian và đảm bảo dữ liệu luôn được cập nhật mới nhất. Hãy áp dụng ngay để nâng cao hiệu quả phân tích dữ liệu tài chính của doanh nghiệp!