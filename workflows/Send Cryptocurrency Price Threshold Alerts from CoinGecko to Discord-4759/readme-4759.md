---
title: "🚀 Tự Động Hóa Cảnh Báo Giá Crypto Trên Discord Từ CoinGecko (Không Cần Code)"
description: "Workflow này tự động theo dõi giá cryptocurrency từ CoinGecko và gửi cảnh báo tức thời lên Discord khi giá vượt ngưỡng cao/ thấp mà bạn thiết lập. Giúp các sếp đầu tư không bỏ lỡ cơ hội hoặc tránh rủi ro mất mát."
slug: "tieu-dong-hoa-can-bo-gia-crypto-coingecko-discord"
tags: [n8n, automation, crypto, discord, coinGecko, finance]
keywords: [tự động hóa crypto, cảnh báo giá crypto, n8n workflow, discord alert, coinGecko api, đầu tư thông minh]
---

# 🚀 **Tự Động Hóa Cảnh Báo Giá Crypto Trên Discord (Không Cần Code)**

### **Giải quyết vấn đề gì?**
Các sếp đầu tư crypto thường phải **thường xuyên theo dõi giá** trên nhiều sàn giao dịch, lo lắng bỏ lỡ cơ hội mua rẻ hoặc bán đắt. Thậm chí, phải **đăng ký nhiều alert trên nhiều nền tảng** (Binance, CoinGecko, TradingView...) và quản lý chúng một cách thủ công. Kết quả là:
❌ **Thời gian bị lãng phí** trên việc kiểm tra giá liên tục.
❌ **Rủi ro bỏ lỡ cơ hội** vì không được thông báo kịp thời.
❌ **Phức tạp** khi phải kết nối nhiều nền tảng khác nhau.

