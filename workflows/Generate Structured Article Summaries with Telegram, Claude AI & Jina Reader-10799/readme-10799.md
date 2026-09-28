---
title: "🚀 Tự động tóm tắt bài viết bằng Claude AI, Telegram và Jina Reader qua n8n"
description: "Xây dựng chatbot Telegram tự động nhận link bài viết, làm sạch nội dung bằng Jina Reader, tóm tắt thông minh bằng Claude 3.5 Haiku và lưu trữ vào Google Sheets."
slug: "tu-dong-tom-tat-bai-viet-telegram-claude-ai-jina-reader-n8n"
tags: [n8n, automation, ai-summarization, telegram, claude-ai, openrouter]
keywords: [n8n workflow, tóm tắt bài viết tự động, telegram bot ai, claude ai n8n, jina reader]
---

# 🚀 Tự động tóm tắt bài viết thông minh với Telegram, Claude AI & Jina Reader

Các sếp có bao nhiêu tab bài báo, tài liệu dài đang mở mà chưa có thời gian đọc? Việc đọc thủ công từng bài viết dài không chỉ tốn thời gian mà còn khiến chúng ta dễ bị "ngợp" thông tin. 

Đừng lo! Workflow n8n này sẽ giúp các sếp giải quyết triệt để vấn đề đó. Chỉ cần gửi bất kỳ đường dẫn (URL) nào vào **Telegram Bot**, hệ thống sẽ tự động lọc, trích xuất nội dung sạch, dùng sức mạnh của **Claude AI (qua OpenRouter)** để tóm tắt thành các ý chính cấu trúc rõ ràng, gửi ngược lại Telegram và đồng thời lưu trữ vào **Google Sheets** để tra cứu sau này. Tất cả diễn ra hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian đọc:** Nhanh chóng nắm bắt nội dung cốt lõi của bài viết dài chỉ trong vài giây.
- **Nội dung sạch, chuẩn xác:** Loại bỏ hoàn toàn quảng cáo, menu rườm rà nhờ Jina Reader.
- **Cấu trúc thông minh:** Nhận kết quả tóm tắt gồm Tiêu đề, Tóm tắt 1 câu và 3-5 ý chính (Key points) ngay trên Telegram.
- **Lưu trữ tự động:** Tự động đồng bộ lịch sử tóm tắt vào Google Sheets để quản lý và ôn tập kiến thức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua BotFather).
- **OpenRouter API Key** (để sử dụng model `anthropic/claude-3.5-haiku`).
- **Google Sheets** (tùy chọn nếu muốn lưu trữ lịch sử).
- **Jina AI API Key** (tùy chọn, giúp tối ưu việc cào bài viết).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm sau:

- **After message is received (`telegramTrigger`)**: Kết nối với tài khoản Telegram Credentials của sếp để lắng nghe tin nhắn gửi tới bot.
- **Check if URL (`filter`)**: Node này đảm bảo bot chỉ xử lý các tin nhắn bắt đầu bằng `http://` hoặc `https://`. Các tin nhắn thông thường sẽ được bỏ qua.
- **Fetch Article Markdown (`httpRequest`)**: Sử dụng Jina Reader API để chuyển đổi trang web thành văn bản Markdown sạch sẽ, tự động loại bỏ quảng cáo và các thành phần thừa.
- **OpenRouter Chat Model (`lmChatOpenRouter`)**: Chọn model `anthropic/claude-3.5-haiku` (hoặc các model LLM khác tùy thích) và kết nối OpenRouter API Key.
- **Summarize Article (`chainLlm`) & Output Parser (`outputParserStructured`)**: Nơi cấu hình prompt và định dạng JSON đầu ra (Tiêu đề, Tóm tắt ngắn, Các ý chính, v.v.). Sếp có thể tinh chỉnh prompt tại đây để bot trả lời bằng tiếng Việt hoặc ngôn ngữ mong muốn.
- **Send Summary to Telegram (`telegram`)**: Gửi kết quả tóm tắt đã được format đẹp mắt kèm emoji về lại chat Telegram cho sếp.
- **Save to Google Sheets (`googleSheets`)**: Cấu hình kết nối Google Drive/Sheets OAuth2, chọn file Sheet và Sheet Name để lưu thông tin bài viết.
- **Notify an error... (`telegram`)**: Các node thông báo lỗi qua Telegram trong trường hợp không fetch được bài viết hoặc lỗi AI xử lý.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một link bài báo bất kỳ vào Telegram Bot của sếp để test.
- Kiểm tra kết quả trả về trên Telegram và Google Sheets.
- Nếu mọi thứ chạy mượt mà, gạt công tắc sang **Active** để khởi Chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh lưu trữ:** Ngoài Google Sheets, các sếp có thể thay thế hoặc bổ sung bằng node Notion, Airtable hoặc Coda để xây dựng cơ sở dữ liệu kiến thức cá nhân (Knowledge Base).
- **Tích hợp thêm thông báo nhóm:** Thay vì chỉ gửi về chat cá nhân, sếp có thể cấu hình bot gửi bản tóm tắt vào một nhóm Telegram hoặc kênh Slack chung của team để cùng đọc sách/báo.
- **Tùy biến ngôn ngữ:** Thêm chỉ dẫn trong node AI prompt để bắt buộc kết quả tóm tắt luôn xuất ra bằng tiếng Việt dù bài báo gốc là tiếng Anh hay ngôn ngữ khác.

### 📌 Kết luận
Một workflow cực kỳ thiết thực giúp nâng cao năng suất cá nhân và quản lý thông tin hiệu quả. Hãy cài đặt ngay để biến chiếc Telegram của sếp thành một trợ lý đọc sách và nghiên cứu tài liệu AI thông minh!