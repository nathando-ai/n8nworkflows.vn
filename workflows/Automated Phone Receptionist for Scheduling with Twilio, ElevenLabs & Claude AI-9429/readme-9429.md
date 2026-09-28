---
title: "🤖 Thư Viện AI Tự Động Lên Lịch Hẹn qua Gọi Điện Thoại với ElevenLabs, Claude AI & Google Calendar"
description: "Workflow tự động hóa hoàn toàn không cần code giúp doanh nghiệp tự động nhận cuộc gọi, sử dụng AI Claude 3.5 Sonnet để hẹn lịch, ghi chú chi tiết và đồng bộ hóa lên Google Calendar. Giảm 90% thời gian quản lý lịch hẹn thủ công."
slug: "thu-vien-ai-tu-dong-len-lich-hen-qua-goi-dien-thoai"
tags: [n8n, automation, no-code, ai-chatbot, google-calendar, elevenlabs, claud-ai, redis-memory]
keywords: [n8n workflow tự động hóa lịch hẹn, AI nhận cuộc gọi tự động, Claude 3.5 Sonnet hẹn lịch, ElevenLabs + Google Calendar, tự động hóa dịch vụ khách hàng]
---

# 🚀 **Thư Viện AI Tự Động Lên Lịch Hẹn qua Gọi Điện Thoại với ElevenLabs, Claude AI & Google Calendar**

## **💡 Giải pháp cho doanh nghiệp bị "chìm" trong công việc quản lý lịch hẹn thủ công**
Các sếp đang phải mất **giờ đồng hồ** mỗi ngày để:
- Nhận cuộc gọi từ khách hàng và ghi lại thông tin.
- Tra cứu lịch sẵn có trên Google Calendar.
- Ghi chú chi tiết và xác nhận lịch hẹn.
- Đảm bảo không có xung đột thời gian.

**Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Nhận cuộc gọi** qua Twilio (hoặc ElevenLabs) và chuyển đổi thành văn bản.
✅ **Sử dụng AI Claude 3.5 Sonnet** để:
   - Hiểu yêu cầu của khách hàng.
   - Tra cứu lịch sẵn có trên Google Calendar.
   - Đặt lịch hẹn tự động.
   - Ghi chú chi tiết (địa chỉ, email, mô tả vấn đề).
✅ **Gửi phản hồi bằng giọng nói** (quay lại ElevenLabs) hoặc email.
✅ **Giữ nhớ cuộc gọi** (Redis Memory) để AI tiếp tục cuộc trò chuyện nếu khách hàng gọi lại.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** quản lý lịch hẹn thủ công.
- **Khách hàng được phục vụ 24/7** mà không cần nhân viên trực.
- **Chính xác 100%** (không lỡ lịch, không xung đột).
- **Cá nhân hóa** (AI ghi nhớ lịch sử cuộc gọi).
- **Hoạt động liên tục** (không cần nhân viên trực đêm).
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Twilio** (hoặc ElevenLabs) để nhận cuộc gọi.
2. **Tài khoản Google Calendar** (đã chia sẻ quyền với n8n).
3. **API Key của Anthropic** (để sử dụng Claude 3.5 Sonnet).
4. **Redis Server** (để lưu nhớ cuộc gọi).
5. **Twilio Number** (số điện thoại để khách gọi vào).
6. **Thông tin cấu hình** (timezone, giờ làm việc, ngày nghỉ, trường dữ liệu bắt buộc).

