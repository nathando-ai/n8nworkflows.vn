---
title: "🚀 Tự động hóa đăng sản phẩm WooCommerce & bài viết WordPress từ link sản phẩm qua Telegram & BrowserAct"
description: "Hướng dẫn xây dựng workflow n8n tự động cào thông tin sản phẩm bằng BrowserAct từ Telegram, tạo sản phẩm WooCommerce và bài viết chuẩn SEO trên WordPress."
slug: "tao-san-pham-woocommerce-wordpress-tu-telegram-browseract"
tags: [n8n, automation, no-code, woocommerce, wordpress, telegram, browseract, ai]
keywords: [n8n workflow, tự động hóa woocommerce, đăng bài wordpress tự động, telegram bot n8n, browseract web scraping]
---

# 🚀 Tự động tạo sản phẩm WooCommerce & bài viết WordPress từ Link sản phẩm qua Telegram

Các sếp có đang mệt mỏi với việc copy-paste thông tin sản phẩm từ các trang thương mại điện tử (như Amazon, AliExpress...) để đăng lên website WooCommerce và viết bài review trên WordPress không? Công việc thủ công này ngốn rất nhiều thời gian, từ việc tải hình ảnh, viết mô tả chuẩn SEO cho đến việc định dạng lại bài viết.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ mạnh mẽ, giải quyết triệt để vấn đề trên. Chỉ với một tin nhắn chứa link sản phẩm gửi qua **Telegram**, hệ thống sẽ tự động hóa từ A-Z: cào dữ liệu, AI viết nội dung bán hàng, đẩy lên **WooCommerce** và xuất bản bài viết review trên **WordPress**. 100% không cần code tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay gián đoạn kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến một quy trình thủ công kéo dài 30 phút thành một câu lệnh chưa đầy 1 phút qua Telegram.
- **Tự động hóa thông minh:** AI (OpenRouter & Gemini) tự động viết lại nội dung mô tả sản phẩm hấp dẫn và bài blog chuẩn SEO.
- **Đồng bộ đa nền tảng:** Vừa tạo sản phẩm trên kho WooCommerce, vừa xuất bản bài viết thu hút khách hàng trên WordPress cùng lúc.
- **Hoạt động 24/7:** Bot Telegram sẵn sàng nhận link và xử lý bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram.
- **BrowserAct Account & API Key:** Nền tảng web scraping thông minh (Cần chuẩn bị sẵn template **WordPress & WooCommerce Product Management** trong tài khoản BrowserAct).
- **OpenRouter API Key:** Để sử dụng các mô hình AI mạnh mẽ (`gpt-4.1`).
- **Google Gemini (PaLM) API Key:** Dùng cho các agent kiểm tra và xử lý dữ liệu.
- **WordPress & WooCommerce:** Website WordPress đã cài đặt plugin WooCommerce và bật REST API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình (hoặc import file JSON được cung cấp từ nguồn gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp nhớ cấu hình chính xác các node sau:
- **User Sends Message to Bot & Telegram nodes:** Kết nối `credentials` bằng Telegram API Token của bot mà các sếp đã tạo.
- **Extract Product Details (BrowserAct):** Điền API Key của BrowserAct và trỏ tới Template ID tương ứng cho việc cào dữ liệu sản phẩm.
- **Generate Product & Generate Article (OpenRouter & Google Gemini):** Thêm API Key của OpenRouter và Google Gemini, chọn các model phù hợp như `openai/gpt-4.1` và `google/gemini-2.5-pro` để AI có văn phong mượt mà nhất.
- **Create a product & Update Product Image (WooCommerce):** Nhập URL website WordPress và WooCommerce Consumer Key / Consumer Secret để n8n có quyền tạo sản phẩm và cập nhật gallery ảnh.
- **Create WordPress Post (WordPress):** Điền thông tin đăng nhập WordPress (Application Passwords được khuyến nghị để bảo mật) để bot tự động xuất bản bài viết.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một link sản phẩm bất kỳ vào bot Telegram của các sếp để test xem dữ liệu có đổ về chuẩn không.
- Nếu mọi thứ xanh đèn và hoạt động trơn tru, hãy bật công tắc **Active** lên để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram Notification:** Thêm một node Telegram hoặc Slack ở cuối workflow để bot gửi thông báo về máy cá nhân ngay khi sản phẩm và bài viết đã lên sàn thành công.
- **Lưu log vào Google Sheets:** Thêm node Google Sheets để lưu lại lịch sử các link đã cào và tạo sản phẩm, tiện cho việc kiểm kê và quản lý sau này.
- **AI lọc ngôn ngữ:** Tinh chỉnh prompt trong các AI Agent để tự động dịch sản phẩm sang tiếng Việt nếu các sếp cào hàng từ các trang nước ngoài (Amazon, Taobao, AliExpress...).

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho anh em làm dropshipping, affiliate marketing hoặc quản trị website thương mại điện tử. Hãy áp dụng ngay để tối ưu hóa thời gian vận hành và bứt phá doanh thu cùng tự động hóa n8n nhé các sếp!