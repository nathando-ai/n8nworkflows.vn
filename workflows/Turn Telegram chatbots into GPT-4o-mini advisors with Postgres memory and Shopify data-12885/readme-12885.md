---
title: "🤖 Tự động hóa Chatbot Telegram với trí nhớ Postgres và dữ liệu Shopify"
description: "Hướng dẫn chi tiết cách tạo chatbot Telegram thông minh với trí nhớ dài hạn, tích hợp dữ liệu Shopify và sử dụng GPT-4o-mini để tư vấn khách hàng"
slug: "tao-chatbot-telegram-voi-tri-nho-postgres-va-du-lieu-shopify"
tags: [n8n, automation, no-code, chatbot, telegram, shopify, postgres, ai]
keywords: [n8n workflow, tự động hóa, chatbot telegram, trí nhớ chatbot, dữ liệu shopify, postgres, gpt-4o-mini]
---

# 🤖 Tự động hóa Chatbot Telegram với trí nhớ Postgres và dữ liệu Shopify

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý nhiều cuộc trò chuyện khách hàng trên Telegram mà không có trí nhớ hoặc dữ liệu sản phẩm cập nhật. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình tư vấn khách hàng qua Telegram
- Ghi nhớ lịch sử trò chuyện của từng khách hàng riêng biệt
- Cung cấp thông tin sản phẩm Shopify cập nhật nhất
- Tiết kiệm thời gian và nhân lực cho đội ngũ chăm sóc khách hàng
- Tạo trải nghiệm mua sắm cá nhân hóa cho khách hàng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token
- API key OpenAI (để sử dụng GPT-4o-mini)
- Cửa hàng Shopify và thông tin xác thực API
- Cơ sở dữ liệu Postgres để lưu trữ lịch sử trò chuyện
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12885)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** (Node 2):
   - Cấu hình credentials "telegramApi" với bot token của bạn
   - Đảm bảo bot đã được thêm vào nhóm hoặc kênh Telegram cần quản lý

2. **OpenAI Chat Model** (Node 4):
   - Cấu hình credentials "openAiApi" với API key của bạn
   - Đảm bảo bạn có quyền truy cập vào model GPT-4o-mini

3. **Get many products** (Node 6):
   - Cấu hình credentials "shopifyOAuth2Api" với thông tin xác thực Shopify
   - Đảm bảo ứng dụng Shopify đã được cấp quyền truy cập vào sản phẩm

4. **Postgres Chat Memory** (Node 7):
   - Cấu hình credentials "postgres" với thông tin kết nối cơ sở dữ liệu
   - Tạo bảng để lưu trữ lịch sử trò chuyện nếu chưa có

5. **Code in JavaScript** (Node 1 và Node 8):
   - Kiểm tra và điều chỉnh các hàm xử lý dữ liệu nếu cần
   - Đảm bảo đầu ra của node 8 là JSON hợp lệ để Telegram có thể xử lý

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu bằng cách gửi một tin nhắn thử nghiệm qua Telegram
2. Kiểm tra các node để đảm bảo dữ liệu được truyền đúng
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh hệ thống thông báo**: Chỉnh sửa thông điệp hệ thống trong node OpenAI Chat Model để phù hợp với giọng điệu và ngành nghề của bạn
2. **Kết nối với nhiều nguồn dữ liệu**: Thay thế hoặc bổ sung node Shopify với các nguồn dữ liệu khác như dữ liệu khách hàng, đơn hàng...
3. **Cấu hình kích thước cửa sổ nhớ**: Điều chỉnh tham số trong node Postgres Chat Memory để phù hợp với nhu cầu lưu trữ lịch sử trò chuyện
4. **Tích hợp với các kênh khác**: Kết nối với Slack, Email hoặc các nền tảng khác để thông báo khi có khách hàng cần hỗ trợ

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa chatbot Telegram với trí nhớ dài hạn và dữ liệu thời gian thực từ Shopify. Bằng cách áp dụng workflow này, các sếp có thể nâng cao trải nghiệm khách hàng, giảm thiểu thời gian phản hồi và tối ưu hóa quy trình chăm sóc khách hàng một cách hiệu quả.