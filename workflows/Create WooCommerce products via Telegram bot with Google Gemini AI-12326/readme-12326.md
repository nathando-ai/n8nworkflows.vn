---
title: "🚀 Tạo sản phẩm WooCommerce tự động qua Telegram Bot kết hợp Google Gemini AI"
description: "Hướng dẫn xây dựng hệ thống quản lý và tạo sản phẩm WooCommerce tự động hoàn toàn bằng Telegram Bot kết hợp trí tuệ nhân tạo Google Gemini AI trên nền tảng n8n."
slug: "tao-san-pham-woocommerce-qua-telegram-bot-google-gemini-ai"
tags: [n8n, automation, woocommerce, telegram, google-gemini, ai-agent, e-commerce]
keywords: [n8n workflow,woocommerce telegram bot,google gemini ai n8n,tao san pham woocommerce tu dong,ai copywriting e-commerce]
---

# 🚀 Tạo sản phẩm WooCommerce tự động qua Telegram Bot kết hợp Google Gemini AI

Việc thêm sản phẩm thủ công lên website thương mại điện tử WooCommerce tốn rất nhiều thời gian từ việc nghĩ mô tả, tối ưu SEO, tạo slug cho đến gắn hình ảnh. Bài toán này trở nên nhẹ nhàng hơn bao giờ hết với workflow tự động hóa n8n tích hợp trợ lý ảo Telegram Bot và Google Gemini AI. Sếp chỉ cần chat với bot, cung cấp thông tin thô, AI sẽ lo phần còn lại và đẩy thẳng lên WooCommerce!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giao diện hội thoại tiện lợi:** Thao tác tạo sản phẩm trực tiếp qua Telegram Bot mọi lúc, mọi nơi.
- **AI Copywriting thông minh:** Google Gemini tự động viết mô tả sản phẩm chuyên nghiệp, mô tả ngắn gọn và tối ưu URL Slug chuẩn SEO.
- **Tối ưu hình ảnh tự động:** AI phân tích hình ảnh sản phẩm để tạo Title và Alt Tag chuẩn SEO.
- **Quản lý trạng thái thông minh:** Hệ thống ghi nhớ bước hiện tại của người dùng, cho phép hủy (`/abort`) hoặc khởi động lại (`/start`) bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. **Telegram Bot Token:** Tạo bot và lấy token thông qua `@BotFather`.
2. **Google Gemini API Key:** Cấp quyền cho các node LangChain và AI Agent.
3. **WooCommerce REST API:** Chuẩn bị Consumer Key và Consumer Secret có quyền **Read/Write**.
4. **n8n Data Tables:** Cần tạo sẵn 2 Data Tables trên n8n:
   - **WooCommerce Product Manager:** Các trường gồm `chat_id`, `current_step`, `product_name`, `image_urls`, `features`, `regular_price`, `sale_price`.
   - **User_Images:** Các trường gồm `chat_id`, `file_id`, `image_url`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Mở n8n Editor, chọn **Import from File** hoặc dán trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger** & Các node `Send a text message...`: Kết nối với tài khoản Telegram Credentials của sếp và cấu hình Bot Token.
- **Google Gemini Chat Model** (các node `lmChatGoogleGemini`): Nhập Google Palm/Gemini API Key.
- **HTTP Request3** & **HTTP Request4** (WooCommerce API): Thay thế URL `https://your-wp-site/` bằng đường dẫn website WordPress thực tế của sếp và điền WooCommerce Credentials (Consumer Key & Consumer Secret).
- **Data Tables Nodes**: Liên kết chính xác các node như `Get User State`, `Upsert row(s)` với 2 Data Tables đã tạo ở phần chuẩn bị.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để kiểm tra dữ liệu mẫu từ Telegram.
- Gửi lệnh `/start` tới bot trên Telegram để bắt đầu tương tác.
- Sau khi kiểm thử thành công, bật trạng thái **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram nhóm:** Thêm node thông báo vào kênh nội bộ mỗi khi có sản phẩm mới được tạo thành công trên WooCommerce.
- **Tự động đăng bài mạng xã hội:** Kết hợp thêm node Facebook/Twitter sau khi sản phẩm được tạo để quảng cáo tự động.
- **Lưu log lỗi:** Sử dụng Error Trigger để bắt lỗi kết nối WooCommerce hoặc lỗi AI và gửi cảnh báo về Telegram cá nhân.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các chủ cửa hàng e-commerce tiết kiệm hàng chục giờ mỗi tuần cho khâu đăng sản phẩm. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình vận hành cửa hàng trực tuyến của các sếp!