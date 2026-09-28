---
title: "🌧️ Theo dõi thời tiết hàng giờ với OpenWeatherMap và Google Sheets"
description: "Tự động hóa theo dõi thời tiết hàng giờ, lưu dữ liệu vào Google Sheets và nhận cảnh báo mưa - giải pháp hoàn hảo cho các sếp quản lý dự án ngoài trời."
slug: "theo-doi-thoi-tiet-hang-gio-voi-openweathermap-va-google-sheets"
tags: [n8n, automation, no-code, weather, google-sheets]
keywords: [n8n workflow, tự động hóa thời tiết, OpenWeatherMap, Google Sheets, cảnh báo mưa]
---

# 🌧️ Theo dõi thời tiết hàng giờ với OpenWeatherMap và Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi thời tiết hàng giờ để lên kế hoạch cho các dự án ngoài trời. Việc kiểm tra thủ công trên ứng dụng thời tiết hoặc trang web thường tốn thời gian và dễ bỏ sót. Workflow này sẽ giúp các sếp tự động hóa quy trình này, lưu dữ liệu vào Google Sheets và nhận cảnh báo mưa một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Dữ liệu thời tiết được cập nhật tự động hàng giờ vào Google Sheets.
- Nhận cảnh báo mưa ngay lập tức để lên kế hoạch kịp thời.
- Tiết kiệm thời gian và giảm thiểu lỗi do quên kiểm tra thời tiết.
- Dễ dàng theo dõi lịch sử thời tiết để phân tích và lập kế hoạch dài hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key từ OpenWeatherMap.
- Thiết lập Credentials cho Google Sheets và OpenWeatherMap trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và nhập URL: [https://n8n.io/workflows/4066](https://n8n.io/workflows/4066).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Thiết lập thời gian chạy hàng giờ (ví dụ: mỗi giờ một lần).
   - Chọn múi giờ phù hợp với khu vực của các sếp.

2. **Google Sheets**:
   - Chọn credentials đã thiết lập cho Google Sheets.
   - Nhập Spreadsheet ID và Sheet Name nơi dữ liệu sẽ được lưu.
   - Đảm bảo tài khoản Google có quyền truy cập vào bảng tính này.

3. **Get Weather Data from OpenWeatherMap**:
   - Chọn credentials đã thiết lập cho OpenWeatherMap.
   - Nhập thông tin thành phố và mã quốc gia (ví dụ: "Hanoi,VN").
   - Đảm bảo API Key từ OpenWeatherMap còn hiệu lực.

4. **If is raining**:
   - Điều kiện kiểm tra: `{{ $node["Get Weather Data from OpenWeatherMap"].json["weather"][0]["main"] }} === "Rain"`.
   - Thiết lập hành động khi điều kiện đúng (ví dụ: gửi cảnh báo qua email hoặc Slack).

5. **Format the data**:
   - Thiết lập các trường dữ liệu cần lưu vào Google Sheets (ví dụ: thời gian, nhiệt độ, độ ẩm, trạng thái thời tiết).

#### 3. Kích hoạt ⚡️
- Nhấn nút "Execute Workflow" để kiểm tra dữ liệu mẫu.
- Sau khi kiểm tra thành công, nhấn "Activate" để workflow chạy tự động hàng giờ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận cảnh báo mưa ngay lập tức.
- Thêm node để gửi báo cáo thời tiết hàng ngày qua email.
- Lưu trữ dữ liệu thời tiết lâu dài để phân tích xu hướng thời tiết.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi thời tiết hàng giờ, lưu dữ liệu vào Google Sheets và nhận cảnh báo mưa một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi do quên kiểm tra thời tiết!