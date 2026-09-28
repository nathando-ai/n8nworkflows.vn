---
title: "🎤 Hệ thống đặt lịch hẹn qua giọng nói với ElevenLabs AI và Cal.com"
description: "Tự động hóa hoàn toàn quá trình đặt lịch hẹn qua giọng nói với AI, kiểm tra lịch trống và đặt lịch thông qua Cal.com - giải pháp tiết kiệm thời gian 100% không cần code."
slug: "he-thong-dat-lich-hen-qua-giong-noi-voi-elevenlabs-ai-va-cal-com"
tags: [n8n, automation, no-code, elevenlabs, cal.com]
keywords: [n8n workflow, tự động hóa lịch hẹn, elevenlabs, cal.com, đặt lịch qua giọng nói]
---

# 🎤 Hệ thống đặt lịch hẹn qua giọng nói với ElevenLabs AI và Cal.com

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải liên tục kiểm tra lịch trống và đặt lịch hẹn cho khách hàng qua email hoặc điện thoại? Với hệ thống đặt lịch hẹn qua giọng nói này, các sếp có thể tự động hóa hoàn toàn quá trình này chỉ trong vài phút, không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quá trình đặt lịch hẹn
- **Chính xác cao**: Kiểm tra lịch trống và đặt lịch thông qua API chính thức của Cal.com
- **Trải nghiệm người dùng tốt**: Đặt lịch chỉ với giọng nói, không cần nhập liệu thủ công
- **Hoạt động liên tục**: Hệ thống hoạt động 24/7, không bị gián đoạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Cal.com với API key (để kiểm tra lịch trống và đặt lịch)
- Webhook endpoint để nhận yêu cầu đặt lịch (có thể sử dụng các dịch vụ như Zapier, Make, hoặc tự host webhook)
- (Tùy chọn) API key của ElevenLabs nếu muốn tích hợp giọng nói AI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Click vào "Import from URL" và nhập URL: `https://n8n.io/workflows/5670`
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/5670) và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đảm bảo đường dẫn webhook là duy nhất và bảo mật
   - Nên sử dụng HTTPS để bảo mật dữ liệu

2. **Node Check available slot in Cal.com**:
   - Cấu hình credentials "calApi" với API key của Cal.com
   - Điền đúng URL endpoint của Cal.com API (thường là `https://api.cal.com/v1/slots`)

3. **Node Book an Appointment**:
   - Cấu hình credentials "calApi" với API key của Cal.com
   - Điền đúng URL endpoint của Cal.com API (thường là `https://api.cal.com/v1/bookings`)

4. **Node Check Is Request For Available Slot**:
   - Cấu hình điều kiện kiểm tra xem yêu cầu có phải là kiểm tra lịch trống hay đặt lịch

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo hoạt động đúng
2. Bật Active workflow để hệ thống bắt đầu hoạt động

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với ElevenLabs để tạo giọng nói tự động thông báo lịch hẹn
- Thêm node gửi email/SMS thông báo lịch hẹn cho khách hàng
- Tích hợp với Slack/Teams để thông báo lịch hẹn trong nhóm làm việc
- Lưu log các yêu cầu đặt lịch để theo dõi và phân tích

### 📌 Kết luận
Hệ thống đặt lịch hẹn qua giọng nói với ElevenLabs AI và Cal.com là giải pháp hoàn hảo cho các doanh nghiệp muốn tự động hóa quá trình đặt lịch hẹn một cách nhanh chóng và hiệu quả. Với chỉ vài bước cấu hình đơn giản, các sếp có thể tiết kiệm hàng giờ mỗi ngày và cung cấp trải nghiệm tốt hơn cho khách hàng. Hãy thử ngay và trải nghiệm sự tiện lợi của tự động hóa!