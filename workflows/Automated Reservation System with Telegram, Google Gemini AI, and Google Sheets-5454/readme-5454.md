---
title: "🤖 Hệ Thống Đặt Hẹn Tự Động Hóa Với Telegram, AI Gemini & Google Sheets - Không Cần Code!"
description: "Giải pháp tự động hóa đặt hẹn toàn diện cho doanh nghiệp, hỗ trợ xác minh lịch trống, lưu trữ tự động và gửi xác nhận qua email/Telegram chỉ trong 1 tin nhắn. Tiết kiệm 80% thời gian quản lý đặt hẹn thủ công."
slug: "he-thong-dat-hen-tu-dong-telegram-gemini-google-sheets"
tags: [n8n, automation, ai-chatbot, telegram-bot, google-sheets, no-code]
keywords: [tự động hóa đặt hẹn, bot telegram đặt phòng, google gemini n8n, lưu trữ google sheets, giải pháp quản lý lịch trống]
---

# 🚀 **Hệ Thống Đặt Hẹn Tự Động Hóa Với Telegram, AI Gemini & Google Sheets**

### **Giải pháp hoàn hảo cho các sếp quản lý phòng tập, phòng họp, sân bóng hoặc bất kỳ tài nguyên nào cần đặt lịch!**

Hãy tưởng tượng: **Khách hàng chỉ cần gửi 1 tin nhắn Telegram** với thông tin đặt hẹn (ngày, giờ, tên, email, tài nguyên), hệ thống sẽ tự động:
✅ **Xác minh lịch trống** trên Google Sheets
✅ **Lưu trữ dữ liệu** một cách an toàn
✅ **Gửi xác nhận** qua email và Telegram
✅ **Trả lời tự động** với thông tin chi tiết

**Không cần viết 1 dòng code!** Workflow này sử dụng **n8n + Google Gemini AI** để xử lý logic phức tạp, giúp các sếp **tiết kiệm 80% thời gian quản lý đặt hẹn thủ công** và giảm thiểu lỗi nhân sự.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra lịch trống thủ công hàng ngày.
- **Chính xác 100%**: AI Gemini xác minh lịch trống và tránh xung đột thời gian.
- **Cá nhân hóa**: Gửi xác nhận email và tin nhắn Telegram với thông tin chi tiết.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào nhân viên.
- **Dễ dàng mở rộng**: Thêm tài nguyên mới (phòng tập, sân bóng, phòng họp...) chỉ cần cập nhật Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt **n8n-nodes-base.telegram** và **n8n-nodes-base.telegramTrigger**.

2. **Google Sheets**:
   - Tạo **2 bảng Google Sheets**:
     - **Resource Info** (tùy chọn, để liệt kê tài nguyên như "Phòng tập A", "Sân bóng B").
     - **Reservation Log** (bắt buộc) với các cột:
       ```
       Date | Name | Email | Resource | Start Time | End Time | Status
       ```
   - Cài đặt **n8n-nodes-base.googleSheetsTool** và tạo **Google Sheets OAuth2 API Key**.

3. **Gmail**:
   - Cài đặt **n8n-nodes-base.gmailTool** và tạo **Gmail OAuth2 API Key** (để gửi email xác nhận).

