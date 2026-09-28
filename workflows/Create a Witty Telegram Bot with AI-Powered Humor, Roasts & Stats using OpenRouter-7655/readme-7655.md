---
title: "🤖 **Tạo Bot Telegram Hài Hước AI-Powered: JokeBot, RoastBot & Analytics Tự Động Hóa với OpenRouter & n8n**"
description: "Cài đặt workflow tự động hóa hoàn chỉnh cho Bot Telegram thông minh, trả lời bằng câu đùa, động viên, roast hài hước và theo dõi thống kê người dùng 24/7. Không cần code, chỉ cần n8n và OpenRouter!"
slug: "tao-bot-telegram-ai-humour-roast-stats-openrouter-n8n"
tags: [n8n, automation, ai-chatbot, telegram-bot, openrouter, postgres, no-code]
keywords: [n8n workflow telegram bot, tự động hóa bot telegram, ai trả lời câu đùa, roastbot tự động, thống kê người dùng telegram, openrouter n8n]
---

# **🚀 Bot Telegram AI Hài Hước: Từ Đùa Đơn Giản Đến Roast & Analytics Tự Động Hóa**

## **😅 Giới Thiệu: Bot Telegram AI Đã "Điên" – Nhưng Đúng Cách!**
Cố gắng tạo một bot Telegram trả lời câu đùa, động viên hay roast hài hước mà không bị "chết" vì viết code? **Không cần lo!** Workflow này giúp các sếp **tự động hóa toàn bộ quy trình** với:
- **Trả lời tự động** bằng câu đùa, động viên, hoặc roast hài hước (không xúc phạm).
- **Theo dõi thống kê** người dùng: số tin nhắn, lệnh sử dụng, và bảng xếp hạng.
- **Bài viết tự động** theo lịch: câu đùa sáng sớm, động viên buổi sáng, hay câu nói triết lý chiều tối.
- **Hỗ trợ AI mạnh mẽ** từ OpenRouter (gồm mô hình **GPT-4 120B**).

**Kết quả?** Một bot Telegram **tự động, thông minh, và luôn có "tính cách"** – không cần viết một dòng code!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code hoặc quản lý bot thủ công.
- **Tính cá nhân hóa cao**: Bot trả lời khác nhau tùy vào lệnh (`/joke`, `/roast`, `/stats`) hoặc khi được nhắc tên (`@GiggleGPTBot`).
- **Hoạt động liên tục 24/7**: Dữ liệu và lịch trình được lưu trữ trên **PostgreSQL**, không bị mất khi n8n tạm ngừng.
- **Thống kê chi tiết**: Bảng xếp hạng người dùng, số lần sử dụng lệnh, và phản ứng của người dùng.
- **Mở rộng dễ dàng**: Thêm lệnh mới (`/quote`, `/fact`) hoặc điều chỉnh lịch trình bài viết.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào **nhóm/channel** muốn sử dụng.
2. **API Key OpenRouter**:
   - Đăng ký tài khoản tại [openrouter.ai](https://openrouter.ai/) và lấy **API Key**.
   - Chọn mô hình **`openai/gpt-oss-120b`** (miễn phí trong giới hạn).
3. **Cơ sở dữ liệu PostgreSQL**:
   - Cài đặt **PostgreSQL** (hoặc sử dụng **Supabase** miễn phí).
   - Các sếp cần **username**, **password**, và **URL kết nối**.
4. **Chat ID của nhóm/channel**:
   - Lấy **Chat ID** từ nhóm/channel để bot gửi tin nhắn tự động (dùng lệnh `/getChatId` trên Telegram).

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/7655) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7655) và dán vào **Create Workflow** → **Import from JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **26 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình Credentials (Bắt buộc)**
| Node | Tham số cần điền | Ghi chú |
|------|------------------|---------|
| **Telegram API** | `telegramApi` | API Token từ BotFather |
| **OpenRouter API** | `openRouterApi` | API Key từ OpenRouter |
| **PostgreSQL** | `postgres` | Username, Password, Host, Port, Database Name |

