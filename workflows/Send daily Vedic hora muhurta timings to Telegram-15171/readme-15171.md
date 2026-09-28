---
title: "🚀 Tự động gửi khung giờ hoàng đạo (Hora Muhurta) hàng ngày lên Telegram với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động theo dõi lịch thiên văn Vedic, lọc khung giờ mặt trời (Sun Hora) và gửi thông báo qua Telegram mỗi ngày."
slug: "tu-dong-gui-gio-hoang-dao-vedic-telegram-n8n"
tags: [n8n, automation, telegram, productivity, webhook, api]
keywords: [n8n workflow, hora muhurta, telegram bot, tu dong hoa n8n, phong thuy vedic, drikpanchang]
---

# 🚀 Tự động gửi khung giờ hoàng đạo (Hora Muhurta) hàng ngày lên Telegram với n8n

Việc theo dõi các khung giờ tốt (khung giờ hoàng đạo hay *Hora Muhurta* theo chiêm tinh học Vedic) để thực hiện các công việc quan trọng, cầu nguyện hay tập trung cao độ thường tốn thời gian tra cứu thủ công mỗi ngày. Nếu quên, các sếp có thể bỏ lỡ những thời điểm năng lượng tốt nhất trong ngày.

Giải pháp ở đây là gì? Hãy để n8n lo! Workflow này sẽ tự động hóa toàn bộ quy trình: quét dữ liệu thiên văn, trích xuất khung giờ mặt trời (*Sun Hora*) và gửi thông báo trực tiếp qua Telegram đúng các mốc thời gian quan trọng trong ngày mà không cần chạm tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tra cứu thủ công trên web mỗi ngày.
- **Đúng giờ, đúng lúc:** Nhận thông báo trước các khung giờ quan trọng (8 AM, 2 PM, 5 PM IST hoặc tùy chỉnh theo múi giờ).
- **Tăng hiệu suất cá nhân:** Tận dụng khung giờ năng lượng tốt (Sun Hora) để thực hiện mục tiêu, thiền định hoặc đưa ra quyết định quan trọng.
- **Hoạt động bền bỉ:** Chạy ngầm 24/7 trên server riêng cực kỳ ổn định.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một server n8n đã được cài đặt (Self-hosted hoặc n8n Cloud).
- Tài khoản Telegram và một **Telegram Bot Token** (tạo qua `@BotFather`).
- **Telegram Chat ID** nơi bot sẽ gửi tin nhắn đến.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã JSON của workflow (hoặc import file) dán trực tiếp vào giao diện n8n của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Daily Schedule Trigger (`scheduleTrigger`):** 
  - Mặc định workflow được thiết lập chạy nhiều lần trong ngày (8 AM, 2 PM, 5 PM). Các sếp có thể điều chỉnh lại mốc thời gian cho phù hợp với múi giờ và nhu cầu cá nhân.
- **Fetch Panchang Data (`httpRequest`):**
  - Node này thực hiện việc lấy dữ liệu lịch từ trang `drikpanchang.com`. Các sếp cần chú ý tham số `geoname-id` trong URL của HTTP Request để đổi thành mã ID địa lý của thành phố/quốc gia các sếp đang sinh sống.
- **Extract Hora Timings (`code`):**
  - Node Javascript này xử lý việc bóc tách 24 khung giờ hành tinh từ dữ liệu thô. Không cần sửa gì thêm trừ khi muốn tùy biến sâu hơn về cấu trúc dữ liệu.
- **Filter Sun Horas (`set`):**
  - Lọc và giữ lại các khung giờ thuộc Mặt Trời (Sun Hora) để phục vụ cho việc manifestation hoặc tập trung công việc.
- **Send Telegram Alert (`telegram`):**
  - Chọn credentials Telegram Bot đã tạo (nhập Bot Token).
  - Điền **Chat ID** của cá nhân hoặc nhóm chat vào trường *Chat ID*.
  - Nội dung tin nhắn đã được định dạng Markdown sẵn sàng hiển thị sinh động trên điện thoại.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thủ công xem tin nhắn có bắn về Telegram hay không.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa trải nghiệm cá nhân, các sếp có thể mở rộng workflow này:
- **Tích hợp thêm thông báo đẩy:** Thay vì chỉ gửi Telegram, có thể bắn thêm tin nhắn qua Slack hoặc Discord.
- **Lưu lịch sử vào Google Sheets:** Ghi lại các mốc thời gian Hora mỗi ngày để tiện tra cứu lại lịch sử.
- **Mở rộng loại Hora:** Ngoài Sun Hora, các sếp có thể tùy chỉnh code để lấy thêm các khung giờ của Kim星 (Venus), Mộc tinh (Jupiter) tùy theo mục đích phong thủy cá nhân.

### 📌 Kết luận
Workflow *Send daily Vedic hora muhurta timings to Telegram* là một ứng dụng nhỏ gọn nhưng cực kỳ thông minh giúp tận dụng tối đa sức mạnh của n8n vào đời sống cá nhân. Hãy cài đặt ngay để không bỏ lỡ những khoảnh khắc năng lượng tốt nhất mỗi ngày các sếp nhé!