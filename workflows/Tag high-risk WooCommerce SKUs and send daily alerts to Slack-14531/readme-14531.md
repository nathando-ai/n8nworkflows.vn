---
title: "🚀 Tự động phân loại sản phẩm WooCommerce theo mức độ rủi ro và cảnh báo Slack hàng ngày"
description: "Workflow n8n tự động phân tích bán hàng 14 ngày gần nhất, đánh giá mức độ rủi ro tồn kho và gửi cảnh báo Slack hàng ngày cho đội ngũ quản lý"
slug: "tu-dong-phan-loai-san-pham-woocommerce-theo-muc-do-rui-ro"
tags: [n8n, automation, no-code, woocommerce, slack]
keywords: [n8n workflow, tự động hóa, woocommerce tồn kho, cảnh báo slack, quản lý bán hàng]
---

# 🚀 Tự động phân loại sản phẩm WooCommerce theo mức độ rủi ro và cảnh báo Slack hàng ngày

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công tình trạng tồn kho của hàng nghìn sản phẩm trên WooCommerce. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ phân tích bán hàng đến cảnh báo rủi ro chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân tích 14 ngày bán hàng mỗi ngày
- **Chính xác cao**: Phân loại sản phẩm theo 4 mức độ rủi ro (OK, Watchlist, High-Risk, Critical)
- **Cảnh báo tức thời**: Gửi báo cáo Slack hàng ngày với thông tin chi tiết
- **Quản lý tập trung**: Tất cả sản phẩm rủi ro được gắn tag trong WooCommerce
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API
- Các tag sản phẩm đã được tạo trong WooCommerce (Watchlist, High-Risk, Critical)
- Tài khoản Slack với quyền gửi tin nhắn vào kênh
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14531](https://n8n.io/workflows/14531)
2. Click "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily inventory risk check"**:
   - Cấu hình thời gian chạy hàng ngày (mặc định: 00:00)

2. **Node "Get last 14 days orders"**:
   - Kiểm tra credentials WooCommerce đã được cấu hình
   - Đảm bảo API có quyền truy cập vào đơn hàng

3. **Node "Calculate Sales & Risk level"**:
   - Điều chỉnh các ngưỡng phân loại rủi ro nếu cần:
     ```javascript
     // Mức độ rủi ro được tính dựa trên số lượng bán trong 14 ngày
     if (unitsSold < 5) {
       riskLevel = "OK";
     } else if (unitsSold < 15) {
       riskLevel = "Watchlist";
     } else if (unitsSold < 25) {
       riskLevel = "High-Risk";
     } else {
       riskLevel = "Critical";
     }
     ```

4. **Node "Notify team for Inventory alert"**:
   - Cấu hình credentials Slack
   - Chọn kênh nhận cảnh báo
   - Kiểm tra định dạng tin nhắn trong node "Build slack alert message"

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra:
   - Các sản phẩm đã được gắn tag đúng mức độ rủi ro
   - Cảnh báo Slack được gửi thành công
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Telegram**: Thêm node gửi cảnh báo qua Telegram cho đội ngũ vận hành
2. **Lưu log hoạt động**: Thêm node lưu log vào Google Sheets để theo dõi lịch sử cảnh báo
3. **Cảnh báo email**: Thêm node gửi email báo cáo hàng tuần cho quản lý cấp cao
4. **Tích hợp với Google Analytics**: Kết nối với Google Analytics để phân tích thêm dữ liệu bán hàng

### 📌 Kết luận
Workflow này giúp các sếp WooCommerce tự động hóa toàn bộ quy trình quản lý tồn kho, giảm thiểu rủi ro và tăng hiệu quả quản lý. Với chỉ 5 phút cài đặt, các sếp có thể nhận được báo cáo hàng ngày về tình trạng tồn kho của cửa hàng một cách tự động và chính xác. Hãy áp dụng ngay để nâng cao hiệu quả kinh doanh của cửa hàng!