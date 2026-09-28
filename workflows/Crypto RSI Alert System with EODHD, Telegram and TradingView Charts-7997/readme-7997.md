---
title: "🚀 Xây Dựng Hệ Thống Cảnh Báo RSI Crypto Tự Động Với EODHD, Telegram và Biểu Đồ TradingView"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n tự động quét thị trường crypto, tính toán chỉ báo RSI và gửi cảnh báo điểm mua bán qua Telegram kèm link biểu đồ TradingView."
slug: "he-thong-canh-bao-rsi-crypto-n8n-eodhd-telegram"
tags: [n8n, automation, crypto, trading, telegram, eodhd, tradingview]
keywords: [n8n workflow, cảnh báo rsi crypto, bot telegram trading, eodhd api, tự động hóa giao dịch crypto]
---

# 🚀 Tự Động Hóa Hệ Thống Cảnh Báo RSI Crypto với n8n, EODHD và Telegram

Các sếp làm trader hay đầu tư crypto chắc chắn đã từng bỏ lỡ những thời điểm giá quá mua (overbought) hoặc quá bán (oversold) chỉ vì không thể canh màn hình 24/7. Việc ngồi soi chart thủ công cho hàng loạt đồng coin vừa tốn thời gian, vừa dễ bỏ lỡ cơ hội vàng.

Workflow n8n này sẽ giải quyết triệt để bài toán đó bằng cách tự động hóa 100%: định kỳ quét danh sách Watchlist, lấy dữ liệu nến 1 giờ từ EODHD, tính toán chỉ số RSI(14) theo thuật toán chuẩn của Wilder, và ngay lập tức bắn thông báo sắc nét về Telegram kèm nút bấm xem trực tiếp biểu đồ trên TradingView ngay khi có tín hiệu xuyên thủng mức 30 hoặc 70!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 24/7:** Hệ thống liên tục theo dõi thị trường theo khung giờ cố định mà không cần sự can thiệp thủ công.
- **Chính xác & Kịp thời:** Tính toán chuẩn xác chỉ báo Wilder's RSI(14) và phát hiện ngay lập tức các điểm giao cắt (crossover) ngưỡng 30/70.
- **Trải nghiệm tối ưu:** Tin nhắn gửi về Telegram định dạng HTML đẹp mắt, đi kèm nút bấm trực tiếp mở nhanh biểu đồ TradingView (BINANCE/USD).
- **Tiết kiệm chi phí:** Tận dụng các API mạnh mẽ (EODHD, Telegram Bot) với chi phí tối ưu hoặc hoàn toàn miễn phí ở mức cơ bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản EODHD:** Lấy API Token để gọi dữ liệu nến lịch sử/intraday (được cấu hình qua biến môi trường `EODHD_TOKEN`).
- **Telegram Bot:** Tạo bot thông qua `@BotFather` và lấy Token, cùng với Chat ID nơi nhận thông báo (`TELEGRAM_CHAT_ID`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã nguồn JSON của workflow, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp (`Add nodes/workflows` -> `Import from Clipboard`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes cốt lõi được sắp xếp khoa học. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Edit Fields (watchlist):** Node này định nghĩa danh sách các đồng coin cần theo dõi (`symbol`). Đảm bảo kiểu dữ liệu đầu ra là **Array (String[])**, không phải dạng String đơn lẻ. 
  *Ví dụ mẫu:* `{ symbol: ["BTC-USD.CC","ETH-USD.CC","SOL-USD.CC"] }`
- **Split Out & Loop Over Items:** Xử lý tách mảng thành từng item riêng biệt và dùng vòng lặp (`splitInBatches`) để xử lý từng đồng coin một, tránh việc trộn lẫn dữ liệu nến giữa các mã (BTC, ETH, SOL).
- **HTTP Request (EODHD intraday 1h):** Node gọi API lấy dữ liệu OHLCV khung 1 giờ. Biến xác thực token được lấy từ biến môi trường `EODHD_TOKEN` để bảo mật thông tin.
- **Code (RSI + message):** Node Javascript thực hiện sắp xếp nến, tính toán chỉ số RSI(14) theo phương pháp của Wilder và kiểm tra điều kiện cắt ngưỡng 30/70. 
  *Mẹo:* Khi kiểm thử (testing), các sếp có thể đặt biến `FORCE_ALERT = true` trong code để ép gửi thông báo test, sau đó nhớ đổi lại thành `false`.
- **Send a text message (Telegram):** Cấu hình Credentials Telegram Bot. Chọn chế độ Parse Mode là **HTML**, nội dung tin nhắn trỏ tới `{{$json.alertTextHtml}}` và thêm nút bấm liên kết trực tiếp biểu đồ TradingView (`{{$json.tradingViewUrl}}`). Chat ID được cấu hình qua biến môi trường `TELEGRAM_CHAT_ID`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** thủ công ở node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế xem tin nhắn có bắn về Telegram chuẩn chỉnh chưa.
- Sau khi test thành công, thay thế hoặc bổ sung thêm Trigger theo lịch trình (Schedule Trigger) nếu muốn, sau đó bật **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa khung thời gian:** Các sếp có thể nhân bản workflow hoặc chỉnh sửa node HTTP Request để quét thêm các khung thời gian ngắn hơn như 15m hoặc dài hơn như 4h.
- **Mở rộng kênh nhận tin:** Kết hợp thêm node Discord, Slack hoặc Google Sheets để lưu lại lịch sử các lần phát tín hiệu RSI nhằm phục vụ việc backtest chiến lược sau này.
- **Quản lý Watchlist linh động:** Thay vìhardcode danh sách coin trong node Edit Fields, các sếp có thể kết nối node **Google Sheets** hoặc **Airtable** để đọc danh sách coin động từ file quản lý cá nhân.

### 📌 Kết luận
Với hệ thống cảnh báo RSI tự động này, các sếp không chỉ tiết kiệm được hàng giờ đồng hồ soi chart mỗi ngày mà còn chủ động nắm bắt các điểm đảo chiều của thị trường crypto một cách nhanh chóng nhất. Hãy cài đặt ngay và tối ưu hóa quy trình đầu tư của mình nhé!