---
title: "🚀 Tạo Bot Telegram vẽ ảnh AI cực đỉnh với GPT-4o và Flux Pro qua n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động hóa việc tạo ảnh AI trên Telegram bằng mô hình Flux Pro, được tối ưu prompt thông minh bởi GPT-4o và quản lý hạn mức qua Google Sheets."
slug: "tao-bot-telegram-ve-anh-ai-gpt-4o-flux-pro-n8n"
tags: [n8n, automation, telegram, ai-image-generation, gpt-4o, flux-pro, google-sheets]
keywords: [n8n workflow, bot telegram tao anh ai, flux pro n8n, gpt-4o prompt enhancer, ai/ml api n8n]
---

# 🚀 Xây dựng Bot Telegram vẽ ảnh AI chuyên nghiệp với GPT-4o & Flux Pro trên n8n

Các sếp đang tìm cách xây dựng một con bot Telegram cho phép người dùng nhập câu lệnh (prompt) và tự động trả về những bức ảnh nghệ thuật cực kỳ sắc nét? Việc tạo ảnh AI thông thường đôi khi gặp vấn đề do prompt của người dùng quá ngắn hoặc thiếu chi tiết. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n hoàn chỉnh: Tự động tiếp nhận yêu cầu từ Telegram, kiểm tra hạn mức sử dụng qua **Google Sheets**, sử dụng **GPT-4o** để "phù phép" làm giàu prompt, gọi mô hình **Flux Pro** vẽ ảnh, viết mô tả sinh động và gửi trả lại người dùng một cách mượt mà nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Người dùng chat với bot Telegram là có ngay ảnh đẹp, không cần thao tác thủ công.
- **Nâng tầm chất lượng ảnh:** GPT-4o tự động biến những câu lệnh đơn sơ thành các đoạn prompt chi tiết, giàu tính nghệ thuật.
- **Kiểm soát chi phí thông minh:** Giới hạn số lượt tạo ảnh mỗi ngày cho từng user thông qua Google Sheets, tránh tình trạng bị lạm dụng API.
- **Lưu trữ minh bạch:** Tự động ghi log toàn bộ lịch sử (user_id, thời gian, từ khóa, link kết quả) lên Google Sheets để tiện tra cứu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo qua `@BotFather`.
- **Tài khoản AI/ML API:** Lấy API Key để kết nối với các mô hình GPT-4o và Flux Pro.
- **Google Sheets:** Chuẩn bị sẵn một Google Sheet để ghi log dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **📩 Receive Telegram Message (Telegram Trigger):** Kết nối với Telegram Credentials của sếp để nhận tin nhắn từ người dùng.
- **📊 Fetch Usage Logs & 📝 Log Successful Generation (Google Sheets):** 
  - Chọn tài khoản Google Sheets Credentials (OAuth2 hoặc Service Account).
  - Trỏ tới file Google Sheet và chọn Sheet chứa dữ liệu với các cột: `user_id`, `date`, `query`, `result_url`.
- **🔢 Set Daily Limit:** Tùy chỉnh số lượng lượt tạo ảnh tối đa cho phép mỗi ngày cho mỗi user (ví dụ: 5 hoặc 10 lần/ngày).
- **🧠 Enhance Prompt (AI/ML API | GPT-4o):** 
  - Chọn AIMLAPI Credentials.
  - Sử dụng model `openai/gpt-4o` để tối ưu hóa câu lệnh từ người dùng thành prompt chi tiết cho việc vẽ ảnh.
- **🎨 Generate Image (AI/ML API | Flux-pro):** 
  - Gọi HTTP Request tới AIMLAPI sử dụng mô hình `flux-pro` để tạo ảnh chất lượng cao dựa trên prompt đã được enhance.
- **🖋 Describe Image (AI/ML API | GPT-4o):** 
  - Tiếp tục dùng GPT-4o để viết một đoạn caption sinh động, trực quan kèm theo bức ảnh chuẩn bị gửi.
- **📤 Send Image to User (Telegram):** Gửi bức ảnh kèm caption hoàn chỉnh về cho người dùng qua Telegram.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử trực tiếp trên Telegram bằng cách nhắn tin cho bot.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để bot chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng tính năng:** Các sếp có thể bổ sung node kiểm tra nội dung nhạy cảm (NSFW filtering) trước khi gọi API tạo ảnh.
- **Thêm lệnh hỗ trợ:** Tích hợp thêm các câu lệnh như `/help` hoặc `/history` để tra cứu lịch sử tạo ảnh cá nhân.
- **Thông báo qua kênh nội bộ:** Kết nối thêm một nhánh gửi thông báo về Slack hoặc Telegram Admin mỗi khi có user chạm mốc giới hạn hoặc tạo ảnh thành công.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các sếp muốn xây dựng dịch vụ tạo ảnh AI riêng hoặc tích hợp công cụ sáng tạo nội dung cho team. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình làm việc và đem lại trải nghiệm tuyệt vời cho người dùng!