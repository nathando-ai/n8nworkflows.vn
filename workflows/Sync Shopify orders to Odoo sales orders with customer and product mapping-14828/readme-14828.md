---
title: "🚀 Tự động đồng bộ đơn hàng Shopify sang Odoo với ánh xạ khách hàng và sản phẩm"
description: "Hướng dẫn chi tiết cách tự động đồng bộ đơn hàng từ Shopify sang Odoo với ánh xạ khách hàng và sản phẩm, tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-don-hang-shopify-sang-odoo"
tags: [n8n, automation, no-code, shopify, odoo]
keywords: [n8n workflow, tự động hóa, shopify odoo, đồng bộ đơn hàng, crm]
---

# 🚀 Tự động đồng bộ đơn hàng Shopify sang Odoo với ánh xạ khách hàng và sản phẩm

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ đơn hàng từ Shopify sang Odoo trong vòng vài giây
- Tiết kiệm 80% thời gian xử lý đơn hàng thủ công
- Giảm thiểu lỗi nhập liệu do thủ công
- Đồng bộ thông tin khách hàng và sản phẩm một cách chính xác
- Tạo đơn hàng ở trạng thái nháp trong Odoo để kiểm tra trước khi xác nhận
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền quản trị
- Tài khoản Odoo với quyền tạo đơn hàng và quản lý khách hàng
- API keys cho cả Shopify và Odoo
- Sản phẩm Shipping đã được cấu hình trong Odoo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14828](https://n8n.io/workflows/14828)
2. Nhấn nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Shopify Webhook**:
   - Cấu hình webhook trong Shopify Admin > Notifications > Webhooks
   - Chọn sự kiện "Order Creation"
   - Điền URL webhook: `https://your-n8n-domain.com/webhook/shopify-order-webhook`

2. **Odoo Credentials**:
   - Tạo credentials mới trong n8n cho Odoo
   - Điền thông tin kết nối Odoo (URL, database, username, password)

3. **Shipping Product**:
   - Mở node "Add Shipping to Order"
   - Thay đổi `product_id: 16` thành ID sản phẩm Shipping tương ứng trong Odoo của bạn

4. **Sales Order Details**:
   - Mở node "Create Sales Order in Odoo"
   - Điều chỉnh các tham số sau để phù hợp với hệ thống của bạn:
     - `pricelist_id`: ID bảng giá mặc định
     - `user_id`: ID người dùng chịu trách nhiệm đơn hàng
     - `source_id`: ID nguồn đơn hàng

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu đơn hàng Shopify
2. Kiểm tra kết quả trong Odoo để đảm bảo thông tin đồng bộ chính xác
3. Bật Active workflow để bắt đầu đồng bộ tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi có đơn hàng mới được đồng bộ
2. **Lưu log hoạt động**: Thêm node ghi log các đơn hàng đã xử lý để theo dõi
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo hàng ngày về các đơn hàng đã đồng bộ
4. **Xử lý đơn hàng lỗi**: Thêm node xử lý các đơn hàng không đồng bộ thành công để thử lại sau

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý đơn hàng giữa Shopify và Odoo. Với khả năng tự động hóa hoàn toàn, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong kinh doanh. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của đội ngũ!