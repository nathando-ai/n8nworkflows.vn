---
title: "🚀 Tự động gửi thông báo đơn hàng Shopify lên WhatsApp qua WOZTELL"
description: "Hướng dẫn tự động hóa gửi thông báo đơn hàng và khách hàng Shopify lên WhatsApp thông qua WOZTELL, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-gui-thong-bao-don-hang-shopify-len-whatsapp-qua-woztell"
tags: [n8n, automation, no-code, shopify, whatsapp]
keywords: [n8n workflow, tự động hóa, shopify, whatsapp, woztell]
---

# 🚀 Tự động gửi thông báo đơn hàng Shopify lên WhatsApp qua WOZTELL

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình gửi thông báo đơn hàng và khách hàng lên WhatsApp
- Tiết kiệm thời gian xử lý thủ công
- Nâng cao trải nghiệm khách hàng với thông báo tức thì
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tích hợp dễ dàng với hệ thống Shopify hiện tại
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập admin
- Tài khoản n8n đã cài đặt và cấu hình
- Tài khoản WOZTELL đã kích hoạt WhatsApp Business Platform
- Template tin nhắn WhatsApp đã được phê duyệt trong WOZTELL
- API keys và credentials cho Shopify và WOZTELL
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [Shopify order and customer updates to WhatsApp via WOZTELL](https://n8n.io/workflows/13640)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Shopify Trigger Nodes** (3 nodes):
   - Shopify Trigger - Order Paid
   - Shopify Trigger - Customer Created
   - Shopify Trigger - Fulfillment Created
   - Cấu hình credentials cho Shopify
   - Đảm bảo các API scopes cần thiết đã được kích hoạt trong ứng dụng Shopify:
     - read_customer_events
     - read_customers
     - read_orders
     - read_fulfillments

2. **If Node**:
   - Kiểm tra xem khách hàng có số điện thoại không
   - Nếu không có số điện thoại, workflow sẽ dừng lại để tránh gửi lỗi

3. **Send message template Node** (WOZTELL):
   - Cấu hình credentials cho WOZTELL (woztellCredentialApi)
   - Chọn kênh gửi tin nhắn
   - Chọn template đã được phê duyệt
   - Mapping dữ liệu từ Shopify vào các biến trong template (ví dụ: tên khách hàng, số đơn hàng)
   - Để tạo access token cho WOZTELL, theo hướng dẫn [tại đây](https://support.woztell.com/portal/en/kb/articles/access-token#Access_Token_Generation)
   - Để tạo token cho Channel API, theo hướng dẫn [tại đây](https://support.woztell.com/portal/en/kb/articles/access-token-channels-in-woztell#How_to_Create_an_Access_Token_for_a_Channel_in_WOZTELL)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Sau khi kiểm tra thành công, bật Active workflow
3. Trong Shopify, chuyển webhook từ Test URL sang Production URL

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi các sự kiện Shopify trigger (đơn hàng được tạo, thanh toán, giao hàng, v.v.)
- Thêm các điều kiện trong node If
- Sử dụng các template WhatsApp khác nhau cho từng sự kiện
- Thêm các node bổ sung cho cảnh báo nội bộ (Slack/email) hoặc cập nhật CRM
- Thay thế trigger Shopify bằng trigger từ các nền tảng e-commerce khác như WooCommerce, Magento, hoặc webhook tùy chỉnh

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình gửi thông báo đơn hàng và khách hàng lên WhatsApp thông qua WOZTELL, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Với cấu hình đơn giản và tích hợp dễ dàng, workflow này là giải pháp hoàn hảo cho các doanh nghiệp muốn nâng cao hiệu quả giao tiếp với khách hàng.