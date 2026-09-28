---
title: "🚀 Xây dựng Trợ lý Quản lý Lịch hẹn AI trên Telegram với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đặt lịch, kiểm tra Google Calendar, gửi Email qua Gmail và trò chuyện thông minh bằng AI Agent trên Telegram."
slug: "meeting-management-agent-n8n"
tags: [n8n, automation, ai-agent, telegram, google-calendar, gmail, openai]
keywords: [n8n workflow, meeting management agent, trợ lý ảo n8n, tự động đặt lịch google calendar, telegram bot ai n8n]
---

# 🚀 Tự động hóa Quản lý Lịch hẹn với AI Agent trên Telegram

Việc quản lý lịch họp, kiểm tra thời gian rảnh, tạo sự kiện trên lịch và gửi email xác nhận thủ công thường chiếm rất nhiều thời gian của các sếp và đội ngũ vận hành. Thiếu sót nhỏ cũng có thể dẫn đến việc trùng lịch (double-booking) hoặc bỏ lỡ các cuộc hẹn quan trọng.

Giải pháp ư? Hãy để **Meeting Management Agent** lo thay các sếp! Workflow n8n này kết hợp sức mạnh của **AI Agent**, **Telegram**, **Google Calendar**, và **Gmail** để tạo ra một trợ lý ảo thông minh 24/7. Trợ lý này có thể giao tiếp tự nhiên với khách hàng hoặc nhân viên qua Telegram, tự động tra cứu lịch trống, tạo sự kiện mới và gửi thiệp mời qua email một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Xử lý yêu cầu đặt lịch trực tiếp qua chat Telegram mà không cần con người can thiệp.
- **Tránh trùng lịch tuyệt đối:** AI tự động kiểm tra Google Calendar trước khi xác nhận bất kỳ cuộc họp nào.
- **Giao tiếp tự nhiên:** Nhờ tích hợp OpenAI GPT, trợ lý hiểu được các câu lệnh linh hoạt như *"Đặt lịch họp vào chiều thứ Hai tới lúc 2 giờ"* hay *"Hủy cuộc họp với anh Nam ngày mai"*.
- **Đồng bộ đa kênh:** Vừa chat qua Telegram vừa gửi email xác nhận, mời họp qua Gmail cho người tham gia.
:::

### 📦 Các Nodes chính trong Workflow
Workflow này sử dụng tổng cộng 11 nodes, kết hợp các công cụ AI và tích hợp hệ thống mạnh mẽ:
- **Telegram Trigger & Telegram:** Nhận tin nhắn từ người dùng và phản hồi kết quả.
- **AI Agent & OpenAI (gpt-4.1-mini):** Bộ não trung tâm xử lý ngôn ngữ tự nhiên và điều phối công việc.
- **Memory (Buffer Window):** Giữ ngữ cảnh trò chuyện theo từng Chat ID của người dùng.
- **Google Calendar (Get, Create, Update, Delete):** Quản lý toàn bộ vòng đời của sự kiện trên lịch.
- **Gmail:** Gửi email thông báo, thư mời và xác nhận cuộc họp.
- **Date & Time:** Cung cấp thông tin thời gian chính xác cho AI tính toán.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Telegram Bot Token** (Lấy từ [@BotFather](https://core.telegram.org/bots#creating-a-new-bot)).
3. **OpenAI API Key** (Lấy từ [OpenAI Platform](https://platform.openai.com/api-keys)).
4. **Tài khoản Google** (Đã cấu hình quyền truy cập Google Calendar và Gmail).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy/paste trực tiếp JSON vào workspace).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hãy cấu hình các kết nối quan trọng sau:

- **Telegram Trigger & Telegram nodes:** 
  - Kết nối với tài khoản Telegram của các sếp bằng cách nhập **Bot Token** lấy từ @BotFather. Điều này giúp bot nhận và gửi tin nhắn trong chat.
- **OpenAI node:** 
  - Thêm Credentials chứa **OpenAI API Key**.
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc model tương đương).
- **Memory node:** 
  - Đảm bảo session key được cấu hình đúng chuẩn để ghi nhớ ngữ cảnh theo `chat.id`.
- **Google Calendar nodes (Get, Create, Update, Delete):** 
  - Kết nối tài khoản Google Calendar của các sếp. Cấu hình này cho phép AI tra cứu lịch trống, chống trùng lịch và tạo sự kiện mới.
- **Date & Time node:** 
  - Kiểm tra và thiết lập múi giờ cho phù hợp (Ví dụ: `Asia/Ho_Chi_Minh` hoặc `Asia/Dhaka` tùy theo vị trí của các sếp). Điều này giúp AI hiểu chính xác các khái niệm *"ngày mai"*, *"thứ Hai tuần tới"*.
- **Gmail node:** 
  - Kết nối tài khoản Gmail để hệ thống tự động gửi thư mời và xác nhận lịch họp tới những người tham gia.
- **AI Agent System Message:** 
  - Node AI Agent đã có sẵn các quy tắc hệ thống (System Prompt) giúp trợ lý luôn tính toán chính xác ngày tháng, kiểm tra lịch trước khi tạo sự kiện và đề xuất thời gian thay thế nếu bị trùng lịch. Hãy giữ nguyên các quy tắc này để bot hoạt động chuyên nghiệp nhất!

#### 3. Kích hoạt ⚡️
- Nhấn **Chat with bot** hoặc gửi tin nhắn thử nghiệm trên Telegram để test luồng hoạt động của AI.
- Sau khi test thành công, gạt công tắc sang **Active** để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể cân nhắc mở rộng thêm:
- **Tích hợp thêm Google Meet:** Thêm công cụ tạo link họp tự động ngay khi tạo sự kiện trên Calendar.
- **Gửi thông báo qua Slack/Telegram nội bộ:** Báo cáo cho quản lý mỗi khi có khách hàng đặt lịch thành công.
- **Lưu log vào Google Sheets:** Ghi lại toàn bộ lịch sử đặt lịch để dễ dàng thống kê và chăm sóc khách hàng sau này.

### 📌 Kết luận
Với **Meeting Management Agent**, các sếp đã sở hữu ngay một trợ lý đặt lịch thông minh hoạt động 24/7 trên Telegram mà không tốn chi phí thuê nhân sự vận hành thủ công. Hãy import workflow ngay và trải nghiệm sự kỳ diệu của tự động hóa n8n!