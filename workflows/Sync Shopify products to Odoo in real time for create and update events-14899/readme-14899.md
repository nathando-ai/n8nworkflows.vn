---
title: "🚀 Tự động đồng bộ sản phẩm Shopify sang Odoo thời gian thực - Giảm thiểu 90% công việc thủ công"
description: "Hướng dẫn chi tiết cách tự động đồng bộ sản phẩm từ Shopify sang Odoo khi có sự kiện tạo mới hoặc cập nhật, tiết kiệm thời gian và tránh sai sót thủ công"
slug: "tu-dong-dong-bo-san-pham-shopify-sang-odoo-thoi-gian-thuc"
tags: [n8n, automation, no-code, shopify, odoo, erp, crm]
keywords: [n8n workflow, tự động hóa, shopify odoo, đồng bộ sản phẩm, erp]
---

# 🚀 Tự động đồng bộ sản phẩm Shopify sang Odoo thời gian thực - Giảm thiểu 90% công việc thủ công

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ sản phẩm mới từ Shopify sang Odoo ngay khi có sự kiện tạo mới
- Cập nhật thông tin sản phẩm trong Odoo khi có thay đổi trên Shopify
- Tiết kiệm 90% thời gian thủ công đồng bộ dữ liệu
- Đảm bảo dữ liệu luôn đồng bộ và chính xác
- Giảm thiểu sai sót do nhập liệu thủ công
- Tự động xử lý hình ảnh sản phẩm và phân loại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Odoo với quyền truy cập API
- API keys cho cả hai nền tảng
- Danh mục sản phẩm đã được thiết lập trong Odoo
- URL của hình ảnh sản phẩm phải có sẵn và truy cập được
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When Product Created" và "When Product Updated"**:
   - Cấu hình Shopify OAuth2 API credentials
   - Đảm bảo webhook đã được kích hoạt trong Shopify

2. **Node "Search Product by Barcode" và "Find Product to Update"**:
   - Cấu hình Odoo API credentials
   - Chỉnh sửa truy vấn để tìm kiếm sản phẩm theo mã vạch (barcode)
   - Đảm bảo trường barcode đã được thiết lập trong cả hai hệ thống

3. **Node "Get Product Category"**:
   - Cấu hình Odoo API credentials
   - Chỉnh sửa truy vấn để lấy thông tin danh mục sản phẩm
   - Đảm bảo mapping giữa danh mục Shopify và Odoo đã được thiết lập đúng

4. **Node "Download Product Image"**:
   - Đảm bảo URL hình ảnh sản phẩm có sẵn và truy cập được
   - Có thể cần cấu hình proxy nếu hình ảnh bị chặn

5. **Node "Create Product in Odoo" và "Update Product in Odoo"**:
   - Cấu hình Odoo API credentials
   - Chỉnh sửa các trường dữ liệu cần đồng bộ (title, price, description, etc.)
   - Đảm bảo mapping giữa các trường dữ liệu của Shopify và Odoo

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo qua Slack/Telegram khi đồng bộ thành công hoặc thất bại
- Lưu log các hoạt động đồng bộ để theo dõi và kiểm tra
- Thiết lập báo cáo định kỳ về số lượng sản phẩm đã đồng bộ
- Kết hợp với các workflow khác để tự động xử lý đơn hàng sau khi sản phẩm được đồng bộ
- Thêm bước xác thực dữ liệu trước khi đồng bộ để giảm thiểu lỗi

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc đồng bộ sản phẩm giữa Shopify và Odoo, giúp các sếp tiết kiệm thời gian và giảm thiểu sai sót thủ công. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quản lý doanh nghiệp.