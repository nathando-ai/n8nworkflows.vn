---
title: "🌤️ **Trợ lý Thời tiết Cá nhân hóa + Lịch Google + AI + Telegram (Tự động hóa 100% không code)**"
description: "Workflow tự động gửi tin nhắn Telegram cá nhân hóa hàng ngày với lịch sự kiện Google Calendar + dự báo thời tiết chính xác từ WeatherAPI + tổng hợp AI bằng Gemini 2.0. Giúp các sếp bắt đầu ngày mới với kế hoạch rõ ràng và thông tin thời tiết quan trọng chỉ trong 1 nháy chuột."
slug: "tro-ly-thoi-tiet-canh-nhan-hoa-google-calendar-ai-telegram"
tags: [n8n, automation, no-code, google-calendar, ai-chatbot, telegram-bot, weather-api]
keywords: [n8n workflow tự động hóa, trợ lý thời tiết cá nhân hóa, tự động hóa lịch Google Calendar, AI tổng hợp thông tin, Telegram bot hàng ngày, Gemini 2.0 tự động hóa]
---

# 🚀 **Trợ lý Thời tiết Cá nhân hóa + Lịch Google + AI + Telegram: Bắt đầu ngày với kế hoạch hoàn hảo**

### **Nỗi đau thực tế của các sếp**
Mỗi sáng, các sếp phải:
- **Mở nhiều tab** để kiểm tra lịch Google Calendar, thời tiết, và dự báo khí hậu cho từng sự kiện.
- **Tốn thời gian** tổng hợp thông tin rải rác từ nhiều nguồn khác nhau.
- **Bị quên hoặc bỏ lỡ** sự kiện quan trọng vì không có cảnh báo tự động.
- **Không biết thời tiết** tại địa điểm của sự kiện, dẫn đến chuẩn bị không đầy đủ (ví dụ: mang ô không cần thiết hoặc không mang áo ấm).

**Workflow này giải quyết tất cả!** Nó tự động tổng hợp **lịch sự kiện Google Calendar + thời tiết chính xác + tổng hợp AI** và gửi cho các sếp qua **Telegram** hàng ngày, giúp họ **bắt đầu ngày một cách hiệu quả và không bị stress**.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Không cần mở nhiều tab, tất cả thông tin được tổng hợp tự động.
✅ **Thông tin chính xác**: Thời tiết được lấy từ **WeatherAPI** (cập nhật theo địa điểm sự kiện).
✅ **Tổng hợp AI thông minh**: Sử dụng **Gemini 2.0** để tạo tin nhắn cá nhân hóa, ngắn gọn và động viên.
✅ **Hoạt động 24/7**: Workflow chạy tự động hàng ngày (mặc định 6h sáng) mà không cần can thiệp.
✅ **Cảnh báo thời tiết quan trọng**: UV index cao, mưa, gió mạnh... được nhắc nhở kịp thời.
✅ **Hoàn toàn cá nhân hóa**: Thời gian, lịch và thời tiết được điều chỉnh theo **múi giờ và địa điểm** của các sếp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Các sếp cần chuẩn bị **5 loại tài khoản/khóa API** sau để workflow hoạt động:
1. **Google Calendar OAuth2**:
   - Tạo **credentials OAuth2** cho Google Calendar trong n8n (hướng dẫn: [n8n Google Calendar Setup](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.googleCalendar/)).
   - **Lưu ý**: Chọn quyền **`https://www.googleapis.com/auth/calendar.readonly`** (đọc lịch).

