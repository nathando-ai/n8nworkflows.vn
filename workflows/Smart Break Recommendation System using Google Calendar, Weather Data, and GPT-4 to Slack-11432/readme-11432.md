---
title: "🚀 Hệ thống gợi ý điểm nghỉ ngơi thông minh sử dụng Google Calendar, dữ liệu thời tiết và GPT-4"
description: "Tự động tìm kiếm điểm nghỉ ngơi lý tưởng giữa các cuộc hẹn trong lịch của bạn, kết hợp thời tiết hiện tại và sở thích cá nhân để gửi thông báo gợi ý lên Slack"
slug: "he-thong-goi-y-diem-nghi-ngoi-thong-minh"
tags: [n8n, automation, no-code, google-calendar, slack, ai-chatbot]
keywords: [n8n workflow, tự động hóa, google calendar, slack, gpt-4, thời tiết, điểm nghỉ ngơi]
---

# 🚀 Hệ thống gợi ý điểm nghỉ ngơi thông minh sử dụng Google Calendar, dữ liệu thời tiết và GPT-4

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tự tìm kiếm điểm nghỉ ngơi phù hợp giữa các cuộc hẹn trong lịch trình bận rộn. Việc này tốn thời gian và đôi khi không chính xác vì không tính đến yếu tố thời tiết và sở thích cá nhân. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên tới 30 phút mỗi ngày cho việc tìm kiếm điểm nghỉ ngơi
- Nhận được gợi ý điểm nghỉ ngơi phù hợp với thời tiết và sở thích cá nhân
- Tự động hóa hoàn toàn quá trình tìm kiếm và gửi thông báo
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar đã được kết nối với n8n
- API key của Google Maps và Google Places
- API key của OpenWeatherMap
- Database Notion để lưu trữ sở thích cá nhân
- Tài khoản Slack đã được kết nối với n8n
- API key của OpenAI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/11432`
4. Nhấn "Import" để tải workflow vào n8n Editor

Hoặc bạn cũng có thể:
1. Truy cập vào link workflow gốc: [Smart Break Recommendation System](https://n8n.io/workflows/11432)
2. Nhấn vào nút "Download" để tải file JSON về máy
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Schedule Trigger**:
   - Cấu hình thời gian chạy workflow (mặc định là mỗi 30 phút)

2. **Set Configuration**:
   - Cấu hình các tham số cơ bản:
     - `currentLocation`: Địa điểm xuất phát của bạn
     - `minGapTimeMinutes`: Thời gian nghỉ tối thiểu để kích hoạt gợi ý (mặc định: 30 phút)
     - Các API keys cần thiết (Google Maps, Google Places, OpenWeatherMap)

3. **Get Next Calendar Event**:
   - Đảm bảo đã kết nối tài khoản Google Calendar với n8n
   - Kiểm tra xem node này có lấy được sự kiện tiếp theo trong lịch của bạn không

4. **Get User Preferences from Notion**:
   - Cấu hình kết nối Notion database chứa sở thích cá nhân của bạn
   - Đảm bảo database có cấu trúc phù hợp với workflow

5. **Get Weather at Destination**:
   - Cấu hình API key của OpenWeatherMap
   - Kiểm tra xem node này có lấy được dữ liệu thời tiết tại điểm đến không

6. **Get Travel Time via Google Maps**:
   - Cấu hình API key của Google Maps
   - Kiểm tra xem node này có tính toán đúng thời gian di chuyển không

7. **AI Generate Recommendations**:
   - Cấu hình API key của OpenAI
   - Kiểm tra xem node này có tạo được gợi ý phù hợp không

8. **Send Slack Notification**:
   - Cấu hình kết nối Slack với n8n
   - Kiểm tra xem thông báo có được gửi đúng đến channel mong muốn không

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấn vào nút "Activate" để kích hoạt workflow
2. Để kiểm tra workflow hoạt động đúng, bạn có thể:
   - Chạy thử với dữ liệu mẫu
   - Kiểm tra các log để đảm bảo không có lỗi xảy ra
   - Xem thông báo trên Slack để xác nhận rằng hệ thống đang hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể mở rộng workflow này bằng cách thêm các node mới để:
  - Gửi thông báo đến Telegram hoặc Discord thay vì Slack
  - Lưu log các gợi ý đã gửi để theo dõi lịch sử
  - Thêm các tiêu chí lọc bổ sung như giá cả, khoảng cách, hoặc đánh giá
  - Tích hợp với các dịch vụ khác như Uber hoặc Grab để đặt xe đến điểm nghỉ ngơi

### 📌 Kết luận
Hệ thống gợi ý điểm nghỉ ngơi thông minh này sẽ giúp các sếp tiết kiệm thời gian và nhận được gợi ý điểm nghỉ ngơi phù hợp với thời tiết và sở thích cá nhân. Với việc tự động hóa hoàn toàn quá trình này, các sếp có thể tập trung vào công việc quan trọng hơn. Hãy thử áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của workflow này!