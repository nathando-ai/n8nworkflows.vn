---
title: "📊 Tự động hóa báo cáo xu hướng bán hàng WooCommerce hàng tuần cho Slack & Google Sheets"
description: "Workflow n8n giúp tự động hóa báo cáo xu hướng bán hàng WooCommerce hàng tuần, so sánh hiệu suất hiện tại với dữ liệu lịch sử và gửi báo cáo đến Slack và Google Sheets."
slug: "tu-dong-hoa-bao-cao-xu-huong-ban-hang-woocommerce-hang-tuan"
tags: [n8n, automation, no-code, WooCommerce, Google Sheets, Slack]
keywords: [n8n workflow, tự động hóa, WooCommerce, báo cáo bán hàng, Google Sheets, Slack]
---

# 📊 Tự động hóa báo cáo xu hướng bán hàng WooCommerce hàng tuần cho Slack & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức trong việc tạo báo cáo thủ công hàng tuần.
- So sánh hiệu suất bán hàng hiện tại với dữ liệu lịch sử một cách dễ dàng.
- Nhận báo cáo xu hướng bán hàng được gửi tự động đến Slack và Google Sheets.
- Dễ dàng theo dõi và phân tích xu hướng bán hàng qua các báo cáo được lưu trữ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API.
- Tài khoản Slack với quyền gửi tin nhắn.
- Tài khoản Google với quyền truy cập Google Sheets.
- ID của Google Sheet để lưu trữ báo cáo.
- URL webhook của Slack để gửi báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/12371](https://n8n.io/workflows/12371).
2. Nhấn vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Global Configuration**:
   - Mở node "Global Configuration" và cấu hình các biến toàn cục:
     - `trend_threshold`: Ngưỡng so sánh xu hướng (ví dụ: 5%).
     - `slack_webhook_url`: URL webhook của Slack để gửi báo cáo.
     - `google_sheet_id`: ID của Google Sheet để lưu trữ báo cáo.

2. **Fetch Sales Nodes**:
   - Mở từng node "Fetch Current Week Sales", "Fetch Last Month Sales", và "Fetch Last Year Sales".
   - Chọn credentials WooCommerce đã cấu hình trước đó.

3. **Log to Google Sheets**:
   - Mở node "Log to Google Sheets" và chọn tài khoản Google để xác thực.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test Workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo ngay lập tức khi có báo cáo mới.
- Lưu trữ báo cáo trong Google Sheets để dễ dàng truy cập và phân tích.
- Tùy chỉnh ngưỡng so sánh xu hướng để phù hợp với nhu cầu kinh doanh.
- Kết hợp với các công cụ khác như Google Data Studio để tạo báo cáo trực quan hơn.

### 📌 Kết luận
Workflow này giúp tự động hóa báo cáo xu hướng bán hàng WooCommerce hàng tuần, tiết kiệm thời gian và công sức cho các sếp. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh!