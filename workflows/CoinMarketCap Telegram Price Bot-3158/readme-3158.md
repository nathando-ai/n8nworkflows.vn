---
title: "🚀 Bot Telegram Tự Động Hiển Thị Giá CoinMarketCap Với AI ChatGPT - Tiết Kiệm 100% Thời Gian Theo Dõi Giá Crypto"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp nhận giá crypto từ CoinMarketCap qua Telegram với phân tích AI, cập nhật tức thì và cá nhân hóa thông báo. Giúp tiết kiệm thời gian theo dõi thị trường 24/7 mà không cần mở ứng dụng."
slug: "bot-telegram-coinmarketcap-ai-chatgpt"
tags: [n8n, automation, finance, crypto, ai-chatgpt, telegram-bot, blockchain]
keywords: [n8n workflow crypto, bot telegram giá coin, tự động hóa theo dõi crypto, chatgpt phân tích giá crypto, coinmarketcap api n8n]
---

# 🚀 Bot Telegram Tự Động Hiển Thị Giá Crypto Với AI ChatGPT

### **Giải pháp hoàn hảo cho các sếp muốn theo dõi thị trường crypto mà không cần mở ứng dụng**

Theo dõi giá crypto 24/7 là một nhiệm vụ mệt mỏi, đặc biệt khi thị trường biến động liên tục. Các sếp phải liên tục mở ứng dụng, tra cứu giá, và phân tích thị trường – điều này không chỉ tốn thời gian mà còn dễ bỏ lỡ cơ hội. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
- **Nhận giá crypto từ CoinMarketCap** qua API.
- **Phân tích giá với AI ChatGPT** (gpt-4o-mini) để cung cấp thông tin chi tiết.
- **Gửi thông báo tức thì qua Telegram** với nội dung cá nhân hóa.
- **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở ứng dụng theo dõi giá thủ công.
- **Cập nhật tức thì**: Nhận thông báo giá crypto ngay khi có thay đổi.
- **Phân tích AI**: ChatGPT cung cấp phân tích chi tiết về xu hướng thị trường.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp.
- **Cá nhân hóa thông báo**: Thông tin được gửi theo yêu cầu cụ thể của từng người dùng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram với quyền gửi tin nhắn.
   - **API Key Telegram**: Lấy từ [@BotFather](https://t.me/BotFather) trên Telegram.
2. **Tài khoản OpenAI**:
   - **API Key OpenAI**: Lấy từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys).
3. **API Key CoinMarketCap**:
   - **Tạo API Key** từ [CoinMarketCap Developer Portal](https://coinmarketcap.com/api/).
4. **Credentials trong n8n**:
   - Thiết lập **credentials** cho:
     - `telegramApi` (để kết nối với Telegram).
     - `openAiApi` (để sử dụng ChatGPT).
     - `httpHeaderAuth` (để gọi API CoinMarketCap).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [n8n.io/workflows/3158](https://n8n.io/workflows/3158).
- **Import vào n8n Editor**:
  - Mở n8n Editor trên trình duyệt.
  - Nhấn **Import** và chọn file JSON tải xuống.
  - Hoặc **copy/paste** JSON từ file vào ô **Import Workflow**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau:

##### **A. Cấu hình Telegram**
- **Node: Telegram Trigger1**
  - Chọn **credentials**: `telegramApi`.
  - Điền **Chat ID** của bot Telegram (lấy từ [@BotFather](https://t.me/BotFather)).
  - Chọn **Command** (ví dụ: `/price` để kích hoạt bot).

- **Node: Telegram Send Message**
  - Chọn **credentials**: `telegramApi`.
  - Điền **Chat ID** của người dùng (hoặc group Telegram).
  - **Tham số động**: Sử dụng `{{ $json }}` để truyền nội dung từ AI.

##### **B. Cấu hình OpenAI (ChatGPT)**
- **Node: OpenAI Chat Model**
  - Chọn **credentials**: `openAiApi`.
  - **Model**: Đặt mặc định là `gpt-4o-mini` (hoặc chọn model khác nếu muốn).
  - **Prompt**: Cấu hình để AI phân tích giá crypto (ví dụ: *"Analyze the current price of [symbol] on CoinMarketCap and provide insights on trends"*).

##### **C. Cấu hình CoinMarketCap API**
- **Node: CoinMarketCap Price**
  - Chọn **credentials**: `httpHeaderAuth`.
  - **URL API**: `https://pro-api.coinmarketcap.com/v1/cryptocurrency/quotes/latest` (hoặc URL tương tự).
  - **Headers**:
    - `X-CMC_PRO_API_KEY`: Điền API Key CoinMarketCap.
    - `Accepts`: `application/json`.
  - **Query Parameters**:
    - `symbol`: Điền mã crypto muốn theo dõi (ví dụ: `BTC,ETH,SOL`).
    - `convert`: `USD` (hoặc USDT, EUR...).

##### **D. Cấu hình Agent & Memory**
- **Node: CoinMarketCap Price Agent**
  - Đây là **Agent AI** kết nối các node để phân tích và gửi thông báo.
  - **Không cần cấu hình thêm** (n8n tự động xử lý).

- **Node: Window Buffer Memory**
  - **Lưu trữ lịch sử** của các yêu cầu trước đó để AI phân tích liên tục.
  - **Không cần chỉnh sửa** (n8n tự động quản lý).

- **Node: Adds SessionId**
  - **Thêm ID phiên** để theo dõi các yêu cầu từ Telegram.
  - **Không cần chỉnh sửa**.

---

#### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Nhấn **Run Workflow** và gửi tin nhắn `/price BTC` đến bot Telegram.
   - Kiểm tra kết quả trên Telegram và log trong n8n Editor.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** từ **Inactive** sang **Active**.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Node: Set** để lập lịch gửi báo cáo giá crypto hàng ngày.
   - Kết hợp với **n8n Node: Telegram Send Message** để gửi tin nhắn tự động.

2. **Phân tích nhiều crypto cùng lúc**:
   - Thay đổi **Query Parameters** trong **CoinMarketCap Price** để theo dõi nhiều crypto (ví dụ: `BTC,ETH,SOL,ADA`).

3. **Cá nhân hóa thông báo**:
   - Sử dụng **AI ChatGPT** để phân tích và gửi thông báo cá nhân hóa (ví dụ: *"Giá BTC tăng 5% trong 24h, đây là cơ hội mua?"*).

4. **Lưu log và phân tích**:
   - Kết nối với **Google Sheets** hoặc **Airtable** để lưu lịch sử giá và phân tích dài hạn.

5. **Kết hợp với Slack**:
   - Thay thế **Telegram Send Message** bằng **Slack Webhook** để gửi thông báo đến Slack.

---

### 📌 Kết luận
Workflow **Bot Telegram Tự Động Hiển Thị Giá CoinMarketCap Với AI ChatGPT** là giải pháp hoàn hảo cho các sếp muốn theo dõi thị trường crypto một cách **tự động hóa, tiết kiệm thời gian và hiệu quả**. Bằng cách kết hợp **API CoinMarketCap, AI ChatGPT và Telegram**, workflow này cung cấp **thông tin tức thì, phân tích chi tiết và hoạt động liên tục 24/7**.

**Hãy áp dụng ngay workflow này và không bao giờ bỏ lỡ cơ hội trong thị trường crypto!** 🚀

---