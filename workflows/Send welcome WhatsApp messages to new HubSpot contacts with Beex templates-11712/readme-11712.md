---
title: "🚀 Tự động gửi tin nhắn chào mừng WhatsApp cho khách hàng mới từ HubSpot với Beex"
description: "Hướng dẫn chi tiết cách tự động gửi tin nhắn chào mừng WhatsApp cho khách hàng mới từ HubSpot bằng n8n và Beex. Tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-gui-tin-nhan-chao-mung-whatsapp-hubspot-beex"
tags: [n8n, automation, no-code, hubspot, whatsapp]
keywords: [n8n workflow, tự động hóa, hubspot, whatsapp, beex]
---

# 🚀 Tự động gửi tin nhắn chào mừng WhatsApp cho khách hàng mới từ HubSpot với Beex

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức khi gửi tin nhắn chào mừng thủ công.
- Tăng cường trải nghiệm khách hàng với tin nhắn cá nhân hóa.
- Tự động hóa quy trình marketing và chăm sóc khách hàng.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền đọc thông tin liên hệ.
- Tài khoản Beex với quyền gửi tin nhắn mẫu.
- Token Beex hợp lệ đã được cấu hình trong node Beex.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Webhook**: Cấu hình URL webhook trong ứng dụng tùy chỉnh của HubSpot để nhận sự kiện tạo liên hệ.
- **Get Contact**: Sử dụng ID liên hệ nhận được từ webhook để lấy các thuộc tính quan trọng như email và số điện thoại.
- **Validate Contact**: Đảm bảo liên hệ có số điện thoại và email hợp lệ.
- **Set Fields**: Chuẩn hóa các trường cần thiết cho tin nhắn WhatsApp. Đảm bảo cấu hình đúng `country_code` và `phone_number` dựa trên khu vực của bạn.
- **Send Template**: Gửi tin nhắn mẫu WhatsApp (ví dụ: `template_name` → `n8n_beex`) sử dụng các trường đã xử lý.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có liên hệ mới.
- Lưu log các tin nhắn đã gửi để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng tin nhắn đã gửi và tỷ lệ mở.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình gửi tin nhắn chào mừng WhatsApp cho khách hàng mới từ HubSpot, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Hãy áp dụng ngay để tối ưu hóa quy trình marketing và chăm sóc khách hàng của bạn!