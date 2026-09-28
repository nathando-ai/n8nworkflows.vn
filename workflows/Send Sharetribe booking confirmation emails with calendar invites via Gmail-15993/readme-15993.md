---
title: "📅 [Tự động hóa] Gửi email xác nhận đặt chỗ với lịch hẹn từ Sharetribe qua Gmail"
description: "Hướng dẫn chi tiết cách tự động gửi email xác nhận đặt chỗ kèm lịch hẹn .ics cho khách hàng khi có đơn đặt chỗ được chấp nhận trên nền tảng Sharetribe của bạn."
slug: "tu-dong-hoa-email-xac-nhan-dat-cho-sharetribe-gmail"
tags: [n8n, automation, no-code, Sharetribe, email-marketing]
keywords: [n8n workflow, tự động hóa, Sharetribe, email xác nhận, lịch hẹn]
---

# 📅 [Tự động hóa] Gửi email xác nhận đặt chỗ với lịch hẹn từ Sharetribe qua Gmail

[Các sếp đang gặp khó khăn khi phải gửi email xác nhận đặt chỗ và lịch hẹn cho khách hàng một cách thủ công trên nền tảng Sharetribe của mình. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải gửi email xác nhận đặt chỗ thủ công cho mỗi đơn hàng.
- Tăng tính chuyên nghiệp: Email xác nhận được gửi kèm lịch hẹn .ics, giúp khách hàng dễ dàng thêm vào lịch của họ.
- Tăng trải nghiệm khách hàng: Khách hàng nhận được thông tin đặt chỗ một cách nhanh chóng và chính xác.
- Tự động hóa hoàn toàn: Quy trình được tự động hóa từ lúc đơn đặt chỗ được chấp nhận đến lúc email được gửi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Sharetribe với quyền truy cập API.
- Tài khoản Gmail với quyền truy cập API.
- URL của nền tảng Sharetribe của bạn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/15993](https://n8n.io/workflows/15993).
3. Nhấn "Import" để tải workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **When Booking Created or Updated**: Cấu hình credentials cho Sharetribe OAuth2 API.
- **Set Marketplace URL**: Thay đổi URL của nền tảng Sharetribe của bạn.
- **Fetch Marketplace Data**: Cấu hình credentials cho Sharetribe OAuth2 API.
- **Fetch Branding Color**: Cấu hình credentials cho Sharetribe OAuth2 API.
- **Fetch Email Footer Text**: Cấu hình credentials cho Sharetribe OAuth2 API.
- **Fetch Booking Transaction**: Cấu hình credentials cho Sharetribe OAuth2 API.
- **Send Booking Confirmation Email**: Cấu hình credentials cho Gmail OAuth2.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để kiểm tra workflow với dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo khi có đơn đặt chỗ mới.
- Lưu log các email đã gửi để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng đơn đặt chỗ và doanh thu.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình gửi email xác nhận đặt chỗ kèm lịch hẹn cho khách hàng trên nền tảng Sharetribe của mình. Hãy áp dụng ngay để tiết kiệm thời gian và tăng trải nghiệm khách hàng!