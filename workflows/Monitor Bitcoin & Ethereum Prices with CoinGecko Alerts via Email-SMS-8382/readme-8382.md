---
title: "🚀 Tự Động Theo Dõi Giá Bitcoin & Ethereum và Cảnh Báo Qua Email - SMS với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động giám sát giá BTC/ETH qua CoinGecko, phát hiện biến động mạnh và gửi cảnh báo tức thì qua Gmail và Twilio SMS."
slug: "tu-dong-theo-doi-gia-crypto-coingecko-email-sms"
tags: [n8n, automation, crypto, coingecko, trading, webhook]
keywords: [n8n workflow, theo dõi giá crypto, cảnh báo bitcoin ethereum, coingecko api n8n, tự động hóa email sms]
---

# 🚀 Tự Động Theo Dõi Giá Bitcoin & Ethereum và Cảnh Báo Qua Email - SMS

Các nhà đầu tư và trader tiền mã hóa (crypto) thường đối mặt với nỗi đau lớn: Giá thị trường biến động 24/7, việc ngồi canh biểu đồ thủ công vừa tốn thời gian, vừa dễ bỏ lỡ các cơ hội "vàng" hoặc các cú sập giá bất ngờ khi đang ngủ hay bận việc. 

Giải pháp? Workflow n8n tự động hóa 100% này sẽ thay bạn theo dõi sát sao giá Bitcoin (BTC) và Ethereum (ETH) qua CoinGecko API, tự động so sánh với các ngưỡng giới hạn (thresholds) định sẵn và bắn thông báo khẩn cấp qua **Gmail** và **Twilio (SMS)** ngay khi có biến động mạnh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giám sát 24/7 không nghỉ:** Hệ thống tự động kiểm tra giá liên tục mỗi 15 phút mà không cần con người can thiệp.
- **Cảnh báo tức thì:** Nhận ngay thông báo qua Email và SMS/WhatsApp khi BTC hoặc ETH vượt mốc kỳ vọng (ví dụ: BTC vượt $110,000 hoặc biến động > 2% trong 24h).
- **Loại bỏ cảm xúc khi giao dịch:** Giúp bám sát chiến lược giá đã định, bảo vệ tài sản kịp thời trước các cú "flash dump" hoặc "moon".
- **Tùy biến linh hoạt:** Dễ dàng thay đổi ngưỡng giá (Targets) và thêm các kênh thông báo khác như Telegram, Slack.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **CoinGecko API:** Không bắt buộc cho dữ liệu cơ bản, nhưng nên chuẩn bị sẵn nếu cần gọi tần suất cao.
- **Gmail Account / Credentials:** Để cấu hình node gửi email cảnh báo.
- **Twilio Account:** Tài khoản Twilio để gửi tin nhắn SMS/MMS/WhatsApp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình kỹ các node sau:
- **Node `Every 15 Minutes` (scheduleTrigger):** Thiết lập lịch chạy định kỳ (mặc định 15 phút/lần). Có thể rút ngắn thời gian nếu muốn cập nhật nhanh hơn.
- **Node `Get Crypto Prices` (httpRequest):** Gọi API tới CoinGecko để lấy giá hiện tại của Bitcoin và Ethereum kèm theo biến động 24h.
- **Node `Compute Threshold Flags` (code):** Nơi đặt các thông số cấu hình cốt lõi. Các sếp cần chỉnh sửa các biến:
  - `BTC_UP` / `BTC_DOWN`: Ngưỡng giá trần/sàn của Bitcoin.
  - `ETH_UP` / `ETH_DOWN`: Ngưỡng giá trần/sàn của Ethereum.
  - `MOVE_ABS`: Ngưỡng biên độ biến động 24h (ví dụ: `2.0` tương ứng ±2%).
- **Node `Any Alert?` (if):** Kiểm tra xem có điều kiện giá nào bị phá vỡ hay không để quyết định có kích hoạt luồng cảnh báo tiếp theo hay dừng lại.
- **Node `Format Alert Email` (code):** Định dạng lại nội dung thông báo cho trực quan, ví dụ: *"BTC broke $110,000 (+2.1% 24h)"*.
- **Node `Send a message` (gmail) & `Send an SMS/MMS/WhatsApp message` (twilio):** Kết nối tài khoản (credentials) tương ứng của Gmail và Twilio để hệ thống có quyền gửi mail và tin nhắn đến số điện thoại của sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử với dữ liệu mẫu từ CoinGecko.
- Kiểm tra hộp thư Gmail và điện thoại xem đã nhận được thông báo chưa.
- Nếu mọi thứ ổn áp, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh Telegram/Slack:** Bạn có thể nối thêm node Telegram Bot vào sau nhánh `Any Alert?` để nhận tin nhắn ngay trên điện thoại cực kỳ tiện lợi và miễn phí.
- **Chống spam cảnh báo (Debounce):** Nếu giá cứ dao động quanh một ngưỡng, bạn sẽ nhận được tin nhắn liên tục. Hãy kết hợp thêm một node Google Sheets hoặc cơ chế lưu trữ memory để ghi nhận lần cảnh báo gần nhất, chỉ báo lại khi giá vượt hẳn một khoảng an toàn.
- **Mở rộng danh mục:** Thêm các đồng coin tiềm năng khác (như Solana, XRP, ADA...) vào node `Get Crypto Prices` để theo dõi cả danh mục đầu tư (Portfolio).

### 📌 Kết luận
Việc tự động hóa theo dõi giá crypto không chỉ giúp các sếp tiết kiệm hàng giờ soi bảng điện tử mỗi ngày mà còn là chìa khóa để phản ứng nhanh trước những biến động thị trường khốc liệt. Hãy cài đặt ngay workflow này lên hệ thống n8n của bạn và làm chủ cuộc chơi tài chính!