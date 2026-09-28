---
title: "🚀 Tự động theo dõi hàng tồn kho WooCommerce và cảnh báo nhập hàng qua Gmail & Slack"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp các sếp theo dõi hàng tồn kho WooCommerce, tính toán lượng hàng cần nhập và gửi cảnh báo qua email và Slack một cách tự động."
slug: "tu-dong-theo-doi-hang-ton-kho-woocommerce"
tags: [n8n, automation, no-code, woocommerce, inventory]
keywords: [n8n workflow, tự động hóa, quản lý hàng tồn kho, cảnh báo nhập hàng, WooCommerce]
---

# 🚀 Tự động theo dõi hàng tồn kho WooCommerce và cảnh báo nhập hàng qua Gmail & Slack

[Các sếp] có bao giờ phải mất hàng giờ mỗi ngày để theo dõi hàng tồn kho WooCommerce và tính toán lượng hàng cần nhập không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng vài phút, tiết kiệm thời gian quý giá và giảm thiểu lỗi con người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình theo dõi hàng tồn kho và tính toán nhập hàng.
- **Chính xác**: Giảm thiểu lỗi con người trong việc tính toán lượng hàng cần nhập.
- **Cá nhân hóa**: Cảnh báo nhập hàng được gửi theo từng sản phẩm, phù hợp với nhu cầu cụ thể.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình đã đặt, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API.
- Tài khoản Gmail với quyền truy cập OAuth2.
- Tài khoản Slack với quyền truy cập API.
- Thông tin về lead time (thời gian giao hàng) và safety stock (hàng tồn kho dự phòng) cho từng sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12874](https://n8n.io/workflows/12874) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.
3. Hoặc copy toàn bộ nội dung JSON từ trang web và paste vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Inventory Check"**: Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 9h sáng).
- **Node "Fetch Orders"**: Cấu hình credentials WooCommerce API và chọn operation "getAll" cho resource "order".
- **Node "Fetch Products"**: Cấu hình credentials WooCommerce API và chọn operation "getAll".
- **Node "Send Email"**: Cấu hình credentials Gmail OAuth2 và điền địa chỉ email người nhận.
- **Node "Slack Alert"**: Cấu hình credentials Slack API và chọn channel để gửi cảnh báo.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Google Sheets" để lưu lịch sử cảnh báo nhập hàng.
- Kết hợp với node "Telegram" để nhận cảnh báo qua ứng dụng này.
- Tạo báo cáo hàng tuần về tình trạng hàng tồn kho và lượng hàng đã nhập.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi hàng tồn kho WooCommerce và cảnh báo nhập hàng một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu suất làm việc!