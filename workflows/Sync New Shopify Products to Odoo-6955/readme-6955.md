```yaml
---
title: "🚀 Tự động đồng bộ sản phẩm Shopify mới sang Odoo - Không cần code"
description: "Hướng dẫn tự động hóa quy trình đồng bộ sản phẩm mới từ Shopify sang Odoo bằng n8n. Tiết kiệm thời gian và tránh lỗi thủ công."
slug: "tu-dong-dong-bo-san-pham-shopify-sang-odoo"
tags: [n8n, automation, no-code, shopify, odoo]
keywords: [n8n workflow, tự động hóa, đồng bộ sản phẩm, shopify odoo]
---

# 🚀 Tự động đồng bộ sản phẩm Shopify mới sang Odoo - Không cần code

[Các sếp] có biết không? Việc phải thủ công nhập sản phẩm mới từ Shopify sang Odoo mỗi ngày thật là mệt mỏi và dễ gây lỗi. Hãy để n8n làm việc này cho các sếp nhé! Workflow này sẽ tự động đồng bộ tất cả sản phẩm mới từ Shopify sang Odoo ngay khi chúng được thêm vào cửa hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập thủ công sản phẩm mới mỗi ngày
- **Giảm lỗi**: Tránh sai sót khi nhập liệu bằng tay
- **Đồng bộ thời gian thực**: Sản phẩm mới xuất hiện ngay trên Odoo ngay khi được thêm vào Shopify
- **Tự động hóa hoàn toàn**: Không cần can thiệp sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Odoo với quyền truy cập API
- API Key và API Secret từ Shopify
- URL của Odoo instance
- Database name của Odoo
- Username và password của tài khoản Odoo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6955](https://n8n.io/workflows/6955)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File"
4. Chọn file JSON vừa tải về và click "Open"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Shopify Trigger Node**:
   - Chọn credentials đã tạo cho Shopify
   - Đảm bảo webhook đã được kích hoạt trong Shopify

2. **Search for Existing Product in Odoo Node**:
   - Chọn credentials đã tạo cho Odoo
   - Điền đúng tên model Odoo (thường là "product.product")
   - Đảm bảo trường tìm kiếm là "default_code" hoặc trường tương ứng trong Odoo

3. **Create Odoo Product Node**:
   - Chọn credentials đã tạo cho Odoo
   - Điền đúng tên model Odoo (thường là "product.product")
   - Cấu hình các trường cần thiết để tạo sản phẩm mới

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow
3. Đảm bảo workflow đang ở trạng thái "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có sản phẩm mới được đồng bộ
- Thêm node để lưu log các sản phẩm đã được đồng bộ
- Tạo báo cáo định kỳ về số lượng sản phẩm đã được đồng bộ
- Kết hợp với các hệ thống khác như ERP để tự động cập nhật kho hàng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi khi đồng bộ sản phẩm từ Shopify sang Odoo. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của các sếp nhé! 🚀
```