---
title: "🚀 Tải video Instagram & Facebook Reels tự động qua Telegram Bot với n8n"
description: "Xây dựng con bot Telegram cá nhân giúp tải nhanh chóng video và Reels từ Instagram hoặc Facebook chỉ bằng một đường link duy nhất với workflow n8n tự động 100%."
slug: "tai-video-instagram-facebook-reels-telegram-bot-n8n"
tags: [n8n, automation, no-code, telegram-bot, video-downloader, instagram, facebook]
keywords: [n8n workflow, tải video facebook, tải video instagram, telegram bot downloader, tự động hóa n8n]
---

# 🚀 Tải video Instagram & Facebook Reels tự động qua Telegram Bot với n8n

Các sếp có bao giờ cảm thấy bực bội khi lướt Facebook hoặc Instagram thấy một chiếc video hay, Reels hài hước nhưng loay hoay mãi không tìm được cách tải về máy? Việc dùng các trang web bên thứ ba thì đầy rẫy quảng cáo, mã độc hoặc giới hạn lượt tải. 

Đừng lo, bài toán này sẽ được giải quyết gọn gàng với **Workflow n8n: Tải video Instagram & Facebook Reels bằng Telegram Bot**. Chỉ cần gửi link vào con bot Telegram của riêng các sếp, hệ thống sẽ tự động bóc tách, lấy link tải và gửi trả lại video nét căng ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần truy cập các website tải video chứa đầy quảng cáo phiền toái.
- **Tự động hóa 2 trong 1:** Hỗ trợ cả hai nền tảng mạng xã hội lớn là Facebook (Videos/Reels) và Instagram (Reels/Videos).
- **Trải nghiệm mượt mà:** Thao tác trực tiếp trên ứng dụng Telegram quen thuộc mọi lúc, mọi nơi.
- **Hoạt động 24/7:** Con bot cá nhân luôn sẵn sàng phục vụ bất cứ khi nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo một bot miễn phí thông qua [@BotFather](https://t.me/BotFather) để lấy API Token kết nối vào n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ nguồn gốc (hoặc tải file JSON), sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để con bot hoạt động trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Telegram Trigger:** 
  - Kết nối với `telegramApi` credentials sử dụng Bot Token lấy từ `@BotFather`.
  - Node này có nhiệm vụ lắng nghe tin nhắn văn bản (chính là đường link Facebook/Instagram) mà các sếp gửi vào bot.
- **FB IG LINK REGEX & URL FINDER & URL DECODER:** 
  - Các node `code` (JavaScript) này đóng vai trò phân tích tin nhắn, nhận diện xem đó là link Facebook hay Instagram, đồng thời xử lý trích xuất mã nguồn/đường dẫn chính xác. **Các sếp không cần sửa code bên trong** trừ khi muốn tùy chỉnh logic nâng cao.
- **FB API FETCHING & INSTA API FETCHING:** 
  - Các node `httpRequest` thực hiện gọi API ngầm để lấy dữ liệu media trực tiếp từ nền tảng.
- **DOWNLOAD INSTA VID & DOWNLOAD FB VID:** 
  - Tải tệp video về bộ nhớ tạm của n8n để chuẩn bị gửi đi.
- **SEND INSTA VIDEO & SEND FB VIDEO:** 
  - Cần cấu hình `telegramApi` credentials và chọn operation `sendVideo` để bot gửi file video trực tiếp vào đoạn chat Telegram với các sếp.
- **INVALID URL:** 
  - Node phản hồi tin nhắn lỗi trong trường hợp các sếp gửi nhầm một đường dẫn không hợp lệ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một link video Instagram hoặc Facebook bất kỳ vào bot Telegram của các sếp để test.
- Nếu video trả về thành công, hãy gạt nút **Active** ở góc trên cùng bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets sau bước nhận link để lưu lại danh sách các video mà các sếp đã tải, tiện cho việc tra cứu lại sau này.
- **Tích hợp thêm thông báo qua Slack/Discord:** Bắn một thông báo nhỏ vào kênh làm việc nhóm mỗi khi có video mới được tải xuống thành công.
- **Hỗ trợ tải Audio (MP3):** Mở rộng code để cho phép bóc tách và chỉ tải phần âm thanh (nhạc nền) của video nếu các sếp cần.

### 📌 Kết luận
Một workflow cực kỳ thiết thực, gọn nhẹ nhưng giải quyết triệt để nhu cầu giải trí và lưu trữ nội dung hàng ngày. Hãy "lên đồ" ngay cho con bot Telegram của các sếp để tối ưu hóa trải nghiệm lướt mạng xã hội nhé! Chúc các sếp thao tác thành công!