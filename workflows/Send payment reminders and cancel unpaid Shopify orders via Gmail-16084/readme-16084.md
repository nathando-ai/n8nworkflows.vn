---
title: "💳 Tự động nhắc nhở thanh toán và hủy đơn hàng chưa thanh toán Shopify qua Gmail"
description: "Hướng dẫn tự động hóa quy trình nhắc nhở thanh toán và hủy đơn hàng chưa thanh toán Shopify thông qua n8n và Gmail, tiết kiệm thời gian và tăng hiệu quả quản lý đơn hàng."
slug: "tu-dong-nhac-nho-thanh-toan-va-huy-don-hang-shopify-qua-gmail"
tags: [n8n, automation, no-code, Shopify, email]
keywords: [n8n workflow, tự động hóa, Shopify, email, nhắc nhở thanh toán]
---

# 💳 Tự động nhắc nhở thanh toán và hủy đơn hàng chưa thanh toán Shopify qua Gmail

[Các sếp đang gặp khó khăn khi phải theo dõi và nhắc nhở khách hàng về các đơn hàng chưa thanh toán một cách thủ công. Việc này tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình nhắc nhở và hủy đơn hàng chưa thanh toán thông qua n8n và Gmail.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý đơn hàng chưa thanh toán.
- Tăng hiệu quả nhắc nhở và giảm tỷ lệ đơn hàng không thanh toán.
- Tự động hủy đơn hàng quá hạn và giải phóng hàng tồn kho.
- Nhận báo cáo hàng ngày về tình trạng đơn hàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API.
- Tài khoản Gmail để gửi email nhắc nhở và báo cáo.
- Thông tin xác thực HTTP Header Authentication cho Shopify.
- Thông tin xác thực OAuth2 cho Gmail.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấp vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/16084](https://n8n.io/workflows/16084).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Set Workflow Config"**: Thay đổi `storeDomain` thành tên miền Shopify của bạn (ví dụ: `yourstore.myshopify.com`).
- **Node "Daily Schedule Trigger"**: Đặt thời gian chạy workflow hàng ngày (mặc định là 8 AM).
- **Node "Fetch Unpaid Shopify Orders"**: Cấu hình thông tin xác thực HTTP Header Authentication cho Shopify.
- **Node "Send Error Notification"**, **Node "Send Cancellation Email"**, **Node "Send Reminder Email"**, **Node "Send Daily Report to Admin"**: Cấu hình thông tin xác thực OAuth2 cho Gmail.
- **Node "Set Workflow Config"**: Cập nhật `adminEmail` với địa chỉ email của quản lý cửa hàng để nhận báo cáo và thông báo lỗi.

#### 3. Kích hoạt ⚡️
- Kiểm tra workflow bằng cách chạy thử dữ liệu mẫu.
- Bật workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh thời gian nhắc nhở**: Thay đổi các giá trị `reminder1Days`, `reminder2Days`, `reminder3Days`, và `cancelDays` trong node "Set Workflow Config" để điều chỉnh thời gian nhắc nhở và hủy đơn hàng.
- **Giới hạn số lượng đơn hàng**: Thay đổi giá trị `fetchOrdersLimit` trong node "Set Workflow Config" để điều chỉnh số lượng đơn hàng được xử lý trong mỗi lần chạy.
- **Kết hợp với Slack**: Thêm node Slack để nhận thông báo lỗi và báo cáo hàng ngày.
- **Lưu log chi tiết**: Thêm node lưu log chi tiết vào cơ sở dữ liệu để theo dõi lịch sử đơn hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình nhắc nhở thanh toán và hủy đơn hàng chưa thanh toán Shopify thông qua n8n và Gmail. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian, tăng hiệu quả quản lý đơn hàng và giảm tỷ lệ đơn hàng không thanh toán.