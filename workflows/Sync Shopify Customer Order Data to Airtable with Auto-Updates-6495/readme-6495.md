---
title: "🚀 Tự động đồng bộ dữ liệu khách hàng Shopify sang Airtable với cập nhật tự động"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu khách hàng từ Shopify sang Airtable, cập nhật thông tin khách hàng mới và cũ một cách tự động, tiết kiệm thời gian và tránh lỗi nhập liệu"
slug: "tu-dong-dong-bo-du-lieu-khach-hang-shopify-sang-airtable"
tags: [n8n, automation, no-code, Shopify, Airtable]
keywords: [n8n workflow, tự động hóa, Shopify, Airtable, CRM]
---

# 🚀 Tự động đồng bộ dữ liệu khách hàng Shopify sang Airtable với cập nhật tự động

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động cập nhật thông tin khách hàng mới và cũ trong Airtable
- Tránh nhập liệu trùng lặp và lỗi
- Tiết kiệm thời gian xử lý dữ liệu khách hàng
- Dữ liệu khách hàng luôn được cập nhật mới nhất
- Hỗ trợ phân tích và quản lý khách hàng hiệu quả hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Airtable với quyền truy cập API
- API Key từ Airtable (Airtable Token API)
- URL webhook từ Shopify để nhận dữ liệu đơn hàng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **customerCreate (Webhook)**: Cấu hình webhook từ Shopify để nhận dữ liệu đơn hàng mới. Cần điền:
  - Path: `customerCreate`
  - HTTP Method: `POST`

- **CCUST (Airtable)**: Cấu hình node để tìm kiếm khách hàng trong Airtable. Cần điền:
  - Airtable Token API: Chọn credentials đã cấu hình
  - Base ID: ID của cơ sở dữ liệu Airtable
  - Table Name: Tên bảng chứa dữ liệu khách hàng
  - Search Field: Trường để tìm kiếm (ví dụ: `Customer ID`)

- **CustomerSheet (Airtable)**: Cấu hình node để tạo mới hoặc cập nhật thông tin khách hàng. Cần điền:
  - Airtable Token API: Chọn credentials đã cấu hình
  - Base ID: ID của cơ sở dữ liệu Airtable
  - Table Name: Tên bảng chứa dữ liệu khách hàng
  - Key Field: Trường khóa (ví dụ: `Customer ID`)
  - Fields to Update: Các trường cần cập nhật (ví dụ: `first_name`, `last_name`, `email`, `phone`, `address`, `city`, `province`, `zip`, `country`, `total_orders`, `total_spent`, `last_order_date`)

- **CustomerSheet4 (Airtable)**: Cấu hình node để tìm kiếm thông tin khách hàng trong Airtable. Cần điền:
  - Airtable Token API: Chọn credentials đã cấu hình
  - Base ID: ID của cơ sở dữ liệu Airtable
  - Table Name: Tên bảng chứa dữ liệu khách hàng
  - Search Field: Trường để tìm kiếm (ví dụ: `Customer ID`)

- **PRDSHEET4 (Airtable)**: Cấu hình node để tạo mới bản ghi sản phẩm. Cần điền:
  - Airtable Token API: Chọn credentials đã cấu hình
  - Base ID: ID của cơ sở dữ liệu Airtable
  - Table Name: Tên bảng chứa dữ liệu sản phẩm
  - Fields to Create: Các trường cần tạo mới (ví dụ: `product_id`, `product_name`, `variant_id`, `variant_name`, `price`, `quantity`)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có đơn hàng mới.
- Lưu log các hoạt động để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về dữ liệu khách hàng và đơn hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ dữ liệu khách hàng từ Shopify sang Airtable, cập nhật thông tin khách hàng mới và cũ một cách tự động, tiết kiệm thời gian và tránh lỗi nhập liệu. Hãy áp dụng ngay để nâng cao hiệu quả quản lý khách hàng!