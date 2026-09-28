---
title: "📞 Hệ thống đặt lịch hẹn qua giọng nói với Vapi, Gemini và Google Calendar"
description: "Tự động hóa đặt lịch hẹn qua giọng nói với AI Vapi, phân tích lịch trống bằng Gemini và quản lý lịch Google Calendar. Tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "he-thong-dat-lich-hen-qua-giong-noi"
tags: [n8n, automation, no-code, ai, google-calendar]
keywords: [n8n workflow, tự động hóa, đặt lịch hẹn, ai chatbot, google calendar]
---

# 📞 Hệ thống đặt lịch hẹn qua giọng nói với Vapi, Gemini và Google Calendar

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình đặt lịch qua giọng nói
- Phân tích lịch trống thông minh bằng AI Gemini
- Quản lý lịch Google Calendar đồng bộ
- Gửi email xác nhận chuyên nghiệp tự động
- Tiết kiệm thời gian và giảm lỗi con người
- Nâng cao trải nghiệm khách hàng với dịch vụ tự động
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Vapi (để tích hợp AI giọng nói)
- Tài khoản Google Calendar (để quản lý lịch)
- Tài khoản Gmail (để gửi email xác nhận)
- API Key Google Gemini (để phân tích lịch trống)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10905](https://n8n.io/workflows/10905)
2. Click vào nút "Import" trên trang workflow
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Webhook - Availability Checker** và **Webhook - Create Appointment**:
   - Cấu hình path và HTTP method đúng như trong workflow
   - Lưu ý URL webhook sẽ được cung cấp sau khi kích hoạt

2. **Get Busy Slots from Calendar**:
   - Chọn tài khoản Google Calendar chính xác
   - Cập nhật múi giờ phù hợp với doanh nghiệp

3. **Google Gemini Chat Model**:
   - Cấu hình API Key cho Google Gemini
   - Đảm bảo tài khoản có quyền truy cập API

4. **Create Calendar Event**:
   - Chọn cùng tài khoản Google Calendar với node trước đó
   - Cập nhật múi giờ và thời gian làm việc

5. **Send Confirmation Email**:
   - Kết nối tài khoản Gmail
   - Tùy chỉnh mẫu email theo thương hiệu doanh nghiệp

6. **AI Availability Analyzer**:
   - Cập nhật thông tin giờ làm việc thực tế
   - Điều chỉnh prompt nếu cần phân tích lịch trống theo cách khác

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu cho cả 2 webhook
2. Kích hoạt workflow sau khi đã cấu hình đầy đủ
3. Cấu hình các webhook trong Vapi assistant:
   - `availability_checker` - Trỏ đến URL webhook đầu tiên
   - `Creating_the_appointment_and_sending_the_confirmation_email` - Trỏ đến URL webhook thứ hai

### ✍️ Mẹo & gợi ý nâng cao
1. Tích hợp thêm Slack/Telegram để thông báo lịch hẹn mới
2. Lưu log các giao dịch đặt lịch để phân tích sau
3. Thiết lập gửi báo cáo hàng ngày về lịch hẹn mới
4. Kết nối với CRM để cập nhật thông tin khách hàng tự động

### 📌 Kết luận
Hệ thống đặt lịch hẹn qua giọng nói này sẽ giúp các sếp tiết kiệm thời gian đáng kể, giảm lỗi con người và nâng cao trải nghiệm khách hàng. Với khả năng tích hợp mạnh mẽ với các công cụ AI và Google Calendar, workflow này là giải pháp hoàn hảo cho bất kỳ doanh nghiệp nào muốn hiện đại hóa quy trình đặt lịch của mình. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!