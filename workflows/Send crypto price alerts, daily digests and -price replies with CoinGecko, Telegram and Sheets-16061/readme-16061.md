---
title: "🚀 **Tự Động Hóa Cảnh Báo Giá Crypto, Tóm Tắt Hàng Ngày & Trả Lời Lệnh Telegram - CoinGecko + Sheets + Telegram**"
description: "Workflow tự động theo dõi giá crypto theo danh sách theo dõi cá nhân, gửi cảnh báo giá thực thời qua Telegram, ghi log vào Google Sheets, và gửi tóm tắt hàng ngày với chỉ số Fear & Greed. Hỗ trợ lệnh `/price` để tra cứu giá tức thì - hoàn toàn không cần code!"
slug: "tieu-dong-hoa-canh-bao-gia-crypto-telegram-sheets"
tags: [n8n, automation, crypto trading, telegram bot, google sheets, no-code, self-hosted]
keywords: [tự động hóa crypto, cảnh báo giá crypto, telegram bot crypto, google sheets crypto, tự động hóa no-code, n8n workflow crypto]
---

# 🚀 **Tự Động Hóa Cảnh Báo Giá Crypto Thông Minh - Telegram + Sheets + CoinGecko**

## **Giới Thiệu**
Các sếp đang phải **theo dõi giá crypto thủ công** hàng ngày, lo lắng bỏ lỡ cơ hội mua/v vendu, hoặc phải **ghi chép log giá** vào Excel để phân tích sau? Hay muốn **tự động nhận cảnh báo** khi giá đạt ngưỡng mục tiêu (ví dụ: BTC tăng 5% so với giá mua) mà không cần ngủ trưa?

Workflow này **giải quyết tất cả** với **3 tính năng chính**:
1. **Cảnh báo giá thực thời** (theo dõi ngưỡng giá, thay đổi %, RSI) → **Telegram**.
2. **Tóm tắt hàng ngày** (giá hiện tại, thay đổi 24h, giá trị portfolio, chỉ số Fear & Greed) → **Telegram**.
3. **Trả lời lệnh `/price`** (ví dụ: `/price btc`) → **Tra cứu giá tức thì** qua Telegram.

**Kết quả?** Các sếp **tiết kiệm 5+ giờ/tuần**, giảm stress, và có **dữ liệu chính xác** được tự động ghi log vào Google Sheets.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động cảnh báo giá** khi đạt ngưỡng mục tiêu (giá, thay đổi %, RSI) → **Không bỏ lỡ cơ hội**.
- **Tóm tắt hàng ngày** với giá trị portfolio, chỉ số Fear & Greed → **Quản lý đầu tư hiệu quả**.
- **Trả lời lệnh `/price`** tức thì qua Telegram → **Tra cứu giá nhanh chóng**.
- **Ghi log tất cả cảnh báo** vào Google Sheets → **Dữ liệu lâu dài, phân tích dễ dàng**.
- **Hoạt động 24/7** → **Không cần theo dõi thủ công**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram (tạo bằng `@BotFather`).
   - **Chat ID** (của cá nhân hoặc nhóm).
   - [Hướng dẫn lấy Chat ID](https://core.telegram.org/bots/api#how-do-i-create-a-bot).
2. **Google Sheets**:
   - Một **bảng Google Sheets** để ghi log cảnh báo.
   - **Quản trị viên** của bảng (để cấp quyền cho n8n).
3. **API Key CoinGecko** (không bắt buộc, nhưng giúp tránh giới hạn free tier).
4. **Thời gian** (~30 phút để cấu hình lần đầu).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16061](https://n8n.io/workflows/16061).
- Trong **n8n Editor**, chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Hoặc** copy toàn bộ JSON và paste vào **Create Workflow** → **Import from JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** nhưng chỉ cần **cấu hình 3 node quan trọng** là có thể chạy ngay:

##### **A. Cấu hình Telegram (4 node)**
- **Tất cả 4 node Telegram** (`Send Alert`, `Send Digest`, `Send Price Reply`, `Send Unknown Command`) **sử dụng cùng một credential**.
  - Mở **Telegram node** → **Credentials** → **Create New**.
  - Nhập **Token bot** (lấy từ `@BotFather`).
  - **Chat ID** (lấy từ `@userinfobot`).
  - **Lưu** và **áp dụng** cho tất cả 4 node.

##### **B. Cấu hình Google Sheets (1 node)**
- Mở node **`Append Alert to Sheets`**.
- **Credentials**:
  - Chọn **Google Sheets OAuth2** (nếu chưa có, tạo mới).
  - **Chọn spreadsheet** và **sheet** muốn ghi log.
  - **Cấu hình cột**:
    - `Timestamp`: Thời gian cảnh báo.
    - `Asset`: Tên coin (ví dụ: BTC).
    - `Price`: Giá hiện tại.
    - `Change`: Thay đổi %.
    - `Alert Type`: Loại cảnh báo (giá, RSI, ...).

##### **C. Cấu hình Danh Sách Theo Dõi (1 node)**
- Mở node **`Configure Watchlist`** (node **Code** đầu tiên).
- **Sửa phần `watchlist`** để thêm/loại bỏ coin theo dõi:
  ```javascript
  const watchlist = [
    {
      "symbol": "bitcoin",       // CoinGecko ID (lowercase)
      "display": "BTC",         // Hiển thị trong cảnh báo
      "threshold": 50000,        // Giá ngưỡng (USD)
      "direction": "above",      // 'above' hoặc 'below'
      "cooldownMinutes": 30,     // Thời gian chờ giữa cảnh báo
      "holdings": 1,             // Số lượng coin sở hữu (0 nếu không)
      "priceChangePct": 5,       // Cảnh báo khi thay đổi ±5%
      "useRSI": true,            // Bật/tắt RSI
      "rsiOversold": 30,         // Ngưỡng RSI bán
      "rsiOverbought": 70        // Ngưỡng RSI mua
    },
    {
      "symbol": "ethereum",
      "display": "ETH",
      "threshold": 3000,
      "direction": "above",
      "cooldownMinutes": 60,
      "holdings": 2,
      "priceChangePct": 3,
      "useRSI": true
    }
  ];
  ```
- **Lưu ý**:
  - **CoinGecko ID** phải là **lowercase** (ví dụ: `bitcoin` chứ không phải `Bitcoin`).
  - **Thay đổi `threshold`** để điều chỉnh giá cảnh báo.
  - **`priceChangePct`** = 0 → Tắt cảnh báo thay đổi %.

##### **D. Cấu hình Tóm Tắt Hàng Ngày (1 node)**
- Mở node **`Configure Daily Digest`**.
- **Sửa `TELEGRAM_CHAT_ID`** để gửi tóm tắt đến chat mong muốn.
- **Sửa `watchlist`** để đồng bộ với **Danh Sách Theo Dõi** (trên).

##### **E. Cấu hình Lệnh `/price` (1 node)**
- Node **`When Telegram Command Received`** sẽ tự động tạo **webhook** khi workflow hoạt động.
- **Không cần cấu hình thêm**, chỉ cần **bật workflow** là xong.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **Active** trên workflow.
  - **Run Workflow** để kiểm tra.
  - **Kiểm tra Telegram** để xem cảnh báo/tóm tắt có được gửi không.
- **Bật Schedule**:
  - Node **`Hourly Trigger`** → **Enable**.
  - Node **`Daily 8am Trigger`** → **Enable** (thời gian UTC, các sếp điều chỉnh theo múi giờ).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm coin mới**:
   - Mở **`Configure Watchlist`** và thêm vào mảng `watchlist`.
   - **Lưu ý**: CoinGecko ID phải chính xác (ví dụ: `solana` chứ không phải `sol`).

2. **Tăng giảm ngưỡng cảnh báo**:
   - Sửa `threshold` trong `Configure Watchlist` để thay đổi giá cảnh báo.
   - Ví dụ: `threshold: 60000` → Cảnh báo khi BTC > 60k.

3. **Bật/tắt RSI**:
   - Sửa `useRSI: true/false` để tắt/bật cảnh báo dựa trên chỉ số RSI.

4. **Gửi tóm tắt hàng ngày đến nhiều chat**:
   - Sửa `TELEGRAM_CHAT_ID` trong **`Configure Daily Digest`** thành một **list chat ID** (nếu cần).

5. **Lưu log cảnh báo vào nhiều sheet**:
   - Sửa node **`Append Alert to Sheets`** để chỉ định **sheet khác**.

6. **Thêm cảnh báo email**:
   - Thêm node **`n8n-nodes-base.email`** sau **`Send Alert on Telegram`** để gửi cảnh báo qua email.

7. **Tự động chia sẻ tóm tắt hàng ngày**:
   - Sử dụng node **`n8n-nodes-base.slack`** để gửi tóm tắt vào Slack.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy đầu tư** thay vì **theo dõi giá thủ công**. Với **cảnh báo thông minh**, **tóm tắt hàng ngày**, và **trả lời lệnh tức thì**, các sếp sẽ **không bỏ lỡ cơ hội** và **quản lý portfolio hiệu quả hơn**.

**Bắt đầu ngay!**
1. **Import workflow** từ link trên.
2. **Cấu hình Telegram + Sheets** theo hướng dẫn.
3. **Bật schedule** và **nhận cảnh báo tự động**!

---
**💡 Cần hỗ trợ?** Đăng câu hỏi trên [Community n8n](https://community.n8n.io/) hoặc liên hệ với **Cybernative Technologies** (tác giả của workflow).