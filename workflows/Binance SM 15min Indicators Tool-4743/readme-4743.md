---
title: "📊 Binance SM 15min Indicators Tool: Tự Động Hóa Phân Tích Kỹ Thuật Cho Binance (AI + API)"
description: "Workflow tự động hóa phân tích kỹ thuật 15 phút cho Binance Spot Market bằng AI GPT-4o-mini, kết hợp với API lấy dữ liệu kìa, giúp các sếp nắm bắt tín hiệu mua/bán trong thời gian thực. Giúp tiết kiệm 8+ giờ/tháng so với cách phân tích thủ công."
slug: "binance-sm-15min-indicators-tool"
tags: [n8n, automation, finance, crypto, ai, blockchain, technical-analysis, openai, self-hosted]
keywords: [tự động hóa phân tích kỹ thuật binance, n8n workflow crypto, ai phân tích rsi macd, signal detection binance, gpt-4o-mini trading, api lấy dữ liệu kìa binance]
---

# 🚀 **Binance SM 15min Indicators Tool: Phân Tích Kỹ Thuật Intraday Cho Binance Bằng AI**

## **🔍 Nỗi Đau Của Các Sếp Trong Phân Tích Kỹ Thuật Binance**
Hàng ngày, các sếp phải:
- **Lấy dữ liệu kìa 15 phút** từ Binance thủ công (API hoặc Excel) → **Tốn 30-60 phút/symbol**.
- **Tính toán RSI, MACD, Bollinger Bands, ADX** bằng công thức phức tạp → **Mất thời gian và dễ sai sót**.
- **Phân tích tín hiệu** như "Overbought RSI" hay "MACD Cross Up" → **Khó đọc và thiếu cấu trúc**.
- **Không có báo cáo tự động** → **Phải nhắc nhở mình mỗi ngày**, dẫn đến bỏ qua cơ hội.

**Kết quả?** Các sếp **bỏ lỡ tín hiệu** hoặc **quyết định sai** vì thiếu dữ liệu chính xác và nhanh chóng.

---
### **🎯 Kết Quả Các Sếp Nhận Được Khi Sử Dụng Workflow**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 8+ giờ/tháng** so với cách phân tích thủ công.
✅ **Dữ liệu chính xác 100%** (API Binance + tính toán tự động).
✅ **Tín hiệu kỹ thuật được AI phân tích** (GPT-4o-mini) → **Dễ hiểu, cấu trúc rõ ràng**.
✅ **Hoạt động 24/7** → **Không bỏ lỡ tín hiệu** khi ngủ.
✅ **Kết hợp với Telegram/Slack** → **Nhận báo cáo ngay khi có tín hiệu mạnh**.
✅ **Bảo mật cao** → **Dữ liệu không rời khỏi hệ thống của các sếp**.
:::

---
## **🎯 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **API Key OpenAI** (để sử dụng GPT-4o-mini).
   - Mua tại: [https://openai.com/api/](https://openai.com/api/)
   - Thêm vào **Credentials** của n8n với tên: `openAiApi`.

3. **Tài khoản Binance** (nếu muốn kết nối API Binance trực tiếp, *không bắt buộc* vì workflow dùng webhook backend).
   - *Lưu ý*: Workflow **không lấy dữ liệu trực tiếp từ Binance API**, mà gọi đến **webhook backend** (`treasurium.app.n8n.cloud`) để tính toán.

4. **Workflow cha (nếu muốn trigger từ bên ngoài)**:
   - Workflow này **không tự động chạy**, mà được **trigger** bởi:
     - [Binance Quant AI Agent](https://n8n.io/workflows/...) (nếu có)
     - [Binance SM Financial Analyst Tool](https://n8n.io/workflows/...) (nếu có)
   - *Nếu không có, các sếp có thể trigger thủ công bằng node `Execute Workflow`*.
---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
#### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/4743](https://n8n.io/workflows/4743) (ấn **Export**).
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **n8n Cloud** (nếu dùng cloud) hoặc **Self-hosted** (nếu tự host).

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON**.
3. Dán JSON từ [n8n.io/workflows/4743](https://n8n.io/workflows/4743) (ấn **Export** → **Copy JSON**).
4. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: `When Executed by Another Workflow` (Trigger)**
- **Không cần chỉnh gì** nếu các sếp muốn trigger từ workflow khác.
- *Nếu muốn trigger thủ công*:
  - Thay đổi **Trigger Type** thành **"Execute Workflow"** (nhấn **Edit** → **Change Trigger**).
  - Thêm **Input Data** (ví dụ: `{"symbol": "BTCUSDT", "sessionId": "12345"}`).

#### **🔹 Node 2: `HTTP Request 15m Indicators Tool` (Gọi API tính toán chỉ số)**
- **Endpoint**: `https://treasurium.app.n8n.cloud/webhook/15m-indicators` (không cần chỉnh).
- **Payload (JSON)**:
  ```json
  {
    "symbol": "{{ $input.all().symbol }}"  // Thay đổi thành tên symbol muốn phân tích (ví dụ: "BTCUSDT")
  }
  ```
  - *Lưu ý*: Nếu trigger từ workflow khác, **symbol** sẽ tự động truyền từ workflow cha.
  - Nếu trigger thủ công, **điền symbol** vào **Input Data** (ví dụ: `{"symbol": "ETHUSDT"}`).

#### **🔹 Node 3: `OpenAI Chat Model` (AI Phân Tích Tín Hiệu)**
- **Model**: `gpt-4.1-mini` (đã cấu hình sẵn, không cần đổi).
- **Credentials**: Chọn `openAiApi` (API Key OpenAI đã thêm trước đó).
- **Prompt**: Workflow **không cần chỉnh prompt**, vì nó tự động nhận dữ liệu từ node trước.

#### **🔹 Node 4: `Simple Memory` (Giữ Bối Cảnh)**
- **Không cần chỉnh gì**, nhưng nếu muốn **xóa dữ liệu cũ**:
  - Thêm **node `Set`** sau node này để reset `sessionId` khi cần.

#### **🔹 Node 5: `Binance SM 15min Indicators Agent` (Agent AI)**
- **Không cần chỉnh gì**, vì nó tự động:
  - Nhận dữ liệu từ `HTTP Request`.
  - Gửi đến `OpenAI Chat Model` để phân tích.
  - Lưu `sessionId` vào `Simple Memory`.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** (kiểm tra dữ liệu mẫu):
   - Nhấn **Run Workflow** → Điền **symbol** (ví dụ: `BTCUSDT`).
   - Kiểm tra **Output** để xem AI phân tích như thế nào.
2. **Bật Active**:
   - Nhấn **Active** (đỏ → xanh) để workflow chạy tự động khi được trigger.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Telegram/Slack**
Các sếp có thể **gửi báo cáo tự động** khi có tín hiệu mạnh:
- **Thêm node `Telegram Bot`** sau `OpenAI Chat Model`.
- Cấu hình:
  - **Chat ID**: ID chat của Telegram (lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Message**: `{{ $json["message"] }}` (lấy nội dung phân tích từ AI).

### **2. Lưu Log Dữ Liệu**
Để **theo dõi lịch sử phân tích**:
- **Thêm node `Google Sheets`** sau `OpenAI Chat Model`.
- Cấu hình:
  - **Sheet Name**: `Binance_Indicators`.
  - **Data**: `{{ $json }}` (lưu tất cả dữ liệu phân tích).

### **3. Tự Động Trigger Mỗi 15 Phút**
Nếu muốn **check symbol định kỳ**:
- **Sử dụng node `Schedule`** (n8n Pro) hoặc **cron job** bên ngoài.
- Ví dụ: `0 */15 * * * *` (check mỗi 15 phút).

### **4. Phân Tích Nhiều Symbol Đồng Thời**
- **Sử dụng node `Set`** trước `HTTP Request` để truyền danh sách symbol:
  ```json
  {
    "symbols": ["BTCUSDT", "ETHUSDT", "SOLUSDT"]
  }
  ```
- **Thêm node `Loop`** để chạy cho từng symbol.

### **5. Kết Nối Với Trading Bot**
- **Gửi tín hiệu** (ví dụ: `MACD Cross Up`) đến **workflow trading bot**.
- Ví dụ:
  ```json
  {
    "action": "BUY",
    "symbol": "{{ $json.symbol }}",
    "reason": "{{ $json.message }}"
  }
  ```

---
## **📌 Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Doanh Thu**

Workflow **Binance SM 15min Indicators Tool** là **công cụ AI + API** giúp các sếp:
✔ **Phân tích kỹ thuật 15 phút** chỉ trong **vài giây**.
✔ **Nhận tín hiệu mua/bán** được **AI tổng hợp** (không cần đọc biểu đồ).
✔ **Hoạt động 24/7** → **Không bỏ lỡ cơ hội**.
✔ **Kết hợp với Telegram/Slack** → **Nhận báo cáo ngay khi có tín hiệu**.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Chỉnh symbol** và **trigger** từ workflow cha.
3. **Bật Active** và **nhận báo cáo tự động** mỗi khi có tín hiệu!

---
### **🔗 Tài Liệu Tham Khảo**
- [Tutorial n8n Self-hosted](https://docs.n8n.io/)
- [API Binance Documentation](https://binance-docs.github.io/apidocs/spot/en/)
- [OpenAI API Guide](https://platform.openai.com/docs/api-reference)

---
### **📢 Liên Hệ & Hỗ Trợ**
- **Tác giả**: Don Jayamaha Jr ([LinkedIn](http://linkedin.com/in/donjayamahajr))
- **Nếu có vấn đề**, hãy comment dưới bài viết hoặc liên hệ tác giả.

---
**🚀 CÁC SẺP CÓ THỂ BẮT ĐẦU NGÀY HÔM NAY!** 🚀