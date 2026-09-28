---
title: "🤖 **Tự Động Hóa Lịch Google + Bot Nhắc Nhở Telegram Sử Dụng AI Gemini & Whisper - Cách Sử Dụng Chi Tiết (2024)""
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp quản lý lịch Google Calendar, nhắc nhở qua Telegram thông minh với AI Gemini, và chuyển đổi giọng nói thành văn bản bằng OpenAI. Tiết kiệm thời gian lên tới 80% trong quản lý lịch hằng ngày!"
slug: "tieu-dong-hoa-lich-google-telegram-ai-gemini-whisper"
tags: [n8n, automation, no-code, ai-chatbot, google-calendar, telegram-bot, gemini-ai, openai]
keywords: [n8n workflow tự động hóa lịch, bot nhắc nhở telegram ai, gemini api n8n, tự động hóa quản lý lịch google, chuyển đổi giọng nói thành văn bản n8n]
---

# 🚀 **Bot Nhắc Nhở Telegram + Lịch Google Tự Động Hóa Với AI Gemini & Whisper**

## **💡 Giải Pháp Cho Nỗi Đau "Quên Lịch" & "Quản Lý Lịch Thủ Công"**
Các sếp đã bao giờ:
- **Quên cuộc họp quan trọng** vì không nhắc nhở kịp thời?
- **Phải mở nhiều tab** để kiểm tra lịch Google và Telegram?
- **Mệt mỏi với việc nhập liệu** khi có sự thay đổi cuối cùng?
- **Không thể sử dụng giọng nói** để tạo lịch mà phải gõ tay?