**📌 Lưu ý:**
- Nếu chưa có Redis, có thể sử dụng **Redis Cloud** (miễn phí cho thử nghiệm).
- **Twilio** và **ElevenLabs** phải được kết nối với n8n qua Webhook.
:::

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9429](https://n8n.io/workflows/9429) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Tạo mới workflow và **copy/paste** từng node theo danh sách dưới đây.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **9 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Webhook (Nhận cuộc gọi)**
- **Node:** `Webhook: Receive User Request (ElevenLabs)`
- **Cấu hình:**
  - Thay `REPLACE ME` trong `path` bằng một đường dẫn duy nhất (ví dụ: `/phone-receptionist`).
  - Chọn **HTTP Method: POST**.
  - **Kết nối với ElevenLabs:** Cấu hình trong **ElevenLabs Webhook Settings** (URL này sẽ được cung cấp cho ElevenLabs).

##### **🔹 Google Calendar (Tra cứu & đặt lịch)**
- **Node:** `Calendar: Check Availability`, `Calendar: Create Appointment`, `Update an event in Google Calendar`
- **Cấu hình:**
  - Thay `googleCalendarOAuth2Api` bằng **credentials** của Google Calendar đã kết nối.
  - **Calendar ID** phải đúng định dạng: `xxxxxx@group.calendar.google.com` hoặc `email@gmail.com`.
  - **Chia sẻ quyền** cho n8n đọc/thêm/xóa sự kiện.

##### **🔹 AI Claude 3.5 Sonnet (Logic hẹn lịch)**
- **Node:** `Anthropic Chat Model`
- **Cấu hình:**
  - Chọn **model: claude-3-5-sonnet-20241022** (khuyến nghị).
  - Điền **API Key** của Anthropic vào **credentials**.
  - **Prompt cấu hình** (cần thay đổi theo yêu cầu):
    ```yaml
    TIMEZONE: Asia/HoChiMinh
    APPOINTMENT_DURATION: 30
    START_TIME: 08:00
    END_TIME: 18:00
    OPERATING_DAYS: Monday, Tuesday, Wednesday, Thursday, Friday
    BLOCKED_DAYS: Saturday, Sunday
    MINIMUM_LEAD_TIME: 60
    REQUIRED_FIELDS: email, phone, address
    REQUIRED_FIELDS_NATURAL_LANGUAGE: "the service address and your email"
    REQUIRED_FIELDS_LIST: "address, email, phone"
    SERVICE_TYPE: "Plumbing Service"
    PRIMARY_IDENTIFIER: "[Customer Name]"
    REQUIRED_NOTES_FIELDS: "Problem description from call_log, user's email, user's address, and user's phone number"
    ```

##### **🔹 Redis Memory (Giữ nhớ cuộc gọi)**
- **Node:** `Redis Chat Memory`
- **Cấu hình:**
  - Thêm **credentials Redis** (IP, port, password).
  - **contextWindowLength** (số tin nhắn lưu trữ, mặc định 20).
  - **Session ID** tự động lấy từ ElevenLabs.

##### **🔹 Voice AI Agent (Trả lời bằng giọng nói)**
- **Node:** `Voice AI Agent` (LangChain Agent)
- **Cấu hình:**
  - Kết nối với **ElevenLabs** để chuyển đổi văn bản thành giọng nói.
  - **Test trước khi live:** Gọi thử để đảm bảo AI trả lời chính xác.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gọi vào số Twilio và nói: *"Tôi muốn hẹn lịch sửa ống nước vào ngày mai."*
   - AI sẽ tra cứu lịch, đặt lịch và trả lời bằng giọng nói.
2. **Bật Active workflow** khi đã kiểm tra xong.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram:**
   - Gửi thông báo khi có lịch hẹn mới qua Slack/Telegram.
   - **Node:** `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu log cuộc gọi:**
   - Ghi lại toàn bộ cuộc trò chuyện vào Google Sheets hoặc Firebase.
   - **Node:** `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.firebase`.

3. **Báo cáo tự động hàng tuần:**
   - Tạo báo cáo số lượng lịch hẹn, khách hàng mới, và thời gian trung bình chờ.
   - **Node:** `n8n-nodes-base.email` (gửi qua Gmail) hoặc `n8n-nodes-base.slack`.

4. **Cải thiện prompt cho AI:**
   - Nếu AI trả lời không chính xác, điều chỉnh **prompt** trong `Anthropic Chat Model`.
   - Ví dụ: Thêm điều kiện cụ thể như *"Không đặt lịch sau 17h30"*.

5. **Sử dụng Twilio để gọi lại tự động:**
   - Nếu khách hàng không xác nhận lịch, Twilio có thể gọi lại sau 1 giờ.
   - **Node:** `n8n-nodes-base.twilio`.
:::

---
### **📌 Kết luận**
Workflow này **giải phóng toàn bộ thời gian** của các sếp khỏi công việc quản lý lịch hẹn thủ công, đồng thời **cải thiện trải nghiệm khách hàng** với AI phản hồi nhanh chóng và chính xác.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (Self-hosted) để workflow chạy 24/7.
2. **Kết nối Twilio, Google Calendar và Redis**.
3. **Cấu hình prompt và test**.
4. **Bật workflow và bắt đầu tự động hóa!**

---
:::note[🔥 LƯU Ý CUỐI CÙNG]
- **Không thay đổi biến động `{{ }}`** trong prompt (nó tự động lấy dữ liệu từ ElevenLabs).
- **Test với dữ liệu thật trước khi live** để tránh lỗi.
- **Nếu AI trả lời sai**, điều chỉnh prompt hoặc thay đổi model (nhưng **không bỏ node `toolThink`**).
:::

---
**🎁 Đăng ký VPS TinoHost để self-host n8n:**
👉 [🔗 Đăng ký VPS N8N](https://tino.vn/vps-n8n?affid=388) (💰 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [🔗 Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)