---
title: "🚀 Tự động log dinh dưỡng bữa ăn từ Telegram vào Google Sheets bằng AI Agent"
description: "Hướng dẫn xây dựng workflow n8n thông minh giúp ghi chép calo và dinh dưỡng bữa ăn qua tin nhắn văn bản hoặc giọng nói trên Telegram, tự động phân tích bằng OpenAI và lưu vào Google Sheets."
slug: "log-dinh-duong-tu-telegram-vao-google-sheets-ai-agent"
tags: [n8n, automation, no-code, ai-agent, telegram, openai, google-sheets]
keywords: [n8n workflow, tự động hóa telegram, log dinh dưỡng ai, openai whisper n8n, google sheets automation]
---

# 🚀 Tự động log dinh dưỡng bữa ăn từ Telegram vào Google Sheets bằng AI Agent

Việc theo dõi lượng calo và các chất dinh dưỡng nạp vào cơ thể mỗi ngày thường rất phiền toái vì phải mở app tra cứu thủ công từng món. Các sếp có bao giờ ước mình chỉ cần nhắn tin nhanh cho một trợ lý ảo những gì vừa ăn (hoặc gửi cả tin nhắn thoại) rồi mọi thứ tự động lưu vào bảng tính không? 

Workflow n8n này do tác giả **PollupAI** phát triển chính là giải pháp tự động hóa 100% không cần code, biến Telegram thành một chuyên gia dinh dưỡng cá nhân hỗ trợ các sếp ghi chép calo cực kỳ nhanh chóng và thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa dạng cách nhập liệu:** Gửi tin nhắn chữ thông thường hoặc ghi âm giọng nói (voice message) khi đang bận rộn.
- **Xử lý AI thông minh:** AI tự động bóc tách tên nguyên liệu, định lượng, tính toán lượng calo, protein, carbs, fat nhờ sử dụng `OpenAI Chat Model` (`gpt-4o-mini`) kết hợp `Structured Output Parser`.
- **Đồng bộ tự động:** Dữ liệu từng thành phần món ăn được phân tách rõ ràng (`Explode the list`) và lưu trữ ngăn nắp vào Google Sheets kèm theo ngày giờ cụ thể.
- **Phản hồi tức thì:** Bot Telegram sẽ gửi lại tin nhắn xác nhận sau khi đã ghi nhận thành công bữa ăn của các sếp.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua `@BotFather`).
- **OpenAI API Key** (Sử dụng cho tính năng Transcribe âm thanh và AI Agent phân tích dinh dưỡng).
- **Google Sheets** (Tạo sẵn một file Google Sheet để lưu dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node quan trọng sau:
- **Receive Telegram message** & **Get Audio File** & **Respond message**: Kết nối với tài khoản Telegram Credentials (`telegramApi`) sử dụng Bot Token của các sếp.
- **OpenAI Chat Model** & **Transcribe Recording**: Kết nối với OpenAI Credentials (`openAiApi`). Node `gpt-4o-mini` sẽ đảm nhận nhiệm vụ đọc hiểu món ăn.
- **List of Ingredients and nutrients (Agent)**: Tùy chỉnh system prompt của AI Agent nếu các sếp muốn nó trả về các chỉ số dinh dưỡng theo ý muốn (Calories, Protein, Carbs, Fat...).
- **Store in sheet**: Chọn file Google Sheets và sheet tương ứng của các sếp, kết nối bằng `Google Sheets OAuth2 API`. Đảm bảo các cột trong Sheet khớp với cấu trúc dữ liệu mà AI trả về (Tên món, Nguyên liệu, Calo, Ngày tháng...).

#### 3. Kích hoạt ⚡️
- Bấm **"Open chat"** hoặc gửi tin nhắn thử nghiệm trực tiếp đến Telegram Bot của các sếp để test nhanh luồng xử lý.
- Kiểm tra xem dữ liệu đã được đẩy chuẩn vào Google Sheets chưa.
- Gạt công tắc sang **Active** để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Báo cáo tổng kết tuần:** Kết hợp thêm node `Cron` để định kỳ tổng hợp số liệu calo từ Google Sheets và bắn tin nhắn báo cáo qua Telegram vào cuối tuần.
- **Mở rộng kho dữ liệu:** Như tác giả chia sẻ, đây là bản "light". Các sếp hoàn toàn có thể nâng cấp bằng cách tích hợp API tra cứu cơ sở dữ liệu thực phẩm (như USDA) để lấy thông số chính xác tuyệt đối cho từng gram nguyên liệu.
- **Cảnh báo sức khỏe:** Thêm node `If` để kiểm tra nếu tổng lượng calo trong ngày vượt quá mức cho phép, bot sẽ gửi lời nhắc nhở hài hước cho các sếp.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI và No-code vào đời sống hàng ngày giúp tiết kiệm thời gian và chăm sóc sức khỏe tốt hơn. Hãy cài đặt ngay và trải nghiệm sự tiện lợi mà trợ lý dinh dưỡng AI mang lại nhé các sếp!