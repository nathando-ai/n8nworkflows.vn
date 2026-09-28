---
title: "☀️ Tự động gửi bản tin thời tiết hàng ngày qua Telegram với n8n"
description: "Xây dựng bot tự động lấy dữ liệu thời tiết từ OpenWeatherMap và gửi báo cáo trực quan kèm emoji đến Telegram mỗi ngày."
slug: "tu-dong-gui-ban-tin-thoi-tiết-telegram-n8n"
tags: [n8n, automation, telegram, openweathermap, productivity]
keywords: [n8n workflow, bot telegram thời tiết, openweathermap n8n, tự động hóa n8n]
---

# ☀️ Tự động gửi bản tin thời tiết hàng ngày qua Telegram với n8n

Mỗi buổi sáng thức dậy, việc đầu tiên các sếp thường làm là gì? Kiểm tra điện thoại xem hôm nay trời nắng hay mưa để chuẩn bị áo mưa hay áo khoác đúng không? Thay vì phải mở app thủ công mỗi ngày, tại sao chúng ta không tự động hóa việc này để một "trợ lý ảo" gửi thẳng thông tin thời tiết vào Telegram cá nhân?

Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ gọn nhẹ (chỉ với 4 nodes) do tác giả **Dariusz Koryto** chia sẻ, giúp tự động cập nhật thời tiết mỗi ngày một cách nhanh chóng và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động thời gian:** Nhận bản tin thời tiết vào đúng khung giờ cố định mỗi sáng (ví dụ: 8:00 AM) mà không cần thao tác.
- **Trực quan, dễ đọc:** Dữ liệu thô từ API được format lại gọn gàng, kèm theo emoji sinh động.
- **Tiện lợi:** Thông báo đẩy trực tiếp vào tài khoản Telegram cá nhân hoặc nhóm làm việc.
- **Hoạt động 24/7:** Chạy tự động không mệt mỏi trên hệ thống n8n tự host.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và hoạt động bình thường.
- **OpenWeatherMap Account:** Tài khoản miễn phí để lấy API Key tại [openweathermap.org](https://openweathermap.org/).
- **Telegram Bot:** Tạo một bot thông qua `@BotFather` trên Telegram để lấy Bot Token và Chat ID.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (Link gốc: [Workflow #8162](https://n8n.io/workflows/8162)) hoặc copy JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Schedule Trigger (Cron):** 
  - Mặc định chạy lúc `8:00 AM` hàng ngày (Biểu thức cron: `0 8 * * *`).
  - Các sếp có thể đổi sang tần suất khác tùy thích như chạy mỗi 6 tiếng (`0 */6 * * *`) hoặc 2 lần/ngày (`0 8,18 * * *`).

- **Get Weather (OpenWeatherMap):** 
  - Thêm OpenWeatherMap API Credentials của sếp vào node này.
  - Cấu hình tên thành phố và quốc gia muốn xem (Ví dụ: `Hanoi,VN`).
  - Chọn ngôn ngữ hiển thị (`en`, `es`, `fr`, `de`, `pl`...). Node sẽ trả về thông tin nhiệt độ, độ ẩm, sức gió,...

- **Format Weather (Function):** 
  - Node này dùng code JavaScript để chuyển đổi dữ liệu thời tiết thô thành văn bản thân thiện, chèn emoji và bố cục lại theo múi giờ địa phương. 
  - Các sếp có thể tùy chỉnh template tin nhắn trực tiếp trong đoạn code của node này nếu muốn đổi cách xưng hô hoặc bổ sung thông tin.

- **Send a text message (Telegram):** 
  - Tạo bot thông qua `@BotFather` trên Telegram để nhận **Bot Token**.
  - Lấy **Chat ID** cá nhân của sếp (có thể nhắn tin cho bot rồi truy cập URL API của Telegram để lấy ID).
  - Thay thế giá trị `XXXXXXX` bằng Chat ID thực tế của sếp trong cấu hình node.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** để chạy thử nghiệm xem Telegram đã nhận được tin nhắn hay chưa.
- Nếu mọi thứ hiển thị đẹp đẽ, hãy bật công tắc **Active** ở góc trên bên phải để bot bắt đầu làm việc tự động mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Cảnh báo mưa/nắng gắt:** Sếp có thể mở rộng workflow bằng cách thêm các điều kiện (`If` node) để nếu nhiệt độ > 35°C hoặc có mưa lớn, gửi thêm lời nhắc mang ô/kem chống nắng.
- **Tích hợp nhóm chat:** Thay vì gửi cho cá nhân, sếp có thể add Telegram Bot vào group chat của công ty/gia đình để mọi người cùng nắm thời tiết trước khi ra đường.
- **Lưu log:** Kết hợp thêm Google Sheets node để lưu lại lịch sử thời tiết mỗi ngày phục vụ việc thống kê.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản cùng 4 nodes cơ bản trong n8n, các sếp đã sở hữu ngay một trợ lý thời tiết cá nhân cực kỳ hữu ích. Hãy "lên đồ" ngay cho hệ thống n8n của mình để không bao giờ bị bất ngờ vì thời tiết nữa nhé!