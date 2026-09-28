---
title: "🚀 Tự động hóa tín hiệu giao dịch chứng khoán với Gemini 2.5 Pro và TwelveData qua Telegram Bot"
description: "Xây dựng trợ lý phân tích kỹ thuật chứng khoán tự động 24/7 sử dụng n8n, AI Gemini và TwelveData API, gửi tín hiệu mua/bán trực tiếp qua Telegram."
slug: "tu-dong-hoa-tin-hieu-chung-khoan-gemini-twelvedata-telegram"
tags: [n8n, automation, ai, gemini, twelvedata, telegram, trading]
keywords: [n8n workflow, tín hiệu chứng khoán, gemini ai, twelvedata api, telegram bot trading, tự động hóa tài chính]
---

# 🚀 Tự động hóa tín hiệu giao dịch chứng khoán với Gemini 2.5 Pro & TwelveData qua Telegram Bot

Việc theo dõi biểu đồ kỹ thuật, tính toán các chỉ báo phức tạp (EMA, RSI, ATR, Support/Resistance) và đưa ra quyết định mua bán chuẩn xác là một thử thách lớn tốn rất nhiều thời gian đối với các nhà đầu tư. Nếu làm thủ công, các sếp rất dễ bỏ lỡ cơ hội vàng khi thị trường biến động mạnh.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: thu thập dữ liệu giá real-time, tính toán các chỉ báo kỹ thuật từ **TwelveData**, phân tích chuyên sâu bằng **Google Gemini AI**, và trả kết quả kèm biểu đồ trực quan thẳng về **Telegram Bot** chỉ trong tích tắc. Không cần code phức tạp, tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tín hiệu chớp nhoáng:** Nhận nhận định thị trường, điểm mua/bán chi tiết ngay trên Telegram bất cứ lúc nào chat với Bot.
- **Phân tích chuẩn AI:** Kết hợp sức mạnh của Gemini AI cùng các chỉ báo kỹ thuật hàng đầu (EMA, RSI, ATR, OHLC, Hỗ trợ/Kháng cự).
- **Biểu đồ trực quan:** Tự động tải và gửi chart 1D sắc nét đi kèm báo cáo phân tích.
- **Hoạt động không nghỉ:** Trợ lý ảo hoạt động 24/7, giúp tiết kiệm hàng giờ soi chart mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted).
- **Telegram Bot Token:** Tạo một bot mới thông qua `@BotFather` trên Telegram.
- **TwelveData API Key:** Tài khoản miễn phí hoặc trả phí tại [TwelveData](https://twelvedata.com/) để lấy dữ liệu chứng khoán.
- **Google Gemini API Key:** Key truy cập mô hình AI Google Gemini.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp bằng cách chọn **New workflow** -> Dán (Ctrl+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Telegram Trigger**: Kết nối với tài khoản Telegram Credentials của các sếp và lắng nghe tin nhắn từ người dùng (nhập mã chứng khoán).
- **Add TwelveData API Key** (Node loại `set`): Điền TwelveData API Key của các sếp vào biến cấu hình để các node gọi dữ liệu phía sau sử dụng.
- **Google Gemini Chat Model** & **Structured Output Parser**: Cung cấp Gemini API Key và cấu hình model (ví dụ: Gemini 2.5 Pro) để AI trả về cấu trúc dữ liệu JSON chuẩn xác cho tín hiệu giao dịch.
- **Send Final Analysis** & **Send 1D Chart** (Node loại `telegram`): Chọn đúng Chat ID của Telegram nơi bot sẽ gửi tin nhắn kết quả phân tích và hình ảnh biểu đồ.
- Các node gọi API giá như `Real Time Price`, `EMA 50 - 1D`, `EMA 200 -1D`, `RSI -1D`, `ATR -1D`, `OHLC -1Day`, `Get Chart URL`, `Download Chart`: Đảm bảo URL endpoint của TwelveData đã điền đúng API key và định dạng mã cổ phiếu (ticker).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một mã cổ phiếu (ví dụ: `AAPL`, `TSLA`) qua Telegram Bot để test run dữ liệu mẫu.
- Kiểm tra xem kết quả và biểu đồ có trả về Telegram thành công hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Tích hợp thêm các chỉ báo Volume Profile, MACD hoặc mở rộng sang thị trường Crypto, Forex thông qua TwelveData.
- **Lưu lịch sử giao dịch:** Thêm node Google Sheets hoặc Airtable để lưu lại toàn bộ các mã cổ phiếu mà người dùng đã tra cứu qua Telegram Bot.
- **Cảnh báo tự động (Alerts):** Thay vì đợi người dùng chat, có thể dùng Cron node để quét danh sách cổ phiếu yêu thích định kỳ mỗi sáng và chủ động bắn tin cảnh báo khi có tín hiệu mua/bán đẹp.

### 📌 Kết luận
Workflow tích hợp AI và dữ liệu tài chính này là một trợ thủ đắc lực không thể thiếu cho các nhà đầu tư hiện đại. Chỉ với vài bước cài đặt đơn giản trên n8n, các sếp đã sở hữu ngay một hệ thống phân tích kỹ thuật chuyên nghiệp ngay trong tầm tay. Áp dụng ngay thôi nào!