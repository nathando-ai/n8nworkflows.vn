---
title: "🌦️ Tự động hóa Dự báo Thời tiết Nhiều Thành phố với AI và Gmail"
description: "Workflow n8n tự động gửi báo cáo thời tiết 5 ngày cho nhiều thành phố với định dạng HTML chuyên nghiệp do AI tạo ra và gửi qua Gmail"
slug: "tu-dong-hoa-du-bao-thoi-tiet-nhieu-thanh-pho-voi-ai-va-gmail"
tags: [n8n, automation, no-code, openweathermap, gmail, ai, openai]
keywords: [n8n workflow, tự động hóa thời tiết, dự báo thời tiết, openweathermap, gmail, ai, openai]
---

# 🌦️ Tự động hóa Dự báo Thời tiết Nhiều Thành phố với AI và Gmail

[Các sếp] có bao giờ phải kiểm tra thời tiết cho nhiều thành phố mỗi ngày không? Với workflow này, các sếp có thể tự động hóa hoàn toàn quá trình này với định dạng HTML chuyên nghiệp do AI tạo ra và gửi qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quá trình lấy dữ liệu và gửi báo cáo
- **Định dạng chuyên nghiệp**: Báo cáo thời tiết được tạo ra với định dạng HTML đẹp mắt và màu sắc theo điều kiện thời tiết
- **Cá nhân hóa**: Có thể chọn tối đa 3 thành phố để theo dõi
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày, không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenWeatherMap API (để lấy dữ liệu thời tiết)
- API key OpenAI (để tạo báo cáo thời tiết bằng AI)
- Tài khoản Gmail và xác thực OAuth2 (để gửi email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và nhập link: https://n8n.io/workflows/9909
3. Hoặc copy nội dung JSON từ file workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "TRIGGER - Input City Names"**:
   - Cấu hình form trigger để nhận tối đa 3 thành phố
   - Đảm bảo các trường nhập liệu có tên là "city1", "city2", "city3"

2. **Node "HTTP - OWM Geocoding"**:
   - Cấu hình credentials với OpenWeatherMap API key
   - Đảm bảo URL là: `https://api.openweathermap.org/geo/1.0/direct`

3. **Node "OpenWeatherMap (OWM) - 5 Day Forecast (by City)"**:
   - Cấu hình credentials với OpenWeatherMap API key
   - Đảm bảo chọn operation là "5DayForecast"

4. **Node "LLM - AI Weather Briefing Composer"**:
   - Cấu hình credentials với OpenAI API key
   - Đảm bảo chọn model là GPT-4
   - Sử dụng prompt sau (có thể tùy chỉnh):
     ```
     You are a professional weather reporter. Create a subject and HTML email body for a weather briefing for the following cities:
     {{{JSON.stringify($node["JS - Bundle Cities for LLM"].json)}}}

     The email should include:
     1. A summary of the weather for each city
     2. Color-coded temperature ranges (green for pleasant, yellow for moderate, red for extreme)
     3. Safety precautions for any extreme weather conditions
     4. A 5-day forecast for each city

     Return the result as a JSON object with "subject" and "html" properties.
     ```

5. **Node "GMAIL - Send Weather Briefing"**:
   - Cấu hình credentials với Gmail OAuth2
   - Điền địa chỉ email người nhận
   - Đảm bảo các trường subject và body được lấy từ output của node trước đó

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra email để đảm bảo báo cáo thời tiết được gửi đúng định dạng
3. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm thông báo Slack/Telegram**: Kết nối thêm node để gửi báo cáo thời tiết đến kênh Slack hoặc nhóm Telegram
2. **Lưu log lịch sử**: Thêm node để lưu trữ lịch sử báo cáo thời tiết vào Google Sheets hoặc cơ sở dữ liệu
3. **Tùy chỉnh định dạng**: Thay đổi prompt cho node LLM để tạo báo cáo thời tiết theo phong cách riêng của công ty
4. **Thêm cảnh báo thời tiết**: Kết hợp với node HTTP để gửi cảnh báo thời tiết khẩn cấp đến các thiết bị IoT

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc theo dõi thời tiết hàng ngày. Với định dạng HTML chuyên nghiệp do AI tạo ra và gửi tự động qua Gmail, các sếp có thể dễ dàng theo dõi thời tiết cho nhiều thành phố trong một báo cáo duy nhất. Hãy thử áp dụng ngay để nâng cao hiệu suất làm việc!