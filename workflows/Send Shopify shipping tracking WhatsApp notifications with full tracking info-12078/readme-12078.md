---
title: "🚀 Tự động gửi thông báo vận chuyển Shopify qua WhatsApp với đầy đủ thông tin tracking"
description: "Hướng dẫn chi tiết cách tự động hóa thông báo vận chuyển Shopify qua WhatsApp bằng n8n, bao gồm cập nhật trạng thái đơn hàng, thông tin tracking và hỗ trợ đa ngôn ngữ."
slug: "tu-dong-gui-thong-bao-van-chuyen-shopify-qua-whatsapp"
tags: [n8n, automation, no-code, Shopify, WhatsApp]
keywords: [n8n workflow, tự động hóa, Shopify, WhatsApp, thông báo vận chuyển]
---

# 🚀 Tự động gửi thông báo vận chuyển Shopify qua WhatsApp với đầy đủ thông tin tracking

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý thủ công
- Cập nhật thông tin vận chuyển tự động cho khách hàng
- Hỗ trợ đa ngôn ngữ (Tiếng Anh và Ả Rập)
- Bảo vệ số điện thoại test khỏi gửi tin nhắn
- Cung cấp thông tin tracking đầy đủ cho khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Shopify với quyền truy cập API
- Cơ sở dữ liệu PostgreSQL với bảng orders và customers
- Tài khoản WhatsApp Business API
- Các thông tin xác thực (credentials) cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và nhập link: https://n8n.io/workflows/12078
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "fulfilment" (Shopify Trigger)**
   - Cấu hình credentials "shopifyAccessTokenApi" với thông tin Shopify của bạn
   - Đảm bảo webhook được kích hoạt trong Shopify

2. **Node "Update Order Shipped1" (PostgreSQL)**
   - Cấu hình credentials "postgres" với thông tin kết nối PostgreSQL
   - Cập nhật câu truy vấn để phù hợp với cấu trúc bảng orders của bạn

3. **Node "Select rows from a table6" (PostgreSQL)**
   - Cấu hình credentials "postgres" với thông tin kết nối PostgreSQL
   - Cập nhật câu truy vấn để phù hợp với cấu trúc bảng orders của bạn

4. **Node "Get Customer1" (PostgreSQL)**
   - Cấu hình credentials "postgres" với thông tin kết nối PostgreSQL
   - Cập nhật câu truy vấn để phù hợp với cấu trúc bảng customers của bạn

5. **Node "WhatsApp Shipped AR" (HTTP Request)**
   - Cấu hình credentials "httpBearerAuth" với token WhatsApp Business API
   - Cập nhật nội dung tin nhắn theo mẫu tiếng Ả Rập của bạn
   - Đảm bảo số điện thoại được định dạng đúng (loại bỏ dấu '+' trước số)

6. **Node "WhatsApp Shipped EN1" (HTTP Request)**
   - Cấu hình credentials "httpBearerAuth" với token WhatsApp Business API
   - Cập nhật nội dung tin nhắn theo mẫu tiếng Anh của bạn
   - Đảm bảo số điện thoại được định dạng đúng (loại bỏ dấu '+' trước số)

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log các tin nhắn đã gửi
- Kết hợp với Slack để nhận thông báo khi có lỗi xảy ra
- Thêm chức năng gửi báo cáo hàng ngày về số lượng tin nhắn đã gửi
- Tích hợp với hệ thống CRM để theo dõi tương tác của khách hàng

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quá trình gửi thông báo vận chuyển qua WhatsApp cho Shopify, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Các sếp hãy thử áp dụng ngay để tối ưu hóa quy trình vận hành của mình!