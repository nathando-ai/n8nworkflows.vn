---
title: "🚀 Xây dựng Trợ lý ảo Đặt lịch khám bệnh tự động với n8n, OpenAI & Google Calendar"
description: "Tự động hóa toàn bộ quy trình đặt, hủy và kiểm tra lịch khám bệnh qua Telegram và WhatsApp sử dụng AI Agent, OpenAI, Google Calendar và Redis."
slug: "tro-ly-ao-dat-lich-kham-benh-tu-dong-n8n"
tags: [n8n, automation, ai-agent, openai, google-calendar, telegram, whatsapp]
keywords: [n8n workflow, đặt lịch khám bệnh tự động, ai agent calendar, openAI chatbot n8n, google calendar integration]
---

# 🚀 Xây dựng Trợ lý ảo Đặt lịch khám bệnh tự động với n8n, OpenAI & Google Calendar

Việc quản lý và sắp xếp lịch hẹn khám bệnh thủ công qua tin nhắn thường khiến các phòng khám, bác sĩ hoặc cơ sở y tế quá tải, dễ dẫn đến trùng lịch hoặc bỏ lỡ khách hàng. Việc phản hồi chậm trễ cũng làm giảm trải nghiệm của bệnh nhân. 

Giải pháp hoàn hảo cho các sếp chính là workflow n8n **Medical Appointment Scheduler** - một trợ lý ảo thông minh hoạt động 24/7 trên cả Telegram và WhatsApp, tích hợp công nghệ AI (OpenAI) để hiểu ngữ cảnh tự nhiên và tự động đồng bộ lịch hẹn trực tiếp lên Google Calendar của phòng khám.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các webhook mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Trợ lý AI tự động trò chuyện, tra cứu lịch trống, đặt lịch và hủy lịch cho bệnh nhân mà không cần nhân sự can thiệp.
- **Đa kênh linh hoạt:** Hỗ trợ đồng thời hai nền tảng nhắn tin phổ biến là Telegram (`Telegram Trigger`, `SEND MESSAGE TELEGRAM`) và WhatsApp (`Evolution API`).
- **Chống spam thông minh:** Tích hợp Redis (`REDIS - DEBOUNCE - GET/SET/DELETE`) và cơ chế chờ (`WAIT TIME - 5 SECONDS DEBOUNCE`) giúp gom tin nhắn liên tục của người dùng thành một luồng xử lý mượt mà, tránh việc AI trả lời dồn dập.
- **Đồng bộ thời gian thực:** Kết nối trực tiếp với Google Calendar (`Check Schedule`, `Create Appointment`, `Cancel Appointment`) để đảm bảo không bao giờ xảy ra tình trạng đặt trùng lịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted trên VPS).
- **OpenAI API Key:** Cho `OpenAI Chat Model` và `Calendar AI Agent`.
- **Google Calendar Account:** Để cấp quyền cho các công cụ check/create/cancel lịch.
- **Redis Server:** Dùng cho cơ chế debounce tin nhắn.
- **Telegram Bot Token:** Tạo qua `@BotFather` (cho Telegram Trigger & Send Message).
- **Evolution API Instance:** (Hoặc cấu hình webhook WhatsApp tương đương) để nhận/gửi tin nhắn WhatsApp qua `on new message (Evolution)`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn cấp.
- Mở n8n Editor, chọn **Add Workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán workflow vào bảng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình kỹ các node trọng điểm sau:
- **`Calendar AI Agent` & `OpenAI Chat Model`**: Kết nối credentials OpenAI và cấu hình System Prompt cho AI hiểu rõ vai trò là trợ lý y tế, biết cách hỏi thông tin bệnh nhân và gọi đúng công cụ lịch.
- **`Check Schedule`, `Create Appointment`, `Cancel Appointment`**: Liên kết tài khoản Google Calendar và trỏ đúng vào Calendar ID của phòng khám/bác sĩ.
- **`on new message (Evolution)` & `SEND MESSAGE WHATSAPP`**: Cấu hình Webhook URL trỏ về n8n và điền thông tin API Key của Evolution API để nhận/gửi tin nhắn WhatsApp.
- **`Telegram Trigger` & `SEND MESSAGE TELEGRAM`**: Nhập Telegram Bot Token hợp lệ để kích hoạt trigger lắng nghe tin nhắn từ Telegram.
- **Các node Redis (`REDIS - DEBOUNCE - SET/GET/DELETE`)**: Đảm bảo kết nối tới Redis Server của sếp đang hoạt động ổn định để cơ chế gom tin nhắn hoạt động chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn mẫu qua Telegram Bot hoặc WhatsApp để kiểm tra luồng hoạt động của AI Agent.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa trợ lý ảo vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu bệnh nhân:** Thêm node Google Sheets hoặc Airtable vào sau bước đặt lịch thành công để lưu lại thông tin tên, số điện thoại và lịch hẹn làm cơ sở dữ liệu chăm sóc khách hàng (CRM).
- **Gửi thông báo nhắc lịch (Reminder):** Tạo thêm một workflow phụ chạy định kỳ mỗi ngày qua Cron node để quét lịch hẹn trên Google Calendar ngày mai và tự động bắn tin nhắn nhắc nhở bệnh nhân qua Telegram/WhatsApp.
- **Bổ sung chuyển tiếp nhân sự:** Thêm node Switch hoặc kiểm tra từ khóa, nếu bệnh nhân có câu hỏi phức tạp mà AI không trả lời được, tự động chuyển cuộc hội thoại sang nhóm Telegram/Slack cho nhân viên y tế xử lý.

### 📌 Kết luận
Workflow Medical Appointment Scheduler là một giải pháp tự động hóa cực kỳ mạnh mẽ, giúp tối ưu hóa quy trình tiếp nhận lịch hẹn, nâng cao chuyên nghiệp và tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi ngày cho cơ sở y tế của các sếp. Hãy triển khai ngay hôm nay!