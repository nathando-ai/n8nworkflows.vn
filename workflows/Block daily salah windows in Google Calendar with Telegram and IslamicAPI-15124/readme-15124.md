---
title: "🕋 **Tự Động Chặn Khung Giờ Nam Azan Trên Google Calendar Với Telegram & IslamicAPI** – Không Cần Code!"
description: "Workflow này tự động tạo 5 sự kiện Google Calendar cho khung giờ Nam Azan (Fajr, Duhr, Asr, Maghrib, Isha) dựa trên yêu cầu từ Telegram, đồng thời ghi log và thông báo kết quả. Giúp các sếp Hồi giáo quản lý thời gian cầu nguyện hiệu quả 100% tự động."
slug: "tieu-dong-chan-khung-gio-nam-azan-google-calendar-telegram"
tags: [n8n, automation, islamic-productivity, google-calendar, telegram-bot, no-code]
keywords: [tự động hóa nam azan, workflow n8n google calendar, tự động hóa cầu nguyện, IslamicAPI n8n, tự động hóa Telegram Google Calendar]
---

# 🕋 **Tự Động Chặn Khung Giờ Nam Azan Trên Google Calendar Với Telegram**

## **🔥 Nỗi Đau Của Các Sếp Hồi Giáo**
Bạn có bao giờ phải:
- **Nhớ nhắc** thời gian Nam Azan hàng ngày?
- **Lo lắng** quên cầu nguyện vì bị bận công việc?
- **Tốn thời gian** phải tra cứu thời gian cầu nguyện trên ứng dụng?
- **Không có hệ thống** để tự động hóa quy trình cầu nguyện?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tạo tự động** 5 sự kiện Google Calendar cho khung giờ Nam Azan (Fajr, Duhr, Asr, Maghrib, Isha).
✅ **Gửi thông báo** kết quả qua Telegram với thời gian cụ thể.
✅ **Ghi log** tất cả các lần đặt lịch vào Google Sheets.
✅ **Chỉ hoạt động** khi bạn gửi lệnh `/salah` từ Telegram (không bị spam).
✅ **Không tốn chi phí** – tất cả API đều miễn phí.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thời gian cầu nguyện hàng ngày.
- **Đảm bảo không quên**: Google Calendar tự động nhắc nhở khi đến giờ.
- **Tính cá nhân hóa**: Thời gian Nam Azan được tính toán chính xác theo vị trí Cairo (có thể điều chỉnh).
- **Ghi chép toàn bộ lịch sử**: Tất cả các lần đặt lịch được lưu vào Google Sheets.
- **Thông báo tức thời**: Kết quả được gửi qua Telegram ngay sau khi đặt lịch.
- **An toàn & riêng tư**: Chỉ người dùng được phép (không bị spam).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo **bot Telegram** và lấy **API Token** từ [@BotFather](https://t.me/BotFather).
   - Lấy **Chat ID** của mình từ [@userinfobot](https://t.me/userinfobot) (gửi tin nhắn `/start`).
2. **Tài khoản Google**:
   - **Google Calendar** (để tạo sự kiện).
   - **Google Sheets** (để lưu log).
   - Cấu hình **OAuth2 Credentials** cho cả 2 dịch vụ trong n8n (hướng dẫn [đây](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)).
3. **API Key IslamicAPI**:
   - Đăng ký miễn phí tại [IslamicAPI](https://islamicapi.com/signup/), lấy **API Key** từ Dashboard.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15124](https://n8n.io/workflows/15124) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15124) và dán vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **3 điểm cần thay đổi** trước khi kích hoạt:

#### **A. Thay đổi Chat ID trong các Node**
- Node **"Validate the sender"** và **"Send the message"** sử dụng placeholder `[Your chat ID]`.
- **Lấy Chat ID** từ [@userinfobot](https://t.me/userinfobot) (gửi `/start` và copy ID trong tin nhắn trả lời).
- **Thay thế** `[Your chat ID]` bằng Chat ID của bạn trong **3 node sau**:
  1. **"Validate the sender"** (trong điều kiện `$.chat.id === "YOUR_CHAT_ID"`).
  2. **"Send the message"** (trong tham số `chat_id`).
  3. **"Send The error"** (trong tham số `chat_id`).

#### **B. Cấu Hình API IslamicAPI**
- Trong node **"Get prayer times"**, điền **API Key** của bạn vào tham số:
  ```json
  {
    "url": "https://api.islamicapi.com/prayer/times?key=YOUR_API_KEY&lat=30.0444&lng=31.2357&method=2&school=1",
    "method": "get"
  }
  ```
  - `lat` và `lng` là tọa độ Cairo (30.0444, 31.2357). **Có thể thay đổi** nếu muốn lấy thời gian cho vị trí khác.

#### **C. Kiểm Tra Credentials Google**
- Đảm bảo đã cấu hình **OAuth2 Credentials** cho:
  - **Google Calendar** (trong node `Book for Fajr`, `Book for Duhr`, ...).
  - **Google Sheets** (trong node `Store Prayer Bookings` và `Append row in sheet`).

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi `/salah` đến bot Telegram của bạn.
   - Kiểm tra:
     - Có 5 sự kiện Google Calendar được tạo không?
     - Thông báo Telegram có hiển thị thời gian không?
     - Dữ liệu có được ghi vào Google Sheets không?
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thay đổi vị trí Nam Azan**:
   - Mở node **"Get prayer times"** và thay đổi `lat` và `lng` theo tọa độ của bạn (ví dụ: Hà Nội: `21.0338, 105.8342`).
2. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp thời gian cầu nguyện hàng tuần qua Telegram.
3. **Kết hợp với Slack**:
   - Thay thế node Telegram bằng **Slack Webhook** để thông báo trong Slack.
4. **Lưu log chi tiết hơn**:
   - Thêm node **Google Sheets** để ghi thêm thông tin như ngày tháng, thời gian thực tế, và trạng thái thành công/thất bại.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Hồi giáo bằng cách tự động hóa quy trình cầu nguyện, đồng thời **đảm bảo không quên giờ** với Google Calendar và **ghi chép toàn bộ lịch sử** vào Google Sheets.

**🚀 Hãy áp dụng ngay để bắt đầu cuộc sống cầu nguyện hiệu quả hơn!**
Nếu có vấn đề, liên hệ với tác giả [Abdullahi Osman](mailto:gureyai2006@gmail.com) hoặc tham khảo tài liệu chi tiết tại [Gurey AI](https://gurey-ai.vercel.app/).

---
**🔹 Lưu ý cuối cùng**:
- **Không cần code** – workflow đã sẵn sàng sử dụng.
- **Miễn phí** – tất cả API đều miễn phí.
- **An toàn** – chỉ hoạt động khi bạn gửi lệnh `/salah`.