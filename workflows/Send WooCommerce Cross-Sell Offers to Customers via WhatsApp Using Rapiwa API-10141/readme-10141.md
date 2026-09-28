---
title: "🚀 Tự động gửi ưu đãi WooCommerce qua WhatsApp bằng Rapiwa API"
description: "Hướng dẫn tự động hóa gửi tin nhắn ưu đãi sản phẩm WooCommerce qua WhatsApp cho khách hàng tiềm năng bằng n8n và Rapiwa API"
slug: "tu-dong-gui-uu-dai-woocommerce-qua-whatsapp-rapiwa-api"
tags: [n8n, automation, no-code, woocommerce, whatsapp]
keywords: [n8n workflow, tự động hóa, woocommerce, whatsapp, rapiwa]
---

# 🚀 Tự động gửi ưu đãi WooCommerce qua WhatsApp bằng Rapiwa API

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quá trình gửi tin nhắn ưu đãi
- Tăng doanh thu: Gửi chính xác sản phẩm phù hợp với khách hàng
- Tăng tương tác: Gửi tin nhắn cá nhân hóa qua WhatsApp
- Dễ quản lý: Theo dõi kết quả gửi tin qua Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API
- Tài khoản Rapiwa với token hợp lệ
- Tài khoản Google với quyền truy cập Google Sheets
- Dữ liệu sản phẩm WooCommerce có cấu hình liên quan (upsell/cross-sell)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Chọn "Import from URL" và dán link: https://n8n.io/workflows/10141
3. Hoặc copy nội dung JSON từ file workflow và chọn "Import from JSON"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Get many customers** (wooCommerce node):
   - Chọn credentials WooCommerce API
   - Đảm bảo tài khoản có quyền truy cập khách hàng

2. **Schedule Trigger**:
   - Cấu hình thời gian gửi tin (hàng ngày/hàng tuần)
   - Thiết lập thời gian phù hợp với chiến dịch

3. **Code (get paying_customer)**:
   - Kiểm tra logic lọc khách hàng đã mua
   - Điều chỉnh nếu sử dụng trường dữ liệu khác

4. **Code (clean data)**:
   - Kiểm tra logic xử lý dữ liệu sản phẩm
   - Đảm bảo dữ liệu đầu ra phù hợp với template tin nhắn

5. **Check valid whatsapp number Using Rapiwa**:
   - Cấu hình credentials Rapiwa API
   - Đảm bảo token hợp lệ và có quyền truy cập

6. **Rapiwa Sender**:
   - Cấu hình template tin nhắn
   - Thay đổi nội dung tin nhắn theo thương hiệu

7. **Save State of Rows in Verified & Sent** (googleSheets node):
   - Cấu hình credentials Google Sheets
   - Điền Sheet ID từ Google Sheets mẫu

8. **Save State of Rows in Unverified & Not sent** (googleSheets node):
   - Cấu hình tương tự node trên

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu
2. Kiểm tra kết quả gửi tin trên Google Sheets
3. Bật Active workflow khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi gửi tin
- Thêm node lưu log chi tiết các bước xử lý
- Tạo báo cáo định kỳ về hiệu quả chiến dịch
- Thiết lập nhiều template tin nhắn khác nhau cho các nhóm khách hàng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình gửi ưu đãi sản phẩm qua WhatsApp, tăng tương tác với khách hàng và tối ưu hóa chiến dịch marketing. Bắt đầu áp dụng ngay để nâng cao hiệu quả kinh doanh!