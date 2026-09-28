---
title: "🚀 Tự động gửi thông báo Telegram cho đơn hàng WooCommerce mới"
description: "Hướng dẫn tự động hóa gửi thông báo Telegram khi có đơn hàng WooCommerce mới, tiết kiệm thời gian và tăng hiệu quả quản lý đơn hàng"
slug: "tu-dong-gui-thong-bao-telegram-woocommerce-moi"
tags: [n8n, automation, no-code, woocommerce, telegram]
keywords: [n8n workflow, tự động hóa, woocommerce, telegram, đơn hàng mới]
---

# 🚀 Tự động gửi thông báo Telegram cho đơn hàng WooCommerce mới

[Các sếp đang quản lý cửa hàng online với WooCommerce chắc hẳn đã gặp khó khăn khi phải theo dõi đơn hàng mới một cách thủ công. Mỗi khi có đơn hàng mới, các sếp phải truy cập vào hệ thống, kiểm tra thông tin và gửi thông báo đến nhân viên. Việc này không chỉ tốn thời gian mà còn dễ gây lỗi và chậm trễ. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý đơn hàng lên tới 80%
- Nhận thông báo tức thì khi có đơn hàng mới
- Giảm thiểu lỗi do thủ công
- Hoạt động liên tục 24/7 không cần can thiệp
- Thông tin đơn hàng được hiển thị rõ ràng, dễ đọc
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce đã kích hoạt
- Tài khoản Telegram cá nhân
- Quyền quản trị trên hệ thống n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/2575](https://n8n.io/workflows/2575)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive WooCommerce Order"**:
   - Đảm bảo đường dẫn webhook duy nhất (path) không bị trùng với các workflow khác
   - Giữ nguyên phương thức HTTP là POST

2. **Node "Check if Order Status is Processing"**:
   - Kiểm tra biểu thức điều kiện đã được thiết lập đúng: `{{ $node["Receive WooCommerce Order"].json["status"] === "processing" }}`

3. **Node "Design Message Template"**:
   - Tùy chỉnh mẫu thông báo theo nhu cầu của các sếp
   - Có thể thêm các trường thông tin khác như tên khách hàng, số điện thoại, địa chỉ giao hàng...

4. **Node "Telegram"**:
   - Tạo credentials mới cho Telegram Bot
   - Nhập API Token đã nhận từ BotFather
   - Nhập Chat ID của kênh/nhóm Telegram muốn nhận thông báo

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Activate" để kích hoạt workflow
2. Thực hiện một đơn hàng thử nghiệm trên WooCommerce
3. Kiểm tra Telegram để xác nhận thông báo đến đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh thông báo**: Thêm các trường thông tin quan trọng như giá trị đơn hàng, phương thức thanh toán, ghi chú của khách hàng...
2. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo đồng thời trên cả Telegram và Slack
3. **Lọc đơn hàng**: Thêm điều kiện lọc để chỉ nhận thông báo cho các đơn hàng có giá trị cao hơn ngưỡng nhất định
4. **Gửi báo cáo định kỳ**: Thêm node để tổng hợp và gửi báo cáo hàng ngày về số lượng đơn hàng mới

### 📌 Kết luận
Workflow này giúp các sếp quản lý cửa hàng WooCommerce một cách hiệu quả hơn bằng cách tự động hóa toàn bộ quá trình nhận thông báo đơn hàng mới. Với việc nhận thông báo tức thì và thông tin chi tiết, các sếp có thể xử lý đơn hàng nhanh chóng và chính xác hơn. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh của cửa hàng!