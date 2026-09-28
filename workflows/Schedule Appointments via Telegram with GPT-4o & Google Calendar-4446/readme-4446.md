---
title: "🤖 Tự Động Hóa Lịch Hẹn qua Telegram với GPT-4o & Google Calendar - Không Cần Code!"
description: "Hướng dẫn chi tiết cách tự động hóa quản lý lịch hẹn, đặt/cancel cuộc họp chỉ với Telegram và AI, tiết kiệm thời gian cho các sếp và doanh nghiệp. Workflow hoạt động 24/7, không cần can thiệp thủ công."
slug: "tu-dong-hoa-lich-hen-telegram-gpt4o-google-calendar"
tags: [n8n, automation, ai, google-calendar, telegram-bot, no-code]
keywords: [tự động hóa lịch hẹn, đặt cuộc họp qua telegram, gpt-4o n8n, quản lý lịch google calendar tự động, workflow n8n ai]
---

# 🚀 **Tự Động Hóa Lịch Hẹn qua Telegram với GPT-4o & Google Calendar**

### **Giải pháp hoàn hảo cho các sếp, doanh nghiệp và freelancer**
Quản lý lịch hẹn thủ công không chỉ tốn thời gian mà còn dễ xảy ra lỗi, quên lịch hoặc trùng lịch. Hãy tưởng tượng một hệ thống **tự động hóa 100%** cho phép khách hàng đặt/cancel cuộc họp chỉ bằng **nhắn tin Telegram**, trong khi AI **GPT-4o** xử lý logic và **Google Calendar** tự động cập nhật. Không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải trả lời hàng chục yêu cầu đặt lịch qua email/Telegram.
- **Tính chính xác cao**: AI **GPT-4o** tự động xác minh và xử lý yêu cầu (đặt/cancel).
- **Trải nghiệm khách hàng tốt**: Khách hàng đặt/cancel lịch chỉ bằng **nhắn tin Telegram**, không cần app phức tạp.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp thủ công.
- **Tích hợp AI**: Sử dụng **GPT-4o** để hiểu ý định của người dùng và xử lý logic phức tạp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Tạo **bot Telegram** bằng cách chat với [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để nhận yêu cầu đặt lịch.

2. **Tài khoản Google Calendar**:
   - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) và tạo **OAuth 2.0 Client ID** để kết nối với Google Calendar.

3. **Tài khoản OpenAI (API Key)**:
   - Đăng ký tại [OpenAI Platform](https://platform.openai.com/) và lấy **API Key** để sử dụng **GPT-4o**.

4. **n8n Self-hosted** (không dùng phiên bản miễn phí):
   - Cài đặt n8n trên **VPS** (hướng dẫn tại [n8n.io](https://n8n.io/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/4446](https://n8n.io/workflows/4446) hoặc sao chép **JSON** từ trang này.
- **Bước 2**: Mở **n8n Editor** và nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Workflow sẽ hiển thị với **6 node** như trong danh sách dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔹 Telegram Trigger (Node đầu tiên)**
- **Credentials**: Chọn **"telegramApi"** (đã cấu hình API Token từ BotFather).
- **Chat ID**: Điền **ID của nhóm/chat** muốn nhận yêu cầu (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
- **Command**: Đặt là `/start` hoặc `/book` để kích hoạt workflow.

##### **🔹 AI Agent (Node xử lý logic)**
- **Model**: Chọn **GPT-4o-mini** (đã cấu hình trong `OpenAI Chat Model`).
- **Memory Buffer**: Sử dụng **Simple Memory** để lưu trữ lịch sử giao tiếp (giúp AI nhớ các yêu cầu trước đó).
- **Prompt**: AI sẽ tự động phân tích yêu cầu đặt/cancel lịch dựa trên **ngôn ngữ tự nhiên** (không cần định dạng cố định).

##### **🔹 OpenAI Chat Model (Node AI)**
- **Credentials**: Chọn **"openAiApi"** (đã điền API Key từ OpenAI).
- **Model**: Chọn **gpt-4o-mini** (mô hình nhanh và hiệu quả).
- **Input**: Dữ liệu từ Telegram (yêu cầu đặt/cancel lịch).

##### **🔹 Google Calendar (Node cập nhật lịch)**
- **Credentials**: Chọn **"googleCalendarOAuth2Api"** (đã cấu hình OAuth 2.0).
- **Action**:
  - **Đặt lịch**: Tạo sự kiện mới với thông tin từ AI (ngày giờ, tiêu đề, danh sách tham gia).
  - **Hủy lịch**: Tìm và xóa sự kiện theo yêu cầu của người dùng.

##### **🔹 Telegram (Node phản hồi)**
- **Credentials**: Chọn **"telegramApi"** (cùng API Token với Telegram Trigger).
- **Message**: Cấu hình tin nhắn phản hồi cho người dùng (ví dụ: *"Lịch đã được đặt thành công!"* hoặc *"Lịch đã bị hủy"*).

---

#### **3. Kích hoạt ⚡️**
- **Bước 1**: **Test Run** với dữ liệu mẫu:
  - Gửi tin nhắn `/book` hoặc `/cancel` đến bot Telegram.
  - Kiểm tra AI có xử lý đúng không (đặt/hủy lịch trên Google Calendar).
- **Bước 2**: Nếu test thành công, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram Group**:
   - Thay vì chỉ chat cá nhân, mở rộng cho **nhóm nhiều người** quản lý lịch chung.

2. **Lưu log hoạt động**:
   - Sử dụng **Sticky Note** để ghi lại tất cả yêu cầu đặt/cancel lịch (dễ theo dõi và debug).

3. **Gửi báo cáo định kỳ**:
   - Tích hợp **Google Sheets** để tự động lưu lịch hẹn vào bảng tính, giúp theo dõi lịch sử.

4. **Cập nhật thông báo tự động**:
   - Sử dụng **Telegram Bot** để gửi **nhắc nhở** trước cuộc họp (ví dụ: *"Cuộc họp với khách hàng sẽ diễn ra trong 1 giờ"*).

5. **Xử lý lỗi tự động**:
   - Nếu AI không hiểu yêu cầu, bot có thể trả lời: *"Xin lỗi, tôi không hiểu. Vui lòng gửi lại yêu cầu với định dạng: 'Đặt lịch ngày 10/10, 2h, với Anh A và B'"*.

---

### 📌 **Kết luận**
Với **workflow này**, các sếp không chỉ **tự động hóa quản lý lịch hẹn** mà còn **cải thiện trải nghiệm khách hàng** bằng cách cho phép họ đặt/cancel lịch chỉ bằng **nhắn tin Telegram**. AI **GPT-4o** đảm bảo logic xử lý chính xác, trong khi **Google Calendar** tự động cập nhật.

**Hãy áp dụng ngay và tiết kiệm thời gian cho mình!** 🚀
Nếu có vấn đề, hãy để lại comment dưới đây hoặc tham khảo [video tutorial của Automate With Marc](https://youtu.be/GzWO7_1lyI8).

---