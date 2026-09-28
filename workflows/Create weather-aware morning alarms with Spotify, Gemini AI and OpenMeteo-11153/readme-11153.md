---
title: "🚀 Tạo báo thức thông minh kết hợp thời tiết, Spotify và AI DJ với n8n"
description: "Tự động hóa buổi sáng của bạn với workflow n8n kết hợp OpenMeteo lấy thời tiết, phát nhạc Spotify ngẫu nhiên và dùng Google Gemini làm DJ chào buổi sáng."
slug: "tao-bao-thuc-thong-minh-spotify-gemini-ai-openmeteo"
tags: [n8n, automation, ai-automation, spotify, google-gemini, openmeteo]
keywords: [n8n workflow, bao thuc thong minh, spotify automation, google gemini ai, openmeteo, tu dong hoa n8n]
---

# 🚀 Tạo báo thức thông minh kết hợp thời tiết, Spotify và AI DJ với n8n

Buổi sáng thức dậy của bạn có đang nhàm chán với tiếng chuông báo thức mặc định đầy căng thẳng? Việc bắt đầu ngày mới thủ công bằng cách kiểm tra thời tiết, chọn nhạc và tự lên dây cót tinh thần ngốn không ít thời gian. 

Đừng lo, workflow n8n này sẽ biến chiếc loa thông minh và tài khoản Spotify của các sếp thành một DJ cá nhân thực thụ. Hệ thống sẽ tự động kiểm tra thời tiết ngoài trời, chọn ngẫu nhiên một bản nhạc rock kinh điển (như Led Zeppelin), và nhờ **Google Gemini AI** viết lời chào đậm chất DJ Radio kết nối giữa thời tiết và âm nhạc, sau đó phát trực tiếp lên thiết bị Spotify của bạn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thức dậy đầy hứng khởi:** Nghe nhạc yêu thích và lời dẫn hài hước, thông minh từ AI DJ mỗi sáng.
- **Cập nhật thời tiết tức thì:** Biết ngay nhiệt độ và tình hình thời tiết ngoài trời trước khi bước chân ra khỏi giường.
- **Tự động hóa 100%:** Kích hoạt đúng 7 giờ sáng mỗi ngày mà không cần chạm tay vào điện thoại.
- **Lưu trữ lịch sử tiện lợi:** Tự động ghi log chi tiết vào Google Sheets và gửi email tổng kết kèm ảnh bìa album nhạc.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản **Spotify Premium** (để điều khiển phát nhạc từ xa qua API).
- **Google Gemini API Key** (Google Palm/Gemini credentials).
- Tài khoản Google (Google Sheets & Gmail) để lưu log và gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy mượt mà:

- **Schedule Trigger (7AM):** Thiết lập lịch chạy đúng giờ thức dậy mong muốn của các sếp (mặc định 7:00 AM mỗi ngày).
- **Workflow Configuration (Set Node):** Mở node này và cấu hình vị trí địa lý (vĩ độ/kinh độ cho OpenMeteo) và tên thiết bị Spotify đích mà các sếp muốn phát nhạc.
- **Get Weather (OpenMeteo) & Get Spotify Devices:** Kiểm tra các thông số gọi API thời tiết và lấy danh sách thiết bị Spotify khả dụng.
- **Find Target Device & Device Found? (Code & IF Node):** Đảm bảo thiết bị Spotify của các sếp đang bật hoặc ở chế độ chờ kết nối.
- **Get Artist Tracks & Pick Random Track:** Nơi cấu hình nghệ sĩ yêu thích (mặc định là Led Zeppelin) và thuật toán chọn ngẫu nhiên bài hát.
- **Message a model (Google Gemini):** Kết nối tài khoản Google Gemini API và tùy chỉnh prompt để AI tạo lời dẫn DJ phù hợp với thời tiết và bài hát.
- **Log to Google Sheets:** Trỏ tới file Google Sheets chuẩn bị sẵn với các cột: `date`, `time`, `weather`, `temperature`, `song`, `artist`.
- **Send DJ Email & Send Error Email (Gmail):** Cấu hình tài khoản Gmail để nhận bản tin DJ buổi sáng và email cảnh báo nếu thiết bị không hoạt động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng cách bấm nút thực thi thủ công để kiểm tra kết nối Spotify và Gemini AI.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang trạng thái **Active** để hệ thống tự động chạy mỗi sáng.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa âm nhạc:** Thay vì chỉ cố định một nghệ sĩ, các sếp có thể mở rộng lấy nhạc từ Playlist yêu thích cá nhân trên Spotify.
- **Tích hợp thêm thông báo:** Kết nối thêm node Telegram hoặc Slack để nhận lời dẫn của DJ ngay trên điện thoại thay vì chỉ qua Email.
- **Báo cáo thông minh hàng tuần:** Tạo thêm một nhánh tổng hợp log từ Google Sheets để gửi báo cáo tóm tắt gu nghe nhạc và thời tiết vào cuối tuần.

### 📌 Kết luận
Một buổi sáng tràn đầy năng lượng đang chờ đón các sếp với trợ lý AI DJ thông minh. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian và tận hưởng sức mạnh tuyệt vời của tự động hóa n8n!