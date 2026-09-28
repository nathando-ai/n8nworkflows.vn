---
title: "🚀 Tìm quán cafe thư giãn thông minh giữa các cuộc họp với n8n, AI & Google Calendar"
description: "Tự động hóa lịch trình của bạn: Kiểm tra Google Calendar, tính toán thời gian trống, tìm quán cafe gần nhất qua Google Maps API, nhờ OpenRouter AI tư vấn và gửi thông báo trực tiếp qua Slack."
slug: "gap-time-cafe-finder-n8n-google-calendar-ai-slack"
tags: [n8n, automation, ai, google-calendar, slack, openrouter]
keywords: [n8n workflow, tự động hóa lịch trình, tìm quán cafe bằng AI, google calendar n8n, openrouter ai agent]
---

# 🚀 Tìm quán cafe thư giãn thông minh giữa các cuộc họp với n8n, AI & Google Calendar

Các sếp có bao giờ rơi vào cảnh trống lịch giữa hai cuộc họp 1-2 tiếng nhưng lại lười không biết đi đâu, hay loay hoay tìm quán cafe phù hợp mà sợ trễ giờ hẹn tiếp theo không? Việc tra cứu lịch trình, tính thời gian di chuyển thủ công rồi tìm kiếm quán cafe vừa ngon vừa gần thực sự tốn thời gian và dễ làm lỡ việc.

Giải pháp đây rồi! Workflow **Gap-Time Cafe Finder** trên n8n sẽ thay các sếp làm toàn bộ quy trình này một cách hoàn toàn tự động 100% không cần code. Hệ thống sẽ tự động quét lịch Google Calendar, tính toán thời gian rảnh thực tế (Gap Time), kết hợp Google Maps để đo thời gian di chuyển, nhờ OpenRouter AI tư vấn quán cafe phù hợp nhất dựa trên sở thích cá nhân, và bắn tin nhắn báo cáo trực tiếp qua Slack. Nếu không đủ thời gian, hệ thống cũng sẽ nhắc nhở các sếp di chuyển ngay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tận dụng tối đa thời gian trống:** Tự động tìm kiếm quán cafe lý tưởng ngay khi có khoảng "gap time" phù hợp.
- **Cá nhân hóa trải nghiệm:** AI tự động chọn quán dựa trên sở thích riêng của các sếp (ưa yên tĩnh, thích espresso, có Wi-Fi...) lưu trên Google Sheets.
- **Không bao giờ trễ hẹn:** Hệ thống tính toán chính xác thời gian di chuyển (Google Maps Distance Matrix) và gửi cảnh báo khẩn cấp qua Slack nếu thời gian quá ít.
- **Hoạt động tự động 24/7:** Chạy định kỳ hàng ngày, giúp các sếp luôn có kế hoạch thư giãn hoàn hảo mà không cần suy nghĩ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Account** (Truy cập Google Calendar & Google Sheets).
- **Google Maps & Places API Key** (Đã bật các dịch vụ Distance Matrix API và Nearby Search API).
- Tài khoản **OpenRouter AI** (Lấy API Key để dùng cho AI Agent).
- Workspace **Slack** (Để nhận thông báo và cảnh báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy toàn bộ JSON từ n8n Hub, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Workflow Configuration (Set Node):** 
  - `currentLocation`: Nhập tọa độ hiện tại của các sếp (ví dụ: `35.6812,139.7671`) hoặc địa chỉ chính xác để tính khoảng cách và tìm quán cafe.
  - `googleMapsApiKey`: Nhập Google Maps API Key hợp lệ.
  - `googlePlacesApiKey`: Nhập Google Places API Key hợp lệ.
  - `minimumGapMinutes`: Thời gian trống tối thiểu để đề xuất đi cafe (mặc định là `30` phút).

- **Get Next Calendar Event (Google Calendar Node):**
  - Chọn đúng tài khoản Google Calendar và lịch cần theo dõi.
  - Thiết lập giới hạn lấy 1 sự kiện sắp diễn ra gần nhất (`Limit = 1`).

- **Get User Preferences (Google Sheets Node):**
  - Trỏ tới Google Sheet lưu sở thích cá nhân của các sếp (Document ID và Sheet Name).

- **OpenRouter Chat Model & AI Agent:**
  - Cấu hình Credentials cho OpenRouter để AI có thể phân tích và đưa ra gợi ý quán cafe chuẩn xác.

- **Send Slack Notification & Send Urgent Move Alert (Slack Nodes):**
  - **CỰC KỲ QUAN TRỌNG:** Thay thế Channel ID mẫu (`C09TPHE5C15`) bằng ID channel Slack thực tế của các sếp (ví dụ: `#general` hoặc channel riêng tư nhận thông báo).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm dữ liệu từ lịch hiện tại.
- Kiểm tra kết quả trên Slack, sau đó bật công tắc **Active** để workflow tự động chạy theo lịch hẹn (Mặc định 12 PM hàng ngày từ Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Có thể kết hợp thêm node Telegram hoặc Discord bên cạnh Slack để nhận thông báo trên nền tảng yêu thích.
- **Tùy biến khung giờ:** Thay đổi Schedule Trigger thành nhiều khung giờ khác nhau trong ngày (ví dụ: 9 AM, 12 PM, 3 PM) để nhận gợi ý linh hoạt hơn.
- **Lưu lịch sử:** Thêm một node Google Sheets ở cuối luồng để ghi lại các quán cafe đã từng ghé thăm, giúp AI đa dạng hóa lựa chọn cho những lần sau.

### 📌 Kết luận
Workflow **Gap-Time Cafe Finder** là một trợ lý thông minh tuyệt vời giúp tối ưu hóa từng phút giây trống trong ngày của các sếp. Hãy cài đặt ngay hôm nay để biến những khoảng thời gian chờ đợi thành những trải nghiệm thư giãn tuyệt vời bên ly cafe yêu thích!