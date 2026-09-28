---
title: "🚀 Tự động gửi tin nhắn WhatsApp quảng cáo sản phẩm mới từ WooCommerce với OpenAI và Google Sheets"
description: "Hướng dẫn tự động hóa gửi tin nhắn WhatsApp quảng cáo sản phẩm mới từ WooCommerce với OpenAI và Google Sheets, tiết kiệm thời gian và tăng hiệu quả marketing"
slug: "tu-dong-gui-tin-nhan-whatsapp-quang-cao-san-pham-moi-tu-woocommerce-voi-openai-va-google-sheets"
tags: [n8n, automation, no-code, whatsapp, openai, google-sheets]
keywords: [n8n workflow, tự động hóa, whatsapp marketing, openai, google sheets]
---

# 🚀 Tự động gửi tin nhắn WhatsApp quảng cáo sản phẩm mới từ WooCommerce với OpenAI và Google Sheets

[Các sếp đang gặp khó khăn khi phải gửi tin nhắn quảng cáo sản phẩm mới cho hàng nghìn khách hàng qua WhatsApp thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình, từ lọc dữ liệu khách hàng đến gửi tin nhắn cá nhân hóa với nội dung được tạo bởi OpenAI.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi tự động gửi tin nhắn cho hàng nghìn khách hàng
- Tăng độ cá nhân hóa với nội dung được tạo bởi OpenAI
- Theo dõi hiệu quả gửi tin nhắn qua Google Sheets
- Tự động xử lý các trường hợp không gửi được tin nhắn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với danh sách khách hàng
- Tài khoản Google với Google Sheets API đã kích hoạt
- Tài khoản OpenAI với API key
- Tài khoản Rapiwa với API key
- Số điện thoại WhatsApp Business API đã được đăng ký
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/13416)
2. Click vào nút "Copy Workflow Code"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán mã đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "WooCommerce Trigger"**:
   - Cấu hình credentials WooCommerce
   - Chọn event "Product Created" để kích hoạt workflow khi có sản phẩm mới

2. **Node "Get All Customer records from the WooCommerce store"**:
   - Cấu hình credentials WooCommerce
   - Đảm bảo có quyền truy cập vào danh sách khách hàng

3. **Node "Create the product description (HTML) into a short"**:
   - Cấu hình credentials OpenAI
   - Điều chỉnh prompt để tạo nội dung phù hợp với thương hiệu

4. **Node "Rapiwa (verify whatsapp number)" và "Rapiwa (send whatsapp message)"**:
   - Cấu hình credentials Rapiwa
   - Đảm bảo số điện thoại WhatsApp Business API đã được đăng ký

5. **Node "Save data in Sheet Verified & Sent1" và "Save data Sheet Unverified & Not sent1"**:
   - Cấu hình credentials Google Sheets
   - Tạo các sheet tương ứng trong Google Sheets
   - Cập nhật ID của Google Sheets và tên sheet trong node

6. **Node "Code (image link detect)"**:
   - Kiểm tra và điều chỉnh logic xử lý link ảnh nếu cần

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra các node Rapiwa để đảm bảo số điện thoại được xác minh và tin nhắn được gửi
3. Kiểm tra Google Sheets để đảm bảo dữ liệu được lưu đúng
4. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi workflow chạy
2. Thêm node lưu log để theo dõi hoạt động của workflow
3. Tạo báo cáo định kỳ về hiệu quả gửi tin nhắn từ Google Sheets
4. Tích hợp với các dịch vụ email marketing để gửi email đồng thời

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình gửi tin nhắn quảng cáo sản phẩm mới từ WooCommerce với nội dung được tạo bởi OpenAI và theo dõi hiệu quả qua Google Sheets. Hãy áp dụng ngay để tăng hiệu quả marketing và tiết kiệm thời gian đáng kể!