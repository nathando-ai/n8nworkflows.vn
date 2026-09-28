---
title: "🚀 Theo dõi giá Top Meme Coin bằng Telegram Bot và CoinGecko API"
description: "Hướng dẫn tự động hóa theo dõi giá các meme coin hàng đầu thông qua Telegram bot, giúp các trader và người theo dõi crypto tiết kiệm thời gian và nhận thông báo tức thì."
slug: "theo-doi-gia-meme-coin-voi-telegram-bot"
tags: [n8n, automation, no-code, crypto, telegram]
keywords: [n8n workflow, tự động hóa, meme coin, CoinGecko, Telegram bot]
---

# 🚀 Theo dõi giá Top Meme Coin bằng Telegram Bot và CoinGecko API

[Các sếp trong ngành crypto luôn gặp khó khăn khi phải theo dõi giá của hàng trăm meme coin mỗi ngày. Với workflow này, các sếp có thể tự động hóa quy trình theo dõi giá các meme coin hàng đầu thông qua Telegram bot, giúp tiết kiệm thời gian và nhận thông báo tức thì khi giá có biến động đáng chú ý.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải mở nhiều tab trình duyệt để theo dõi giá.
- Nhận thông báo tức thì: Được cảnh báo ngay khi giá của meme coin có biến động đáng chú ý.
- Tăng hiệu quả giao dịch: Nhận thông tin chính xác và nhanh chóng để đưa ra quyết định giao dịch tốt hơn.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram (có thể tạo tại [BotFather](https://t.me/BotFather)).
- API Key từ CoinGecko (có thể đăng ký tại [CoinGecko API](https://www.coingecko.com/en/api)).
- ID của Telegram group hoặc channel mà các sếp muốn gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/5634](https://n8n.io/workflows/5634).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Cấu hình credentials cho Telegram API.
   - Điền ID của Telegram group hoặc channel mà các sếp muốn nhận thông báo.
   - Đảm bảo bot Telegram đã được thêm vào group/channel.

2. **If /memecoin**:
   - Cấu hình điều kiện để kích hoạt workflow khi nhận lệnh "/memecoin" từ người dùng.

3. **Fetch Meme Coins**:
   - Cấu hình URL API của CoinGecko để lấy dữ liệu về các meme coin.
   - Đảm bảo API Key đã được thêm vào credentials.

4. **Format Message**:
   - Chỉnh sửa hàm JavaScript để định dạng thông báo theo ý muốn.
   - Ví dụ: Thêm thông tin về biến động giá, thời gian cập nhật, v.v.

5. **Send to Telegram**:
   - Cấu hình credentials cho Telegram API.
   - Đảm bảo bot Telegram đã được thêm vào group/channel.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. Bật Active workflow để bắt đầu theo dõi giá các meme coin.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm các lệnh khác như "/top10" để theo dõi top 10 meme coin hàng đầu.
- Tích hợp với các dịch vụ khác như Slack, Discord để nhận thông báo trên nhiều nền tảng.
- Lưu log các lệnh đã thực hiện để theo dõi lịch sử giao dịch.
- Gửi báo cáo định kỳ về biến động giá của các meme coin hàng ngày.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và nhận thông báo tức thì về biến động giá của các meme coin hàng đầu. Với việc tự động hóa quy trình theo dõi giá, các sếp có thể tập trung vào việc phân tích và đưa ra quyết định giao dịch tốt hơn. Hãy áp dụng ngay để tối ưu hóa quá trình giao dịch của các sếp!