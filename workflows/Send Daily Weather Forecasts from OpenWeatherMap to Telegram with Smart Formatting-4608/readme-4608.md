---
title: "🚀 Tự động gửi dự báo thời tiết hàng ngày lên Telegram từ OpenWeatherMap với n8n"
description: "Xây dựng bot tự động lấy dữ liệu thời tiết thông minh qua OpenWeatherMap, xử lý bằng Code node và gửi bản tin chi tiết kèm định dạng đẹp mắt lên Telegram mỗi sáng."
slug: "gui-du-bao-thoi-tiet-telegram-tu-openweathermap-n8n"
tags: [n8n, automation, telegram, openweathermap, ai, no-code, webhook]
keywords: [n8n workflow, bot telegram thoi tiet, openweathermap api n8n, tu dong gui thoi tiet, huong dan n8n]
---

# 🚀 Tự động gửi dự báo thời tiết hàng ngày lên Telegram với n8n

Các sếp có bao giờ cảm thấy phiền toái khi mỗi sáng phải mở các app thời tiết, dò dẫm xem hôm nay có mưa không, nhiệt độ thế nào để chọn trang phục? Việc này lặp đi lặp lại mỗi ngày và rất dễ quên, nhất là khi cần chuẩn bị đồ đạc gấp.

Thay vì làm thủ công, tại sao các sếp không để n8n lo trọn gói? Workflow này sẽ tự động gọi API lấy thông tin thời tiết mỗi sáng, xử lý thông minh kèm theo các icon vui nhộn, lời khuyên thiết thực (như nhớ mang ô, mặc áo ấm) và gửi thẳng vào Telegram cá nhân hoặc nhóm chat của các sếp đúng giờ hẹn. Hoàn toàn tự động 100% và không tốn một xu tiền code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động thời gian**: Nhận bản tin thời tiết chi tiết lúc 7:50 sáng mỗi ngày mà không cần thao tác gì.
- **Thông minh & Trực quan**: Tin nhắn Telegram được định dạng HTML sạch sẽ, tích hợp emoji thời tiết động dựa trên nhiệt độ và tình trạng mưa gió.
- **Lời khuyên hữu ích**: Tự động gợi ý mang ô, mặc áo ấm hay kem chống nắng dựa trên dữ liệu dự báo thực tế.
- **Hoạt động bền bỉ**: Chạy tự động ngầm 24/7 trên n8n với cơ chế xử lý dữ liệu chuẩn xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenWeatherMap Account**: Tài khoản miễn phí để lấy API Key [tại đây](https://openweathermap.org/api).
- **Telegram Bot**: Tạo một bot thông qua `@BotFather` để lấy Token và Chat ID.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template hoặc copy toàn bộ mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần cấu hình các thông số sau:

- **Daily Morning Trigger (`scheduleTrigger`)**: 
  - Mặc định chạy lúc **7:50 AM** hàng ngày. 
  - Các sếp có thể đổi giờ tuỳ ý trong cấu hình của node (lưu ý múi giờ trên server n8n, ví dụ múi giờ Việt Nam là UTC+7).

- **OpenWeather API Request (`httpRequest`)**:
  - Lấy API Key miễn phí từ OpenWeatherMap và thay vào tham số URL (`appid=YOUR_API_KEY`).
  - Thay đổi địa điểm theo ý muốn tại tham số `q=` (Mặc định đang để `q=Strassen` ở Luxembourg. Các sếp có thể đổi thành `q=Hanoi,VN` hoặc `q=HoChiMinh,VN`).

- **Weather Data Processor (`code`)**:
  - Node này dùng code JavaScript để tính toán các chỉ số: biên độ nhiệt, tổng lượng mưa, tốc độ gió (km/h), mức độ ẩm và chèn các emoji thông minh tương ứng với thời gian ngày/đêm. Không cần sửa code trừ khi các sếp muốn tùy biến thêm nội dung hiển thị.

- **Send Weather Update (`telegram`)**:
  - Chọn hoặc tạo mới **Credentials** loại `telegramApi` và điền Bot Token nhận được từ `@BotFather`.
  - Cập nhật đúng `chatId` của cá nhân hoặc nhóm chat Telegram nơi bot sẽ gửi tin nhắn đến.
  - Bật tính năng định dạng tin nhắn HTML (`Parse Mode: HTML`) để tin nhắn hiển thị đẹp mắt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm xem Telegram có nhận được tin nhắn hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bot chính thức "lên sóng" mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng kênh nhận tin**: Kết nối thêm node Slack hoặc Discord song song với Telegram để gửi bản tin thời tiết cho cả team cùng nắm.
- **Lưu lịch sử**: Thêm node Google Sheets để lưu lại dữ liệu thời tiết hàng ngày phục vụ cho việc thống kê sau này.
- **Cảnh báo thời tiết xấu**: Thêm nhánh điều kiện (If node), nếu lượng mưa lớn hoặc gió bão, bot sẽ gửi thêm thông báo khẩn cấp để các sếp kịp chuẩn bị áo mưa, áo gió.

### 📌 Kết luận
Một workflow nhỏ nhưng cực kỳ thiết thực cho cuộc sống hằng ngày. Chỉ với vài phút thiết lập, các sếp đã có ngay một trợ lý ảo báo thời tiết tận tâm trên Telegram. Triển khai ngay thôi nào các sếp ơi!