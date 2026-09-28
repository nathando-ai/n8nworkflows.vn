---
title: "🚀 Tự động đồng bộ sản phẩm mới từ Shopify sang Odoo - Giải pháp tiết kiệm thời gian 100% không code"
description: "Hướng dẫn chi tiết cách tự động đồng bộ sản phẩm mới từ Shopify sang Odoo bằng n8n, giúp tiết kiệm thời gian và giảm lỗi thủ công"
slug: "tu-dong-dong-bo-san-pham-moi-shopify-sang-odoo"
tags: [n8n, automation, no-code, shopify, odoo]
keywords: [n8n workflow, tự động hóa, shopify odoo, đồng bộ sản phẩm]
---

# 🚀 Tự động đồng bộ sản phẩm mới từ Shopify sang Odoo - Giải pháp tiết kiệm thời gian 100% không code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải đồng bộ thủ công sản phẩm giữa hai hệ thống Shopify và Odoo. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc đồng bộ sản phẩm mới
- Giảm thiểu lỗi thủ công trong quá trình đồng bộ dữ liệu
- Đồng bộ dữ liệu sản phẩm mới ngay lập tức khi có thay đổi trên Shopify
- Tự động hóa quy trình làm việc giữa hai hệ thống Shopify và Odoo
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Tài khoản Odoo với quyền truy cập API
- Access Token từ Shopify
- Thông tin kết nối Odoo (URL, Database, Username, Password)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Shopify Trigger** (Node đầu tiên):
   - Chọn credentials là "shopifyAccessTokenApi"
   - Điền Access Token từ Shopify
   - Chọn event là "Product Created" để kích hoạt khi có sản phẩm mới được tạo

2. **Odoo6** (Node thứ hai):
   - Chọn credentials là "odooApi"
   - Điền thông tin kết nối Odoo (URL, Database, Username, Password)
   - Chọn operation là "getAll" và resource là "custom" để lấy danh sách sản phẩm hiện có

3. **Filter2** (Node thứ ba):
   - Thiết lập điều kiện lọc để chỉ đồng bộ những sản phẩm mới chưa có trong Odoo
   - Ví dụ: Lọc theo trường "id" hoặc "title" của sản phẩm

4. **Code** (Node thứ tư):
   - Thiết lập mã JavaScript để xử lý dữ liệu trước khi đồng bộ
   - Ví dụ: Chuyển đổi định dạng dữ liệu, thêm thông tin bổ sung

5. **Odoo7** (Node cuối cùng):
   - Chọn credentials là "odooApi"
   - Điền thông tin kết nối Odoo (URL, Database, Username, Password)
   - Chọn resource là "custom" để tạo sản phẩm mới trong Odoo

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi đồng bộ thành công
- Lưu log các hoạt động đồng bộ để theo dõi và kiểm tra
- Thiết lập gửi báo cáo định kỳ về số lượng sản phẩm đã đồng bộ
- Tự động cập nhật thông tin sản phẩm khi có thay đổi trên Shopify

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc đồng bộ sản phẩm mới giữa Shopify và Odoo. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn và giảm thiểu lỗi thủ công. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của doanh nghiệp!