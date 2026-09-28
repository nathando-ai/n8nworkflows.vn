---
title: "🌤️ Tự Động Hóa Báo Cáo Thời Tiết Tự Động Với Bright Data & n8n – Không Cần Code!"
description: "Workflow này giúp các sếp tự động lấy dữ liệu thời tiết từ website, xử lý thông tin và ghi vào Google Sheets 24/7 – tiết kiệm thời gian lên đến 80% so với cách làm thủ công. Phù hợp cho nghiên cứu khí tượng, dự báo thời tiết cá nhân hoặc xây dựng dashboard thời tiết chuyên nghiệp."
slug: "tieu-dong-hoa-bao-cao-thoi-tiet-voi-bright-data-n8n"
tags: [n8n, automation, no-code, web-scraping, google-sheets, ai, bright-data]
keywords: [n8n workflow thời tiết, tự động hóa lấy dữ liệu thời tiết, Bright Data proxy, scrape website thời tiết, Google Sheets tự động, không cần code]
---

# 🚀 **Tự Động Hóa Báo Cáo Thời Tiết Tự Động Với Bright Data & n8n**

## **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** thông tin thời tiết từ nhiều nguồn khác nhau (website, app, API).
- **Ghi chép lại** dữ liệu vào Excel/Google Sheets một cách mệt mỏi, dễ sai sót.
- **Không có dữ liệu lịch sử** để phân tích xu hướng thời tiết dài hạn.
- **Lo ngại bị chặn IP** khi scrape website thời tiết (nhất là với các trang có bảo vệ chống bot).

**Workflow này giải quyết tất cả!** Với chỉ một cú nhấp chuột, n8n sẽ:
✅ **Lấy dữ liệu thời tiết** từ website (même với bảo vệ chống bot).
✅ **Trích xuất thông tin quan trọng** (nhiệt độ, độ ẩm, tình trạng thời tiết).
✅ **Ghi tự động vào Google Sheets** để theo dõi lịch sử và phân tích.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và không bị gián đoạn**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh phụ thuộc vào phiên bản miễn phí có giới hạn.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải copy-paste dữ liệu mỗi ngày (giảm 80% công việc thủ công).
- **Dữ liệu chính xác**: Tránh sai sót khi ghi chép thủ công.
- **Lịch sử dài hạn**: Theo dõi xu hướng thời tiết trong nhiều năm để dự báo.
- **Không bị chặn**: Bright Data giúp scrape website an toàn, không lo bị IP bị block.
- **Cá nhân hóa**: Thêm cột tùy chỉnh (ví dụ: "Lưu ý đặc biệt" như mưa lớn, gió lốc).
- **Hoạt động tự động**: Bật workflow và nó sẽ chạy mỗi ngày (hoặc theo lịch trình).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape website an toàn):
   - [Đăng ký miễn phí Bright Data](https://get.brightdata.com/1tndi4600b25) (sẽ nhận commission nhỏ giúp hỗ trợ nội dung miễn phí).
   - **Lưu ý**: Chọn gói **Residential Proxies** để tránh bị chặn.
2. **Tài khoản Google Sheets** và một **Google Sheet trống** để lưu dữ liệu.
3. **API Key Google Sheets OAuth2**:
   - Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và cấp quyền cho n8n.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí có giới hạn).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5226) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào tab "Import" của n8n.

**Cách import nhanh:**
1. Mở n8n Editor → Nhấn **"Import"** ở góc trên bên phải.
2. Chọn **"From JSON"** và dán nội dung JSON từ file.
3. Nhấn **"Import"** để workflow xuất hiện trên canvas.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **4 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **Node 1: Start Workflow (manualTrigger)**
- **Loại**: Trigger thủ công hoặc theo lịch.
- **Cách sử dụng**:
  - Nhấn **"Run"** để chạy ngay.
  - **Khuyến nghị**: Thêm **Schedule Trigger** (n8n-nodes-base.scheduleTrigger) để chạy tự động hàng ngày (ví dụ: 8h sáng).
  - **Cấu hình**:
    - Chọn **"Manual Trigger"** (hoặc **"Schedule"** nếu muốn tự động).
    - Đặt tên node là **"Bắt đầu lấy dữ liệu thời tiết"**.

##### **Node 2: Request/Fetch Weather via Bright Data (httpRequest)**
- **Loại**: Gửi yêu cầu HTTP đến website thời tiết.
- **Cấu hình quan trọng**:
  - **URL**: Điền **URL của trang thời tiết** bạn muốn scrape (ví dụ: `https://www.weather.com/weather/today/l/...`).
  - **Headers**:
    - Thêm `User-Agent`: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`.
  - **Proxy Bright Data**:
    - Trong tab **"Advanced"**, chọn **"Use Proxy"** và điền:
      - **Proxy URL**: `http://<your-brightdata-ip>:<port>` (tham khảo tài liệu Bright Data).
      - **Username/Password**: Điền credentials từ tài khoản Bright Data.
  - **Method**: `GET`.
  - **Response Format**: `JSON` (hoặc `Text` nếu cần).

##### **Node 3: Extract Weather Info (html)**
- **Loại**: Trích xuất dữ liệu từ HTML.
- **Cấu hình quan trọng**:
  - **Operation**: `extractHtmlContent`.
  - **CSS Selectors**:
    - Các sếp cần **tìm hiểu CSS selectors** của trang thời tiết mục tiêu (sử dụng công cụ như [Chrome DevTools](https://developer.chrome.com/docs/devtools/)) và điền vào:
      - **Temperature**: `div.weather-temp` (ví dụ).
      - **Humidity**: `span.humidity-value`.
      - **Conditions**: `div.weather-description`.
    - **Lưu ý**: Nếu không biết CSS selectors, hãy liên hệ với tác giả Yaron Been qua [LinkedIn](https://www.linkedin.com/in/yaronbeen/) để hỗ trợ.

##### **Node 4: Log to Weather Sheet (googleSheets)**
- **Loại**: Ghi dữ liệu vào Google Sheets.
- **Cấu hình quan trọng**:
  - **Credentials**: Chọn **"googleSheetsOAuth2Api"** (đã cấu hình trước).
  - **Operation**: `append` (thêm dữ liệu mới vào cuối sheet).
  - **Sheet Name**: Điền tên **Google Sheet** bạn muốn lưu dữ liệu (ví dụ: `"Báo cáo thời tiết"`).
  - **Range**: `Sheet1!A1` (hoặc tên cột cụ thể như `"A1:D1"` nếu muốn định dạng).
  - **Headers**: Bật **"Use as headers"** (nếu lần đầu tiên chạy).
  - **Data Format**:
    - **Temperature**: `$json["temperature"]`.
    - **Humidity**: `$json["humidity"]`.
    - **Conditions**: `$json["conditions"]`.
    - **Timestamp**: `$now` (để ghi thời gian lấy dữ liệu).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run"** trên node **Start Workflow** để kiểm tra.
   - Kiểm tra **Google Sheets** xem dữ liệu có được ghi không.
2. **Bật Active**:
   - Chuyển tất cả node sang trạng thái **"Active"**.
   - Nếu muốn **tự động hóa**, thêm **Schedule Trigger** vào node đầu tiên.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm cảnh báo thời tiết khẩn cấp**:
   - Sử dụng **n8n-nodes-base.if** để kiểm tra nếu nhiệt độ > 40°C hoặc có mưa lớn → gửi thông báo qua **Slack/Email** (n8n-nodes-base.slack hoặc n8n-nodes-base.email).
   - **Cách làm**:
     ```json
     {
       "operation": "if",
       "condition": "$json['temperature'] > 40",
       "then": "nodeNameSendAlert"
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm **n8n-nodes-base.stickyNote** để ghi lại lỗi hoặc thông tin debug.
   - Ví dụ: `"Lỗi: $errorMessage"` (nếu request thất bại).

3. **Tích hợp với Telegram/Email báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.telegram** hoặc **n8n-nodes-base.email** để gửi báo cáo hàng tuần.
   - **Cấu hình**:
     - **Subject**: `"Báo cáo thời tiết tuần ${$now.format('YYYY-MM-DD')}"`.
     - **Body**: `"Nhiệt độ trung bình: $avgTemp\nĐộ ẩm: $avgHumidity"`.

4. **Tự động hóa với API thời tiết**:
   - Thay vì scrape website, các sếp có thể sử dụng **API thời tiết** (ví dụ: OpenWeatherMap) để lấy dữ liệu chính xác hơn.
   - **Cách làm**:
     - Thêm node **n8n-nodes-base.httpRequest** với URL API.
     - Thay thế node **Extract Weather Info** bằng **n8n-nodes-base.set** để định dạng dữ liệu.

5. **Tạo dashboard thời tiết**:
   - Sử dụng **Google Data Studio** hoặc **Power BI** để tạo dashboard từ dữ liệu trong Google Sheets.
   - **Bước 1**: Xuất dữ liệu từ Sheets.
   - **Bước 2**: Tạo biểu đồ nhiệt độ, độ ẩm theo thời gian.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần:
✔ **Tự động hóa lấy dữ liệu thời tiết** mà không cần code.
✔ **Tiết kiệm thời gian** và tránh sai sót khi ghi chép thủ công.
✔ **Xây dựng lịch sử dữ liệu** để phân tích xu hướng.
✔ **Hoạt động 24/7** trên VPS riêng.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình Bright Data + Google Sheets.
3. **Bật tự động hóa** và bắt đầu theo dõi thời tiết như một chuyên gia!

---
**Cần hỗ trợ?**
- Liên hệ tác giả Yaron Been qua [LinkedIn](https://www.linkedin.com/in/yaronbeen/).
- Đăng ký **Bright Data** qua [link này](https://get.brightdata.com/1tndi4600b25) để hỗ trợ nội dung miễn phí.
- Theo dõi kênh YouTube của Yaron: [@YaronBeen](https://www.youtube.com/@YaronBeen/videos).