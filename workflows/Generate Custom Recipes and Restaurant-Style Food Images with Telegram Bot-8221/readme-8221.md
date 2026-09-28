---
title: "🚀 Tự động tạo công thức nấu ăn & hình ảnh món ăn chuẩn nhà hàng với Telegram Bot và n8n"
description: "Xây dựng AI Chef Bot trên Telegram sử dụng n8n, OpenRouter (GPT-4o-mini) để tự động trả về công thức nấu ăn chi tiết và hình ảnh món ăn siêu thực chỉ với một tin nhắn."
slug: "tao-cong-thuc-nau-an-va-anh-mon-an-telegram-bot-n8n"
tags: [n8n, automation, telegram-bot, ai-agent, openrouter, multimodal-ai]
keywords: [n8n workflow, telegram bot ai, tao cong thuc nau an ai, ai chef bot, openrouter n8n, tao anh mon an ai]
---

# 🚀 Tự động tạo công thức nấu ăn & hình ảnh món ăn chuẩn nhà hàng với Telegram Bot

Các sếp có bao giờ nghĩ đến việc sở hữu một đầu bếp AI riêng ngay trên Telegram? Thay vì phải loay hoay tìm kiếm công thức trên mạng rồi tự tưởng tượng ra thành phẩm, giờ đây chỉ cần nhắn tên một món ăn, bot sẽ lập tức gửi về công thức chi tiết từ A-Z kèm theo hình ảnh món ăn được bày trí đẹp mắt như nhà hàng 5 sao.

Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình tích hợp Multimodal AI (AI đa phương thức) kết hợp giữa OpenRouter và Telegram Bot, hoạt động 24/7 mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7**: Bot Telegram tự động tiếp nhận tên món ăn và trả kết quả chỉ trong vài giây.
- **Công thức chuẩn xác, chi tiết**: Sử dụng AI Agent kết hợp mô hình ngôn ngữ mạnh mẽ (`gpt-4o-mini` qua OpenRouter) để viết công thức nấu ăn đầy đủ nguyên liệu và cách làm.
- **Hình ảnh món ăn siêu thực**: Tự động sinh ảnh món ăn với phong cách bày trí chuyên nghiệp (Restaurant-Style Plating) và gửi trực tiếp dưới dạng hình ảnh trên Telegram.
- **Trải nghiệm mượt mà**: Lưu trữ ngữ cảnh cuộc trò chuyện với `Window Buffer Memory`, giúp bot hiểu rõ các yêu cầu trao đổi tiếp theo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token**: Tạo bot thông qua `@BotFather` trên Telegram để lấy API Token.
- **OpenRouter API Key**: Tài khoản OpenRouter để sử dụng các mô hình AI (`gpt-4o-mini` hoặc các mô hình hỗ trợ sinh ảnh/văn bản tương ứng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy đoạn mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình các credentials và tham số quan trọng sau:

- **Telegram Trigger**: 
  - Tạo hoặc chọn **Telegram API Credentials** bằng cách nhập Bot Token lấy từ `@BotFather`.
  - Node này sẽ đóng vai trò lắng nghe tin nhắn từ người dùng gửi tới bot.
- **OpenRouter Chat Model & OpenRouter Chat Model1**: 
  - Tạo **OpenRouter API Credentials** bằng cách điền API Key của sếp.
  - Cấu hình model (mặc định là `openai/gpt-4o-mini` hoặc tùy chỉnh theo nhu cầu).
- **AI Recipe & Restaurant-Style Plating prompt**: 
  - Các AI Agent này chịu trách nhiệm xử lý logic tạo văn bản (công thức) và tạo prompt/hình ảnh món ăn.
- **Nano 🍌 (HTTP Request) & Convert to File**: 
  - Xử lý việc gọi API tạo hình ảnh hoặc chuyển đổi dữ liệu trả về thành tệp tin nhị phân (`toBinary`).
- **Send a text message & Send a photo message**: 
  - Đảm bảo các node Telegram này đã được liên kết đúng với Telegram API Credentials để gửi kết quả dạng chữ và ảnh về đúng chat ID của người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm gửi một tin nhắn mẫu (ví dụ: *"Polpette di pesce"*) tới bot Telegram của sếp.
- Sau khi kiểm tra mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang chế độ **Active** để bot chính thức "lên sóng".

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ**: Kết nối thêm node **Google Sheets** hoặc **Postgres** để lưu lại lịch sử các món ăn mà khách hàng/người dùng đã tra cứu.
- **Tích hợp đa kênh**: Nhân bản nhánh Telegram Trigger thành **Slack Trigger** hoặc **Facebook Messenger Trigger** để phục vụ khách hàng trên nhiều nền tảng khác nhau.
- **Cá nhân hóa thực đơn**: Tinh chỉnh system prompt trong AI Agent để tư vấn công thức phù hợp với chế độ ăn kiêng (Eat clean, Keto, Vegan...) dựa trên yêu cầu người dùng.

### 📌 Kết luận
Workflow **AI Chef Bot** là một minh họa tuyệt vời cho sức mạnh của AI đa phương thức kết hợp cùng tự động hóa no-code trên n8n. Triển khai ngay hôm nay để mang lại trải nghiệm tương tác cực kỳ ấn tượng cho cộng đồng hoặc ứng dụng vào mô hình kinh doanh ẩm thực của các sếp!