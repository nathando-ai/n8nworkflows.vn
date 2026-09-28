---
title: "🚀 Xây dựng Trợ lý ảo Telegram thông minh với GPT-4o-mini, Google Calendar & Gmail"
description: "Tự động hóa quản lý lịch trình, danh bạ và gửi email trực tiếp qua Telegram Bot sử dụng AI Agent, GPT-4o-mini và các dịch vụ Google."
slug: "quan-ly-lich-trinh-danh-ba-telegram-bot-gpt-4o-mini"
tags: [n8n, automation, telegram-bot, ai-agent, gpt-4o-mini, google-workspace]
keywords: [n8n workflow, telegram bot ai, gpt-4o-mini n8n, google calendar automation, quan ly lich trinh tu dong]
---

# 🚀 Xây dựng Trợ lý ảo Telegram thông minh với GPT-4o-mini, Google Calendar & Gmail

Các sếp có đang cảm thấy quá tải khi phải liên tục chuyển đổi giữa Google Calendar, danh bạ Google Sheets, hòm thư Gmail và ứng dụng nhắn tin để sắp xếp công việc hàng ngày? Việc quản lý thủ công này không chỉ tốn thời gian mà còn dễ dẫn đến sót lịch hẹn quan trọng.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp biến **Telegram** thành một trung tâm điều khiển toàn năng. Chỉ cần nhắn tin cho Bot, **AI Agent** sử dụng mô hình **GPT-4o-mini** sẽ hiểu ý, tự động tra cứu danh bạ, kiểm tra/thêm lịch hẹn vào Google Calendar, gửi email qua Gmail và thậm chí tra cứu thông tin trên Wikipedia hay Google Search. Tự động hóa 100% mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý lịch trình thông minh:** Thêm, sửa, xóa hoặc xem lịch hẹn Google Calendar chỉ bằng câu lệnh tự nhiên trên Telegram.
- **Tích hợp Gmail & Danh bạ mượt mà:** Tra cứu thông tin liên hệ từ Google Sheets và gửi email trực tiếp thông qua trợ lý ảo.
- **AI Đa năng (Multimodal AI):** Kết hợp khả năng lập luận của GPT-4o-mini cùng các công cụ tìm kiếm (Wikipedia, SerpAPI) để trả lời mọi thắc mắc.
- **Hoạt động 24/7:** Trợ lý ảo luôn túc trực trên Telegram để hỗ trợ các sếp mọi lúc, mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **OpenAI API Key** (để sử dụng model `gpt-4o-mini`).
- **Google Account Credentials** (OAuth2 cho Google Calendar, Gmail và Google Sheets).
- **SerpAPI Key** (để cung cấp tính năng tìm kiếm web cho AI Agent).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc sao chép đoạn mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình các node cốt lõi sau:

- **Telegram Trigger & Telegram Response**: 
  - Kết nối với tài khoản Telegram của các sếp bằng cách tạo *Telegram API Credential* thông qua Bot Token nhận được từ `@BotFather`.
- **OpenAI Chat Model**: 
  - Chọn model `gpt-4o-mini` (như cấu hình sẵn) và thiết lập *OpenAI API Key Credential*.
- **Google Calendar (Tools & Get Calendar Events)**: 
  - Xác thực tài khoản Google của các sếp để cho phép AI Agent đọc và ghi sự kiện vào lịch.
- **Gmail Tool**: 
  - Cấp quyền OAuth2 cho Gmail để Bot có thể soạn và gửi email hộ các sếp.
- **Get Contacts (Google Sheets Tool)**: 
  - Kết nối tới file Google Sheets chứa danh bạ khách hàng/đối tác của các sếp để AI Agent có thể tra cứu khi cần.
- **Web Search (SerpAPI) & Wikipedia Tool**: 
  - Nhập SerpAPI Key để kích hoạt tính năng tìm kiếm thông tin ngoài Internet cho AI Agent.

#### 3. Kích hoạt ⚡️
- Nhấn **Chat with Bot** trên Telegram và gửi thử một tin nhắn (ví dụ: *"Lịch trình ngày mai của tôi có gì?"* hoặc *"Tìm thông tin về..."*).
- Kiểm tra kết quả phản hồi trực tiếp trên Telegram.
- Sau khi test thành công, gạt công tắc sang **Active** để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông tin:** Các sếp có thể thay thế hoặc kết nối thêm **Slack** hoặc **Telegram Group** để nhận thông báo tổng kết công việc hàng ngày.
- **Lưu trữ lịch sử chat:** Tận dụng node `Conversation Memory` kết hợp lưu log cuộc trò chuyện vào Google Sheets để phân tích nhu cầu người dùng.
- **Tự động hóa Marketing:** Kết hợp workflow này với việc tự động gửi tin nhắn chăm sóc khách hàng định kỳ dựa trên dữ liệu Google Calendar.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một "thư ký riêng" đắc lực trên Telegram với chi phí cực kỳ tối ưu nhờ GPT-4o-mini. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian và nâng cao hiệu suất công việc!