---
title: "📅 [Tự động hóa] Gửi email nhắc hẹn lại sau khi khách hàng bỏ lỡ cuộc hẹn"
description: "Hướng dẫn tự động hóa gửi email nhắc hẹn lại cho khách hàng bỏ lỡ cuộc hẹn thông qua webhook và Gmail hoàn toàn không cần code"
slug: "tu-dong-hoa-gui-email-nhac-hen-lai-khach-hang-bo-lo-cuoc-hen"
tags: [n8n, automation, no-code, email-marketing, crm]
keywords: [n8n workflow, tự động hóa email, nhắc hẹn lại, quản lý cuộc hẹn, tự động hóa không code]
---

# 📅 [Tự động hóa] Gửi email nhắc hẹn lại sau khi khách hàng bỏ lỡ cuộc hẹn

[Các sếp đang gặp khó khăn khi phải theo dõi và nhắc nhở khách hàng bỏ lỡ cuộc hẹn một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình gửi email nhắc hẹn lại thông qua webhook và Gmail, giúp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi email nhắc hẹn lại cho khách hàng bỏ lỡ cuộc hẹn
- Tiết kiệm thời gian quản lý khách hàng bỏ lỡ cuộc hẹn
- Tăng cường trải nghiệm khách hàng với thông báo nhắc hẹn lại chuyên nghiệp
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi email nhắc hẹn lại
- API key hoặc credentials của Gmail
- Dịch vụ CRM hoặc hệ thống đặt lịch hẹn để gửi webhook
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/16155](https://n8n.io/workflows/16155)
3. Hoặc tải file JSON về và import từ máy tính

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Configure recovery message"**:
   - Thiết lập tên doanh nghiệp, URL đặt lịch và chủ đề email
   - Ví dụ:
     ```
     Business Name: "Công ty XYZ"
     Booking URL: "https://congtyxyz.com/dat-lich"
     Subject: "Nhắc nhở: Hẹn lại cuộc hẹn của bạn"
     ```

2. **Node "Send rescheduling email"**:
   - Kết nối với credentials của Gmail
   - Đảm bảo tài khoản Gmail được cấu hình đúng và có quyền gửi email

3. **Node "Receive missed appointment"**:
   - Đảm bảo đường dẫn webhook là "missed-appointment-recovery"
   - Phương thức HTTP là POST

#### 3. Kích hoạt ⚡️
1. Gửi payload mẫu để test workflow:
```json
{
  "event_id": "evt_test_001",
  "contact": {
    "name": "Khách hàng Test",
    "email": "email-test@example.com",
    "transactional_contact_allowed": true
  },
  "appointment": {
    "id": "apt_test_001",
    "status": "missed"
  }
}
```
2. Kiểm tra email nhận được từ tài khoản Gmail
3. Chỉ kích hoạt workflow sau khi đã kiểm tra kỹ và được sự đồng ý của doanh nghiệp

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi có khách hàng bỏ lỡ cuộc hẹn
2. Lưu log các email đã gửi để theo dõi hiệu quả nhắc hẹn
3. Thiết lập gửi báo cáo định kỳ về tỷ lệ nhắc hẹn thành công
4. Tích hợp với hệ thống CRM để cập nhật trạng thái khách hàng sau khi gửi email nhắc hẹn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gửi email nhắc hẹn lại cho khách hàng bỏ lỡ cuộc hẹn, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý khách hàng của doanh nghiệp!