---
title: "🚀 Tự động tạo quảng cáo sản phẩm chuyên nghiệp qua Telegram với Google Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Telegram và Google Gemini AI để biến ảnh sản phẩm thô thành banner quảng cáo đẳng cấp thương hiệu chỉ trong vài giây."
slug: "tao-quang-cao-san-pham-tu-dong-qua-telegram-voi-gemini-ai"
tags: [n8n, automation, google-gemini, telegram, ai-content-creation, image-generation]
keywords: [n8n workflow, tao quang cao tu dong, telegram bot ai, google gemini ai, xu ly anh ai n8n]
---

# 🚀 Tự động tạo quảng cáo sản phẩm chuyên nghiệp qua Telegram với Google Gemini AI

Các sếp kinh doanh online có bao giờ cảm thấy mệt mỏi vì tốn hàng giờ thiết kế banner quảng cáo trên Canva, thuê Designer chỉnh sửa ảnh sản phẩm, hay chật vật nghĩ caption hút khách? Việc làm thủ công này vừa tốn kém chi phí, vừa chậm trễ tiến độ chạy chiến dịch.

Giải pháp ở đây là gì? Hãy để n8n tự động hóa toàn bộ quy trình này! Với workflow **"Generate Professional Product Advertisements with Google Gemini AI via Telegram"**, các sếp chỉ cần gửi một bức ảnh sản phẩm kèm chú thích thô qua Telegram bot, hệ thống sẽ tự động phân tích và trả về một banner quảng cáo sắc nét, chuyên nghiệp chuẩn "luxury-brand" ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giữ nguyên 100% sản phẩm gốc:** AI chỉ làm đẹp background, bố cục và không làm biến dạng sản phẩm của các sếp.
- **Tối ưu hóa nội dung:** Tự động trích xuất và tối ưu caption text từ tin nhắn Telegram của người dùng.
- **Chất lượng cao cấp:** Tạo ra các hình ảnh chuẩn kích thước, bố cục chuyên nghiệp sẵn sàng đăng tải lên Instagram, Pinterest hoặc Facebook.
- **Hoạt động 24/7 tự động:** Bot Telegram luôn sẵn sàng nhận yêu cầu mọi lúc mọi nơi mà không cần nhân sự trực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Gemini API Key** (Được kích hoạt Generative Language API).
- **API Key dịch vụ tạo ảnh nâng cao** (Nano Banana Pro hoặc tương thích với HTTP Request node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node quan trọng sau:

- **Telegram Trigger**: Kết nối với Telegram Credentials của sếp để bot có thể lắng nghe tin nhắn và hình ảnh gửi vào từ chat.
- **Download Image File**: Node này dùng để tải file ảnh gốc từ Telegram về bộ nhớ tạm của n8n xử lý.
- **Image to Base65 (extractFromFile)**: Chuyển đổi định dạng file ảnh sang chuỗi Base64 để các mô hình AI có thể đọc và phân tích dễ dàng.
- **AI Design Analysis (googleGemini)**: Điền Gemini API Key, cấu hình prompt để AI nhận diện sản phẩm, phân tích bố cục và đưa ra chỉ dẫn thiết kế (design instructions) cực kỳ chi tiết.
- **Prepare API Payload (code)**: Node JavaScript tùy chỉnh giúp gom nhóm hình ảnh gốc và kết quả phân tích từ Gemini thành cấu trúc JSON chuẩn để gửi sang API tạo ảnh.
- **Generate Enhanced Image (httpRequest)**: Gọi API (Nano Banana Pro hoặc tương tự) để tiến hành tái tạo và nâng cấp hình ảnh quảng cáo.
- **Convert Base64 to Image / Send Image**: Chuyển đổi phản hồi dạng Base64 của ảnh mới về dạng binary và gửi trả kết quả trực tiếp cho người dùng qua Telegram.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một bức ảnh sản phẩm kèm chú thích vào Telegram Bot của các sếp để kiểm tra kết quả.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ lịch sử:** Kết nối thêm một Google Sheets hoặc Airtable node để lưu lại thông tin ảnh gốc, prompt của AI và ảnh thành phẩm phục vụ cho việc quản lý chiến dịch marketing.
- **Tích hợp đa kênh:** Thay vì chỉ nhận/gửi qua Telegram, các sếp có thể mở rộng thêm nhánh kết nối với Slack, Zalo OA hoặc Microsoft Teams.
- **Đa dạng phong cách:** Tùy chỉnh system prompt trong Google Gemini node để ép AI tạo ra các phong cách thiết kế khác nhau (tối giản, sang trọng, trẻ trung năng động...).

### 📌 Kết luận
Tự động hóa quy trình sáng tạo nội dung và thiết kế quảng cáo chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và Google Gemini AI. Hãy thiết lập ngay con bot Telegram này để tối ưu hóa hiệu suất làm việc và bứt phá doanh số cùng các chiến dịch marketing chuyên nghiệp ngay hôm nay!