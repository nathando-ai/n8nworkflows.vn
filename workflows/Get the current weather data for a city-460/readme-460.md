---
title: "☀️ Lấy dữ liệu thời tiết tự động theo thời gian thực với OpenWeatherMap và n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy thông tin thời tiết hiện tại của bất kỳ thành phố nào qua OpenWeatherMap chỉ với 2 nodes đơn giản."
slug: "lay-du-lieu-thoi-tiet-tu-dong-n8n-openweathermap"
tags: [n8n, automation, no-code, weather-api, openweathermap]
keywords: [n8n workflow, lấy dữ liệu thời tiết, openweather map n8n, tự động hóa n8n, api thời tiết]
---

# ☀️ Lấy dữ liệu thời tiết tự động theo thời gian thực với OpenWeatherMap và n8n

Các sếp có bao giờ cần tích hợp dữ liệu thời tiết vào hệ thống CRM, gửi cảnh báo thời tiết tự động cho khách hàng, hay đơn giản là kiểm tra thời tiết cho các ứng dụng cá nhân nhưng lại ngán ngẩm việc code tích hợp API phức tạp? Việc gọi thủ công hoặc viết code script riêng vừa tốn thời gian, vừa khó quản lý.

Đừng lo! Workflow n8n này sẽ giúp các sếp giải quyết bài toán trên trong một nốt nhạc. Chỉ với một cú click, hệ thống sẽ tự động kết nối với **OpenWeatherMap** và trả về toàn bộ thông tin thời tiết chi tiết của thành phố mà các sếp muốn tra cứu. 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và sẵn sàng mở rộng tích hợp với các hệ thống khác, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Lấy dữ liệu thời tiết (nhiệt độ, độ ẩm, sức gió, mây...) tức thì mà không cần thao tác thủ công.
- **Tiết kiệm thời gian:** Tận dụng ngay lập tức API của bên thứ ba mà không cần viết một dòng code nào.
- **Dễ dàng mở rộng:** Dễ dàng kết hợp kết quả trả về để gửi thông báo qua Telegram, Slack hoặc lưu trữ vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **OpenWeatherMap** (miễn phí) để lấy API Key (`openWeatherMapApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ cấu trúc 2 nodes cơ bản dưới đây để dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này siêu tối giản với chỉ 2 nodes chính, các sếp cần chú ý cấu hình kỹ ở node sau:

- **Node `On clicking 'execute'` (Manual Trigger):** 
  - Đây là điểm khởi đầu dạng thủ công để test workflow. Các sếp có thể thay thế node này bằng `Webhook`, `Schedule Trigger` (để chạy định kỳ hàng ngày), hoặc `Chat Trigger` tùy theo nhu cầu thực tế.
- **Node `OpenWeatherMap`:**
  - **Credentials:** Các sếp cần tạo một **OpenWeatherMap API Key** miễn phí tại trang chủ OpenWeatherMap, sau đó cấu hình thông tin này vào phần Credentials của node.
  - **Parameters:** Điền tên thành phố (City) hoặc mã quốc gia mà các sếp muốn truy vấn thông tin thời tiết (ví dụ: `Hanoi`, `Ho Chi Minh`, `Tokyo`...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để test thử xem dữ liệu trả về từ OpenWeatherMap có chính xác hay không.
- Nếu mọi thứ hiển thị mượt mà, các sếp có thể đổi trigger thành dạng tự động và bật **Active workflow** lên để chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow này trở nên hữu ích thực tế hơn trong công việc hàng ngày, các sếp có thể nâng cấp bằng cách:
1. **Kết hợp Telegram/Slack Bot:** Thêm node gửi tin nhắn để tự động thông báo thời tiết buổi sáng cho đội ngũ hoặc nhóm chat gia đình.
2. **Lưu lịch sử vào Google Sheets:** Ghi lại nhiệt độ, độ ẩm từng ngày để phân tích xu hướng thời tiết.
3. **Cảnh báo thông minh:** Thêm node `If` để kiểm tra: Nếu trời mưa hoặc nhiệt độ quá cao/quá thấp, tự động gửi cảnh báo khẩn cấp.

### 📌 Kết luận
Một workflow siêu nhỏ gọn nhưng cực kỳ hữu ích để làm quen với việc gọi API bên thứ ba trên n8n. Hãy áp dụng ngay vào dự án của các sếp để tối ưu hóa các tác vụ liên quan đến dữ liệu thời tiết nhé!