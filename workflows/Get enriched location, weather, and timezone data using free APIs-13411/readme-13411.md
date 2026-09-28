---
title: "🚀 Tự động lấy dữ liệu Vị trí, Thời tiết & Múi giờ chi tiết bằng API miễn phí trong n8n"
description: "Hướng dẫn xây dựng workflow n8n chuyển đổi tọa độ GPS thành dữ liệu thông tin địa điểm toàn diện (28 trường thông tin) sử dụng các API miễn phí như OpenStreetMap, OpenWeatherMap, TimezoneDB."
slug: "lay-du-lieu-vi-tri-thoi-tiet-mui-gio-mien-phi-n8n"
tags: [n8n, automation, api, openweathermap, market-research, webhook]
keywords: [n8n workflow, api thời tiết miễn phí, lấy múi giờ qua tọa độ, openstreetmap n8n, tự động hóa n8n]
---

# 🚀 Tự động lấy dữ liệu Vị trí, Thời tiết & Múi giờ chi tiết bằng API miễn phí trong n8n

Các sếp có bao giờ cần tích hợp dữ liệu địa lý vào hệ thống CRM hoặc ứng dụng của mình nhưng lại đau đầu vì các dịch vụ trả phí đắt đỏ? Việc gọi thủ công nhiều nguồn API khác nhau (địa chỉ, thời tiết, múi giờ, mặt trời mọc/lặn) rồi gom nhóm lại cực kỳ tốn thời gian và dễ xảy ra sai sót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp gom toàn bộ dữ liệu chỉ với một cú gọi webhook đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tổng hợp 28 trường dữ liệu phong phú**: Nhận ngay địa chỉ chi tiết, múi giờ, thời gian thực, thời tiết hiện tại và thời gian mặt trời mọc/lặn chỉ từ tọa độ `lat` & `lon`.
- **Sử dụng API 100% miễn phí**: Tận dụng các nguồn uy tín như OpenStreetMap (Nominatim), TimezoneDB, OpenWeatherMap và Sunrise-Sunset mà không tốn phí bản quyền.
- **Tốc độ phản hồi cực nhanh**: Xử lý song song (parallel) các nguồn dữ liệu giúp giảm thiểu thời gian chờ đợi của ứng dụng.
- **Đầu ra chuẩn JSON**: Dễ dàng tích hợp trực tiếp vào chatbot, CRM, hệ thống báo cáo hoặc website.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản OpenWeatherMap**: Lấy API Key miễn phí tại [openweathermap.org](https://openweathermap.org/).
- **Tài khoản TimezoneDB**: Lấy API Key miễn phí tại [timezonedb.com](https://timezonedb.com/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này (hoặc tải file JSON từ kho lưu trữ n8n) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình các điểm sau:
- **Webhook - Accepts Coordinates**: Đảm bảo đường dẫn (path) được thiết lập là `geo-details`. Đây là endpoint nhận tọa độ `lat` và `lon`.
- **HTTP Request (Nominatim)**: Gọi API từ OpenStreetMap để lấy tên đường, quận, thành phố, quốc gia dựa vào tọa độ (Không cần API Key).
- **HTTP Request (TimezoneDB)**: Cần cấu hình `Credentials` loại Header/Query Auth với API Key lấy từ TimezoneDB để lấy thông tin múi giờ chính xác.
- **OpenWeatherMap**: Thêm `OpenWeatherMap API Credentials` của các sếp vào node này để lấy thông tin nhiệt độ, độ ẩm, trạng thái thời tiết.
- **HTTP Request (Sunrise-Sunset)**: Gọi API tính thời gian mặt trời mọc, lặn và độ dài ban ngày (Không cần API Key).
- **Merge & Edit Fields - Format & Structure Output**: Gộp toàn bộ kết quả từ 4 nguồn lại và định dạng thành 28 trường dữ liệu sạch sẽ, trực quan trước khi trả về qua **Respond to Webhook**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng cách gửi một request mẫu với `lat` và `lon` (Ví dụ: `lat=27.1751495&lon=78.0395673` - Taj Mahal).
- Kiểm tra xem kết quả JSON trả về đã đầy đủ 28 trường chưa.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

---

**Ví dụ Request mẫu:**
```bash
curl "https://n8n.example.com/webhook/geo-details?lat=27.1751495&lon=78.0395673"
```

**Phản hồi (Response JSON):**
```json
[
  {
    "lat": 27.1751495,
    "lon": 78.0395673,
    "timezone": "Asia/Kolkata",
    "timezone_short": "IST",
    "current_time": "10:25 PM",
    "current_date": "15-Feb-2026",
    "address_full": "Cicuit House Road, Taj Ganj, Agra, Uttar Pradesh, 282004, India",
    "temperature": "18.96",
    "weather_main": "Clear",
    "weather_description": "clear sky",
    "country_flag": "https://flagsapi.com/IN/flat/64.png"
  }
]
```

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử tra cứu**: Kết nối thêm node Google Sheets hoặc Supabase sau node `Respond to Webhook` để lưu lại lịch sử các tọa độ mà khách hàng hoặc hệ thống đã tra cứu.
- **Tích hợp Telegram/Slack Bot**: Tạo một lệnh `/weather [lat, lon]` trên Telegram để bot tự động gọi webhook này và trả về thông tin thời tiết tận nơi cho các sếp.
- **Cache dữ liệu**: Nếu một tọa độ được tra cứu nhiều lần, hãy thêm một bước kiểm tra database trước khi gọi API để tiết kiệm số lượng request miễn phí mỗi ngày.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại giá trị rất cao cho các ứng dụng cần khai thác dữ liệu không gian (Geospatial Data). Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình dữ liệu ngay hôm nay!