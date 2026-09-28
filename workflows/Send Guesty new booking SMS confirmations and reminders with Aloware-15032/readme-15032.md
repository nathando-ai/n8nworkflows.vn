---
title: "🚀 Tự động gửi SMS xác nhận đặt phòng Guesty và chăm sóc khách hàng qua Aloware"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình gửi tin nhắn xác nhận, nhắc nhở check-in và xin review sau khi trả phòng từ Guesty qua Aloware."
slug: "tu-dong-gui-sms-dat-phong-guesty-aloware"
tags: [n8n, automation, no-code, guesty, aloware, crm, sms]
keywords: [n8n workflow, guesty aloware integration, tự động hóa đặt phòng, gui sms khach san, quan ly booking n8n]
---

# 🚀 Tự động gửi SMS xác nhận đặt phòng Guesty và chăm sóc khách hàng qua Aloware

Trong ngành dịch vụ lưu trú (cho thuê ngắn hạn, homestay, khách sạn), việc chào đón khách hàng chu đáo và gửi hướng dẫn check-in đúng giờ là yếu tố sống còn để đạt đánh giá 5 sao. Tuy nhiên, nếu làm thủ công, các sếp rất dễ quên gửi tin nhắn nhắc nhở trước ngày nhận phòng hoặc bỏ lỡ thời điểm vàng để xin review sau khi khách rời đi.

Được thiết kế bởi chuyên gia Maxim Dudnik, workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% vòng đời nhắn tin chăm sóc khách hàng từ Guesty thông qua hệ thống tổng đài/SMS Aloware.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Ngay khi có khách đặt phòng mới trên Guesty, hệ thống tự động khởi chạy chuỗi chăm sóc.
- **Cá nhân hóa trải nghiệm**: Gửi tin nhắn xác nhận tức thì, nhắc nhở check-in (trước 3 ngày, trước 1 ngày, trong ngày nhận phòng kèm mã cửa).
- **Tối ưu đánh giá 5 sao**: Tự động kích hoạt chuỗi tin nhắn xin review sau khi khách checkout 18 tiếng.
- **Tiết kiệm thời gian**: Loại bỏ hoàn toàn thao tác copy-paste thông tin khách hàng thủ công sang hệ thống SMS.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản quản lý nhà cho thuê **Guesty** (hỗ trợ tạo Webhook).
- Tài khoản tổng đài/SMS **Aloware** (đã cấu hình Line Phone và các Sequence nhắn tin).
- Các biến môi trường (n8n Variables) cần thiết:
  - `ALOWARE_API_TOKEN`
  - `ALOWARE_LINE_PHONE`
  - `ALOWARE_CHECKIN_SEQUENCE_ID`
  - `ALOWARE_REVIEW_SEQUENCE_ID`
  - `PROPERTY_COMPANY_NAME`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được liên kết chặt chẽ. Các sếp cần cấu hình kỹ các điểm sau:

- **Guesty: New Reservation (Webhook)**: 
  - Cấu hình phương thức `POST` và lấy đường dẫn Webhook URL do n8n cung cấp.
  - Sang hệ thống Guesty, tạo một Webhook mới lắng nghe sự kiện *"New Reservation"* và trỏ về URL của n8n.
- **Normalize Reservation Data (Set)**: 
  - Node này làm sạch và chuẩn hóa dữ liệu đầu vào từ Guesty bao gồm: Tên khách, số điện thoại, ngày check-in/check-out, tên căn hộ (listing) và mã xác nhận đặt phòng.
- **Aloware: Create Guest Contact (HTTP Request)**: 
  - Kết nối tới API của Aloware để tạo mới liên hệ (Contact) của khách hàng với đầy đủ thông tin đặt phòng vừa được chuẩn hóa.
- **Aloware: Send Booking Confirmation SMS (HTTP Request)**: 
  - Gửi ngay lập tức một tin nhắn SMS xác nhận đặt phòng thành công cho khách hàng thông qua Aloware Line Phone.
- **Aloware: Enroll in Check-in Reminder Sequence (HTTP Request)**: 
  - Đưa khách hàng vào chuỗi kịch bản nhắc nhở tự động của Aloware (Gợi ý: Trước 3 ngày gửi thông tin property, trước 1 ngày gửi hướng dẫn + WiFi, ngày nhận phòng gửi mã cửa/door code).
- **Wait Until After Checkout (Wait)**: 
  - Node tạm dừng thông minh, chờ cho đến thời điểm 18 giờ sau khi khách chính thức checkout.
- **Aloware: Enroll in Post-Stay Review Sequence (HTTP Request)**: 
  - Sau thời gian chờ, tự động đưa khách vào chuỗi tin nhắn xin đánh giá (Review Request) để nâng cao uy tín cholisting trên các kênh OTA.

#### 3. Kích hoạt ⚡️
- Thực hiện **Execute Node** hoặc **Test workflow** bằng cách tạo một booking giả lập trên Guesty để kiểm tra luồng dữ liệu chạy qua từng node.
- Kiểm tra kết quả thực tế trên Aloware (xem contact đã được tạo, tin nhắn đã gửi chưa).
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc phụ**: Có thể mở rộng thêm node gửi thông báo qua Telegram hoặc Slack cho đội ngũ vận hành (Ops team) mỗi khi có booking mới.
- **Lưu trữ dữ liệu khách hàng**: Thêm node Google Sheets hoặc Airtable ngay sau bước chuẩn hóa dữ liệu để lưu danh sách khách hàng phục vụ cho các chiến dịch marketing dài hạn sau này.
- **Xử lý lỗi (Error Handling)**: Bật tính năng Error Workflow trong n8n để nhận cảnh báo qua email/Telegram nếu API của Aloware hoặc Guesty gặp sự cố kết nối.

### 📌 Kết luận
Workflow tự động hóa đặt phòng Guesty kết hợp Aloware là giải pháp hoàn hảo giúp các chủ nhà và đơn vị vận hành chuyên nghiệp tối ưu hóa quy trình chăm sóc khách hàng, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để mang lại trải nghiệm 5 sao cho khách hàng của bạn!