---
title: "🚀 Tự động săn deal hời eBay với AI GPT-4, Decodo và Telegram"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu deal eBay, chấm điểm chất lượng bằng GPT-4 và gửi thông báo chớp nhoáng qua Telegram."
slug: "tu-dong-san-deal-ebay-gpt4-decodo-telegram"
tags: [n8n, automation, no-code, ai-agent, telegram, web-scraping]
keywords: [n8n workflow, san deal ebay, tu dong hoa, gpt-4, decodo, telegram notification]
---

# 🚀 Tự động săn deal hời eBay với AI GPT-4, Decodo và Telegram

Các sếp có bao giờ tốn hàng giờ lướt trang eBay Deals để tìm kiếm những món hàng giảm giá hời nhưng cuối cùng lại bỏ lỡ vì quá chậm chân? Việc theo dõi thủ công không chỉ tốn thời gian mà còn dễ bỏ sót các cơ hội vàng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, giải quyết triệt để bài toán trên. Workflow này sẽ tự động cào dữ liệu, lọc thông tin, dùng **AI (GPT-4)** để đánh giá chất lượng deal và bắn thẳng thông báo về **Telegram** ngay khi có sản phẩm "ngon bổ rẻ" xuất hiện. Hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần canh me thủ công, hệ thống tự động quét 24/7 theo lịch trình định sẵn.
- **Lọc nhiễu thông minh:** Kết hợp JavaScript và AI Agent để trích xuất dữ liệu gọn gàng, loại bỏ HTML rác, chấm điểm chất lượng và phân loại sản phẩm chuẩn xác.
- **Chỉ nhận deal chất lượng cao:** Sử dụng node **If** để thiết lập quy tắc ngầm (giá tiền, điểm số AI), đảm bảo chỉ những deal hời thực sự mới được đẩy về Telegram.
- **Thông báo chớp nhoáng:** Nhận ngay thông tin chi tiết sản phẩm kèm link mua hàng trực tiếp trên điện thoại qua Telegram Bot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Decodo:** Lấy Decodo API key để cào dữ liệu eBay vượt qua các cơ chế chống bot.
- **OpenAI API Key:** Sử dụng cho mô hình GPT-4 (hoặc OpenAI Chat Model) để chấm điểm deal.
- **Telegram Bot:** Tạo một Bot thông qua `@BotFather` và lấy **Bot Token** cùng **Chat ID** để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow vận hành trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Decodo Node:** Thêm **Decodo API credentials** vào node này. Các sếp cũng có thể tùy chỉnh lại URL trang eBay Deals mục tiêu nếu muốn săn các danh mục ngách khác.
- **Code in JavaScript & Code in JavaScript1:** Các node này giúp tinh gọn dữ liệu thô từ HTML thành cấu trúc JSON sạch sẽ trước khi gửi cho AI, giúp tiết kiệm token và tăng độ chính xác.
- **AI Agent & OpenAI Chat Model:** Thêm OpenAI API credentials và chọn mô hình (`gpt-4.1-nano` hoặc các bản GPT-4 phù hợp). AI sẽ đóng vai trò chuyên gia đánh giá mức độ hời của sản phẩm.
- **If Node:** Tinh chỉnh các quy tắc kinh doanh (giới hạn mức giá, điểm số tối thiểu từ AI). Chỉ những sản phẩm vượt qua điều kiện này mới được đi tiếp.
- **Send a text message (Telegram):** Thêm **Telegram Bot Token** và điền chính xác `chat_id` của các sếp (hoặc nhóm chat) để nhận tin nhắn cảnh báo.

#### 3. Kích hoạt ⚡️
- Bấm **‘Execute workflow’** thủ công qua node `When clicking ‘Execute workflow’` để test thử lần đầu.
- Kiểm tra kết quả trả về trên Telegram. Nếu mọi thứ OK, hãy gạt công tắc sang **Active** để hệ thống tự động chạy theo `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Telegram, các sếp có thể kết hợp thêm node Discord, Slack hoặc gửi Email hàng ngày tổng hợp top các deal tốt nhất.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Airtable vào sau bước If để lưu lại danh sách các deal đã gửi, tiện cho việc phân tích xu hướng giá sau này.
- **Mở rộng nguồn hàng:** Nhân bản luồng cào dữ liệu từ các sàn thương mại điện tử khác ngoài eBay (ví dụ: Amazon, Shopee, Lazada) để gom deal toàn diện hơn.

### 📌 Kết luận
Workflow săn deal eBay tự động với GPT-4 và Telegram là một "vũ khí" tuyệt vời cho cả nhu cầu mua sắm cá nhân lẫn các sếp muốn làm Affiliate Marketing tự động. Hãy cài đặt ngay hôm nay để không bỏ lỡ bất kỳ cơ hội kiếm lời hoặc sở hữu sản phẩm giá hời nào!