2. **WeatherAPI Key**:
   - Đăng ký miễn phí tại [weatherapi.com](https://www.weatherapi.com/) và lấy **API Key**.
   - **Gói miễn phí** cho phép **1,000 request/ngày** (đủ cho cá nhân).

3. **Telegram Bot Token & Chat ID**:
   - Tạo **bot Telegram** tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - **Chat ID** của các sếp: Gửi tin nhắn cho bot và lấy ID từ [this page](https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates).

4. **OpenRouter API Key**:
   - Đăng ký tại [openrouter.ai](https://openrouter.ai/) và lấy **API Key**.
   - **Model mặc định**: `google/gemini-2.0-flash-exp:free` (miễn phí).

5. **Múi giờ (Timezone)**:
   - Các sếp cần biết **múi giờ địa phương** (ví dụ: `Asia/Ho_Chi_Minh` cho Hà Nội).
   - **Danh sách múi giờ**: [List of Timezones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/6593](https://n8n.io/workflows/6593) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n Community trên cloud** (n8n.io) vì không hỗ trợ **OpenRouter** và **Telegram Bot** ổn định.
- **Cài đặt n8n Self-hosted** trên **VPS** để workflow hoạt động 24/7.
:::

---

#### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** cho từng node quan trọng:

##### **A. Schedule Trigger (Đặt lịch chạy)**
- **Thời gian mặc định**: 6h sáng hàng ngày.
- **Cách chỉnh**:
  - Nhấp vào node **Schedule Trigger** → **Edit**.
  - Đổi **cron expression** thành:
    ```plaintext
    0 6 * * *  # Chạy lúc 6h sáng hàng ngày
    ```
  - **Lưu ý**: Nếu các sếp muốn chạy vào **7h sáng**, thay thành:
    ```plaintext
    0 7 * * *
    ```

##### **B. Set Timezone (Đặt múi giờ)**
- **Node**: `Set Timezone`
- **Cách chỉnh**:
  - Nhấp vào **Set** → **Edit**.
  - Thay `UTC` thành **múi giờ địa phương** của các sếp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Danh sách múi giờ**: [Timezone Database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

##### **C. Google Calendar (Lấy lịch sự kiện)**
- **Node**: `Get many events`
- **Cách chỉnh**:
  1. **Credentials**:
     - Chọn **`googleCalendarOAuth2Api`** (đã tạo trước).
  2. **Calendar ID**:
     - Mặc định là **`primary`** (lịch chính).
     - Nếu muốn lấy lịch cụ thể, thay bằng **ID lịch** (hướng dẫn lấy ID: [Google Calendar API Guide](https://developers.google.com/calendar/api/guides/overview)).
  3. **Time Range**:
     - Workflow mặc định lấy **hôm nay và ngày mai**.
     - **Không cần chỉnh** nếu muốn giữ nguyên.

##### **D. WeatherAPI (Lấy thông tin thời tiết)**
- **Node**: `HTTP Request`
- **Cách chỉnh**:
  1. **URL**:
     - Thay `YOUR_WEATHERAPI_KEY` bằng **API Key** của các sếp.
     - **URL mẫu**:
       ```plaintext
       https://api.weatherapi.com/v1/current.json?key=YOUR_WEATHERAPI_KEY&q={location}&aqi=no
       ```
  2. **Location**:
     - Workflow tự động lấy **địa điểm sự kiện** từ Google Calendar.
     - **Không cần chỉnh** nếu đã cấu hình Google Calendar đúng.

##### **E. OpenRouter (AI Gemini 2.0)**
- **Node**: `OpenRouter Chat Model` và `OpenRouter Chat Model2`
- **Cách chỉnh**:
  1. **Credentials**:
     - Tạo **credentials** mới trong n8n với **OpenRouter API Key**.
     - Chọn **`@n8n/n8n-nodes-langchain.lmChatOpenRouter`**.
  2. **Model**:
     - Mặc định là `google/gemini-2.0-flash-exp:free`.
     - **Không cần chỉnh** nếu muốn dùng model miễn phí.

##### **F. Telegram Bot (Gửi tin nhắn)**
- **Node**: `Send a text message` và `Send a text message1`
- **Cách chỉnh**:
  1. **Credentials**:
     - Tạo **credentials** mới trong n8n với:
       - **Bot Token**: API Token từ @BotFather.
       - **Chat ID**: ID của các sếp (lấy từ [this page](https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates)).
  2. **Message**:
     - Workflow tự động **tổng hợp tin nhắn** từ AI, không cần chỉnh.

---

#### **3. Kích hoạt ⚡️ Workflow**
1. **Test Run** (kiểm tra trước khi chạy thực):
   - Nhấp vào **Run Workflow** và chọn **Test Run**.
   - Kiểm tra **Telegram** xem có nhận được tin nhắn mẫu không.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH TĂNG CƯỜNG HỆ THỐNG**]
1. **Thêm cảnh báo thời tiết đặc biệt**:
   - Sử dụng **node `If`** để kiểm tra **UV index > 5** hoặc **mưa > 80%** và gửi tin nhắn cảnh báo riêng.

2. **Lưu lịch và thời tiết vào Google Sheets**:
   - Thêm **node `googleSheets`** sau `Set Timezone` để lưu dữ liệu lịch và thời tiết vào bảng tính.

3. **Kết hợp với Slack**:
   - Thay vì Telegram, các sếp có thể **gửi tin nhắn qua Slack** bằng node `slack`.

4. **Tự động gửi báo cáo tuần**:
   - Sử dụng **node `scheduleTrigger`** với cron `0 8 * * 0` (mỗi Chủ Nhật 8h sáng) để gửi **tóm tắt tuần** qua Telegram.

5. **Cập nhật thời tiết theo giờ**:
   - Thay vì lấy thời tiết 1 lần, các sếp có thể **lấy thời tiết theo giờ** bằng cách thêm **node `scheduleTrigger`** mới với cron `0 * * * *` (mỗi giờ).
:::

---

### 📌 **Kết luận: Bắt đầu ngày một cách thông minh!**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **tìm kiếm, tổng hợp và nhớ lịch sự kiện + thời tiết**. Với **AI Gemini 2.0**, tin nhắn được **tổng hợp một cách cá nhân hóa, động viên và ngắn gọn**, giúp các sếp **bắt đầu ngày một cách hiệu quả và không bị stress**.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và **cấu hình** theo hướng dẫn trên.
3. **Bật Active** và **chờ tin nhắn đầu tiên** vào sáng mai!

**💡 Mẹo cuối**: Nếu các sếp muốn **thêm tính cá nhân hóa hơn**, có thể **tùy chỉnh prompt** cho AI bằng cách chỉnh node `AI Agent` và `AI Agent2`.

---
**Chúc các sếp tự động hóa thành công!** 🚀