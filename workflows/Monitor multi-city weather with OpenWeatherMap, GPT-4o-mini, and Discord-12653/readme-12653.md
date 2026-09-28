---
title: "🚀 Tự động giám sát thời tiết đa thành phố với OpenWeatherMap, GPT-4o-mini và Discord"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu thời tiết, dự báo 5 ngày, chỉ số AQI, phân tích bằng AI và gửi cảnh báo thông minh qua Discord."
slug: "tu-dong-giam-sat-thoi-tiet-da-thanh-pho-n8n"
tags: [n8n, automation, openweathermap, openai, discord, google-sheets]
keywords: [n8n workflow, giám sát thời tiết tự động, openweathermap n8n, gpt-4o-mini weather, discord alert n8n]
---

# 🚀 Tự động giám sát thời tiết đa thành phố với OpenWeatherMap, GPT-4o-mini và Discord

Việc theo dõi thủ công tình hình thời tiết, chất lượng không khí (AQI) ở nhiều thành phố khác nhau cho các hoạt động kinh doanh, du lịch hay nghiên cứu thị trường tốn rất nhiều thời gian. Chưa kể, việc bỏ lỡ các cảnh báo thời tiết cực đoan có thể gây ảnh hưởng lớn.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: lấy dữ liệu thời tiết, dự báo, chỉ số không khí, dùng AI phân tích, gửi cảnh báo thông minh đến Discord và lưu trữ lịch sử vào Google Sheets. Tất cả đều diễn ra mượt mà mà không cần một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chạy định kỳ mỗi 6 giờ để cập nhật liên tục thời tiết của nhiều thành phố cùng lúc.
- **Phân tích thông minh bằng AI:** Sử dụng GPT-4o-mini để tính toán "Chỉ số thoải mái" (Comfort Index) và viết bản tin tóm tắt tự nhiên như con người.
- **Cảnh báo thông minh:** Tự động phân luồng gửi cảnh báo khẩn cấp (nếu thời tiết nguy hiểm/AQI kém) hoặc báo cáo định kỳ qua Discord.
- **Lưu trữ dữ liệu lịch sử:** Tự động ghi nhận toàn bộ thông tin vào Google Sheets để tiện theo dõi và tra cứu sau này.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng hoạt động (Cloud hoặc Self-hosted).
- **API Keys:**
  - **OpenWeatherMap API Key** (để lấy thời tiết và dự báo).
  - **OpenAI API Key** (cho node gọi GPT-4o-mini phân tích dữ liệu).
  - **Discord Webhook URL** (để gửi tin nhắn thông báo).
  - **Google Sheets Credentials** (để ghi log dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Set Monitoring Locations**: Mở node này và cấu hình danh sách các thành phố cần theo dõi thông qua tọa độ vĩ độ (Lat) và kinh độ (Lon).
- **Get Current Weather & Get 5-Day Forecast**: Kết nối tài khoản **OpenWeatherMap** (Credentials).
- **AI Weather Analysis (HTTP Request)**: Điền **OpenAI API Key** và cấu hình model `gpt-4o-mini` để AI tiến hành phân tích dữ liệu thời tiết.
- **Send Discord Alert & Send Discord Report**: Cập nhật **Discord Webhook URL** của các kênh tương ứng trên server Discord của các sếp.
- **Log to Google Sheets**: Chọn Credentials tài khoản Google, điền chính xác **Spreadsheet ID** và **Sheet Name** để hệ thống bắt đầu ghi log.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem các node đã kết nối mượt mà chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch trình của `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Ngoài Discord, các sếp có thể nhân bản nhánh thông báo để bắn tin nhắn song song lên nhóm Telegram hoặc Slack của công ty.
- **Tùy biến Prompt cho AI:** Tại node `AI Weather Analysis`, các sếp có thể tinh chỉnh system prompt để AI viết bản tin theo văn phong hài hước, trang trọng hoặc ngắn gọn tùy nhu cầu.
- **Mở rộng danh sách thành phố:** Dễ dàng thêm hàng chục thành phố khác tại node `Set Monitoring Locations` mà không làm thay đổi cấu trúc logic bên dưới.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho các tổ chức, cá nhân cần theo dõi thời tiết diện rộng phục vụ du lịch, nông nghiệp, logistics hay marketing theo mùa. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa thời gian và công sức!