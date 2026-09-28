---
title: "🚀 Cảnh báo giá Crypto giảm sâu (Dip) tự động qua Telegram, Slack và SMS"
description: "Tự động theo dõi giá Bitcoin và Ethereum mỗi 30 phút, phát hiện nhịp giảm mạnh và gửi cảnh báo tức thì qua Telegram, Slack, Twilio giúp bạn không bỏ lỡ cơ hội 'bắt đáy'."
slug: "canh-bao-gia-crypto-giam-sau-telegram-slack-sms"
tags: [n8n, automation, crypto, trading, telegram, slack, twilio]
keywords: [n8n workflow, crypto dip alert, bot canh bao gia bitcoin, tu dong hoa trading, coingecko n8n]
---

# 🚀 Cảnh báo giá Crypto giảm sâu (Dip) tự động qua Telegram, Slack và SMS

Các sếp là nhà đầu tư crypto chắc chắn hiểu cảm giác mệt mỏi khi phải dán mắt vào biểu đồ cả ngày chỉ để chờ những phiên "đỏ lửa" nhằm bắt đáy (Buy the Dip). Việc canh chừng thủ công không chỉ tốn thời gian mà còn dễ khiến các sếp bỏ lỡ những cơ hội vàng khi thị trường biến động mạnh trong đêm.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình theo dõi giá Bitcoin (BTC) và Ethereum (ETH), tự động quét thị trường mỗi 30 phút và bắn tin nhắn cảnh báo ngay lập tức về Telegram, Slack hoặc SMS nếu giá giảm vượt ngưỡng cho phép. Không cần code, hoạt động bền bỉ 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ bỏ lỡ bất kỳ nhịp giảm giá nào của thị trường, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt đáy kịp thời:** Nhận cảnh báo ngay khi BTC/ETH sụt giảm vượt ngưỡng (mặc định dưới -2.5%) mà không cần cắm mặt vào chart.
- **Đa kênh thông báo:** Nhận tin nhắn tức thì qua Telegram cá nhân/channel, kênh Slack của nhóm hoặc tin nhắn SMS qua Twilio.
- **Tiết kiệm thời gian & tâm lý:** Giải phóng bản thân khỏi việc theo dõi giá liên tục, giữ tâm lý vững vàng hơn trong giao dịch.
- **Hoạt động 24/7 không nghỉ:** Chạy tự động liên tục nhờ lịch trình được thiết lập sẵn trên n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo qua `@BotFather` nếu muốn nhận tin nhắn qua Telegram.
- **Slack App / Webhook:** Nếu muốn đẩy thông báo lên kênh Slack.
- **Twilio Account:** (Tùy chọn) Nếu muốn nhận tin nhắn SMS/WhatsApp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính. Các sếp cần chú ý cấu hình các điểm sau:

- **Every 30 Minutes (`scheduleTrigger`):** Node khởi chạy định kỳ. Các sếp có thể đổi tần suất chạy (ví dụ: mỗi 15 phút hoặc 1 giờ) nếu muốn.
- **Get Crypto Prices (`httpRequest`):** Node gọi API công khai từ CoinGecko để lấy giá hiện tại và biên độ biến động 24h của Bitcoin & Ethereum. Không cần thay đổi gì nếu API hoạt động bình thường.
- **Dip Check (`code`):** Node xử lý logic JavaScript. **QUAN TRỌNG:** Các sếp hãy vào node này, tìm biến `DIP` (mặc định đang để `-2.5`) và thay đổi thành mức % giảm giá mà các sếp muốn nhận cảnh báo (Ví dụ: `-3.0` hoặc `-5.0`).
- **Is Dip? (`if`):** Node kiểm tra điều kiện. Nếu mức giảm thực tế vượt qua ngưỡng cấu hình ở node Code, luồng sẽ đi tiếp nhánh True.
- **Send Telegram (`telegram`) / Send a message (`slack`) / Send an SMS (`twilio`):** 
  - Kết nối credentials tương ứng của các sếp (Telegram Bot Token, Slack OAuth/Webhook, Twilio Account SID & Auth Token).
  - Chọn chat ID hoặc kênh nhận tin nhắn phù hợp để bot bắn thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem dữ liệu từ CoinGecko có trả về và bot có bắn tin nhắn thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng danhsách coin:** Các sếp có thể sửa API URL trong node `Get Crypto Prices` để theo dõi thêm các altcoin khác như Solana (SOL), Ripple (XRP)...
- **Lưu lịch sử vào Google Sheets:** Nối thêm một node Google Sheets sau node `Is Dip?` để lưu lại lịch sử mỗi lần thị trường sập, phục vụ việc phân tích dữ liệu sau này.
- **Tích hợp AI phân tích:** Kết hợp thêm một OpenAI Node trước bước gửi tin nhắn để AI viết một đoạn nhận định ngắn về tình hình thị trường dựa trên mức độ giảm giá.

### 📌 Kết luận
Việc săn dip trong thị trường crypto chưa bao giờ dễ dàng đến thế khi đã có trợ lý tự động lo phần canh giá. Hãy cài đặt ngay workflow này lên hệ thống n8n của các sếp để tối ưu hóa chiến lược giao dịch ngay hôm nay!