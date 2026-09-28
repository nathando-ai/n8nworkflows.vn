---
title: "💰 Tự Động Cập Nhật Tỷ Giá Hối Đoái Hàng Ngày Cho Telegram (Không Code) - Dùng API Exchange Rate"
description: "Workflow tự động hóa lấy tỷ giá hối đoái từ API Exchange Rate API và gửi báo cáo hàng ngày lên Telegram, giúp các sếp Crypto Trading theo dõi thị trường 24/7 mà không cần can thiệp thủ công."
slug: "tich-hop-api-exchange-rate-telegram"
tags: [n8n, automation, crypto-trading, api-exchange-rate, telegram-bot]
keywords: [tự động hóa tỷ giá hối đoái, n8n workflow, gửi báo cáo Telegram, API Exchange Rate, crypto trading]
---

# 🚀 **Tự Động Cập Nhật Tỷ Giá Hối Đoái Hàng Ngày Cho Telegram (Không Code)**

### **Giải quyết vấn đề gì?**
Các sếp Crypto Trading hay người đầu tư ngoại tệ thường phải **tìm kiếm tỷ giá hối đoái thủ công** hàng ngày trên các trang web như Forex, OANDA, hoặc API để theo dõi xu hướng thị trường. Điều này **tốn thời gian, dễ sai sót** và không hiệu quả khi thị trường hoạt động 24/7.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Lấy tỷ giá hối đoái từ API Exchange Rate** (hoặc API khác) theo lịch trình.
✅ **Chuẩn bị báo cáo** dưới dạng văn bản hoặc bảng tính.
✅ **Gửi báo cáo lên Telegram** mỗi ngày (hoặc theo lịch trình tùy chọn).
✅ **Không cần code** – chỉ cần cấu hình n8n trên VPS.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu tỷ giá thủ công hàng ngày.
- **Dữ liệu chính xác**: Lấy trực tiếp từ API, giảm thiểu sai sót.
- **Theo dõi thị trường 24/7**: Nhận báo cáo tự động mỗi sáng (hoặc theo lịch trình).
- **Tích hợp Telegram**: Nhận thông báo ngay trên nhóm chat hoặc cá nhân.
- **Mở rộng dễ dàng**: Có thể kết hợp với Slack, Email, hoặc lưu log vào Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key của Exchange Rate API** (hoặc API khác hỗ trợ lấy tỷ giá).
   - [Đăng ký miễn phí tại Exchange Rate API](https://www.exchangerate-api.com/) (hoặc [Fixer.io](https://fixer.io/)).
2. **Token Telegram Bot** (để gửi thông báo).
   - Hướng dẫn tạo bot: [@BotFather](https://t.me/BotFather) trên Telegram.
3. **Tham số `currency`** (ví dụ: `USD`, `EUR`, `BTC`, `JPY`).
4. **Lịch trình chạy** (ví dụ: mỗi sáng 8h hoặc theo tuần).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6185](https://n8n.io/workflows/6185).
- **Import vào n8n Editor**:
  - Mở n8n Workflow Editor → Nhấn **"Import"** → Chọn file JSON.
  - Hoặc **copy/paste JSON** từ file vào ô **"Import Workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Động cơ lịch trình)**
- **Thiết lập lịch chạy**:
  - Chọn **"Cron"** (ví dụ: `0 8 * * *` để chạy mỗi sáng 8h).
  - Hoặc chọn **"Time"** (chọn ngày giờ cụ thể).
- **Lưu ý**: Nếu muốn chạy **hàng ngày**, dùng `0 8 * * *` (8h sáng).

##### **🔹 Node 2: Set Currency (Đặt tiền tệ)**
- **Tham số `currency`**:
  - Điền mã tiền tệ cần theo dõi (ví dụ: `USD`, `EUR`, `BTC`, `JPY`).
  - Nếu muốn theo dõi **nhiều loại**, có thể chia thành nhiều workflow hoặc sử dụng **node `set`** để lưu vào biến.

##### **🔹 Node 3: Convert Currency (Lấy tỷ giá từ API)**
- **Cấu hình `httpRequest`**:
  - **Method**: `GET`
  - **URL**: `https://api.exchangerate-api.com/v4/latest/{currency}` (thay `{currency}` bằng mã tiền tệ từ Node 2).
  - **Headers**:
    - `apikey`: Điền **API Key** từ Exchange Rate API.
  - **Response Format**: Chọn **"JSON"**.
- **Lưu ý**:
  - Nếu API không trả về dữ liệu, kiểm tra **API Key** và **mã tiền tệ**.
  - Có thể thay thế API bằng [Fixer.io](https://fixer.io/) với URL: `https://data.fixer.io/api/latest?access_key={API_KEY}&symbols={currency}`.

##### **🔹 Node 4: Report: Prepare (Chuẩn bị báo cáo)**
- **Code Node**:
  - Mặc định, node này **lấy dữ liệu tỷ giá** từ Node 3 và **chuẩn bị văn bản** để gửi.
  - Nếu muốn **cải tiến**, các sếp có thể mở rộng bằng **JavaScript** để:
    - Lấy **tỷ giá trước đó** (so sánh xu hướng).
    - Thêm **biểu đồ** (nếu kết hợp với Google Sheets).
  - **Mẫu code cơ bản**:
    ```javascript
    // Lấy tỷ giá từ Node 3
    const rate = $input.all()[0].json["rates"][currency];

    // Chuẩn bị thông điệp
    return {
      json: {
        message: `💰 Tỷ giá ${currency} hôm nay: 1 ${currency} = ${rate} VND`,
        timestamp: new Date().toLocaleString()
      }
    };
    ```

##### **🔹 Node 5: Send a text message (Gửi Telegram)**
- **Cấu hình Telegram Bot**:
  - **Credentials**: Chọn `"telegramApi"` (đã cấu hình trước).
  - **Chat ID**: Điền **ID nhóm chat** hoặc **ID cá nhân** (lấy từ `@userinfobot` trên Telegram).
  - **Message**: Chọn **`json.message`** từ Node 4.
- **Lưu ý**:
  - Nếu muốn **gửi hình ảnh/bảng**, có thể kết hợp với **Google Sheets** hoặc **Markdown**.
  - Ví dụ gửi **bảng tỷ giá**:
    ```markdown
    # Tỷ giá hôm nay
    | Tiền tệ | Tỷ giá (VND) |
    |----------|--------------|
    | USD      | 23,500       |
    | EUR      | 25,000       |
    ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Run Workflow"** để kiểm tra.
   - Kiểm tra **Telegram Bot** có nhận được thông báo không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật "Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Google Sheets**:
   - Thay thế Node 4 bằng **Google Sheets** để lưu lịch sử tỷ giá.
   - Cấu hình **node `googleSheets`** để ghi dữ liệu vào sheet.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `scheduleTrigger`** với **lịch trình khác** (ví dụ: mỗi tuần).
   - Ví dụ: `0 9 * * 1` (chạy mỗi thứ 2 lúc 9h sáng).

3. **Tích hợp Slack**:
   - Thay thế **Telegram** bằng **Slack Webhook** để gửi báo cáo lên Slack.

4. **Lưu log vào Database**:
   - Sử dụng **node `database`** (MySQL/PostgreSQL) để lưu lịch sử tỷ giá.

5. **Cảnh báo khi tỷ giá thay đổi đột ngột**:
   - Sử dụng **node `code`** để so sánh tỷ giá hôm nay vs hôm qua.
   - Nếu khác biệt >5%, gửi **thông báo ưu tiên** lên Telegram/Slack.

---

### 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa việc theo dõi tỷ giá hối đoái**, tiết kiệm thời gian và giảm thiểu sai sót. **Không cần code**, chỉ cần cấu hình n8n trên VPS và kết nối với API + Telegram.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/6185](https://n8n.io/workflows/6185).
2. **Cấu hình API Key** và **Telegram Bot**.
3. **Bật Active** và theo dõi thị trường 24/7!

---
**💡 Cần hỗ trợ?**
- Hỏi đáp trên [Community n8n](https://community.n8n.io/).
- Liên hệ admin VPS nếu gặp vấn đề về hạ tầng.