---
title: "🚀 Quản lý cửa hàng WooCommerce tự động bằng AI Telegram Bot kết hợp OpenRouter"
description: "Hướng dẫn xây dựng trợ lý AI trên Telegram để quản lý đơn hàng, cập nhật sản phẩm WooCommerce, lưu log Google Sheets và gửi email tự động với n8n."
slug: "quan-ly-woocommerce-bang-ai-telegram-bot-openrouter"
tags: [n8n, automation, woocommerce, telegram, ai-agent, openrouter, google-sheets]
keywords: [n8n workflow, telegram bot woocommerce, quản lý woocommerce bằng ai, openrouter n8n, tự động hóa cửa hàng online]
---

# 🚀 Quản lý cửa hàng WooCommerce tự động bằng AI Telegram Bot kết hợp OpenRouter

Việc quản lý một cửa hàng WooCommerce đôi khi khiến các sếp "ngập mặt" với hàng loạt thao tác thủ công: tra cứu đơn hàng, cập nhật kho, kiểm tra sản phẩm, hay trả lời yêu cầu khách hàng qua email. Mở laptop liên tục chỉ để check vài thông số cơ bản thật sự tốn thời gian và kém linh hoạt.

Giải pháp là đây! Workflow n8n này sẽ biến ứng dụng **Telegram** thành một trợ lý AI thông minh, giúp các sếp quản lý toàn bộ hệ thống WooCommerce ngay trên điện thoại chỉ bằng cách nhắn tin trò chuyện tự nhiên mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Quản lý mọi lúc mọi nơi:** Tra cứu đơn hàng, kiểm tra và cập nhật sản phẩm trực tiếp qua Telegram.
- **Tự động hóa đa nền tảng:** Kết hợp mượt mà giữa WooCommerce, Google Sheets (lưu log dữ liệu) và Gmail (gửi báo cáo).
- **Trí tuệ nhân tạo linh hoạt:** Sử dụng OpenRouter Chat Model để hiểu chính xác ý định của người dùng và gọi đúng công cụ (tools) cần thiết.
- **Vận hành 24/7:** Bot luôn sẵn sàng nhận lệnh và phản hồi tức thì bất kể ngày đêm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Telegram Bot Token:** Tạo bot mới thông qua `@BotFather` trên Telegram.
- **OpenRouter API Key:** Tài khoản OpenRouter để sử dụng các mô hình ngôn ngữ lớn (LLM).
- **WooCommerce API Keys:** Consumer Key và Consumer Secret từ trang quản trị WordPress/WooCommerce của sếp.
- **Google Sheets & Gmail:** Tài khoản Google để cấu hình phân quyền OAuth2 lưu trữ database và gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp lên màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:
- **Telegram Trigger & Send a text message:** Kết nối tài khoản Telegram thông qua `telegramApi` bằng cách điền Bot Token từ BotFather. Node *Telegram Trigger* sẽ nhận tin nhắn từ sếp, còn node *Send a text message* sẽ gửi câu trả lời từ AI ngược lại cho sếp.
- **OpenRouter Chat Model:** Thêm credentials `openRouterApi` và chọn model yêu thích (ví dụ: Claude 3.5 Sonnet, GPT-4o-mini...). Node này đóng vai trò bộ não AI hiểu ngôn ngữ tự nhiên.
- **Simple Memory:** Giúp AI ghi nhớ ngữ cảnh cuộc trò chuyện (Buffer Window) để các sếp có thể chat liên tục mà không cần nhắc lại từ đầu.
- **Get orders, Get products, Update product:** Cấu hình WooCommerce credentials (`wooCommerceApi`) bằng URL website WordPress và API keys. Các node này hoạt động dưới dạng tool để AI tự động gọi khi cần lấy danh sách đơn hàng, sản phẩm hoặc cập nhật thông tin sản phẩm.
- **database (Google Sheets):** Kết nối tài khoản Google và trỏ tới file Google Sheets chuyên dụng dùng để lưu trữ log dữ liệu, đơn hàng hoặc báo cáo từ cửa hàng.
- **Send email (Gmail):** Kết nối OAuth2 của Gmail để trợ lý AI có thể tự động soạn và gửi email thông báo, báo cáo khi có lệnh từ sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhắn tin cho bot trên Telegram (ví dụ: *"Kiểm tra đơn hàng gần đây nhất"* hoặc *"Lấy danh sách sản phẩm"*).
- Khi thấy bot phản hồi chính xác, các sếp chỉ cần gạt nút **Active** ở góc trên bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh thông báo khác:** Tích hợp thêm node Slack hoặc Discord để nhận thông báo tổng hợp doanh thu hàng ngày.
- **Báo cáo định kỳ:** Kết hợp thêm node *Cron (Schedule Trigger)* để tự động yêu cầu AI quét đơn hàng mỗi tối và gửi email báo cáo doanh thu qua Gmail mà không cần nhắn lệnh thủ công.
- **Mở rộng kho dữ liệu:** Sử dụng Google Sheets để thống kê lịch sử tương tác của trợ lý AI phục vụ việc audit sau này.

### 📌 Kết luận
Workflow tích hợp AI Telegram Bot và WooCommerce này chính là mảnh ghép hoàn hảo giúp tự động hóa khâu quản lý vận hành cửa hàng online. Triển khai ngay hôm nay để tiết kiệm hàng giờ thao tác thủ công mỗi ngày, các sếp nhé!