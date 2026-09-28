---
title: "🤖 **Tự Động Hóa Đặt Khách Sạn & Bàn Ăn qua Gọi Điện AI + Telegram – Không Cần Code!**"
description: "Workflow này tự động hóa việc đặt phòng khách sạn và bàn ăn thông qua cuộc gọi AI qua RetellAI, đồng thời gửi thông báo kết quả qua Telegram. Giúp tiết kiệm thời gian lên đến 80% cho các sếp quản lý khách hàng và dịch vụ."
slug: "tieu-dong-hoa-dat-khach-san-restaurant-voi-ai-telegram"
tags: [n8n, automation, ai-chatbot, google-calendar, telegram-bot, retellai, no-code]
keywords: [n8n workflow tự động hóa, đặt phòng khách sạn tự động, gọi điện AI, telegram bot quản lý, retellai n8n, tự động hóa đặt bàn ăn]
---

# 🚀 **Tự Động Hóa Đặt Khách Sạn & Bàn Ăn qua Gọi Điện AI + Telegram**

### **Giải quyết vấn đề gì?**
Các sếp quản lý khách sạn, nhà hàng hoặc dịch vụ du lịch thường phải mất **giờ đồng hồ** mỗi ngày để:
✅ **Liên lạc khách hàng** để xác nhận đặt phòng/bàn ăn.
✅ **Quản lý lịch trình** trên Google Calendar để tránh xung đột.
✅ **Gửi thông báo kết quả** một cách cá nhân hóa.

