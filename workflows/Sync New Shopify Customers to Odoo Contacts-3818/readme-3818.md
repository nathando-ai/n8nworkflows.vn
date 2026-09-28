```yaml
---
title: "🚀 Tự động đồng bộ khách hàng mới từ Shopify sang Odoo - Giải pháp tiết kiệm thời gian 100%"
description: "Hướng dẫn chi tiết cách tự động đồng bộ khách hàng mới từ Shopify sang Odoo bằng n8n, giúp tiết kiệm thời gian và tránh lỗi thủ công"
slug: "tu-dong-dong-bo-khach-hang-moi-shopify-sang-odoo"
tags: [n8n, automation, no-code, shopify, odoo]
keywords: [n8n workflow, tự động hóa, shopify odoo, đồng bộ khách hàng]
---
```

# 🚀 Tự động đồng bộ khách hàng mới từ Shopify sang Odoo - Giải pháp tiết kiệm thời gian 100%

[Các sếp đang gặp khó khăn khi phải thủ công nhập liệu khách hàng mới từ Shopify sang Odoo hàng ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, đảm bảo dữ liệu luôn đồng bộ và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày với việc tự động đồng bộ khách hàng mới
- Giảm thiểu lỗi nhập liệu thủ công
- Dữ liệu khách hàng luôn đồng bộ giữa Shopify và Odoo
- Tự động hóa quy trình marketing và bán hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Odoo với quyền truy cập API
- Access Token từ Shopify
- Credentials Odoo API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io](https://n8n.io) và đăng nhập
2. Nhấn vào "Workflows" trên thanh điều hướng
3. Chọn "Import from URL" và nhập link: https://n8n.io/workflows/3818
4. Hoặc copy/paste nội dung JSON từ link trên vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Shopify Trigger Node**:
   - Chọn credentials là "shopifyAccessTokenApi"
   - Đảm bảo đã cấp quyền truy cập "read_customers" cho token

2. **Search Odoo Contact Node**:
   - Chọn credentials là "odooApi"
   - Điền "odoo.model" là "res.partner" (mặc định cho contacts trong Odoo)
   - Đảm bảo đã cấu hình đúng endpoint API trong credentials

3. **Create Contact Node**:
   - Chọn credentials là "odooApi"
   - Điền "odoo.model" là "res.partner"
   - Cấu hình các trường dữ liệu cần đồng bộ (thường là email, tên, số điện thoại)

4. **Filter Node**:
   - Cấu hình điều kiện lọc để chỉ xử lý khách hàng mới (ví dụ: created_at > ngày bắt đầu theo dõi)

5. **Code Node**:
   - Kiểm tra và điều chỉnh logic xử lý dữ liệu nếu cần (mặc định đã xử lý chuyển đổi dữ liệu từ Shopify sang Odoo)

#### 3. Kích hoạt ⚡️
1. Nhấn "Execute Node" để test với dữ liệu mẫu
2. Kiểm tra kết quả trên Odoo để đảm bảo dữ liệu được đồng bộ chính xác
3. Chuyển workflow sang trạng thái "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi có khách hàng mới được đồng bộ
- Kết hợp với Slack để nhận thông báo tức thời
- Thêm node lưu log hoạt động để theo dõi hiệu suất workflow
- Tự động gửi email chào mừng khách hàng mới (kết hợp với node Mailchimp hoặc SendGrid)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá, giảm thiểu lỗi và đảm bảo dữ liệu khách hàng luôn đồng bộ giữa Shopify và Odoo. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh!