---
title: "🌿 **Tự Động Hóa Nhắc Nhở Chăm Sóc Thực Vật Với OpenWeather, Google Sheets & Telegram** – Không Cần Code!"
description: "Workflow tự động nhắc nhở chăm sóc cây trồng thông minh với dự báo thời tiết, lịch trình tưới nước và bón phân, đồng thời ghi log tất cả hành động. Giúp các sếp tiết kiệm thời gian, tránh quên chăm sóc cây và tối ưu hóa sức khỏe thực vật 24/7."
slug: "tieu-dong-hoa-nhac-nho-cham-soc-thuc-vat"
tags: [n8n, automation, no-code, google-sheets, telegram-bot, openweather-api, personal-productivity]
keywords: [tự động hóa chăm sóc cây, nhắc nhở tưới nước, bón phân tự động, n8n workflow, google sheets api, telegram bot, openweather api]
---

# 🌿 **Tự Động Hóa Nhắc Nhở Chăm Sóc Thực Vật Với OpenWeather, Google Sheets & Telegram**

## **🌱 Bạn đã bao giờ quên tưới nước cho cây?**
Cây trồng của các sếp không chỉ là trang trí mà còn là một phần của gia đình, văn phòng hoặc không gian sống. Tuy nhiên, với cuộc sống bận rộn, việc nhớ đến việc tưới nước, bón phân và theo dõi điều kiện thời tiết để chăm sóc cây một cách khoa học là một thách thức lớn. **Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình chăm sóc cây thông minh, kết hợp dữ liệu thời tiết, lịch trình cá nhân hóa và nhắc nhở qua Telegram!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động nhắc nhở tưới nước và bón phân** dựa trên lịch trình cá nhân hóa.
- **Dự báo thời tiết** từ OpenWeather API để điều chỉnh lịch trình (không tưới nếu mưa).
- **Ghi log tất cả hành động** trên Google Sheets để theo dõi lịch sử chăm sóc.
- **Cá nhân hóa thông báo** qua Telegram với các tùy chọn như "Chế độ nghỉ mát" (vacation mode).
- **Tối ưu hóa sức khỏe cây** bằng cách kết hợp dữ liệu thời tiết và nhu cầu riêng của từng loại cây.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **Google Sheets** với 3 bảng dữ liệu:
   - **plants** (thông tin về cây trồng).
   - **settings** (cài đặt chung như chế độ nghỉ mát và múi giờ).
   - **log** (ghi log tất cả hành động).
3. **API Key OpenWeather** (để lấy dữ liệu thời tiết).
4. **Bot Telegram** và **Chat ID** của các sếp (để nhận thông báo).
5. **URL Webhook** (để xác nhận hành động tưới nước/bón phân).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này bao gồm **2 phần chính**:
- **Workflow chính** (lịch trình tự động nhắc nhở).
- **Sub-workflow Webhook** (xác nhận hành động từ Telegram).

**Cách import:**
1. Tải file JSON của workflow từ [n8n.io/workflows/9953](https://n8n.io/workflows/9953).
2. Mở **n8n Editor** và chọn **Import Workflow** (từ menu).
3. Chọn file JSON và nhấn **Import**.
4. Lặp lại bước trên cho **Sub-workflow Webhook**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **📌 Cấu hình Google Sheets**
Các sếp cần tạo **3 bảng Google Sheets** với cấu trúc sau:

| **Bảng**  | **Cột**                          | **Giá trị mẫu**                          |
|------------|-----------------------------------|------------------------------------------|
| **plants** | id, plant, last_water, water_freq, last_fert, fert_freq, lat, lon, weather_delay, indoor, thirst_level | `p001, Monstera, Monstera deliciosa, indoor, 33.44, 94.04, 2025-10-20, 2d, 2025-10-20, 4m, TRUE, med` |
| **settings** | vacation_mode, timezone          | `off, Europe/Madrid`                     |
| **log**     | ts, plant_id, action             | (Auto ghi log khi thực hiện hành động) |

##### **📌 Cấu hình OpenWeather API**
- Trong node **OpenWeather request**, các sếp cần điền:
  - `lat` và `lon` (tọa độ vị trí của cây).
  - `appid` (API Key từ OpenWeather).
  - `units=metric` (đơn vị đo nhiệt độ là Celsius).

##### **📌 Cấu hình Telegram Bot**
1. Tạo bot Telegram và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
2. Trong node **Telegram**, điền:
   - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
   - **Chat ID**: Thay thế `{YOUR_CHAT_ID}` bằng Chat ID của các sếp.
   - **Parse Mode**: Chọn **HTML** (để thông báo đẹp hơn).
   - **Inline Button URL**: Thay thế `{YOUR_PROJECT_URL}` bằng URL Webhook của các sếp (ví dụ: `https://tinohost.vn/webhook/plant-confirm`).

##### **📌 Cấu hình Webhook**
1. Trong node **Webhook**, các sếp cần:
   - Chọn **keyParameters > path**: `plant-confirm`.
   - Điền **URL Webhook** vào **Principal Workflow** (trong node **Prepare Data**).
   - Kích hoạt Webhook để nhận xác nhận từ Telegram.

##### **📌 Cấu hình Schedule Trigger**
- Trong node **Schedule Trigger**, các sếp có thể chọn:
  - **Lịch trình chạy hàng ngày** (ví dụ: 8h sáng).
  - **Múi giờ** phù hợp (đối chiếu với `timezone` trong bảng **settings**).

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy workflow và kiểm tra thông báo Telegram.
   - Kiểm tra bảng **log** để xác nhận ghi log thành công.
2. **Bật Active workflow**:
   - Sau khi kiểm tra xong, các sếp có thể **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm nhiều vị trí cây**:
   - Mỗi cây có thể có tọa độ khác nhau (lat/lon) để lấy dữ liệu thời tiết chính xác.
2. **Cài đặt chế độ nghỉ mát (Vacation Mode)**:
   - Khi đi du lịch, các sếp chỉ cần đổi `vacation_mode` thành **"on"** trong bảng **settings**, workflow sẽ ngừng gửi nhắc nhở.
3. **Tự động cập nhật thời gian tưới/bón**:
   - Sau khi xác nhận hành động qua Telegram, workflow sẽ tự động cập nhật `last_water` và `last_fert` trong bảng **plants**.
4. **Gửi báo cáo định kỳ**:
   - Sử dụng **Google Sheets API** để gửi báo cáo tổng hợp về tình trạng cây qua Telegram hàng tuần.
5. **Kết hợp với Home Assistant**:
   - Nếu các sếp sử dụng **Home Assistant**, có thể kết nối với workflow này để tự động mở van tưới nước khi nhận được nhắc nhở.

---

### 📌 **Kết luận**
Workflow này không chỉ giúp các sếp **không bao giờ quên chăm sóc cây** mà còn tối ưu hóa quy trình chăm sóc bằng cách kết hợp **dữ liệu thời tiết, lịch trình cá nhân hóa và tự động hóa hoàn toàn**. **Hãy thử ngay và biến không gian xanh của mình trở nên thông minh hơn!**

👉 **Bắt đầu tự động hóa ngay hôm nay!**
[🔗 Tải workflow từ n8n.io](https://n8n.io/workflows/9953) | [📌 Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)