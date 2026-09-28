---
title: "🚀 Tự động gửi báo cáo thị trường Crypto hàng giờ từ Binance lên Telegram bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu giá BTC, ETH, SOL từ Binance, phân tích xu hướng và gửi bản tin thị trường qua Telegram mỗi giờ."
slug: "gui-bao-cao-crypto-hourly-binance-telegram-n8n"
tags: [n8n, automation, crypto, binance, telegram, finance]
keywords: [n8n workflow, crypto telegram bot, binance api n8n, tu dong hoa crypto, btc eth sol price bot]
---

# 🚀 Tự động gửi báo cáo thị trường Crypto hàng giờ từ Binance lên Telegram

Việc theo dõi biến động giá crypto liên tục để bắt sóng thị trường là một "nỗi đau" tốn rất nhiều thời gian của các trader. Nếu cứ F5 màn hình Binance mỗi giờ, chắc chắn các sếp sẽ mệt mỏi và dễ bỏ lỡ cơ hội. 

Giải pháp ở đây là gì? Hãy để **n8n** tự động hóa toàn bộ quy trình: cứ mỗi giờ, hệ thống sẽ tự động quét dữ liệu từ Binance, phân tích các chỉ số quan trọng (tăng/giảm, biên độ dao động, khối lượng giao dịch...) của các đồng coin top như BTC, ETH, SOL và gửi thẳng một bản tin cực kỳ trực quan vào nhóm Telegram của các sếp! Hoàn toàn tự động, không tốn một đồng phí API.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở sàn liên tục, thông tin tự động đổ về Telegram đúng giờ.
- **Dữ liệu phân tích chuyên sâu:** Báo cáo không chỉ có giá mà còn đo lường độ biến động (Volatility), biên độ Bid-Ask, lực đẩy (Momentum) và so sánh với trung bình thị trường.
- **Định dạng HTML đẹp mắt:** Tin nhắn được chia nhỏ thông minh, trình bày sắc nét, dễ đọc trên điện thoại.
- **Hoạt động 24/7:** Chạy ổn định tự động mỗi giờ, không bỏ lỡ bất kỳ biến động nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **Telegram** và một Bot Token được tạo sẵn qua `@BotFather`.
- Không cần tài khoản hay API Key của Binance vì workflow sử dụng public endpoint hoàn toàn miễn phí.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc sử dụng tính năng import file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác 2 node quan trọng sau:

- **Schedule Trigger:** Node này mặc định chạy **mỗi giờ** (vào phút thứ 5 của mỗi giờ với cron expression `5 * * * *`). Các sếp có thể giữ nguyên hoặc thay đổi lịch chạy tùy ý.
- **Binance 24h Price Change:** Node dùng HTTP Request gọi trực tiếp vào API public của Binance để lấy thông tin 24h của các cặp giao dịch **BTCUSDC**, **ETHUSDC**, **SOLUSDC**. Node này không yêu cầu API Key nên chỉ cần đảm bảo VPS có kết nối internet ổn định.
- **Analyze & Format Market Data (Function Node):** Node này xử lý logic tính toán các chỉ số gainers/losers, volume, momentum. Nếu các sếp muốn theo dõi thêm các đồng coin khác, hãy tìm dòng code sau trong Function node và thêm mã giao dịch (phải có hậu tố `USDC`):
  ```js
  const relevantSymbols = ['SOLUSDC', 'BTCUSDC', 'ETHUSDC'];
  ```
- **Send Telegram Message:** 
  - Tạo một Telegram Bot thông qua [@BotFather](https://t.me/BotFather).
  - Thêm bot vào nhóm chat Telegram hoặc chat cá nhân của các sếp.
  - Kết nối `Telegram API` credentials bằng Bot Token vừa nhận được.
  - Điền chính xác `chatId` của nhóm hoặc tài khoản cá nhân vào cấu hình của node.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test chạy thử thủ công và kiểm tra tin nhắn bắn về Telegram.
- Nếu mọi thứ hiển thị mượt mà, gạt công tắc sang **Active** để bot chính thức "lên sóng" tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng danh mục coin:** Thêm các coin hot khác như `XRPUSDC`, `DOGEUSDC` vào Function node để cập nhật danh mục đa dạng hơn.
- **Tích hợp cảnh báo giá (Alert):** Kết hợp thêm điều kiện trong Function node, nếu biên độ giá biến động quá lớn (> 5%), có thể kích hoạt nhánh gửi cảnh báo khẩn cấp riêng qua Telegram hoặc Slack.
- **Lưu trữ lịch sử:** Kết nối thêm một node **Google Sheets** hoặc **Supabase** để lưu lại dữ liệu giá mỗi giờ, phục vụ cho việc backtest hoặc vẽ biểu đồ sau này.

### 📌 Kết luận
Một workflow cực kỳ gọn nhẹ nhưng mang lại giá trị thực chiến rất cao cho các anh em chơi crypto. Hãy cài đặt ngay để biến chiếc Telegram của các sếp thành một trạm phát tin tức tài chính tự động 24/7! Chúc các sếp trade-bot thành công!