---
title: "🎬 Tự động cập nhật lịch chiếu phim từ TMDB vào Google Calendar qua Telegram Bot với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động quét danh sách phim sắp chiếu từ TMDB, gửi thông báo qua Telegram và thêm vào Google Calendar chỉ với 1 chạm."
slug: "tu-dong-them-phim-tmdb-vao-google-calendar-qua-telegram"
tags: [n8n, automation, tmdb, telegram, google-calendar, productivity]
keywords: [n8n workflow, tự động hóa lịch phim, TMDB API, Telegram bot, Google Calendar integration]
---

# 🎬 Tự động cập nhật lịch chiếu phim từ TMDB vào Google Calendar qua Telegram Bot

Các sếp có bao giờ bỏ lỡ suất chiếu của bộ phim bom tấn yêu thích chỉ vì quên mất lịch phát hành? Việc phải thủ công tra cứu ngày ra rạp từ The Movie Database (TMDB) rồi nhập tay vào Google Calendar vừa tốn thời gian, lại dễ bỏ sót.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Hệ thống sẽ thay các sếp "săn" phim mới, gửi thông báo trực quan qua Telegram, và chỉ cần một cú click nút bấm, lịch chiếu sẽ tự động nằm gọn trong Google Calendar của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Mỗi ngày hệ thống sẽ tự động kiểm tra các bộ phim sắp ra mắt mà không cần con người nhúng tay.
- **Tránh trùng lặp**: Sử dụng n8n Data Table để ghi nhớ các phim đã thông báo, không lo bị làm phiền nhiều lần vì cùng một bộ phim.
- **Tương tác mượt mà**: Gửi thông báo kèm nút bấm (inline button) trực tiếp trên Telegram, thêm lịch chỉ với 1 chạm.
- **Đồng bộ thông minh**: Tự động tạo sự kiện đúng ngày công chiếu trên Google Calendar cá nhân.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **TMDB API Access Token**: Tài khoản miễn phí từ The Movie Database để lấy dữ liệu phim.
- **Telegram Bot Token & Chat ID**: Tạo bot qua `@BotFather` để gửi tin nhắn và nhận lệnh.
- **Google Calendar OAuth2**: Tài khoản Google để cấp quyền cho n8n tạo sự kiện lịch.
- **n8n Data Table**: Một bảng dữ liệu trong n8n dùng để lưu trữ metadata của phim tránh gửi trùng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng mã nguồn workflow từ n8n template (ID: `12005`) bằng cách import file JSON trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Config TMDB token and Telegram chat ID` (Set)**: 
  Điền chính xác TMDB API Token, Telegram Bot Token và Telegram Chat ID của các sếp vào các biến cấu hình trong node này.
- **Node `Get movies` (HTTP Request)**: 
  Đảm bảo endpoint gọi API tới TMDB sử dụng đúng token đã cấu hình để lấy danh sách phim sắp chiếu (`upcoming`).
- **Node `If new` & `Add movie data to table` (Data Table)**: 
  Trỏ tới n8n Data Table chuẩn bị sẵn để hệ thống ghi nhận và kiểm tra trạng thái phim (`rowNotExists`).
- **Node `Ask to add to calendar` (Telegram) & `Add to calendar button pressed` (Telegram Trigger)**: 
  Kết nối với Credentials Telegram API của các sếp. Node này sẽ gửi tin nhắn kèm nút bấm tương tác (callback button).
- **Node `Create an event` (Google Calendar)**: 
  Xác thực bằng Google Calendar OAuth2 API, cấu hình chọn đúng lịch (Calendar) muốn thêm sự kiện phim vào.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm thủ công với lịch trình hàng ngày (`Every Noon`).
- Kiểm tra tin nhắn Telegram xem bot đã bắn thông tin phim về chưa và bấm thử nút "Add to calendar".
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Telegram, các sếp có thể nhân bản nhánh gửi thông báo sang Slack, Discord hoặc Zalo OA tùy theo thói quen sử dụng.
- **Ghi log chi tiết**: Tận dụng n8n Data Table để lưu lại lịch sử các bộ phim đã được thêm vào calendar nhằm tạo bảng thống kê cá nhân (xem lại các phim đã xem/đã lên lịch).
- **Cảnh báo thời gian**: Tùy biến node Google Calendar để đặt thêm thời gian nhắc nhở (Reminder) trước giờ chiếu 1 ngày hoặc 1 tiếng.

### 📌 Kết luận
Một workflow cực kỳ thiết thực cho các tín đồ điện ảnh và những ai muốn tối ưu hóa thời gian giải trí cá nhân. Hãy áp dụng ngay để không bao giờ bỏ lỡ bất kỳ bộ phim hay nào ra rạp nhé các sếp!