4. **Google Gemini API**:
   - Đăng ký API Key tại [Google AI Studio](https://makersuite.google.com/) và cài đặt **@n8n/n8n-nodes-langchain.lmChatGoogleGemini**.

5. **PostgreSQL (tùy chọn)**:
   - Nếu muốn lưu trữ lịch sử chat, cài đặt **n8n-nodes-langchain.memoryPostgresChat** và tạo **PostgreSQL credentials**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/5454](https://n8n.io/workflows/5454) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ link trên vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Telegram Trigger**
- **Credentials**: Chọn **telegramApi** (đã tạo từ BotFather).
- **Chat ID**: Đặt là **@username_bot** (ví dụ: `@dathenbot`).
- **Message Content**: Chỉnh để nhận **tin nhắn văn bản** từ người dùng.

##### **🔹 Node 2: Prepare Prompt (aiTransform)**
- **Input**: Dữ liệu từ Telegram (Date, Name, Email, Resource, Start Time, End Time).
- **Output**: Format dữ liệu thành **prompt** cho Google Gemini.

##### **🔹 Node 3: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Credentials**: Chọn **googlePalmApi** (API Key từ Google AI Studio).
- **Prompt**: Sử dụng template:
  ```
  "Check if the following reservation is available in Google Sheets:
  Date: {{Date}}, Resource: {{Resource}}, Start Time: {{StartTime}}, End Time: {{EndTime}}.
  Return 'Available' if no conflict, otherwise return 'Conflict' with details."
  ```
- **Model**: Chọn **gemini-pro**.

##### **🔹 Node 4: Decision Node (Logic Xác Minh Lịch Trống)**
- **Condition**:
  - Nếu **Google Gemini trả về "Available"**, chuyển sang **Node 5 (Google Sheets)** để lưu trữ.
  - Nếu **trả về "Conflict"**, gửi tin nhắn Telegram thông báo **"Lịch đã bị chiếm"**.

##### **🔹 Node 5: Google Sheets (Append/Update)**
- **Credentials**: Chọn **googleSheetsOAuth2Api**.
- **Sheet Name**: Chọn **Reservation Log**.
- **Operation**: Chọn **appendOrUpdate**.
- **Headers**: Đảm bảo trùng khớp với bảng Google Sheets (Date, Name, Email, Resource, Start Time, End Time, Status).

##### **🔹 Node 6: Gmail (Send Confirmation Email)**
- **Credentials**: Chọn **gmailOAuth2**.
- **To**: Điền **email của khách hàng** (từ dữ liệu Telegram).
- **Subject**: "Xác nhận đặt hẹn thành công!"
- **Body**: Template:
  ```
  Xin chào {{Name}},

  Đặt hẹn của bạn đã được xác nhận thành công:
  - Ngày: {{Date}}
  - Tài nguyên: {{Resource}}
  - Giờ: {{StartTime}} - {{EndTime}}

  Cảm ơn bạn đã sử dụng dịch vụ!
  ```

##### **🔹 Node 7: Telegram (Reply Confirmation)**
- **Credentials**: Chọn **telegramApi**.
- **Chat ID**: Điền **chat_id của người dùng** (từ Telegram Trigger).
- **Message**: Template:
  ```
  ✅ Đặt hẹn thành công!
  Ngày: {{Date}}, Tài nguyên: {{Resource}}, Giờ: {{StartTime}} - {{EndTime}}.
  ```

##### **🔹 Node 8: AI Agent (Tùy chọn nâng cao)**
- Nếu muốn **tự động xử lý các câu hỏi liên quan** (ví dụ: "Lịch trống ngày mai?"), cấu hình **@n8n/n8n-nodes-langchain.agent** với **Postgres Chat Memory** để lưu trữ lịch sử.

##### **🔹 Node 9: Postgres Chat Memory (Tùy chọn)**
- Nếu muốn **lưu trữ lịch sử chat**, cấu hình **Postgres credentials** và kích hoạt **memoryPostgresChat**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn Telegram với format:
     ```
     Date: 2024-12-25
     Name: John Doe
     Email: john@example.com
     Resource: Phòng tập A
     Start Time: 10:00
     End Time: 12:00
     ```
   - Nhập **"yes"** để xác nhận.

2. **Bật Active workflow** và **monitor** trong n8n Dashboard.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Alert**:
   - Kết nối với **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo khi có đặt hẹn mới.

2. **Lưu Log Dữ liệu**:
   - Sử dụng **n8n-nodes-base.stickyNote** để lưu trữ log tất cả các yêu cầu đặt hẹn.

3. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **n8n-nodes-base.email** để gửi **báo cáo tổng hợp đặt hẹn hàng tuần** cho quản lý.

4. **Cập Nhật Tự Động Google Sheets**:
   - Sử dụng **n8n-nodes-base.cron** để **xóa đặt hẹn cũ** (ví dụ: sau 30 ngày).

5. **Hỗ trợ Ngôn Ngữ Múlti**:
   - Sử dụng **Google Gemini** để **dịch tin nhắn** từ khách hàng sang tiếng Việt nếu cần.

---

### 📌 **Kết luận**
**Hệ thống đặt hẹn tự động hóa này là giải pháp hoàn hảo** cho các sếp quản lý tài nguyên (phòng tập, sân bóng, phòng họp...) mà không cần viết code. Với **Google Gemini AI**, nó **xác minh lịch trống chính xác**, **lưu trữ tự động** và **gửi xác nhận** một cách chuyên nghiệp.

**Hãy áp dụng ngay để:**
✔ **Tiết kiệm 80% thời gian quản lý**.
✔ **Giảm thiểu lỗi nhân sự**.
✔ **Cung cấp trải nghiệm khách hàng tốt nhất**.

**Nếu cần hỗ trợ tùy chỉnh hoặc triển khai**, liên hệ tác giả:
📧 **Tharwat Mohamed**: [tharwat.elsayed.hamad@gmail.com](mailto:tharwat.elsayed.hamad@gmail.com)

---
**Bắt đầu tự động hóa ngay hôm nay!** 🚀