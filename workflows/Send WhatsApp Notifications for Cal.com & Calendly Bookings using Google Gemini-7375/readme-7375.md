---
title: "🚀 Tự động gửi thông báo WhatsApp cho lịch hẹn Cal.com & Calendly bằng Google Gemini"
description: "Hướng dẫn tự động hóa gửi thông báo WhatsApp khi có sự kiện lịch hẹn từ Cal.com và Calendly, sử dụng trí tuệ nhân tạo Google Gemini để tạo nội dung thông báo chuyên nghiệp."
slug: "tu-dong-gui-thong-bao-whatsapp-cal-com-calendly-google-gemini"
tags: [n8n, automation, no-code, whatsapp, google-gemini, cal-com, calendly]
keywords: [n8n workflow, tự động hóa, whatsapp, google gemini, cal.com, calendly]
---

# 🚀 Tự động gửi thông báo WhatsApp cho lịch hẹn Cal.com & Calendly bằng Google Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận thông báo tức thì trên WhatsApp khi có sự kiện lịch hẹn mới, thay đổi hoặc hủy.
- Tiết kiệm thời gian quản lý lịch hẹn thủ công.
- Tạo nội dung thông báo chuyên nghiệp bằng trí tuệ nhân tạo Google Gemini.
- Tự động hóa hoàn toàn quy trình thông báo lịch hẹn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Cal.com và Calendly đã kết nối với n8n.
- Tài khoản Google Cloud với API key cho Google Gemini.
- Tài khoản WhatsApp Business API và số điện thoại được ủy quyền.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7375](https://n8n.io/workflows/7375) để tải file JSON của workflow.
2. Trong n8n Editor, chọn **Import from File** và chọn file JSON đã tải về.
3. Hoặc copy/paste nội dung JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Gemini Chat Model**:
   - Thêm credentials cho Google Palm API.
   - Cấu hình các tham số như `model`, `temperature`, `maxOutputTokens`.

2. **Cal.com Events**:
   - Thêm credentials cho Cal API.
   - Cấu hình các tham số như `eventType`, `timezone`.

3. **Calendly Events**:
   - Thêm credentials cho Calendly OAuth2 API.
   - Cấu hình các tham số như `eventType`, `timezone`.

4. **WhatsApp Notification**:
   - Thêm credentials cho WhatsApp API.
   - Cập nhật số điện thoại nhận thông báo trong tham số `to`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu nhận thông báo tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Tùy chỉnh nội dung thông báo trong node **Message Generator** để phù hợp với giọng điệu thương hiệu.
- Kết hợp với Slack hoặc Telegram để nhận thông báo đa kênh.
- Lưu log các sự kiện lịch hẹn vào Google Sheets hoặc Notion để theo dõi lịch sử.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc gửi thông báo WhatsApp cho lịch hẹn từ Cal.com và Calendly, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc!