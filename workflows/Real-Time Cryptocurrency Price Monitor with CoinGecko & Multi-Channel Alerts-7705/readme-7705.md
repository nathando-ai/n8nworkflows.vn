---
title: "🚀 **Hệ Thống Theo Dõi Giá Crypto Thực Tế + Cảnh Báo Tự Động (CoinGecko + Email/Telegram/Discord)**"
description: "Tự động theo dõi giá Bitcoin, Ethereum và 1000+ coin khác 24/7, phát hiện các tín hiệu breakout/breakdown, và gửi cảnh báo tức thời qua Email, Telegram và Discord. Giúp trader và nhà đầu tư không bỏ lỡ cơ hội thị trường với dữ liệu từ CoinGecko API miễn phí."
slug: "thong-doi-gia-crypto-thuc-te-coingecko-multi-channel-alerts"
tags: [n8n, crypto trading, tự động hóa, CoinGecko API, Telegram, Discord, Email, Google Sheets]
keywords: [tự động hóa crypto, cảnh báo giá crypto, theo dõi coin 24/7, n8n workflow crypto, alert breakout breakdown, CoinGecko API tự động]
---

# 🚀 **Hệ Thống Theo Dõi Giá Crypto Thực Tế + Cảnh Báo Tự Động (Multi-Channel)**

## **🔥 Nỗi Đau Của Trader Crypto Hiện Nay**
Crypto thị trường **không ngủ**, nhưng bạn có thể? Giá Bitcoin, Ethereum và các altcoin thay đổi từng giây, và **một cơ hội mua/vào bán chỉ trong vài phút** có thể biến mất nếu bạn không theo dõi kịp thời. Thay vì phải **ngồi chờ** trên các trang web như CoinGecko, Binance, hoặc CoinMarketCap, hoặc **check liên tục** trên Telegram/Discord, **hãy để n8n làm việc thay bạn**!

Với workflow này, các sếp sẽ:
✅ **Theo dõi 1000+ coin** (BTC, ETH, SOL, BNB, và cả các altcoin nhỏ) **24/7** mà không cần code.
✅ **Nhận cảnh báo tức thời** khi giá **vượt ngưỡng mục tiêu** (breakout) hoặc **rơi dưới ngưỡng cảnh báo** (breakdown).
✅ **Tùy chỉnh cảnh báo** cho từng coin với **ngưỡng cao/thấp**, **hướng di chuyển** (above/below/both), và **thời gian cooldown** để tránh spam.
✅ **Nhận thông báo đa kênh**: **Email chi tiết**, **Telegram trên điện thoại**, và **Discord cho nhóm trader**.
✅ **Lưu lịch sử cảnh báo** trên Google Sheets để **phân tích sau này**.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần phải **check giá liên tục** trên nhiều nền tảng.
- **Cảnh báo chính xác**: Phát hiện **breakout/breakdown** ngay khi xảy ra, với dữ liệu từ **CoinGecko API miễn phí**.
- **Cá nhân hóa cảnh báo**: Đặt **ngưỡng riêng** cho từng coin (ví dụ: BTC/USDT ở 45k, ETH ở 3k).
- **Hoạt động liên tục**: **24/7/365**, không cần can thiệp thủ công.
- **Tích hợp đa kênh**: **Email** (chi tiết), **Telegram** (tức thời), **Discord** (nhóm trader).
- **Lưu trữ lịch sử**: **Google Sheets** ghi lại tất cả cảnh báo để **phân tích sau này**.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý** |
|----------------------|--------------------------------------------------|------------|
| **Google Sheets**    | - Tài khoản Google (để tạo sheet theo mẫu)     | Sheet phải có **cấu trúc cột chính xác** (xem dưới đây). |
|                      | - **Google API Key** (để kết nối n8n)          | [Cách tạo API Key](https://developers.google.com/sheets/api/quickstart/python) |
| **Email (SMTP)**     | - Tài khoản Email (Gmail, Outlook,...)          | Cần **SMTP credentials** (Host, Port, Username, Password). |
|                      | - **SMTP API Key** (nếu dùng Gmail)             | [Cách cấu hình SMTP cho Gmail](https://myaccount.google.com/apppasswords) |
| **Telegram**         | - **Bot Token** (tạo từ [@BotFather](https://t.me/BotFather)) | Cần **ID Chat** của cá nhân hoặc nhóm. |
| **Discord**          | - **Bot Token** (tạo từ [Discord Developer Portal](https://discord.com/developers/applications)) | Cần **ID Channel** để gửi thông báo. |

### **2. Google Sheets Mẫu (Cấu Trúc Cột)**
Các sếp phải tạo một **Google Sheet** với **cấu trúc cột chính xác** như sau:

| **Cột (A-G)**       | **Mô Tả**                                                                 | **Ví Dụ**          |
|----------------------|----------------------------------------------------------------------------|--------------------|
| **Symbol**           | Ký hiệu coin (BTC/USDT, bitcoin, ETH, ethereum,...)                     | BTC/USDT, bitcoin  |
| **Upper Limit**      | Ngưỡng giá **cao** để cảnh báo (breakout)                                | 45000 (BTC)        |
| **Lower Limit**      | Ngưỡng giá **thấp** để cảnh báo (breakdown)                             | 40000 (BTC)        |
| **Direction**        | Hướng cảnh báo: `above` (chỉ cao), `below` (chỉ thấp), `both` (cả hai)   | both               |
| **Cooldown (min)**   | Thời gian **chờ** trước khi cảnh báo lại (tránh spam)                   | 10                 |
| **Last Price**       | **Không điền** (n8n tự cập nhật)                                        | (trống)            |
| **Last Time**        | **Không điền** (n8n tự cập nhật)                                        | (trống)            |

**📌 Lưu ý:**
- **Sheet Name** phải là **"Crypto Watchlist"** (n8n sẽ tự động tìm sheet này).
- **Mỗi hàng** là một coin khác nhau.
- **Ký hiệu coin** có thể là:
  - **Trading Pair**: `BTC/USDT`, `ETH/USDT`
  - **CoinGecko ID**: `bitcoin`, `ethereum`
  - **Symbol ngắn**: `BTC`, `ETH`, `SOL`

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ JSON**
Các sếp có **2 cách** để import workflow:
#### **Cách 1: Tải JSON từ n8n.io**
1. Truy cập [link workflow gốc](https://n8n.io/workflows/7705).
2. Nhấn **"Export"** (phải góc trên).
3. **Copy toàn bộ JSON** hoặc **tải xuống file**.
4. Trong **n8n Editor**, nhấn **"Import"** và **dán/paste** JSON.

#### **Cách 2: Copy/Paste JSON trực tiếp**
- **Copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/7705/export).
- Trong **n8n Editor**, nhấn **"Import"** → **"Paste JSON"**.

---
### **2. Các Bước Cấu Hình BẮT BUỘC**
Sau khi import, các sếp **phải chỉnh** các node sau:

#### **📌 Node 1: "24/7 Crypto Trigger" (Cron)**
- **Cấu hình**: `* * * * *` (chạy **mỗi phút**).
- **Lưu ý**: Nếu muốn **giảm tải API**, có thể điều chỉnh thành `*/5 * * * *` (mỗi 5 phút).

#### **📌 Node 2: "Read Crypto Watchlist" (Google Sheets)**
- **Credentials**: Chọn **"googleApi"** (đã cấu hình trước).
- **Sheet Name**: **"Crypto Watchlist"** (phải trùng với sheet các sếp tạo).
- **Range**: `Sheet1!A1:G` (lấy toàn bộ dữ liệu từ sheet).

#### **📌 Node 3: "Parse Crypto Data" (Code)**
- **Không cần chỉnh**, n8n tự động **chuyển đổi ký hiệu coin** (ví dụ: `BTC/USDT` → `bitcoin/usd`).

#### **📌 Node 4: "Fetch Live Crypto Price" (HTTP Request)**
- **URL**: `https://api.coingecko.com/api/v3/simple/price?ids={coin}&vs_currencies=usd&include_24hr_change=true`
- **Headers**:
  ```
  Accept: application/json
  ```
- **Lưu ý**: **Không cần API Key** (CoinGecko miễn phí cho 1000+ request/ngày).

#### **📌 Node 5-6: "Smart Crypto Alert Logic" & "Check Crypto Alert Conditions" (Code & If)**
- **Không cần chỉnh**, n8n tự động **kiểm tra ngưỡng** và **so sánh giá hiện tại** với **Upper/Lower Limit**.

#### **📌 Node 7-9: "Send Crypto Email Alert", "Send Telegram Crypto Alert", "Send Discord Crypto Alert"**
- **Email (SMTP)**:
  - **Credentials**: Chọn **"smtp"** (đã cấu hình trước).
  - **Subject**: `🚨 ALERT: {coin} - {price} USD` (ví dụ: `🚨 ALERT: BTC - 45,000 USD`).
  - **Body**: Nội dung chi tiết bao gồm:
    - Giá hiện tại.
    - 24h change (%).
    - Market cap.
    - Link CoinGecko.

- **Telegram**:
  - **Credentials**: Chọn **"telegramApi"** (đã cấu hình trước).
  - **Chat ID**: ID của cá nhân hoặc nhóm (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).

- **Discord**:
  - **Credentials**: Chọn **"discordBotApi"** (đã cấu hình trước).
  - **Channel ID**: ID của channel muốn gửi thông báo.

#### **📌 Node 10: "Update Crypto Alert History" (Google Sheets)**
- **Credentials**: **"googleApi"**.
- **Sheet Name**: **"Crypto Alert History"** (n8n sẽ tự tạo sheet này nếu không có).
- **Range**: `Sheet1!A1:D` (ghi lại: **Coin, Price, Time, Alert Type**).

#### **📌 Node 11-12: "Success Notification" & "Error Notification" (Email)**
- **Dùng để thông báo trạng thái workflow**:
  - **Success**: Gửi khi workflow chạy thành công.
  - **Error**: Gửi khi có lỗi (ví dụ: API CoinGecko down).

---
### **3. Kích Hoạt Workflow**
1. **Test Run** với **dữ liệu mẫu**:
   - Nhấn **"Run Workflow"** và chọn **1 hàng dữ liệu** từ Google Sheets.
   - Kiểm tra **Email, Telegram, Discord** có nhận được cảnh báo không.
2. **Bật Active**:
   - Sau khi **test thành công**, chuyển **status** từ **"Inactive"** sang **"Active"**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tăng Cường Cảnh Báo với AI (LLM)**
- **Thêm node `n8n-nodes-base.llm`** (OpenAI, Mistral) để **tự động phân tích**:
  - **"Giá BTC vừa vỡ ngưỡng 45k, có nên mua không?"**
  - **"ETH đang ở mức support 3k, có nguy cơ dump không?"**
- **Cách làm**:
  - Sau node **"Fetch Live Crypto Price"**, thêm **node LLM** với **prompt**:
    ```
    Analyze the following crypto data and suggest a trading decision:
    - Coin: {coin}
    - Current Price: {price} USD
    - 24h Change: {change}%
    - Market Cap: {market_cap}
    - Is this a breakout/breakdown signal? Should I buy/sell/hold?
    ```

### **2. Lưu Log Cảnh Báo vào Database**
- Thay vì **Google Sheets**, các sếp có thể **lưu vào Firebase, Airtable, hoặc PostgreSQL** để:
  - **Tìm kiếm nhanh** các cảnh báo cũ.
  - **Xây dựng dashboard** theo dõi lịch sử.
- **Cách làm**:
  - Thay node **"Update Crypto Alert History"** bằng **node Firebase/PostgreSQL**.

### **3. Cảnh Báo Cho Nhóm Trader (Slack)**
- Nếu không dùng Discord, có thể **thêm Slack** với node `n8n-nodes-base.slack`.
- **Cách làm**:
  - Tạo **bot Slack** từ [API Slack](https://api.slack.com/apps).
  - Thêm node **Slack Webhook** sau **"Check Crypto Alert Conditions"**.

### **4. Tự Động Cập Nhật Ngưỡng Cảnh Báo**
- **Thêm node `n8n-nodes-base.googleSheets`** để:
  - **Tự động tăng/giảm ngưỡng** dựa trên **moving average 7 ngày**.
  - **Cập nhật cooldown** theo **volatility** của coin.

---
## 📌 **Kết Luận: Đừng Bỏ Lỡ Cơ Hội Crypto Nữa!**

Với **workflow này**, các sếp sẽ:
✔ **Theo dõi giá crypto 24/7** mà không cần ngồi chờ.
✔ **Nhận cảnh báo tức thời** qua **Email, Telegram, Discord**.
✔ **Tự động phân tích** và **cập nhật lịch sử** để **trading hiệu quả hơn**.
✔ **Tiết kiệm thời gian** và **giảm stress** khi theo dõi thị trường.

**🚀 Hãy import ngay và bắt đầu tự động hóa trading của mình!**

---
### **🎁 Bonus: Đăng Ký VPS TinoHost cho n8n (Self-Hosted)**
:::info[**Hạ Tầng Chuyên Nghiệp cho Workflow**]
Để workflow **chạy 24/7 không gián đoạn**, các sếp nên **self-host n8n** trên **VPS**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow crypto).

**💡 Lợi ích:**