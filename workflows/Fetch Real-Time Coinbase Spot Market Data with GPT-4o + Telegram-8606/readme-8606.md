---
title: "🚀 Tự động hóa Tra cứu Giá & Phân tích Thị trường Coinbase Real-time với AI Agent và Telegram"
description: "Xây dựng hệ thống AI Agent thông minh tích hợp n8n, OpenAI GPT-4o-mini và Coinbase API để tra cứu giá spot, order book, nến klines và gửi báo cáo trực tiếp qua Telegram."
slug: "workflow-n8n-coinbase-ai-agent-telegram"
tags: [n8n, automation, crypto, openai, telegram, ai-agent]
keywords: [n8n workflow, coinbase spot market, ai agent telegram, openai gpt-4o, crypto automation, tu dong hoa giao dịch]
---

# 🚀 Xây dựng Hệ thống Tra cứu Giá & Phân tích Thị trường Coinbase Real-time bằng AI Agent và Telegram

Các nhà đầu tư và trader tiền mã hóa thường mất rất nhiều thời gian để theo dõi biểu đồ, kiểm tra sổ lệnh (order book), dữ liệu nến (OHLCV) và các thông số thị trường trên sàn Coinbase. Việc tra cứu thủ công qua nhiều tab trình duyệt vừa tốn thời gian, vừa dễ bỏ lỡ các cơ hội biến động giá chớp nhoáng.

Bài viết này sẽ hướng dẫn các sếp cách triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia Blockchain Don Jayamaha Jr thiết kế: **Hệ thống AI Agent tự động kết nối Coinbase Exchange REST API**, cho phép người dùng chat trực tiếp qua **Telegram** để lấy dữ liệu thị trường real-time, tính toán toán học, phân tích và trả về báo cáo định dạng HTML cực kỳ chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi tin nhắn qua Telegram bot để truy vấn ngay lập tức dữ liệu giá, order book, nến (candles) của bất kỳ cặp giao dịch nào trên Coinbase (ví dụ: `BTC-USD`, `ETH-USD`).
- **Trợ lý AI thông minh:** Sử dụng OpenAI GPT-4o-mini làm bộ não điều phối, gọi song song nhiều API công cụ (tools) khác nhau để tổng hợp dữ liệu chuẩn xác.
- **Báo cáo định dạng HTML sạch sẽ:** Kết quả trả về Telegram được format chuyên nghiệp, dễ đọc trên cả máy tính lẫn điện thoại.
- **Quản lý phân quyền & Bộ nhớ (Memory):** Tích hợp xác thực Telegram ID và ghi nhớ ngữ cảnh hội thoại (multi-turn interaction) giúp trải nghiệm mượt mà như chat với chuyên gia tài chính riêng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy trơn tru, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Telegram Bot Token** (tạo qua [@BotFather](https://t.me/BotFather)) để làm giao diện chat.
- **OpenAI API Key** (dùng cho model `gpt-4o-mini` điều phối agent và format dữ liệu).
- **Coinbase Exchange REST API**: Hoàn toàn công khai (Public endpoints), **không cần API Key hay xác thực** cho các dữ liệu thị trường spot.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON.
- Mở giao diện **n8n Editor UI**, chọn **Add workflow** -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 17 nodes được tổ chức xung quanh một **Coinbase AI Agent**. Các sếp cần cấu hình kỹ các điểm sau:

- **Telegram Trigger & Telegram Node:** 
  - Điền thông tin **Telegram API Credentials** của bot do các sếp tạo.
- **User Authentication (Replace Telegram ID) (Node Code):** 
  - Tại đây, hãy cấu hình danh sách `allowed_chat_ids` của các sếp hoặc đội ngũ để ngăn chặn người lạ spam bot.
- **OpenAI Chat Model:** 
  - Chọn credential OpenAI đã chuẩn bị. Đảm bảo thông số model được đặt là `gpt-4o-mini` để tối ưu chi phí và tốc độ phản hồi.
- **Các HTTP Request Tools (24h Stats1, Order Book Depth1, Price (Latest)1, Best Bid/Ask1, Klines (Candles)1, Average Price, Recent Trades1):** 
  - Các node này sử dụng endpoint công khai của Coinbase (ví dụ: `https://api.exchange.coinbase.com/products/{product_id}/ticker`). Không cần đổi credentials nhưng cần kiểm tra tính kết nối mạng của VPS.
- **Splits message is more than 4000 characters (Node Code):** 
  - Xử lý tự động chia nhỏ nội dung nếu báo cáo từ AI quá dài, tránh việc Telegram từ chối gửi tin nhắn do vượt quá giới hạn 4000 ký tự.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn mẫu qua Telegram bot (ví dụ: *"Cho tôi biết giá và độ sâu sổ lệnh của BTC-USD"*).
- Kiểm tra kết quả trả về trên Telegram và bật công tắc **Active** để chạy tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống hoàn hảo hơn, các sếp có thể mở rộng:
1. **Tích hợp thêm Cảnh báo giá (Price Alerts):** Kết hợp thêm Cron node để định kỳ check giá và chủ động bắn tin nhắn về Telegram khi coin vượt ngưỡng cắt lỗ/chốt lời.
2. **Lưu lịch sử chat vào Google Sheets / Database:** Ghi log các câu hỏi và dữ liệu truy vấn của user để phục vụ việc phân tích hành vi hoặc backtest chiến lược.
3. **Mở rộng kênh thông báo:** Nhân bản luồng Telegram sang **Discord Webhook** hoặc **Slack** để phục vụ group trading của team.

---

### 📌 Kết luận
Hệ thống **Coinbase Spot Market AI Agent với Telegram** là một minh chứng tuyệt vời cho sức mạnh của n8n kết hợp với AI LangChain Agents. Chỉ với vài bước cấu hình, các sếp đã sở hữu ngay một trợ lý crypto thông minh chạy tự động 24/7. Đừng chần chừ, hãy lên đồ và tự động hóa công việc trading của mình ngay hôm nay!