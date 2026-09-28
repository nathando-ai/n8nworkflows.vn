---
title: "🚀 Tự Động Hóa Cảnh Báo Sao Chổi Gần Trái Đất với NASA API, Slack & Google Calendar"
description: "Workflow tự động hóa 24/7 tra cứu và cảnh báo về các thiên thạch gần Trái Đất từ NASA API, gửi thông báo trên Slack và thêm sự kiện vào Google Calendar. Giúp các sếp theo dõi an toàn không gian một cách chuyên nghiệp và không cần code."
slug: "tieu-dong-hoa-can-bao-sao-choi-nhat-qua-nasa-api-slack-google-calendar"
tags: [n8n, automation, no-code, api-integration, nasa, google-calendar, slack, schedule-trigger]
keywords: [n8n workflow tự động hóa, cảnh báo thiên thạch NASA, tự động hóa Slack, API NASA, Google Calendar tự động, cảnh báo không gian]
---

# 🚀 **Tự Động Hóa Cảnh Báo Sao Chổi Gần Trái Đất với NASA API, Slack & Google Calendar**

### **Giải quyết vấn đề gì?**
Các sếp quản lý an toàn hoặc công ty nghiên cứu không gian thường phải theo dõi thủ công các thông tin về thiên thạch gần Trái Đất từ NASA API. Việc này tốn thời gian, dễ bỏ sót và không thể thực hiện liên tục 24/7. **Workflow này tự động hóa toàn bộ quy trình:**
- Tra cứu dữ liệu thiên thạch gần Trái Đất từ NASA API **hai lần/ngày**.
- Lọc ra các thiên thạch nguy hiểm (cách gần, kích thước lớn).
- Gửi **thông báo cảnh báo** trên Slack.
- **Tạo sự kiện** trong Google Calendar để theo dõi lịch sử và cảnh báo tương lai.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần tra cứu thủ công hàng ngày.
- **Cảnh báo kịp thời:** Nhận thông báo ngay khi có thiên thạch nguy hiểm.
- **Tự động hóa hoàn toàn:** Chạy 24/7 mà không cần can thiệp.
- **Tích hợp đa nền tảng:** Slack + Google Calendar cho quản lý dễ dàng.
- **Cá nhân hóa:** Điều chỉnh độ nhạy của cảnh báo theo yêu cầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **NASA API Key** (miễn phí):
   - Đăng ký tại [api.nasa.gov](https://api.nasa.gov/) và lấy **API Key** riêng.
   - *Lưu ý:* Key demo có giới hạn nghiêm ngặt, không phù hợp cho sử dụng thường xuyên.
2. **Credentials Slack OAuth2**:
   - Tạo bot Slack tại [api.slack.com](https://api.slack.com/apps) và lấy **OAuth Token**.
   - Chọn **channel** để gửi cảnh báo (ví dụ: `#asteroid-alerts`).
3. **Credentials Google Calendar OAuth2**:
   - Tạo ứng dụng Google Calendar tại [Google Cloud Console](https://console.cloud.google.com/).
   - Lấy **Client ID** và **Client Secret** để kết nối.
4. **Tài khoản Google Calendar** để lưu trữ sự kiện.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [liên kết gốc](https://n8n.io/workflows/9877) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ mã JSON từ [liên kết trên] và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình NASA API**
- **Node:** *"Get an asteroid neo feed"*
  - Đi đến **Credentials** và chọn `nasaApi`.
  - Thay thế `DEMO_KEY` trong **keyParameters** bằng **NASA API Key** của bạn.
  - Ví dụ:
    ```json
    "apiKey": "TUYEN_API_KEY_CUA_BAN"
    ```

##### **B. Điều chỉnh tiêu chí lọc thiên thạch**
- **Node:** *"Filter and Process Asteroids"* (Code Node)
  - Mở **Code Editor** và chỉnh sửa hai biến:
    ```javascript
    const MAX_DISTANCE_KM = 7500000; // Giá trị mặc định: 75 triệu km (điều chỉnh thành 7.5 triệu km)
    const MIN_DIAMETER_METERS = 100; // Kích thước tối thiểu: 100 mét
    ```
  - *Lưu ý:* Giá trị mặc định trong demo quá lớn (75 tỷ km), nên điều chỉnh xuống để phù hợp.

##### **C. Cấu hình Slack**
- **Node:** *"Send Slack Alert"*
  - Chọn **Credentials** và chọn `slackOAuth2Api`.
  - Chọn **channel** muốn gửi cảnh báo (ví dụ: `#asteroid-alerts`).
  - *Lưu ý:* Bot Slack cần quyền **post** vào channel đó.

##### **D. Cấu hình Google Calendar**
- **Node:** *"Create an event"*
  - Chọn **Credentials** và chọn `googleCalendarOAuth2Api`.
  - Chọn **Google Calendar** muốn lưu sự kiện.
  - *Tùy chọn:* Thay đổi tiêu đề, mô tả và màu sắc sự kiện trong **Code Node** *"Format Alert Messages"*.

##### **E. Xử lý trường hợp "Không có thiên thạch"**
- **Node:** *"No Operation, do nothing"*
  - Hiện tại, workflow sẽ **ngừng hoạt động** khi không có cảnh báo.
  - *Mẹo:* Thay thế bằng **node Slack** để gửi tin nhắn **"All Clear"** hàng ngày.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run:** Chọn **Run Workflow** và kiểm tra kết quả.
2. **Bật Active:** Đặt **Active** thành `true` để workflow chạy tự động theo lịch.
3. **Kiểm tra Slack & Calendar:** Đảm bảo cảnh báo được gửi đúng.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng độ nhạy cảnh báo:**
   - Giảm `MAX_DISTANCE_KM` xuống **1 triệu km** để bắt kịp thiên thạch nguy hiểm hơn.
   - Giảm `MIN_DIAMETER_METERS` xuống **50 mét** (những thiên thạch nhỏ cũng có thể gây nguy hiểm).

2. **Tích hợp Telegram:**
   - Thêm **node Telegram Bot** để gửi cảnh báo song song với Slack.

3. **Lưu log cảnh báo:**
   - Thêm **node Google Sheets** để ghi lại lịch sử cảnh báo cho phân tích dài hạn.

4. **Báo cáo định kỳ:**
   - Sử dụng **node Email** để gửi báo cáo tuần/month về các thiên thạch đã cảnh báo.

5. **Cảnh báo SMS:**
   - Kết nối với **Twilio API** để gửi tin nhắn SMS cho quản lý khi có thiên thạch nguy hiểm.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** việc theo dõi thiên thạch gần Trái Đất, giảm thiểu rủi ro và tiết kiệm thời gian. **Bắt đầu ngay bằng cách:**
1. Import workflow và cấu hình các credentials.
2. Điều chỉnh tiêu chí lọc theo nhu cầu.
3. Bật **Active** và theo dõi cảnh báo trên Slack & Google Calendar!

**🚀 Hãy tự động hóa không gian của bạn ngay hôm nay!** 🌍✨