**Workflow này giải quyết tất cả đó!** Nó **tự động theo dõi giá crypto** từ CoinGecko và **gửi cảnh báo tức thời lên Discord** khi giá vượt ngưỡng cao/ thấp mà bạn thiết lập. **Không cần code, chỉ cần cấu hình vài bước đơn giản.**

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian** lên đến **80%** trong việc theo dõi giá crypto.
- **Không bỏ lỡ cơ hội** với cảnh báo tức thời khi giá đạt ngưỡng mục tiêu.
- **Cảnh báo cá nhân hóa** với thông tin chi tiết (giá hiện tại, biến động, thời gian).
- **Hoạt động liên tục 24/7** (không cần phải mở app hoặc website).
- **Kết nối với Discord** để nhận thông báo ngay trên nhóm chat yêu thích.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản CoinGecko API** (miễn phí, [đăng ký tại đây](https://www.coingecko.com/en/api)).
2. **Bot Discord** (để gửi thông báo):
   - Tạo bot trên [Discord Developer Portal](https://discord.com/developers/applications).
   - Nhận **Webhook URL** từ nhóm Discord muốn nhận cảnh báo.
3. **Tài khoản n8n** (self-hosted hoặc dùng miễn phí trên [n8n.cloud](https://n8n.io/)).
4. **Giá trị ngưỡng** (giá thấp và giá cao) cho coin muốn theo dõi.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
1. **Tải workflow** từ [n8n.io/workflows/4759](https://n8n.io/workflows/4759).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn "Import from URL"** và dán link trên.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **8 node chính**, các sếp cần cấu hình như sau:

##### **A. Cấu hình Trigger (Bắt đầu workflow)**
- **Lựa chọn giữa 2 cách kích hoạt:**
  - **Manual Trigger** (nút "Run Workflow" để chạy thủ công).
  - **Schedule Trigger** (đặt lịch chạy tự động, ví dụ: **mỗi 1 giờ**).
  - *Gợi ý:* Đặt **Schedule Trigger** để workflow chạy tự động (không cần nhấn nút).

##### **B. Cấu hình CoinGecko (Lấy giá crypto)**
- **Node "CoinGecko"** (type: `coinGecko`):
  - **Operation:** Chọn `market` (lấy dữ liệu thị trường).
  - **Credentials:** Điền **API Key** từ CoinGecko (đăng ký miễn phí).
  - **Parameters:**
    - `vs_currency`: Chọn `usd` (hoặc `vnd` nếu muốn giá tiền Việt).
    - `id`: Nhập **tên coin** (ví dụ: `bitcoin`, `ethereum`, `solana`).
    - *Lưu ý:* Các sếp có thể **thay đổi coin** bằng cách chỉnh `id` trong node này.

##### **C. Thiết lập ngưỡng giá (Low & High)**
- **Node "Set Low and High"** (type: `set`):
  - **Giá thấp (Low):** Nhập giá **mua** (ví dụ: `15.000.000 VND`).
  - **Giá cao (High):** Nhập giá **bán** (ví dụ: `20.000.000 VND`).
  - *Lưu ý:* Giá này sẽ được so sánh với giá hiện tại từ CoinGecko.

##### **D. Logic kiểm tra biến động**
- **Node "Check movement"** (type: `if`):
  - **Condition:** So sánh giá hiện tại với ngưỡng `Low` và `High`.
  - *Cấu hình:*
    - `{{ $json["price_usd"] }} > {{ $json["high"] }}` → Trả về `true` nếu giá cao hơn ngưỡng.
    - `{{ $json["price_usd"] }} < {{ $json["low"] }}` → Trả về `true` nếu giá thấp hơn ngưỡng.

- **Node "Check Direction"** (type: `if`):
  - **Condition:** Xác định **giá tăng** (`High`) hay **giá giảm** (`Low`).
  - *Cấu hình:*
    - `{{ $json["price_usd"] }} > {{ $json["high"] }}` → Chạy nhánh `High`.
    - `{{ $json["price_usd"] }} < {{ $json["low"] }}` → Chạy nhánh `Low`.

##### **E. Gửi cảnh báo lên Discord**
- **Node "Message High"** và **"Message Low"** (type: `discord`):
  - **Credentials:** Chọn **discordBotApi** (cấu hình trước khi import).
  - **Webhook URL:** Nhập **Webhook URL** từ nhóm Discord.
  - **Message Content:** Cấu hình nội dung cảnh báo (ví dụ):
    ```
    **🚨 ALERT: Giá {{ $json["coin"] }} đã vượt ngưỡng HIGH!**
    - Giá hiện tại: **{{ $json["price_usd"] }} VND**
    - Ngưỡng cao: **{{ $json["high"] }} VND**
    - Thời gian: **{{ $json["timestamp"] }}**
    ```
  - *Lưu ý:* Các sếp có thể **thay đổi nội dung** để phù hợp với nhóm Discord.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra logic.
   - Kiểm tra **Discord** xem có nhận được cảnh báo không.
2. **Bật Active Workflow** nếu test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm nhiều coin** vào workflow:
   - Sử dụng **loop** (node `set`) để lấy giá của nhiều coin khác nhau.
   - Ví dụ: `bitcoin`, `ethereum`, `solana` trong cùng một workflow.
2. **Lưu lịch sử cảnh báo** vào **Google Sheets/Excel**:
   - Thêm node `googleSheets` để ghi lại tất cả cảnh báo.
   - Dễ dàng **tổng hợp báo cáo** về biến động giá.
3. **Kết nối với Telegram**:
   - Thay vì Discord, các sếp có thể sử dụng **Telegram Bot** để nhận cảnh báo.
   - Cấu hình node `telegram` thay vì `discord`.
4. **Tự động gửi email cảnh báo**:
   - Thêm node `email` (ví dụ: Gmail) để gửi cảnh báo qua email.
5. **Cảnh báo với âm thanh**:
   - Kết hợp với **IFTTT** hoặc **Zapier** để phát âm thanh khi có cảnh báo.
:::

---

### 📌 **Kết luận**
Workflow này **giúp các sếp đầu tư crypto tự động hóa cảnh báo giá**, tiết kiệm thời gian và **không bỏ lỡ cơ hội**. **Không cần code**, chỉ cần **cấu hình vài bước đơn giản** và workflow sẽ hoạt động **liên tục 24/7**.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/4759](https://n8n.io/workflows/4759).
2. **Cấu hình CoinGecko API** và **Discord Webhook**.
3. **Đặt lịch chạy tự động** và **nhận cảnh báo tức thời**!

**🎁 Bonus:** Các sếp có thể **tăng cường workflow** bằng cách thêm **nhiều coin**, **lưu log** hoặc **kết nối với Telegram** để đa dạng hóa cảnh báo.

**Chúc các sếp đầu tư thành công!** 🚀💰