**Workflow này tự động hóa toàn bộ quá trình** bằng cách:
- **Gọi điện AI** (RetellAI) để liên lạc với khách hàng.
- **Phân tích cuộc gọi** bằng Gemini 2.0 (Google AI) để xác nhận thông tin.
- **Tự động đặt lịch** trên Google Calendar.
- **Gửi thông báo kết quả** qua Telegram (hoặc Slack, Email).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gọi điện và xác nhận đặt phòng/bàn ăn **không cần can thiệp thủ công**.
- **Chính xác 100%**: AI phân tích cuộc gọi và cập nhật lịch trình chính xác.
- **Cá nhân hóa**: Gửi thông báo kết quả qua Telegram với thông tin chi tiết.
- **Hoạt động liên tục**: Chạy 24/7, không cần người quản lý trực tiếp.
- **Dễ dàng mở rộng**: Thêm các dịch vụ khác như đặt xe, tour du lịch.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản RetellAI** (để gọi điện AI):
   - Tạo **agent** và lấy **API Key** từ [RetellAI](https://www.retell.ai/).
   - Cài đặt **webhook** từ RetellAI đến node `Retell Webhook` trong n8n.

✔ **Bot Telegram**:
   - Tạo bot từ [@BotFather](https://t.me/BotFather) và lấy **Token API**.
   - Lấy **Chat ID** của bot (gửi tin nhắn cho bot và copy ID từ link Telegram).

✔ **Google Calendar API**:
   - Bật **Google Calendar API** trong [Google Cloud Console](https://console.cloud.google.com/).
   - Tạo **OAuth 2.0 Credentials** và thêm **callback URL** của n8n vào danh sách **Authorized Redirect URIs**.

✔ **API Key Google Gemini**:
   - Lấy **API Key** từ [Google AI Studio](https://aistudio.google/) để sử dụng **Gemini 2.0 Flash**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9850](https://n8n.io/workflows/9850) hoặc copy toàn bộ JSON từ link trên.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình RetellAI (Gọi điện AI)**
- **Node `Retell Create Call`**:
  - Đặt **Credentials** là `httpBearerAuth` (tạo mới với API Key từ RetellAI).
  - Điền **`from_number`** (số điện thoại xuất phát) và **`to_number`** (số khách hàng).
  - **Test**: Gọi một số mẫu để kiểm tra kết nối.

- **Node `Retell Webhook`**:
  - Đảm bảo **URL webhook** trong RetellAI trùng với URL của node này trong n8n.
  - **Key Parameters**:
    - `path`: `retell-webhook-agent`
    - `httpMethod`: `POST`

##### **B. Cấu hình Telegram Bot**
- **Node `Telegram Trigger`**:
  - Đặt **Credentials** là `telegramApi` (tạo mới với Token từ BotFather).
  - **Test**: Gửi tin nhắn từ Telegram để kích hoạt workflow.

- **Node `Send a text message`**:
  - Điền **`chat_id`** (lấy từ bot Telegram).
  - **Test**: Gửi tin nhắn mẫu để kiểm tra.

##### **C. Cấu hình Google Calendar**
- **Node `Get an event in Google Calendar` & `Create an event in Google Calendar`**:
  - Đặt **Credentials** là `googleCalendarOAuth2Api` (tạo mới và authorize).
  - **Key Parameters**:
    - `calendarId`: Thay bằng **ID Calendar** của bạn (tìm trong Google Calendar → URL).
    - `summary`: Tên sự kiện (ví dụ: "Đặt phòng khách sạn").
    - `start` & `end`: Thời gian đặt lịch (sử dụng `{{ $node["Get an event in Google Calendar"].json }}` để lấy từ cuộc gọi AI).

##### **D. Cấu hình Gemini 2.0 (AI Phân tích)**
- **Node `Google Gemini Chat Model` & `Gemini 2.0 Flash`**:
  - Đặt **Credentials** là `googlePalmApi` (tạo mới với API Key).
  - **Prompt mẫu** (cần tùy chỉnh theo yêu cầu):
    ```json
    {
      "role": "user",
      "content": "Analyze the call transcript and confirm booking details. Extract party size, time, and property name. Return structured JSON."
    }
    ```
  - **Node `Structured Output Parser`**: Đảm bảo **schema** phù hợp với output từ Gemini.

##### **E. Cấu hình AI Agent (Phân loại & Xử lý)**
- **Node `Switch`**:
  - **Route logic**:
    - Nếu cuộc gọi liên quan đến **đặt phòng khách sạn** → Chuyển đến `AI Agent: Property Viewings`.
    - Nếu liên quan đến **đặt bàn ăn** → Chuyển đến `AI Agent Reserva Restaurantes`.

- **Node `AI Agent: Property Viewings` & `AI Agent Reserva Restaurantes`**:
  - **Test Prompt**:
    ```json
    {
      "role": "user",
      "content": "Generate a call script to confirm booking for {{propertyName}} at {{time}}. Extract key details and schedule on Google Calendar."
    }
    ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn từ Telegram để kích hoạt workflow.
  - Kiểm tra **log** trong n8n để đảm bảo tất cả node hoạt động.
- **Bật Active**:
  - Nhấn **Active** trên workflow để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Email Notifications**:
   - Sử dụng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` để gửi thông báo thay vì Telegram.

2. **Lưu Log Cuộc Gọi**:
   - Thêm node `n8n-nodes-base.stickyNote` để lưu transcript cuộc gọi và kết quả phân tích.

3. **Báo cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.dateTime` + `n8n-nodes-base.aggregate` để tổng hợp dữ liệu đặt phòng/bàn ăn hàng ngày và gửi báo cáo qua Email/Telegram.

4. **Tích hợp với CRM**:
   - Nếu sử dụng **HubSpot, Zoho CRM** hoặc **Salesforce**, thêm node tương ứng để cập nhật thông tin khách hàng tự động.

5. **Tùy chỉnh Prompt AI**:
   - Đối với **đặt phòng khách sạn**, prompt có thể là:
     ```json
     "Analyze the call and extract: Property name, check-in/check-out dates, number of guests, special requests. Return in JSON format."
     ```
   - Đối với **đặt bàn ăn**, prompt có thể là:
     ```json
     "Extract: Restaurant name, party size, preferred time, special dietary needs. Confirm booking and schedule on Google Calendar."
     ```

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý khách sạn, nhà hàng và dịch vụ du lịch bằng cách tự động hóa:
✅ **Gọi điện AI** để liên lạc với khách hàng.
✅ **Phân tích cuộc gọi** bằng Gemini 2.0.
✅ **Đặt lịch tự động** trên Google Calendar.
✅ **Gửi thông báo kết quả** qua Telegram.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với số mẫu** trước khi áp dụng cho khách hàng thực.
3. **Mở rộng** bằng cách thêm các dịch vụ khác (đặt xe, tour du lịch).

**🚀 Cài đặt n8n trên VPS và bắt đầu tự động hóa ngay hôm nay!** 🚀