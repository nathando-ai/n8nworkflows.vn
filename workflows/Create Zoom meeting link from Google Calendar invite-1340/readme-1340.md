---
title: "🚀 Tự động tạo link họp Zoom từ Google Calendar cực nhanh với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét lịch Google Calendar hàng ngày, kiểm tra và tạo ngay phòng họp Zoom cho các sự kiện một cách mượt mà."
slug: "tu-dong-tao-zoom-meeting-tu-google-calendar-voi-n8n"
tags: [n8n, automation, no-code, zoom, google-calendar, productivity]
keywords: [n8n workflow, tạo zoom meeting tự động, google calendar zoom, tự động hóa n8n, workflow 1340]
---

# 🚀 Tự động tạo link họp Zoom từ Google Calendar cực nhanh với n8n

Các sếp có bao giờ cảm thấy mệt mỏi vì mỗi khi tạo lịch họp trên Google Calendar lại phải mở Zoom lên, tạo một meeting mới, copy link rồi paste ngược lại vào phần mô tả sự kiện không? Việc này lặp đi lặp lại hàng ngày tốn không ít thời gian và rất dễ sót link.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n "Create Zoom meeting link from Google Calendar invite" (tác giả: **Jason Foster**) lo trọn gói từ A-Z. Workflow này sẽ tự động hóa hoàn toàn quy trình kiểm tra lịch hẹn và tạo phòng họp Zoom mà các sếp không cần phải nhấc một ngón tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không còn thao tác thủ công chuyển đổi giữa Google Calendar và Zoom.
- **Tránh nhầm lẫn, sót link:** Đảm bảo 100% các cuộc họp đều có link Zoom sẵn sàng trước khi diễn ra.
- **Hoạt động tự động 24/7:** Chạy ngầm theo lịch trình thiết lập sẵn, luôn sẵn sàng phục vụ các sếp.
- **Tối ưu hóa quy trình làm việc:** Giúp đội ngũ chuyên nghiệp hơn trong mắt khách hàng và đối tác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn:
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Calendar (cần cấp quyền OAuth2).
- Tài khoản Zoom (cần tài khoản có quyền tạo meeting và cấu hình OAuth2 API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n Workflow #1340](https://n8n.io/workflows/1340) hoặc copy toàn bộ mã JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Cron Once a Day`**: Node này đóng vai trò kích hoạt workflow chạy tự động theo lịch định kỳ (ví dụ: mỗi ngày một lần hoặc tùy chỉnh theo ý muốn các sếp).
- **Node `Google Calendar`**: 
  - Chọn tài khoản kết nối (`googleCalendarOAuth2Api`).
  - Thiết lập tham số lấy danh sách sự kiện (`getAll`) để quét các lịch họp sắp diễn ra.
- **Node `Date & Time`**: Giúp chuẩn hóa định dạng thời gian để hệ thống Zoom và Google Calendar hiểu nhau chính xác.
- **Node `IF Zoom meeting`**: Bộ lọc thông minh kiểm tra xem sự kiện trên lịch đã có link Zoom hay chưa, tránh việc tạo trùng lặp phòng họp cho cùng một sự kiện.
- **Node `Zoom`**: 
  - Chọn tài khoản kết nối (`zoomOAuth2Api`).
  - Cấu hình các tham số tạo phòng họp (tiêu đề, thời gian bắt đầu, thời lượng) lấy dữ liệu truyền qua từ Google Calendar.

#### 3. Kích hoạt ⚡️
- Bấm nút **On clicking 'execute'** (`manualTrigger`) để test thử nghiệm dữ liệu mẫu xem luồng chạy có mượt không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "xịn xò" hơn nữa, các sếp có thể mở rộng thêm một vài tính năng:
- **Tích hợp Slack hoặc Telegram**: Gửi thông báo về điện thoại/nhóm chat ngay khi phòng Zoom được tạo thành công.
- **Cập nhật ngược lại Google Calendar**: Tự động update link Zoom vừa tạo vào phần Description hoặc Location của sự kiện trên Google Calendar.
- **Log dữ liệu**: Lưu lịch sử tạo meeting vào Google Sheets để tiện theo dõi.

### 📌 Kết luận
Một workflow nhỏ nhưng mang lại hiệu suất cực lớn, giúp các sếp giải phóng thời gian khỏi những tác vụ lặp đi lặp lại hàng ngày. Hãy cài đặt ngay hôm nay để tận hưởng sức mạnh của tự động hóa n8n!