---
title: "🚀 Tự Động Gửi Bản Tin Thời Tiết Hàng Ngày và Theo Yêu Cầu Lên Telegram với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu thời tiết từ OpenWeatherMap và gửi bản tin chi tiết qua Telegram theo lịch trình hoặc yêu cầu tức thì."
slug: "tu-dong-gui-ban-tin-thoi-tiet-telegram-openweathermap-n8n"
tags: [n8n, automation, no-code, telegram, weather, openweathermap, productivity]
keywords: [n8n workflow, tu dong hoa thoi tiet, telegram bot weather, openweathermap n8n, gui tin nhan telegram tu dong]
---

# 🚀 Tự Động Gửi Bản Tin Thời Tiết Hàng Ngày và Theo Yêu Cầu Lên Telegram

Các sếp có bao giờ cảm thấy bất tiện khi mỗi sáng phải mở các ứng dụng thời tiết để kiểm tra nhiệt độ, độ ẩm trước khi ra ngoài, hay muốn chủ động tra cứu thời tiết bất cứ lúc nào mà không cần rườm rà? Việc cập nhật thông tin thủ công này tốn thời gian và dễ bị lãng quên.

Giải pháp ở đây là để **n8n** tự động hóa hoàn toàn! Workflow này sẽ giúp các sếp nhận bản tin thời tiết chính xác mỗi sáng lúc 8:00 AM, hoặc bất cứ lúc nào các sếp muốn thông qua một form yêu cầu trực tuyến – tất cả đều được gửi thẳng về tài khoản Telegram cá nhân hoặc nhóm chat.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Nhận bản tin thời tiết tự động vào mỗi 8:00 sáng mà không cần thao tác.
- **Linh hoạt tra cứu:** Có thể chủ động gửi yêu cầu xem thời tiết bất cứ lúc nào qua Form trực tuyến.
- **Tiện lợi tối đa:** Thông tin thời tiết chi tiết (nhiệt độ, độ ẩm, trạng thái bầu không khí...) được gửi trực tiếp qua Telegram quen thuộc.
- **Tiết kiệm thời gian:** Không cần mất công tra cứu thủ công trên nhiều ứng dụng khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Tài khoản Telegram & Bot:** Cần tạo một Telegram Bot qua `@BotFather` để lấy `Access Token` và biết `Chat ID` nhận tin nhắn.
- **Tài khoản OpenWeatherMap:** Đăng ký tài khoản miễn phí để lấy API Key gọi dữ liệu thời tiết.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này (hoặc tải file JSON) và dán trực tiếp vào n8n Editor để hệ thống tự động sinh ra các nodes.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần chú ý cấu hình các điểm sau:

- **Schedule Trigger:** Node này được thiết lập mặc định chạy định kỳ hàng ngày vào lúc **08:00 AM**. Các sếp có thể thay đổi khung giờ này nếu muốn nhận tin vào thời điểm khác.
- **On form submission:** Node dạng Webhook Form giúp các sếp kích hoạt lấy thời tiết theo yêu cầu. Có thể cấu hình thêm các trường nhập liệu (như tên thành phố) nếu muốn mở rộng.
- **Get Weather Data (`httpRequest`):** Node gọi API tới OpenWeatherMap. Các sếp cần điền API Key của mình vào phần Header hoặc Query Parameters và cấu hình tọa độ/tên thành phố cần lấy thời tiết.
- **Format Weather Message (`set`):** Node dùng để xử lý và định dạng lại dữ liệu thô từ API thành một bản tin thời tiết sinh động, dễ đọc (bao gồm thông tin nhiệt độ, khí quyển, thời gian...).
- **Send Telegram Message (`telegram`):** Kết nối với tài khoản Telegram của các sếp. Cần chọn **Credentials** là `telegramApi`, điền `Chat ID` chính xác và ánh xạ dữ liệu từ node `Format Weather Message` vào nội dung tin nhắn (`Text`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem tin nhắn đã bắn về Telegram thành công chưa.
- Sau khi kiểm tra mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng địa điểm:** Thêm nhiều node HTTP Request hoặc dùng vòng lặp để lấy thời tiết của nhiều thành phố khác nhau cùng lúc (phù hợp cho các sếp hay đi công tác).
- **Cảnh báo thời tiết xấu:** Kết hợp thêm điều kiện (If Node) để nếu trời mưa hoặc nhiệt độ quá cao/quá thấp, bot sẽ gửi thêm icon cảnh báo đặc biệt.
- **Lưu trữ lịch sử:** Kết nối thêm Google Sheets để lưu lại lịch sử thời tiết các ngày phục vụ việc phân tích sau này.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại sự tiện ích lớn cho đời sống và công việc hàng ngày. Hãy cài đặt ngay để mỗi sáng thức dậy, các sếp đã nắm trọn thông tin thời tiết trong lòng bàn tay!