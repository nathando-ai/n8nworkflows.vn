---
title: "🚀 Tự động gửi thông báo đơn hàng WooCommerce qua WhatsApp với MoltFlow"
description: "Hướng dẫn tự động hóa gửi thông báo đơn hàng WooCommerce qua WhatsApp ngay khi có đơn hàng mới, tiết kiệm thời gian và tăng hiệu quả kinh doanh"
slug: "tu-dong-gui-thong-bao-don-hang-woocommerce-qua-whatsapp"
tags: [n8n, automation, no-code, woocommerce, whatsapp]
keywords: [n8n workflow, tự động hóa, woocommerce, whatsapp, thông báo đơn hàng]
---

# 🚀 Tự động gửi thông báo đơn hàng WooCommerce qua WhatsApp với MoltFlow

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng phải mất hàng giờ mỗi ngày để theo dõi đơn hàng WooCommerce và gửi thông báo thủ công qua WhatsApp. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong 5 phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần theo dõi đơn hàng thủ công
- Tăng hiệu quả kinh doanh: Nhận thông báo ngay khi có đơn hàng mới
- Tăng cường tương tác: Gửi thông báo tự động đến khách hàng
- Hoạt động liên tục: Không bị lỡ đơn hàng nào
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce
- Tài khoản MoltFlow (để gửi WhatsApp)
- API Key của MoltFlow
- Số điện thoại của chủ cửa hàng (để nhận thông báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" và nhập URL: `https://n8n.io/workflows/13487`
3. Hoặc copy/paste JSON từ link trên vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node WooCommerce Webhook**:
   - Đảm bảo đã cấu hình webhook trong WooCommerce:
     - Vào WooCommerce → Settings → Advanced → Webhooks
     - Thêm webhook mới với event là "Order created"
     - Điền URL webhook từ n8n (sẽ được hiển thị sau khi kích hoạt node này)

2. **Node Format Order**:
   - Cần cấu hình 2 biến môi trường:
     - `YOUR_SESSION_ID`: ID phiên của bạn trong MoltFlow
     - `OWNER_PHONE`: Số điện thoại của chủ cửa hàng để nhận thông báo

3. **Node Send WhatsApp**:
   - Cần cấu hình credentials:
     - Tạo mới credential loại "HTTP Header Auth"
     - Điền API Key của MoltFlow vào trường "Header Value"

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu nhận thông báo đơn hàng mới

### ✍️ Mẹo & gợi ý nâng cao
- Có thể thêm node gửi thông báo đến khách hàng ngay sau khi đơn hàng được tạo
- Có thể lưu log chi tiết đơn hàng vào Google Sheets để theo dõi
- Có thể kết hợp với Slack để nhận thông báo trên kênh Slack
- Có thể gửi báo cáo hàng ngày về số lượng đơn hàng mới

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình nhận thông báo đơn hàng WooCommerce qua WhatsApp chỉ trong 5 phút. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả kinh doanh!