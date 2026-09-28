---
title: "💰 Tự động đồng bộ giá sản phẩm Shopify & WooCommerce với cảnh báo giá"
description: "Workflow n8n giúp tự động đồng bộ giá sản phẩm giữa Shopify và WooCommerce, cảnh báo giá giảm lớn và lưu log thay đổi giá. Tiết kiệm thời gian và tránh sai sót giá."
slug: "tu-dong-dong-bo-gia-shopify-woocommerce"
tags: [n8n, automation, no-code, ecommerce, shopify, woocommerce]
keywords: [n8n workflow, tự động hóa giá sản phẩm, đồng bộ giá Shopify WooCommerce, cảnh báo giá giảm, lưu log giá]
---

# 💰 Tự động đồng bộ giá sản phẩm giữa Shopify & WooCommerce với cảnh báo giá

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ giá sản phẩm giữa 2 nền tảng Shopify và WooCommerce
- Cảnh báo giá giảm lớn thông qua email
- Lưu log thay đổi giá vào Google Sheets
- Tiết kiệm thời gian và tránh sai sót giá
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify và WooCommerce
- Tài khoản Google với Google Sheets và Gmail
- API keys cho Shopify, WooCommerce và Google
- Biết cách tạo và quản lý credentials trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12902](https://n8n.io/workflows/12902)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Shopify Price Update** (shopifyTrigger):
   - Cấu hình credentials: `shopifyAccessTokenApi`
   - Thiết lập để lắng nghe sự kiện `product.updated`

2. **WooCommerce Price Update** (wooCommerceTrigger):
   - Cấu hình credentials: `wooCommerceApi`
   - Thiết lập để lắng nghe sự kiện `product.updated`

3. **Shopify Configuration** (set):
   - Thiết lập `priceChangeThreshold` cho Shopify (ví dụ: 500)

4. **WooCommerce Configuration** (set):
   - Thiết lập `priceChangeThreshold` cho WooCommerce (ví dụ: 150)

5. **Log Price Changes** (googleSheets):
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tên sheet là `Price_Changes_Log`
   - Đảm bảo sheet có các cột: `Product ID`, `Platform`, `Old Price`, `New Price`, `Change Percentage`, `Timestamp`

6. **Notify Team - Sync Complete** (gmail):
   - Cấu hình credentials: `gmailOAuth2`
   - Thiết lập địa chỉ email nhận thông báo

7. **Alert Team - Major Price Drop** (gmail):
   - Cấu hình credentials: `gmailOAuth2`
   - Thiết lập địa chỉ email nhận cảnh báo giá giảm lớn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách kích hoạt các trigger
2. Kiểm tra log trong Google Sheets
3. Kiểm tra email nhận thông báo và cảnh báo
4. Bật Active workflow khi đã kiểm tra và xác nhận hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm cảnh báo qua Slack hoặc Telegram bằng cách kết nối với các node tương ứng
- Tạo báo cáo định kỳ về thay đổi giá bằng cách kết hợp với node scheduleTrigger
- Thiết lập các quy tắc giá khác nhau cho các danh mục sản phẩm khác nhau
- Kết nối với các hệ thống CRM khác để cập nhật giá tự động

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ giá sản phẩm giữa Shopify và WooCommerce, cảnh báo giá giảm lớn và lưu log thay đổi giá. Với việc tự động hóa quy trình này, các sếp có thể tiết kiệm thời gian và tránh sai sót giá, đồng thời đảm bảo giá sản phẩm trên cả hai nền tảng luôn đồng bộ và chính xác. Hãy áp dụng ngay để tối ưu hóa quy trình kinh doanh của bạn!