**Workflow này giải quyết tất cả!** Với **AI Gemini** xử lý yêu cầu tự nhiên, **OpenAI Whisper** chuyển đổi giọng nói thành văn bản, và **nhắc nhở tự động** qua Telegram, các sếp sẽ **tự động hóa 100% quản lý lịch** mà không cần code!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa quản lý lịch** – Không cần mở nhiều tab, chỉ cần nói hoặc gõ lệnh.
✅ **Nhắc nhở thông minh** – Bot nhắc nhở **45-60 phút trước** mỗi sự kiện.
✅ **Chuyển đổi giọng nói thành văn bản** – Gửi voice message qua Telegram, bot tự động chuyển thành lịch.
✅ **AI xử lý yêu cầu tự nhiên** – "Schedule meeting tomorrow at 2 PM" → Bot tự động tạo lịch.
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công, bot làm việc liên tục.
✅ **Tiết kiệm thời gian lên tới 80%** – Không phải nhập liệu, kiểm tra lịch thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**
   - Tạo bot tại [@BotFather](https://t.me/botfather) và lấy **API Token**.
   - Thêm bot vào nhóm/đối thoại cá nhân để test.

2. **Google Calendar OAuth2 Credentials**
   - Tạo **OAuth2 Client ID** tại [Google Cloud Console](https://console.cloud.google.com/).
   - Chọn **Web Application** và thêm `https://your-n8n-domain.com` vào **Authorized JavaScript Origins**.

3. **OpenAI API Key**
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Cần cho **chuyển đổi giọng nói thành văn bản (Whisper)**.

4. **Google Gemini API Key**
   - Đăng ký tại [Google AI Studio](https://aistudio.google/) và lấy **API Key**.
   - Cần cho **AI xử lý yêu cầu tự nhiên**.

5. **N8n Instance (Self-hosted hoặc Cloud)**
   - Nếu dùng **n8n Cloud**, cần nâng cấp lên **Pro Plan** để sử dụng các node AI.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [n8n.io/workflows/5784](https://n8n.io/workflows/5784).
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** → Chọn file JSON → **Import**.
  - **Hoặc** copy toàn bộ JSON và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **3 phần chính**: **AI Processor**, **Calendar Agent**, và **Reminder Agent**. Dưới đây là hướng dẫn cấu hình chi tiết:

##### **🔹 Cấu Hình Telegram Bot**
- **Node**: `Start` (Telegram Trigger), `Send Typing Indicator`, `Send AI Response`, `Send Reminder`, `📥 Download Voice`, `Typing 2`
  - **Credentials**: Chọn `telegramApi` → Điền **API Token** từ BotFather.
  - **Chat ID**: Nếu chưa biết, gửi `/getid` cho bot và copy ID từ Telegram.

##### **🔹 Cấu Hình Google Calendar**
- **Node**: `Get Upcoming Events`, `Create Event`, `Update Event`, `Delete event`, `Get events`
  - **Credentials**: Chọn `googleCalendarOAuth2Api` → **Connect OAuth2** và cho phép quyền truy cập.
  - **Sheet Name**: Điền tên **Calendar cụ thể** (ví dụ: "Lịch cá nhân").

##### **🔹 Cấu Hình AI (Gemini & OpenAI)**
- **Node**: `Google Gemini Model` (AI xử lý yêu cầu)
  - **Credentials**: Chọn `googlePalmApi` → Điền **API Key** từ Google AI Studio.
- **Node**: `OpenAI` (Chuyển đổi giọng nói)
  - **Credentials**: Chọn `openAiApi` → Điền **API Key** từ OpenAI.

##### **🔹 Cấu Hình Nhắc Nhở (Reminder)**
- **Node**: `Reminder Schedule` (Schedule Trigger)
  - **Cron Job**: Đặt lịch **lặp lại mỗi 15 phút** (`*/15 * * * *`) để bot kiểm tra lịch và nhắc nhở.
- **Node**: `Filter Duplicate Reminders`
  - **Operation**: Đảm bảo chọn `removeItemsSeenInPreviousExecutions` để tránh nhắc nhở trùng lặp.

##### **🔹 Cấu Hình AI Agent**
- **Node**: `Reminder Message Agent`, `Calendar Manage!`
  - **Prompt Template**: Các sếp có thể **tùy chỉnh** prompt để AI trả lời chính xác hơn.
  - **Memory Buffer**: `Simple Memory` (memoryBufferWindow) giúp AI nhớ các yêu cầu trước đó.

##### **🔹 Cấu Hình Chuyển Đổi Giọng Nói**
- **Node**: `📥 Download Voice`
  - **Resource**: Chọn `file` → Bot sẽ tự động tải file âm thanh từ Telegram.
- **Node**: `OpenAI` (Transcribe)
  - **Operation**: Chọn `transcribe` → **Audio** → Bot sẽ chuyển giọng nói thành văn bản.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **lệnh mẫu** qua Telegram (ví dụ: *"Schedule meeting tomorrow at 2 PM"*).
  - Kiểm tra bot có tạo lịch trên Google Calendar không.
  - Test **giọng nói** bằng cách gửi voice message.
- **Bật Active**:
  - Nhấn **Active** trên workflow → Bot sẽ bắt đầu hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Email**
   - Thêm **node Slack** hoặc **Email** để nhận thông báo khi có sự kiện mới.
   - Ví dụ: Bot gửi email báo cáo lịch hàng tuần.

2. **Lưu Log & Monitoring**
   - Thêm **node Log** để theo dõi hoạt động của bot.
   - Sử dụng **n8n Dashboard** để giám sát workflow.

3. **Tùy Chỉnh Nhắc Nhở**
   - Thay đổi **thời gian nhắc nhở** (ví dụ: 30 phút thay vì 45 phút) bằng cách chỉnh **Cron Job** trong `Reminder Schedule`.

4. **Hỗ Trợ Nhiều Ngôn Ngữ**
   - Cập nhật **prompt AI** để hỗ trợ nhiều ngôn ngữ (Tiếng Anh, Tiếng Nhật, Tiếng Trung...).

5. **Tự Động Xóa Lịch Trùng Lặp**
   - Sử dụng **node Switch** để kiểm tra và xóa lịch trùng lặp tự động.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý lịch** mà không cần code. Với **AI Gemini** xử lý yêu cầu tự nhiên, **OpenAI Whisper** chuyển đổi giọng nói, và **nhắc nhở tự động** qua Telegram, các sếp sẽ **tiết kiệm thời gian, giảm stress và tăng hiệu suất làm việc**.

**🚀 Hãy áp dụng ngay và trải nghiệm sự tự động hóa hoàn toàn!**
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với **Khaisa Studio** qua [n8n.io](https://n8n.io/workflows/5784).

---
**#TựĐộngHóa #N8n #AIChatbot #GoogleCalendar #TelegramBot**