---
title: "🚀 Tự động gửi tin nhắn SMS nhắc lịch hẹn Google Calendar qua RCSZilla"
description: "Hướng dẫn xây dựng hệ thống tự động quét lịch hẹn Google Calendar mỗi ngày và gửi tin nhắn SMS nhắc nhở khách hàng qua RCSZilla một cách chuyên nghiệp."
slug: "tu-dong-gui-sms-nhac-lich-hen-google-calendar-rcszilla"
tags: [n8n, automation, google-calendar, rcszilla, sms-marketing, no-code]
keywords: [n8n workflow, nhắc lịch hẹn google calendar, rcszilla sms, tự động hóa tin nhắn, n8n việt nam]
---

# 🚀 Tự động gửi tin nhắn SMS nhắc lịch hẹn Google Calendar qua RCSZilla

Quên lịch hẹn, khách “bùng” giờ chót luôn là nỗi ám ảnh lớn của các doanh nghiệp dịch vụ, phòng khám, salon hay đơn vị tư vấn. Việc gọi điện hoặc nhắn tin thủ công từng khách hàng mỗi ngày vừa tốn thời gian, vừa dễ sót việc.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100%: Hệ thống sẽ quét lịch hẹn ngày mai trên Google Calendar, kiểm tra điều kiện đồng ý nhận tin nhắn (consent) của khách hàng, sau đó tự động xếp hàng và gửi tin nhắn SMS thông qua cổng RCSZilla sử dụng chính chiếc điện thoại Android của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần thủ công kiểm tra lịch và nhắn tin cho khách mỗi sáng.
- **Tôn trọng quyền riêng tư (Bảo mật):** Chỉ gửi tin nhắn cho những khách hàng thực sự đồng ý nhận SMS (`SMS consent: yes`).
- **Tối ưu chi phí:** Sử dụng RCSZilla kết nối trực tiếp với điện thoại Android làm cổng SMS gateway (miễn phí phần mềm, chỉ tốn cước viễn thông nhà mạng).
- **Vận hành liên tục:** Chạy tự động đều đặn mỗi ngày vào lúc 09:00 sáng hoặc bất kỳ khung giờ nào các sếp muốn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Calendar** có chứa lịch hẹn.
- **Cài đặt Community Node:** `n8n-nodes-rcszilla`.
- **Điện thoại Android** kết nối với ứng dụng RCSZilla để làm cổng gửi SMS (Xem hướng dẫn cài đặt tại [RCSZilla Docs](https://docs.rcszilla.com/?page=get_started)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào không gian làm việc (n8n Editor) của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Every day at 09:00` (scheduleTrigger):** Thiết lập lại khung thời gian chạy tự động nếu muốn gửi tin nhắn sớm hơn hoặc muộn hơn trong ngày.
- **Node `Get tomorrow's appointments` (googleCalendar):** Kết nối tài khoản Google Calendar của các sếp và chọn đúng lịch hẹn (Calendar) cần quản lý.
- **Node `Prepare reminder SMS` (code):** Node này có nhiệm vụ đọc tiêu đề, thời gian, địa điểm và phần mô tả (description) của sự kiện để trích xuất thông tin khách hàng theo định dạng mẫu:
  ```text
  Name: Maria
  Phone: +40700000000
  SMS consent: yes
  ```
- **Node `Has phone and SMS consent?` (if):** Kiểm tra điều kiện xem khách hàng có số điện thoại hợp lệ và đã đồng ý nhận SMS chưa.
- **Node `Queue appointment SMS with RCSZilla` (n8n-nodes-rcszilla.rcsZilla):** Cấu hình credentials của RCSZilla và kết nối với thiết bị Android để đẩy tin nhắn vào hàng đợi gửi đi.

#### 3. Kích hoạt ⚡️
- Tạo một sự kiện thử nghiệm (test event) trên Google Calendar với đúng định dạng mô tả ở trên.
- Chạy thử công cụ (Test run) để kiểm tra xem tin nhắn đã được xếp vào hàng đợi của RCSZilla chưa.
- Sau khi test thành công, bật nút **Active** để workflow tự động chạy mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node thông báo về kênh nội bộ để đội ngũ nhân sự biết hôm nay có bao nhiêu tin nhắn nhắc lịch đã được gửi đi và bao nhiêu lịch bị bỏ qua.
- **Lưu lịch sử vào Google Sheets:** Thêm bước ghi lại log các cuộc hẹn đã gửi SMS thành công để tiện theo dõi chăm sóc khách hàng.
- **Tùy chỉnh nội dung:** Viết lại đoạn code tạo chuỗi tin nhắn để cá nhân hóa thương hiệu, thêm thông tin mã giảm giá hoặc link xác nhận lịch hẹn.

### 📌 Kết luận
Việc tự động hóa quy trình nhắc lịch hẹn bằng n8n và RCSZilla giúp doanh nghiệp nâng cao trải nghiệm khách hàng, giảm tỷ lệ vắng mặt mà không tốn kém chi phí phần mềm đắt đỏ. Hãy triển khai ngay hôm nay để tối ưu hóa vận hành cho cửa hàng hoặc doanh nghiệp của các sếp!