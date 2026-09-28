---
title: "🚀 Trợ lý ảo AI quản lý Google Calendar trực tiếp qua WhatsApp với GPT-4"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa lịch trình cá nhân bằng AI Agent, cho phép tạo, sửa, xóa và tìm kiếm sự kiện Google Calendar qua tin nhắn WhatsApp."
slug: "quan-ly-google-calendar-qua-whatsapp-voi-gpt4-n8n"
tags: [n8n, automation, ai-agent, openai, google-calendar, whatsapp]
keywords: [n8n workflow, trợ lý ảo whatsapp, quản lý lịch google calendar tự động, openai gpt-4 n8n, timepilot agent]
---

# 🚀 Trợ lý ảo AI quản lý Google Calendar trực tiếp qua WhatsApp với GPT-4

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở ứng dụng Calendar, chọn ngày, điền tiêu đề và thời gian thủ công mỗi khi có lịch họp mới không? Việc quản lý lịch trình đôi khi chiếm quá nhiều thời gian quý giá.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một trợ lý ảo thông minh (mang tên **TimePilot**) kết hợp giữa **n8n**, **OpenAI GPT-4**, **WhatsApp** và **Google Calendar**. Chỉ bằng một tin nhắn thoại hoặc văn bản bình thường trên WhatsApp (ví dụ: *"Đặt lịch họp với Anna lúc 4h chiều mai"*), trợ lý ảo sẽ tự động phân tích và cập nhật lịch trình cho các sếp ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Xử lý yêu cầu tạo, sửa, xóa, tìm kiếm lịch họp chỉ qua tin nhắn chat đơn giản.
- **Xử lý ngôn ngữ tự nhiên thông minh:** Nhờ GPT-4 (`gpt-4-turbo-preview`), trợ lý hiểu được các mốc thời gian linh hoạt (như "ngày mai", "tuần tới", "chiều nay").
- **Duy trì ngữ cảnh hội thoại:** Nhờ `Simple Memory`, các sếp có thể trò chuyện nối tiếp mà không cần lặp lại thông tin chi tiết.
- **Phản hồi tức thì:** Gửi tin nhắn xác nhận kết quả trực tiếp về WhatsApp cho người dùng ngay sau khi hoàn tất.
:::

### yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Meta Developer / WhatsApp Business Cloud** (đã cấu hình số điện thoại và Webhook).
- **Tài khoản Google** (để kết nối Google Calendar).
- **OpenAI API Key** (với quyền sử dụng GPT-4).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy file JSON của workflow này từ link gốc n8n (ID: 5368) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node cốt lõi sau cần được cấu hình chính xác:

- **WhatsApp Trigger**: Kết nối với `whatsAppTriggerApi`. Nhận tin nhắn từ webhook của Meta gửi đến khi có tin nhắn mới trên WhatsApp.
- **TimePilot (Agent)**: Node AI Agent trung tâm điều phối các công cụ (Tools). Sẽ liên kết với OpenAI Chat Model và các Google Calendar Tools.
- **OpenAI Chat Model**: Chọn model `gpt-4-turbo-preview` và cấu hình `openAiApi` credentials.
- **Create Event / Update Event / Delete Event / Search Event**: Các công cụ kết nối với Google Calendar. Cần cấu hình `googleCalendarOAuth2Api` để cấp quyền cho n8n thao tác với lịch của các sếp.
- **Simple Memory**: Giúp AI ghi nhớ ngữ cảnh trò chuyện gần nhất.
- **WhatsApp Business Cloud**: Node gửi tin nhắn phản hồi, sử dụng `whatsAppApi` để gửi kết quả xác nhận (thành công/thất bại) về lại số WhatsApp của người dùng.

#### 3. Kích hoạt ⚡️
1. Gửi một tin nhắn thử nghiệm qua WhatsApp đến số đã kết nối, ví dụ: *"Create a meeting with Anna at 4pm tomorrow"* (Tạo cuộc họp với Anna lúc 4h chiều mai).
2. Kiểm tra log trên n8n xem AI Agent đã gọi đúng tool **Create Event** và phản hồi lại qua WhatsApp chưa.
3. Bật **Active workflow** để hệ thống hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo Slack/Telegram:** Ngoài việc gửi tin nhắn về WhatsApp, các sếp có thể mở rộng workflow để bắn thông báo nhắc nhở vào nhóm làm việc nội bộ.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets để log lại toàn bộ các yêu cầu mà trợ lý ảo đã thực hiện nhằm phục vụ việc kiểm tra sau này.
- **Mở rộng công cụ (Tools):** Thêm các công cụ kiểm tra thời tiết, gửi email tự động hoặc tạo task trong Notion ngay trong cùng một Agent.

### 📌 Kết luận
Với workflow TimePilot này, các sếp đã sở hữu ngay một trợ lý AI quản lý thời gian cá nhân cực kỳ mạnh mẽ ngay trên ứng dụng nhắn tin quen thuộc. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc của mình nhé!