---
title: "☀️ Tự động gửi báo cáo thời tiết hàng ngày qua Gmail với n8n và OpenWeatherMap"
description: "Hướng dẫn thiết lập workflow n8n tự động lấy dữ liệu thời tiết mỗi sáng và gửi email báo cáo chi tiết đến hộp thư của bạn hoàn toàn miễn phí."
slug: "tu-dong-gui-bao-cao-thoi-tiet-hang-ngay-qua-gmail"
tags: [n8n, automation, gmail, openweathermap, productivity]
keywords: [n8n workflow, tự động hóa thời tiết, gửi email tự động, openweathermap api, gmail oauth2]
---

# ☀️ Tự động gửi báo cáo thời tiết hàng ngày qua Gmail với n8n và OpenWeatherMap

Mỗi buổi sáng thức dậy, việc đầu tiên các sếp thường làm là gì? Kiểm tra thời tiết để quyết định mặc áo khoác hay mang theo ô, đúng không? Nhưng nếu quên kiểm tra, các sếp rất dễ bị dính những cơn mưa bất chợt. Thay vì phải mở ứng dụng thủ công mỗi ngày, tại sao chúng ta không để hệ thống tự động gửi bản tin thời tiết chi tiết vào email lúc 8 giờ sáng? 

Workflow n8n này do chuyên gia David Olusola thiết kế sẽ giúp các sếp giải quyết bài toán đó một cách mượt mà và hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động thời gian:** Nhận báo cáo thời tiết chính xác vào đúng 8h sáng hàng ngày trước khi bước chân ra khỏi nhà.
- **Tiện lợi & Tự động:** Không cần thao tác thủ công, mọi thứ diễn ra ngầm 24/7 trên con bot n8n của các sếp.
- **Dữ liệu trực quan:** Thông tin thời tiết được code lại gọn gàng, dễ nhìn trước khi gửi vào Gmail.
- **Miễn phí 100%:** Sử dụng gói Free của OpenWeatherMap kết hợp với tài khoản Gmail cá nhân.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng chạy (Self-hosted hoặc n8n Cloud).
- **OpenWeatherMap Account:** Đăng ký một tài khoản miễn phí để lấy API Key.
- **Gmail Account:** Tài khoản Google để kết nối gửi email qua OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này dán trực tiếp vào Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác 4 nodes trong hệ thống:

- **Node `Daily Schedule (8 AM)` (Cron):** 
  - Mặc định lịch chạy là 8:00 sáng mỗi ngày. Các sếp có thể bấm vào node này để thay đổi khung giờ (ví dụ 6:30 sáng) tùy theo thói quen sinh hoạt.
- **Node `Fetch Weather Data` (HTTP Request):** 
  - Thay thế chuỗi `YOUR_OPENWEATHERMAP_API_KEY` trong URL bằng API Key thực tế của các sếp lấy từ trang OpenWeatherMap.
  - Thay đổi địa danh (mặc định là `London`) trong URL thành thành phố các sếp đang sống hoặc muốn theo dõi (ví dụ: `Hanoi`, `Ho Chi Minh`).
- **Node `Format Weather Report` (Code):** 
  - Node này nhận dữ liệu JSON thô từ OpenWeatherMap và dùng Javascript để định dạng lại thành một nội dung bản tin dễ đọc, đẹp mắt. Các sếp có thể giữ nguyên không cần chỉnh sửa gì.
- **Node `Send Email Report` (Gmail):** 
  - Kết nối Credentials loại **Gmail OAuth2**.
  - Thay thế `your_email@example.com` bằng địa chỉ email thực tế của các sếp để nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thử nghiệm xem email có được gửi về hộp thư thành công hay không.
- Nếu mọi thứ hiển thị đẹp đẽ, hãy bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
Muốn hệ thống "xịn" hơn nữa? Các sếp có thể triển khai thêm các ý tưởng sau:
- **Đa kênh thông báo:** Nhân bản node gửi email thành node **Telegram** hoặc **Slack** để nhận tin nhắn ngay trên điện thoại thay vì phải mở Gmail.
- **Cảnh báo mưa:** Thêm một nhánh điều kiện (If Node), nếu dự báo có mưa hoặc độ ẩm cao, hệ thống sẽ tự động gửi kèm lời nhắc *"Hôm nay nhớ mang theo ô nhé sếp!"*.
- **Lưu lịch sử:** Ghi lại dữ liệu nhiệt độ từng ngày vào **Google Sheets** để làm biểu đồ theo dõi thời tiết trong tháng.

### 📌 Kết luận
Chỉ với vài phút thiết lập, các sếp đã có ngay một trợ lý ảo thời tiết cực kỳ thông minh chạy trên n8n. Hãy áp dụng ngay để cuộc sống thêm phần thảnh thơi và chủ động nhé!