#### **B. Cấu hình PostgreSQL (Bắt buộc chạy 1 lần)**
1. **Chạy node `Init Database`**:
   - Mở node này và **test run** để tạo bảng dữ liệu (`user_messages`, `bot_responses`, `user_stats`, ...).
   - Nếu lỗi, kiểm tra **credentials PostgreSQL** có đúng không.

2. **Thêm lịch trình bài viết (Optional nhưng khuyến nghị)**
   - Mở node **`Adding a schedule`** và **test run** để thêm:
     - **Câu đùa sáng sớm** (6h sáng).
     - **Động viên buổi sáng** (9h sáng).
     - **Câu nói triết lý chiều tối** (17h chiều).
   - Điền **`chat_id`** của nhóm/channel muốn gửi tin nhắn tự động.

#### **C. Cấu hình Telegram Webhook**
- Mở node **`Webhook Telegram`** và điền:
  - **`Webhook URL`**: `https://<tên-domain>/webhook` (n8n self-hosted).
  - **`Token`**: API Token từ BotFather.
  - **`Update Type`**: Chọn `message` và `edited_message`.

#### **D. Cấu hình AI (OpenRouter)**
- Node **`OpenRouter Commands`** đã mặc định sử dụng mô hình **`openai/gpt-oss-120b`**.
- Nếu muốn thay đổi, mở node và chỉnh **`model`** trong **`keyParameters`**.

#### **E. Cấu hình Lịch trình (Schedule Trigger)**
- Node **`Schedule`** chạy **mỗi giờ** để kiểm tra bài viết đã lên lịch.
- Nếu muốn thay đổi thời gian, mở node và chỉnh **`cron`** (ví dụ: `0 6 * * *` cho 6h sáng).

---

### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi lệnh `/help` đến bot và kiểm tra phản hồi.
   - Gửi `@GiggleGPTBot` một tin nhắn và xem bot có trả lời không.
2. **Bật Active workflow**:
   - Chuyển trạng thái từ **Draft** sang **Active**.

---

## **✍️ Mẹo & gợi ý nâng cao**
### **1. Thêm lệnh mới**
- Sử dụng node **`Switch`** để thêm lệnh mới (ví dụ `/quote`).
- Tạo một **node `If`** mới để kiểm tra lệnh và gọi **`AI response to command`**.

### **2. Lưu log và báo cáo**
- Sử dụng node **`Log message + statistics`** để lưu tất cả hoạt động vào PostgreSQL.
- Tạo một **workflow riêng** để gửi báo cáo thống kê hàng tuần qua Telegram.

### **3. Tích hợp với Slack/Telegram**
- Sử dụng node **`Telegram`** để gửi thông báo khi có tin nhắn mới.
- Hoặc kết nối với **Slack API** để báo cáo thống kê.

### **4. Localize (Dịch đa ngôn ngữ)**
- Thay đổi **prompt** trong node **`AI response to command`** để hỗ trợ nhiều ngôn ngữ.
- Ví dụ: `Prompt: "Trả lời bằng tiếng Việt và tiếng Anh, tùy vào ngôn ngữ người dùng."`

---

## **📌 Kết luận**
Với workflow này, các sếp đã có một **Bot Telegram AI hài hước, tự động hóa hoàn chỉnh**, không cần viết code! Bot sẽ:
✅ Trả lời câu đùa, động viên, roast hài hước.
✅ Theo dõi thống kê người dùng và bảng xếp hạng.
✅ Gửi bài viết tự động theo lịch.
✅ Hoạt động 24/7 mà không cần can thiệp thủ công.

**Hành động ngay!** Import workflow, cấu hình credentials, và **chạy bot của mình trong vòng 30 phút**! 🚀

---
**💡 Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ admin để cài đặt nhanh chóng!