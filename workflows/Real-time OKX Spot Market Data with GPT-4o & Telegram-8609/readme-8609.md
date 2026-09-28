---
title: "🚀 Tự Động Hóa Dữ Liệu Thị Trường Spot OKX Thời Gian Thực Tế Với GPT-4o & Telegram"
description: "Workflow này tự động lấy dữ liệu thị trường Spot OKX (giá hiện thời, bảng lệnh, candle, thống kê 24h, giao dịch gần đây) và gửi báo cáo định kỳ dưới dạng Telegram bot với GPT-4o. Giúp trader theo dõi thị trường 24/7 mà không cần code."
slug: "tieu-dong-hoa-du-lieu-thi-truong-okx-spot-voi-gpt-4o-telegram"
tags: [n8n, automation, crypto trading, ai chatbot, blockchain, telegram bot]
keywords: [n8n workflow crypto, tự động hóa thị trường spot, okx api, gpt-4o telegram bot, data fetching automation]
---

# 🚀 **Tự Động Hóa Dữ Liệu Thị Trường Spot OKX Thời Gian Thực Tế Với GPT-4o & Telegram**

## **🔥 Giới Thiệu**
Trader và nhà đầu tư crypto thường phải mất nhiều thời gian để theo dõi **giá hiện thời, bảng lệnh, candle, thống kê 24h, và giao dịch gần đây** trên OKX. Thông thường, việc này yêu cầu phải **check nhiều tab, copy-paste dữ liệu, và phân tích thủ công** – điều này không chỉ tốn thời gian mà còn dễ gây lỗi.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động lấy dữ liệu thị trường Spot OKX** (BTC-USDT, ETH-USDT, SOL-USDT,...) từ API REST **không cần API key**.
✅ **Sử dụng GPT-4o-mini** để **tự động định dạng và tổng hợp** dữ liệu thành báo cáo dễ đọc.
✅ **Gửi báo cáo trực tiếp qua Telegram** (hoặc Slack, Email) **mỗi khi có yêu cầu**.
✅ **Phân tích và cảnh báo** (ví dụ: thay đổi giá, spread, hoặc tín hiệu giao dịch).
✅ **Hoạt động 24/7** mà không cần can thiệp người dùng.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần check thủ công trên OKX Web3 hoặc App.
- **Dữ liệu chính xác**: Lấy từ API chính thức OKX, không bị lỗi manual entry.
- **Báo cáo cá nhân hóa**: Dữ liệu được định dạng theo yêu cầu (HTML, Markdown, hoặc văn bản).
- **Hoạt động liên tục**: Chạy tự động mỗi khi có yêu cầu từ Telegram.
- **Tín hiệu giao dịch**: GPT-4o có thể phân tích và đề xuất chiến lược (nếu cấu hình).
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram** (để nhận báo cáo).
✔ **Bot Telegram** (để trigger workflow).
✔ **API Key OpenAI** (để sử dụng GPT-4o-mini).
✔ **OKX API** (không cần API key, chỉ cần kết nối HTTP).
✔ **n8n Self-hosted** (để chạy 24/7, không dùng phiên bản miễn phí).

👉 **🎁 Mã giảm giá VPS cho n8n (50k/tháng):**
🔹 [TinoHost](https://tino.vn/vps-n8n?affid=388) (mã: **VPSN8N**)
🔹 [BNIX](https://my.bnix.one/aff.php?aff=172) (VPS Xeon 4GB)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Workflow gồm **17 node** và **8 workflow con** (mỗi node tương ứng với một API endpoint OKX). Các sếp có thể:
- **Tải JSON từ [n8n.io/workflows/8609](https://n8n.io/workflows/8609)** và import vào n8n Editor.
- **Copy/paste JSON** vào n8n và chạy.

:::warning[LƯU Ý]
- **Không dùng phiên bản n8n miễn phí** (cloud) vì không hỗ trợ Webhook và Telegram Trigger 24/7.
- **Cài đặt n8n trên VPS** để đảm bảo hoạt động liên tục.
:::

---

### **2. Các bước cấu hình bắt buộc 📌**

#### **A. Thiết lập Credentials**
Trước khi chạy, các sếp phải **cấu hình 3 credentials chính**:
1. **OpenAI API Key**
   - Đăng nhập [OpenAI](https://platform.openai.com/), lấy **API Key** và thêm vào n8n dưới **Credentials → Add Credential → OpenAI**.
   - **Model mặc định**: `gpt-4.1-mini` (rẻ hơn GPT-4o nhưng vẫn hiệu quả).

2. **Telegram Bot Token**
   - Tạo **bot Telegram** tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm vào n8n dưới **Credentials → Add Credential → Telegram API**.
   - **Cấu hình Telegram Trigger**:
     - Node: `Telegram Trigger`
     - **Command**: `/okx` (hoặc tùy chỉnh).
     - **Chat ID**: Thêm **ID Telegram của bạn** vào node **User Authentication (Replace Telegram ID)** (sẽ hướng dẫn sau).

3. **OKX API (không cần key)**
   - Workflow **sử dụng HTTP Request Tool** để gọi API OKX REST (không cần API key).
   - Các endpoint được cấu hình sẵn trong node `OKX AI Agent`.

---

#### **B. Cấu hình Node Quan Trọng**
##### **1. Node: `Telegram Trigger`**
- **Chức năng**: Nhận lệnh từ Telegram và trigger workflow.
- **Cấu hình**:
  - **Command**: `/okx` (hoặc `/btc`, `/eth` tùy chọn).
  - **Credentials**: Chọn `telegramApi` (đã thêm trước đó).

##### **2. Node: `User Authentication (Replace Telegram ID)`**
- **Chức năng**: Kiểm tra **ID Telegram** của người dùng có được phép truy cập không.
- **Cách sửa**:
  - Mở node **Code** này và thay thế:
    ```javascript
    const allowedIds = ["YOUR_TELEGRAM_ID_HERE"]; // Thêm ID Telegram của bạn
    const chatId = $input.all().telegram.message.chat.id;
    if (!allowedIds.includes(chatId)) {
      throw new Error("Access denied. Please contact admin.");
    }
    ```
  - **Lấy ID Telegram**:
    - Gửi tin nhắn cho bot Telegram của bạn.
    - Mở [@userinfobot](https://t.me/userinfobot) và chat với nó để lấy `id`.

##### **3. Node: `Adds "SessionId"`**
- **Chức năng**: Tạo **Session ID** để lưu trữ trạng thái trong workflow.
- **Không cần sửa**, nhưng nếu muốn **cá nhân hóa**, có thể thêm:
  ```javascript
  $node["set"].json = {
    sessionId: $input.all().telegram.message.chat.id + "_" + new Date().getTime()
  };
  ```

##### **4. Node: `OKX AI Agent` (Core Orchestrator)**
- **Chức năng**: Lấy dữ liệu từ **8 API endpoint OKX** và gửi cho GPT-4o định dạng.
- **Cấu hình**:
  - **Model**: `gpt-4.1-mini` (hoặc `gpt-4o` nếu có budget).
  - **Prompt**: Sẽ tự động lấy dữ liệu từ các node `httpRequestTool` sau.

##### **5. Node: `httpRequestTool` (8 Node API OKX)**
Mỗi node tương ứng với một API endpoint OKX. **Không cần sửa**, nhưng các sếp có thể:
- **Thay đổi `instId`** (ví dụ: `BTC-USDT` → `ETH-USDT`).
- **Đổi `bar` (timeframe)** trong node `Klines (Candles)` (ví dụ: `15m` → `1H`).

**Danh sách API được gọi:**
| Node | Endpoint | Mô tả |
|------|----------|-------|
| `24h Stats` | `/api/v5/market/ticker` | Giá hiện thời, open/close 24h, volume |
| `Order Book Depth` | `/api/v5/market/books` | Bảng lệnh (bid/ask) |
| `Price (Latest)` | `/api/v5/market/ticker` | Giá hiện thời |
| `Best Bid/Ask` | `/api/v5/market/ticker` | Best bid/ask |
| `Klines (Candles)` | `/api/v5/market/candles` | Candle (OHLCV) |
| `Average / Mark Price` | `/api/v5/market/mark-price` | Giá trung bình (mark price) |
| `Recent Trades` | `/api/v5/market/trades` | Giao dịch gần đây |

**Ví dụ cấu hình `Klines (Candles)`:**
```json
{
  "method": "GET",
  "url": "https://www.okx.com/api/v5/market/candles",
  "parameters": {
    "instId": "BTC-USDT",
    "bar": "15m",
    "limit": 20
  }
}
```

##### **6. Node: `Splits message is more than 4000 characters`**
- **Chức năng**: Nếu báo cáo quá **4000 ký tự**, node này sẽ **chia nhỏ thành nhiều phần** để Telegram không bị lỗi.
- **Không cần sửa**, nhưng nếu muốn **tùy chỉnh ngưỡng**, mở node **Code** và thay đổi:
  ```javascript
  const maxLength = 4000; // Thay đổi nếu cần
  ```

##### **7. Node: `Telegram sendMessage`**
- **Chức năng**: Gửi báo cáo cuối cùng về Telegram.
- **Cấu hình**:
  - **Chat ID**: `$input.all().telegram.message.chat.id` (tự động lấy từ trigger).
  - **Message**: Dữ liệu định dạng từ GPT-4o.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi lệnh `/okx` đến bot Telegram.
   - Kiểm tra **Log** trong n8n để xem workflow có chạy không.
2. **Bật Active**:
   - Chọn **Active** ở góc trên bên phải của workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Thêm nhiều cặp giao dịch**:
   - Sửa node `OKX AI Agent` để lấy dữ liệu cho **ETH-USDT, SOL-USDT, DOGE-USDT**...
   - Ví dụ:
     ```javascript
     const symbols = ["BTC-USDT", "ETH-USDT", "SOL-USDT"];
     ```

2. **Kết hợp với Slack/Email**:
   - Thay node `Telegram sendMessage` bằng `Slack Webhook` hoặc `Email Node`.

3. **Lưu log vào Google Sheets**:
   - Thêm node `Google Sheets` sau `Telegram sendMessage` để lưu dữ liệu lịch sử.

4. **Cảnh báo giá đột biến**:
   - Sử dụng node `Calculator` để tính **% thay đổi** và gửi cảnh báo nếu giá biến động >5%.

5. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow mỗi **15 phút/1 giờ**.

6. **Tùy chỉnh prompt GPT-4o**:
   - Mở node `OpenAI Chat Model` và thay đổi **prompt** để GPT-4o phân tích sâu hơn (ví dụ: đề xuất chiến lược giao dịch).
   - Ví dụ:
     ```json
     {
       "role": "user",
       "content": "Analyze this OKX data and suggest trading signals. Focus on BTC-USDT."
     }
     ```
:::

---
## 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa việc theo dõi thị trường Spot OKX**, tiết kiệm thời gian và giảm thiểu lỗi. Với **GPT-4o**, dữ liệu được định dạng tự động, và **Telegram Bot** giúp nhận báo cáo ngay trên điện thoại.

**🚀 Bắt đầu ngay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá trên).
2. **Import workflow** và cấu hình credentials.
3. **Gửi lệnh `/okx`** và bắt đầu theo dõi thị trường **một cách thông minh!**

---
**🔗 Tài liệu tham khảo:**
- [OKX API Documentation](https://www.okx.com/docs-v5/en/)
- [n8n Workflow Original](https://n8n.io/workflows/8609)
- [GPT-4o API Guide](https://platform.openai.com/docs/models/gpt-4o)