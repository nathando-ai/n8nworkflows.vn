---
title: "🚀 Quản lý Google Calendar bằng Giọng nói & Tin nhắn với GPT-4 và Telegram qua n8n"
description: "Hướng dẫn xây dựng trợ lý ảo AI trên Telegram giúp tạo, sửa, xóa và tra cứu lịch Google Calendar hoàn toàn tự động bằng tin nhắn văn bản hoặc giọng nói nhờ OpenAI GPT-4 và Whisper."
slug: "quan-ly-calendar-voi-ai-telegram-google-calendar"
tags: [n8n, automation, ai, openai, google-calendar, telegram]
keywords: [n8n workflow, trợ lý ảo lịch, tự động hóa telegram google calendar, openai whisper gpt-4, quan ly lich bang giong noi]
---

# 🚀 Xây dựng Trợ lý Quản lý Lịch Thông Minh bằng AI (Giọng nói & Văn bản) trên Telegram

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở ứng dụng Lịch (Google Calendar), chọn ngày giờ, điền tiêu đề sự kiện thủ công mỗi khi có cuộc hẹn mới? Việc này không chỉ tốn thời gian mà còn dễ gây nhầm lẫn khi đang bận rộn. 

Giải pháp hoàn hảo cho các sếp đây: một trợ lý ảo tích hợp trực tiếp vào **Telegram**, cho phép các sếp **gửi tin nhắn văn bản hoặc gửi... tin nhắn thoại** (nói "Lên lịch họp với đối tác A vào lúc 3 giờ chiều mai nhé"), và AI sẽ tự động xử lý, đồng bộ hóa mọi thứ lên **Google Calendar** trong chớp mắt! Toàn bộ quy trình này được tự động hóa 100% không cần code bằng n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác tự nhiên:** Nhắn tin hoặc gửi voice note qua Telegram như trò chuyện với trợ lý riêng.
- **Xử lý đa năng:** Hỗ trợ đầy đủ 4 thao tác quan trọng: Tạo sự kiện mới (`Create Event`), Xem lịch (`Get events`), Cập nhật (`Update Calendar`) và Xóa sự kiện (`Detele Event`).
- **Tự động hóa giọng nói:** Tích hợp OpenAI Whisper để tự động chuyển đổi file ghi âm (.ogg) thành văn bản chuẩn xác trước khi phân tích.
- **Hoạt động 24/7:** Phản hồi kết quả ngay lập tức vào đoạn chat Telegram sau khi thao tác với lịch hoàn tất.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Telegram Bot** (tạo qua BotFather để lấy API Token).
- Tài khoản **OpenAI** có sẵn API Key (hỗ trợ mô hình GPT-4 và Whisper).
- Tài khoản **Google** có quyền truy cập Google Calendar.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n chọn **New Workflow** -> Bấm tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên màn hình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình các credentials và tham số quan trọng sau:

- **Receive User Input (Telegram):** Kết nối với Telegram Bot Credentials (nhập Bot Token lấy từ BotFather). Node này đóng vai trò kích hoạt workflow mỗi khi có tin nhắn gửi tới bot.
- **Is Voice Message? (IF Node):** Kiểm tra xem tin nhắn đến là dạng văn bản hay file ghi âm giọng nói.
- **Download Voice File & Transcribe Voice to Text:** 
  - Node *Download Voice File* dùng để tải file `.ogg` từ Telegram.
  - Node *Transcribe Voice to Text* (sử dụng OpenAI API) sẽ gọi mô hình **Whisper** để dịch file âm thanh thành văn bản tiếng Việt cực kỳ chuẩn xác.
- **Extract Text Message (Set Node):** Trích xuất nội dung văn bản trong trường hợp người dùng nhắn tin trực tiếp bằng chữ.
- **AI Calendar Assistant (LangChain) & GPT-4 Language Model:**
  - Kết nối OpenAI Credentials cho model `GPT-4` (hoặc `gpt-4.1`).
  - Nhiệm vụ của Agent này là đọc hiểu ý định của người dùng (muốn tạo, sửa, xóa hay xem lịch) và gọi đúng công cụ (Tool) tương ứng.
- **Google Calendar Tools (Create Event, Get events, Update Calendar, Detele Event):**
  - Cấu hình **Google Calendar OAuth2 API** cho tất cả 4 node công cụ này.
  - Chọn đúng tài khoản Google Calendar chính mà các sếp muốn trợ lý quản lý.
- **Send Response to Telegram:** Node cuối cùng gửi thông báo xác nhận thành công hoặc kết quả tra cứu ngược lại cho người dùng trên Telegram.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tin nhắn thoại hoặc văn bản đến Bot Telegram của sếp (ví dụ: *"Thêm lịch nhắc nhở nộp báo cáo vào lúc 5 giờ chiều thứ Sáu"*).
- Kiểm tra xem sự kiện đã xuất hiện trên Google Calendar chưa và bot đã trả lời lại chưa.
- Nếu mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Phân quyền người dùng:** Thêm một node IF ở đầu luồng để kiểm tra `Chat ID` của người gửi, chỉ cho phép tài khoản của chính sếp hoặc đồng nghiệp thân thiết được quyền can thiệp vào lịch.
- **Tích hợp thêm thông báo dự phòng:** Gửi thêm một bản copy thông báo qua Google Chat hoặc Slack nếu các sếp làm việc nhóm.
- **Lưu lịch sử hoạt động:** Lưu lại các câu lệnh và kết quả thao tác vào Google Sheets để tiện tra cứu lại sau này.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một trợ lý AI quản lý thời gian cực kỳ chuyên nghiệp ngay trên chiếc điện thoại qua Telegram. Không cần mở ứng dụng phức tạp, chỉ cần nói hoặc gõ, mọi lịch trình đều được sắp xếp gọn gàng. Chúc các sếp cài đặt thành công!