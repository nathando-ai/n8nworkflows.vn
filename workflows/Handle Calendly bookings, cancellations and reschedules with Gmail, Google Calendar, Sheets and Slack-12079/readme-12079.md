---
title: "🚀 Tự động hóa lịch hẹn Calendly với Gmail, Google Calendar, Sheets và Slack"
description: "Đồng bộ hóa toàn bộ lịch hẹn Calendly: tự động tạo sự kiện Google Calendar, ghi log vào Google Sheets, gửi email xác nhận qua Gmail và thông báo qua Slack cho cả 3 kịch bản: Đặt lịch mới, Hủy lịch và Dời lịch."
slug: "tu-dong-hoa-lich-hen-calendly-voi-gmail-google-calendar-sheets-slack"
tags: [n8n, automation, no-code, calendly, google-calendar, slack, gmail]
keywords: [n8n workflow, tự động hóa calendly, tích hợp calendly google calendar, quản lý lịch hẹn tự động, n8n webhook]
---

# 🚀 Tự động hóa lịch hẹn Calendly với Gmail, Google Calendar, Sheets và Slack

Các sếp có đang đau đầu vì mỗi khi khách hàng đặt lịch, hủy lịch hoặc dời lịch trên Calendly lại phải thủ công cập nhật Google Calendar, ghi chép vào bảng tính, rồi lọ mọ soạn email gửi khách và hú hét thông báo cho đội ngũ trên Slack? Việc này không chỉ tốn thời gian mà còn cực kỳ dễ bỏ sót, gây ảnh hưởng chuyên nghiệp trong mắt khách hàng.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Hệ thống sẽ tự động hóa 100% quy trình xử lý lịch hẹn từ A-Z ngay khi có sự kiện diễn ra trên Calendly.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% 3 kịch bản:** Xử lý mượt mà cả lịch hẹn mới (New booking), Hủy lịch (Cancellation) và Dời lịch (Reschedule).
- **Đồng bộ đa nền tảng:** Lịch Google Calendar luôn chuẩn xác, dữ liệu khách hàng tự động lưu trữ gọn gàng trong Google Sheets.
- **Cá nhân hóa trải nghiệm khách hàng:** Gửi email xác nhận/hủy/dời lịch chuyên nghiệp qua Gmail ngay lập tức.
- **Cảnh báo thông minh:** Đội ngũ sales/support nhận thông báo thời gian thực trên Slack, kèm kênh bắt lỗi riêng biệt (`#errors`) nếu có sự cố xảy ra.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Calendly** (có quyền tạo Webhook).
- Các tài khoản kết nối (Credentials): **Gmail**, **Google Calendar**, **Google Sheets**, và **Slack**.
- Một **Google Sheet** chuẩn bị sẵn với tab có tên `Bookings` để lưu log.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node cốt lõi sau để workflow hoạt động trơn tru:

- **Calendly Webhook:** Lấy Production/Test URL từ node này và dán vào phần cấu hình Webhook trong tài khoản Calendly của các sếp để lắng nghe sự kiện (`invitee.created`, `invitee.canceled`,...).
- **Parse Calendly Event & Prepare Email Nodes (Code nodes):** Các node xử lý dữ liệu viết bằng JavaScript giúp bóc tách thông tin khách hàng, thời gian, link họp một cách chính xác.
- **Event Router (Switch node):** Phân luồng sự kiện đến nhánh tương ứng dựa trên loại hành động từ Calendly (New booking, Cancellation, Reschedule).
- **Log to Google Sheets, Log Cancellation, Log Reschedule:** Kết nối tài khoản Google Sheets của các sếp, chọn đúng file tài liệu (`YOUR_DOCUMENT_ID`) và chọn sheet `Bookings`.
- **Create Calendar Event:** Cấu hình để tự động thêm sự kiện vào Google Calendar với thời gian và email của khách hàng.
- **Slack (New Booking, Cancellation, Rescheduled, Error Alert1):** Kết nối với Workspace Slack và trỏ đúng các kênh thông báo (Ví dụ: kênh `#bookings` để thông báo lịch, kênh `#errors` để bắt lỗi hệ thống).
- **Send Confirmation / Cancellation / Reschedule Email (Gmail nodes):** Chọn tài khoản Gmail gửi đi và kiểm tra lại nội dung template email được chuẩn bị từ các node Code phía trước.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thực hiện một lịch hẹn thử nghiệm (test booking) trên Calendly để kiểm tra dữ liệu chảy qua các node.
- Nếu mọi thứ chạy xanh mướt, hãy bật công tắc **Active** để workflow chính thức vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm CRM:** Có thể nối thêm node HubSpot hoặc Salesforce ngay sau bước nhận Webhook để đồng bộ khách hàng tiềm năng.
- **Gửi tin nhắn Zalo/Telegram:** Bên cạnh Slack, các sếp có thể nhân bản luồng thông báo sang Telegram Bot để đội ngũ nhận tin nhanh hơn trên điện thoại cá nhân.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy lịch (Schedule Trigger) để tổng hợp số lượng lịch hẹn trong tuần từ Google Sheets và gửi báo cáo vào email quản lý.

### 📌 Kết luận
Việc tự động hóa quy trình quản lý lịch hẹn với Calendly, Google Workspace và Slack sẽ giúp doanh nghiệp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần, đồng thời mang lại trải nghiệm chuyên nghiệp tuyệt đối cho khách hàng. Chúc các sếp cài đặt thành công!