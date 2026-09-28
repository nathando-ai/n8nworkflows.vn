---
title: "🚀 Gửi mã giảm giá WooCommerce tới khách hàng qua WhatsApp bằng Rapiwa API"
description: "Tự động hóa gửi mã giảm giá WooCommerce tới khách hàng qua WhatsApp bằng Rapiwa API, tiết kiệm thời gian và tăng doanh số bán hàng"
slug: "gui-ma-giam-gia-woocommerce-qua-whatsapp-rapiwa-api"
tags: [n8n, automation, no-code, woocommerce, whatsapp]
keywords: [n8n workflow, tự động hóa, woocommerce, whatsapp, mã giảm giá]
---

# 🚀 Gửi mã giảm giá WooCommerce tới khách hàng qua WhatsApp bằng Rapiwa API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho nhân viên marketing
- Tăng tỷ lệ chuyển đổi bằng cách gửi mã giảm giá cá nhân hóa tới khách hàng
- Tự động hóa quy trình gửi tin nhắn qua WhatsApp
- Theo dõi trạng thái gửi mã giảm giá thông qua Google Sheets
- Tăng doanh số bán hàng bằng cách thúc đẩy khách hàng sử dụng mã giảm giá
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API
- Tài khoản Rapiwa và API key hợp lệ
- Tài khoản Google với quyền truy cập Google Sheets
- Dữ liệu khách hàng trong WooCommerce bao gồm số điện thoại
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang workflow gốc: [https://n8n.io/workflows/10140](https://n8n.io/workflows/10140)
2. Click vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về
4. Hoặc copy toàn bộ nội dung JSON và paste vào ô "Import from JSON" trong n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node WooCommerce Trigger**:
   - Cấu hình credentials WooCommerce API
   - Đảm bảo webhook `coupon.created` được kích hoạt trong WooCommerce

2. **Node Clean WhatsApp Number**:
   - Kiểm tra trường dữ liệu chứa số điện thoại (thường là `billing.phone`)

3. **Node Check valid whatsapp number Using Rapiwa**:
   - Cấu hình credentials HTTP Bearer với API key của Rapiwa
   - Đảm bảo endpoint API của Rapiwa là chính xác: `https://app.rapiwa.com/api/verify-whatsapp`

4. **Node Send Message Using Rapiwa**:
   - Cấu hình credentials HTTP Bearer với API key của Rapiwa
   - Chỉnh sửa nội dung tin nhắn để phù hợp với thương hiệu và mã giảm giá
   - Đảm bảo endpoint API của Rapiwa là chính xác: `https://app.rapiwa.com/api/send-message`

5. **Node Save State of Rows in Verified & Sent**:
   - Cấu hình credentials Google Sheets OAuth2
   - Thay đổi ID của Google Sheet và tên sheet phù hợp với dữ liệu của bạn
   - Đảm bảo các cột trong Google Sheet phù hợp với dữ liệu được lưu

6. **Node Save State of Rows in Unerified & Not sent**:
   - Cấu hình credentials Google Sheets OAuth2
   - Thay đổi ID của Google Sheet và tên sheet phù hợp với dữ liệu của bạn
   - Đảm bảo các cột trong Google Sheet phù hợp với dữ liệu được lưu

#### 3. Kích hoạt ⚡️
1. Kiểm tra cấu hình của tất cả các node
2. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
3. Kích hoạt workflow bằng cách click vào nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung tin nhắn**: Chỉnh sửa nội dung tin nhắn trong node "Send Message Using Rapiwa" để phù hợp với thương hiệu và mã giảm giá
2. **Thêm điều kiện gửi**: Sử dụng node "If" để thêm các điều kiện gửi tin nhắn (ví dụ: chỉ gửi tới khách hàng đã mua hàng trong 30 ngày qua)
3. **Tích hợp với các kênh khác**: Kết nối với Slack hoặc Telegram để nhận thông báo khi gửi tin nhắn thành công
4. **Lập lịch gửi**: Sử dụng node "Wait" để lập lịch gửi tin nhắn vào thời gian cụ thể

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình gửi mã giảm giá WooCommerce tới khách hàng qua WhatsApp bằng Rapiwa API, tiết kiệm thời gian và tăng doanh số bán hàng. Bằng cách sử dụng Google Sheets để theo dõi trạng thái gửi mã giảm giá, các sếp có thể tối ưu hóa chiến dịch marketing và tăng tỷ lệ chuyển đổi. Hãy áp dụng ngay workflow này để nâng cao hiệu quả kinh doanh của bạn!