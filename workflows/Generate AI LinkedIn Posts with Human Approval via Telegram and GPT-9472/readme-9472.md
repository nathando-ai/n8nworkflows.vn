---
title: "🚀 Tự động tạo bài viết LinkedIn chuyên nghiệp với AI và Phê duyệt qua Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình viết bài LinkedIn bằng AI Agent kết hợp tìm kiếm web Tavily, duyệt nội dung qua Telegram và lưu trữ tự động vào Google Sheets."
slug: "tao-bai-viet-linkedin-tu-dong-voi-ai-telegram"
tags: [n8n, automation, ai-agent, telegram, openai, google-sheets, content-marketing]
keywords: [n8n workflow, tu dong hoa linkedin, ai agent telegram, viet bai linkedin ai, openai telegram n8n]
---

# 🚀 Tự động tạo bài viết LinkedIn chuyên nghiệp với AI và Phê duyệt qua Telegram

Viết nội dung đều đặn trên LinkedIn là chìa khóa để xây dựng thương hiệu cá nhân và doanh nghiệp, nhưng công việc này ngốn rất nhiều thời gian từ việc nghiên cứu ý tưởng, tra cứu thông tin thị trường cho đến khâu chấp bút. Nếu làm thủ công, các sếp sẽ dễ rơi vào cảnh cạn kiệt ý tưởng hoặc tốn hàng giờ liền cho mỗi bài đăng.

Workflow n8n này do chuyên gia **Yasser Sami** xây dựng sẽ giải quyết triệt để vấn đề trên. Hệ thống kết hợp sức mạnh của **AI Agent**, công cụ tìm kiếm thông minh **Tavily**, và quy trình phê duyệt trực tiếp qua **Telegram** trước khi tự động lưu bài hoàn thiện vào **Google Sheets**. Toàn bộ quy trình hoàn toàn tự động, không cần code và kiểm soát nội dung 100% trong tay các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian**: AI tự động tìm kiếm thông tin mới nhất trên web và viết nháp bài đăng chuẩn SEO LinkedIn chỉ trong vài giây.
- **Kiểm soát tuyệt đối**: Tính năng `Send a text message` (với chế độ chờ duyệt) gửi thẳng bài viết vào Telegram, cho phép các sếp bấm Duyệt hoặc Góp ý chỉnh sửa ngay trên điện thoại.
- **Tự động lưu trữ**: Khi bài viết được duyệt, hệ thống sẽ tự động đưa vào Google Sheets, sẵn sàng để lên lịch xuất bản.
- **Thông minh hóa liên tục**: Nếu chưa ưng ý, AI Revision Agent sẽ tự động tiếp thu phản hồi của các sếp để viết lại cho đến khi hoàn hảo.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **OpenAI API Key** (cho các mô hình GPT xử lý ngôn ngữ).
- **Tavily API Key** (để AI Agent tìm kiếm thông tin thực tế trên web).
- **Google Sheets** (chuẩn bị sẵn một file Google Sheet để lưu bài viết).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Telegram Trigger**: Kết nối với `telegramApi` của Bot Telegram mà các sếp quản lý. Node này sẽ nhận yêu cầu từ chat (ví dụ: *“Viết bài LinkedIn về xu hướng AI 2024”*).
- **AI Agent & OpenAI Chat Model**: 
  - Chọn credentials `openAiApi`.
  - Thiết lập model (mặc định sử dụng `gpt-4.1-mini` hoặc các dòng GPT mới nhất). AI Agent sẽ đóng vai trò là cây bút chiến lược kết hợp thông tin tìm được.
- **Tavily Tool**: Cung cấp `tavilyApi` để AI có quyền truy cập internet, giúp bài viết có số liệu và thông tin thời sự chính xác.
- **Send a text message (Telegram)**: 
  - Cài đặt key parameter `operation` thành `sendAndWait`. 
  - Node này cực kỳ quan trọng vì nó sẽ gửi nội dung bài nháp ra Telegram kèm theo các nút tương tác để hỏi *"Good to go?"* (Duyệt chưa?).
- **Text Classifier**: Phân loại phản hồi từ người dùng (đã duyệt để sang Google Sheets, hay yêu cầu chỉnh sửa tiếp).
- **Basic LLM Chain (Revision Agent)**: Xử lý các yêu cầu chỉnh sửa bổ sung nếu các sếp chưa hài lòng với bản nháp đầu tiên.
- **Append row in sheet (Google Sheets)**:
  - Chọn credentials `googleSheetsOAuth2Api`.
  - Trỏ tới File Sheet và chọn Sheet Name tương ứng để lưu nội dung bài đăng LinkedIn chính thức sau khi được phê duyệt.

#### 3. Kích hoạt ⚡️
- Gửi thử một tin nhắn mẫu đến Telegram Bot của sếp để test luồng chạy (Test run).
- Kiểm tra xem Telegram có nhận được yêu cầu duyệt bài hay không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & Gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Telegram, các sếp có thể kết nối thêm Slack hoặc Discord để đội ngũ content cùng tham gia duyệt bài.
- **Tích hợp tự động đăng bài**: Thay vì chỉ dừng lại ở việc lưu vào Google Sheets, các sếp có thể nối tiếp node Google Sheets với **LinkedIn API** để hệ thống tự động xuất bản bài viết lên trang cá nhân hoặc Fanpage công ty.
- **Lưu lịch sử hội thoại**: Thêm một bước ghi log vào cơ sở dữ liệu (như Airtable hoặc Notion) để dễ dàng theo dõi hiệu suất tạo nội dung hàng tuần.

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung chưa bao giờ dễ dàng đến thế. Với workflow n8n kết hợp AI và Telegram này, các sếp vừa có thể chủ động nguồn nội dung chất lượng cao, vừa tiết kiệm được thời gian kiểm duyệt mà không cần ngồi kè kè trước máy tính. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc!