---
title: "🚀 Giám sát sức khỏe API Amadeus & Booking.com tự động với WhatsApp SLA Alerts"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra uptime và SLA của Amadeus Flight API và Booking.com Hotel API mỗi 10 phút, gửi cảnh báo qua WhatsApp khi có sự cố."
slug: "giam-sat-api-amadeus-booking-whatsapp-sla-alerts"
tags: [n8n, automation, devops, api-monitoring, whatsapp, amadeus, booking-com]
keywords: [n8n workflow, giám sát api, amadeus api, booking.com api, whatsapp alert, sla monitoring, devops automation]
---

# 🚀 Giám sát sức khỏe API Amadeus & Booking.com tự động với WhatsApp SLA Alerts

Các sếp làm trong ngành du lịch, lữ hành chắc chắn hiểu rõ cảm giác "đứng ngồi không yên" khi các API cốt lõi như Amadeus Flight hay Booking.com gặp sự cố mà khách hàng hoặc đội ngũ sale đã bắt đầu phàn nàn. Việc kiểm tra thủ công hay dùng các công cụ giám sát phức tạp đôi khi tốn kém và thiếu linh hoạt. 

Được phát triển bởi **Oneclick AI Squad**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp chủ động giám sát trạng thái, đo lường SLA và nhận cảnh báo tức thì qua WhatsApp ngay khi hệ thống có dấu hiệu bất ổn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát thời gian thực:** Tự động kiểm tra đồng thời cả 2 API lớn (Amadeus & Booking.com) mỗi 10 phút.
- **Cảnh báo tức thì:** Gửi tin nhắn WhatsApp ngay lập tức khi phát hiện vi phạm SLA hoặc API chết, giúp xử lý sự cố trước khi khách hàng kịp kêu ca.
- **Minh bạch trạng thái:** Phân luồng rõ ràng giữa log trạng thái bình thường và log cảnh báo lỗi để dễ dàng tra cứu.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên n8n mà không cần sự can thiệp thủ công.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản truy cập **Amadeus Flight API** (Client ID & Client Secret / API Key).
- Tài khoản truy cập **Booking.com Hotel API**.
- Tài khoản **Meta / WhatsApp Business API** (để cấu hình node gửi tin nhắn WhatsApp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link: `https://n8n.io/workflows/6263`) hoặc copy đoạn JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node quan trọng sau đây để workflow hoạt động chính xác:

- **Monitor Schedule (`scheduleTrigger`):** Mặc định thiết lập chạy tự động mỗi 10 phút. Các sếp có thể thay đổi tần suất tùy theo nhu cầu thực tế của doanh nghiệp.
- **Amadeus Flight API & Booking Hotel API (`httpRequest`):** Điền endpoint API chuẩn, phương thức request (GET/POST), và thêm các header xác thực (Authorization/API Key) tương ứng của Amadeus và Booking.com.
- **Calculate Health & SLA (`code`):** Node này chứa đoạn mã Javascript xử lý dữ liệu trả về từ 2 API, tính toán thời gian phản hồi (response time), uptime và trạng thái SLA. Các sếp có thể tinh chỉnh ngưỡng (threshold) thời gian phản hồi tối đa tại đây.
- **Alert Check (`if`):** Node điều kiện kiểm tra kết quả từ bước tính toán. Nếu có lỗi hoặc vi phạm SLA, workflow sẽ rẽ nhánh sang luồng cảnh báo.
- **Send message (`whatsApp`):** 
  - Chọn hoặc thêm mới **WhatsApp API Credentials**.
  - Điền số điện thoại nhận cảnh báo và nội dung tin nhắn mẫu thông báo sự cố API.
- **SLA Breach Alert & Normal Status Log (`debugHelper`):** Các sếp có thể giữ nguyên để ghi nhận log debug, hoặc thay thế bằng các node lưu trữ như Google Sheets, Slack hoặc Telegram nếu muốn lưu lịch sử chi tiết hơn.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thủ công lần đầu với dữ liệu gọi API thực tế.
- Kiểm tra các nhánh `True`/`False` tại node `Alert Check` xem đã chạy đúng ý chưa.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ gửi WhatsApp, các sếp có thể kết nối thêm node Telegram hoặc Slack để gửi cảnh báo song song cho đội ngũ kỹ thuật (DevOps/Dev).
- **Lưu lịch sử Uptime:** Nối thêm node Google Sheets hoặc Notion vào sau node `Calculate Health & SLA` để vẽ biểu đồ theo dõi hiệu suất API theo ngày/tuần.
- **Tự động retry:** Thêm logic gọi lại API (Retry node) nếu phát hiện lỗi mạng tạm thời trước khi chính thức bắn tin nhắn báo động qua WhatsApp.

### 📌 Kết luận
Với workflow **Monitor Amadeus & Booking.com API Health with WhatsApp SLA Alerts**, các sếp đã sở hữu ngay một hệ thống "canh gác" API tự động, chuyên nghiệp mà không tốn chi phí thuê các dịch vụ giám sát bên thứ ba đắt đỏ. Hãy cài đặt ngay để bảo vệ chất lượng dịch vụ của doanh nghiệp mình!