---
title: "🚀 Xây dựng Bot Telegram Tra cứu Dữ liệu Crypto Real-time từ Bybit với GPT-4.1-mini trên n8n"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n tích hợp AI Agent và Bybit Spot API để tra cứu giá, order book, nến kline real-time trực tiếp qua Telegram bot."
slug: "bot-telegram-crypto-bybit-gpt-n8n"
tags: [n8n, automation, crypto, telegram, ai-agent, openai]
keywords: [n8n workflow, bot telegram crypto, bybit spot api, ai agent n8n, tra cuu gia crypto tu dong]
---

# 🚀 Tự động hóa Bot Telegram tra cứu dữ liệu Crypto Real-time từ Bybit với GPT-4.1-mini

Các sếp trong làng trader hay Web3 thường đau đầu vì phải liên tục mở nhiều tab trình duyệt, check app sàn giao dịch để xem giá, sổ lệnh (order book) hay biểu đồ nến (kline). Việc tra cứu thủ công này vừa mất thời gian, vừa bỏ lỡ các biến động thị trường chớp nhoáng.

Bài toán này sẽ được giải quyết triệt để với **n8n workflow** cực kỳ mạnh mẽ do chuyên gia Don Jayamaha Jr xây dựng. Workflow này đóng vai trò như một trợ lý ảo trên Telegram, sử dụng **AI Agent (kết hợp OpenAI GPT-4.1-mini)** để điều phối các công cụ gọi trực tiếp vào **Bybit Spot API (v5)**, sau đó trả về thông tin thị trường real-time cực kỳ sạch sẽ, chuẩn định dạng HTML ngay trên Telegram của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu tốc độ cao:** Lấy giá, 24h stats, order book, kline của bất kỳ cặp coin Spot nào trên Bybit chỉ bằng một tin nhắn chat trên Telegram.
- **Bảo mật tuyệt đối:** Tích hợp tính năng xác thực User ID, chỉ cho phép các Telegram ID được định nghĩa sẵn mới có quyền truy cập bot.
- **Trình bày trực quan:** Kết quả trả về dạng HTML gọn gàng trên Telegram, tự động chia nhỏ tin nhắn nếu vượt quá ký tự cho phép.
- **Hoạt động 24/7:** Bot túc trực liên tục, hỗ trợ ghi nhớ ngữ cảnh (Memory Buffer) để các sếp tra cứu mượt mà nhiều lần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo bot thông qua [@BotFather](https://t.me/botfather) để lấy API Token.
- **OpenAI API Key:** Tài khoản OpenAI có quyền sử dụng model `gpt-4.1-mini` (hoặc GPT-4o-mini).
- **Bybit API:** Không bắt buộc API Key cho các public market data endpoints v5 Spot API, nhưng chuẩn bị sẵn sàng giúp hệ thống mượt mà hơn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp (Ctrl+V) vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần trọng yếu sau trong workflow:
- **Node `Telegram Trigger` & `Telegram`:** Chọn `credentials` là tài khoản **Telegram API** của các sếp (nhập Bot Token từ BotFather).
- **Node `OpenAI Chat Model`:** Chọn `credentials` là **OpenAI API** và đảm bảo thông số model được điền chính xác là `gpt-4.1-mini`.
- **Node `User Authentication (Replace Telegram ID)`:** Đây là node code quan trọng để bảo mật. Các sếp cần thay thế danh sách Telegram ID mẫu bằng **Telegram Chat ID thực tế** của bản thân để cấp quyền sử dụng bot.
- **Các HTTP Request Tools (24h Stats1, Order Book Depth1, Price (Latest)1, Best Bid/Ask1, Klines (Candles)1, Ticker, Recent Trades1):** Các node này kết nối trực tiếp với Bybit Spot REST API (v5) như `/v5/market/tickers`, `/v5/market/orderbook`, `/v5/market/kline` theo đúng các tham số đã được chú thích sẵn trên canvas.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn mã coin (ví dụ: `BTCUSDT` hoặc `Cho toi xem gia BTC`) vào bot Telegram của các sếp để test.
- Kiểm tra kết quả trả về. Nếu mọi thứ xanh mướt, hãy bật **Active** để chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm cảnh báo giá:** Kết hợp thêm node cảnh báo qua Slack hoặc gửi email khi giá vượt ngưỡng mong muốn.
- **Lưu lịch sử tra cứu:** Nối thêm node Google Sheets hoặc Database để lưu trữ lại các câu lệnh và dữ liệu tra cứu phục vụ việc phân tích hành vi.
- **Mở rộng đa sàn:** Tích hợp thêm các tool gọi API của Binance hoặc OKX vào chung AI Agent để so sánh giá chéo (arbitrage).

### 📌 Kết luận
Với workflow n8n kết hợp AI Agent và Bybit API này, các sếp đã sở hữu ngay một "terminal" crypto thu nhỏ ngay trong ứng dụng Telegram quen thuộc. Triển khai ngay hôm nay để tối ưu hóa tốc độ nắm bắt thông tin thị trường của các sếp!