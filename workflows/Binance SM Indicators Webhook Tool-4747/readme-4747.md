---
title: "📈 **Binance SM Indicators Webhook Tool – Tự Động Hóa Tính Toán Chỉ Số Kỹ Thuật Binance 100% Không Code**"
description: "Workflow tự động hóa lấy dữ liệu k-line từ Binance và tính toán 6 chỉ số kỹ thuật (RSI, MACD, Bollinger Bands, SMA, EMA, ADX) cho 4 thời gian khung (15m, 1h, 4h, 1d) qua Webhook. Giúp các nhà đầu tư và bot trading tiết kiệm thời gian, tăng độ chính xác và tự động hóa hoàn toàn quy trình phân tích."
slug: "binance-sm-indicators-webhook-tool"
tags: [n8n, automation, blockchain, trading-bot, technical-analysis, finance]
keywords: [n8n workflow Binance, tự động hóa chỉ số kỹ thuật, RSI MACD Bollinger Bands, SMA EMA ADX, webhook trading, API Binance tự động]
---

# 🚀 **Binance SM Indicators Webhook Tool – Tự Động Hóa Chỉ Số Kỹ Thuật Cho Bot Trading**

## **🔍 Giới Thiệu: Tại Sao Các Sếp Cần Workflow Này?**
Hiện nay, việc phân tích thị trường crypto thủ công bằng các chỉ số kỹ thuật như **RSI, MACD, Bollinger Bands, SMA, EMA, ADX** là một quá trình **tốn thời gian, dễ sai sót** và **không thể hoạt động 24/7**. Các sếp thường phải:
- **Lấy dữ liệu k-line** từ Binance thủ công (hoặc qua API) và tính toán từng chỉ số một.
- **Sao chép dữ liệu** giữa các sheet Excel/Google Sheets để so sánh.
- **Đợi kết quả** từ các công cụ phân tích bên thứ ba (thường có phí).
- **Không thể tự động hóa** khi thị trường thay đổi đột ngột.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động lấy dữ liệu k-line** từ Binance theo 4 thời gian khung (15m, 1h, 4h, 1d).
✅ **Tính toán 6 chỉ số kỹ thuật** (RSI, MACD, Bollinger Bands, SMA, EMA, ADX) **một cách chính xác và nhanh chóng**.
✅ **Trả về kết quả dưới dạng JSON** để các bot trading hoặc hệ thống phân tích khác sử dụng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tính toán thủ công hoặc sao chép dữ liệu giữa các công cụ.
- **Chính xác 100%**: Dữ liệu lấy trực tiếp từ API Binance, không bị lỗi nhân bản.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào máy tính cá nhân.
- **Tích hợp dễ dàng**: Kết quả JSON có thể được sử dụng cho **bot trading, Telegram/Slack alert, Google Sheets, hoặc các workflow n8n khác**.
- **Tương thích với nhiều thời gian khung**: Đa dạng từ **15 phút đến 1 ngày**, phù hợp với mọi chiến lược trading.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản Binance** (API Key không bắt buộc vì sử dụng API công khai, nhưng có thể cần cho các tính năng nâng cao).
2. **n8n Self-hosted** (không thể chạy trên n8n Cloud vì cần Webhook riêng).
3. **VPS** (để workflow chạy 24/7). 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
4. **Khả năng gửi POST request** từ các bot hoặc workflow khác để kích hoạt tính toán chỉ số.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4747](https://n8n.io/workflows/4747).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **4 Webhook riêng biệt** cho từng thời gian khung:
| **Webhook Path**               | **Thời Gian Khung** | **Mô Tả**                          |
|----------------------------------|---------------------|-------------------------------------|
| `39cc366c-af5f-472a-9d48-bbe30a4fe3ea` | 15 phút            | Dùng để tính toán chỉ số cho 15m.  |
| `78948764-5cdb-4808-8ef9-2155f10dd721` | 1 giờ              | Dùng để tính toán chỉ số cho 1h.    |
| `55fd9665-ed4a-4e1a-8062-890cad0fb6ac` | 4 giờ              | Dùng để tính toán chỉ số cho 4h.    |
| `23c8ec04-5aec-49c6-9c2c-c352ccec11b4` | 1 ngày             | Dùng để tính toán chỉ số cho 1d.    |

#### **Cấu Hình Cần Thay Đổi:**
1. **Node `HTTP Request` (lấy dữ liệu k-line từ Binance):**
   - **URL:** `https://api.binance.com/api/v3/klines`
   - **Headers:** Thêm `X-MBX-APIKEY` (nếu cần) hoặc để trống (API công khai).
   - **Query Parameters:**
     ```json
     {
       "symbol": "{{$node["Extract Symbol"].json["symbol"]}}",
       "interval": "{{$node["Webhook 15m Indicators"].path.split('-')[0]}}m" // hoặc "1h", "4h", "1d"
     }
     ```
   - **Lưu ý:** Các node `HTTP Request` đã được cấu hình sẵn cho từng thời gian khung, nhưng các sếp nên kiểm tra lại **symbol** và **interval** để phù hợp với chiến lược trading.

2. **Node `Webhook` (để các bot gọi):**
   - **Không cần thay đổi gì** vì các Webhook đã được cấu hình với **path** riêng biệt.
   - **Khi gọi Webhook**, các sếp phải gửi **payload JSON** như sau:
     ```json
     {
       "symbol": "BTCUSDT" // hoặc BNBUSDT, ETHUSDT, etc.
     }
     ```
   - **Ví dụ POST request bằng cURL:**
     ```bash
     curl -X POST \
     https://[DOMAIN_N8N]/webhook/39cc366c-af5f-472a-9d48-bbe30a4fe3ea \
     -H "Content-Type: application/json" \
     -d '{"symbol": "BTCUSDT"}'
     ```

3. **Node `Code` (tính toán chỉ số):**
   - **Không cần chỉnh sửa** vì logic tính toán đã được tối ưu hóa.
   - Các chỉ số được tính toán bao gồm:
     - **RSI (Relative Strength Index)**
     - **MACD (Moving Average Convergence Divergence)**
     - **Bollinger Bands**
     - **SMA (Simple Moving Average)**
     - **EMA (Exponential Moving Average)**
     - **ADX (Average Directional Index)**

4. **Node `Merge` (trả về kết quả):**
   - **Không cần chỉnh sửa**, nó sẽ tự động gộp tất cả chỉ số thành một JSON duy nhất.

### **3. Kích Hoạt ⚡️**
- **Test run** với một **symbol** như `BTCUSDT` để đảm bảo workflow hoạt động.
- **Bật Active workflow** sau khi kiểm tra thành công.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Kết hợp với Telegram/Slack Alert:**
   - Sau khi workflow trả về kết quả, các sếp có thể **gửi thông báo** qua Telegram/Slack khi chỉ số đạt ngưỡng nhất định (ví dụ: RSI > 70 hoặc MACD cross bullish).
   - **Cách làm:** Sử dụng node `slack` hoặc `telegram` sau node `Respond to Webhook`.

2. **Lưu log vào Google Sheets/Notion:**
   - Các sếp có thể **lưu dữ liệu chỉ số** vào Google Sheets để theo dõi lịch sử.
   - **Cách làm:** Sử dụng node `googleSheets` và cấu hình để ghi dữ liệu từ `Respond to Webhook`.

3. **Tích hợp với Bot Trading:**
   - Kết quả JSON từ workflow có thể được **đọc bởi bot trading** (ví dụ: bot Python sử dụng `requests` để gọi Webhook).
   - **Ví dụ mã Python:**
     ```python
     import requests

     def get_binance_indicators(symbol, interval):
         url = f"https://[DOMAIN_N8N]/webhook/{interval}-indicators"
         payload = {"symbol": symbol}
         response = requests.post(url, json=payload)
         return response.json()

     # Ví dụ sử dụng
     data = get_binance_indicators("BTCUSDT", "15m")
     print(data)
     ```

4. **Tự động hóa báo cáo định kỳ:**
   - Sử dụng **n8n Cron Trigger** để gọi workflow mỗi ngày/lần để lấy chỉ số và gửi báo cáo qua email.
   - **Cách làm:** Tạo một workflow mới với node `cron` → gọi Webhook của `Binance SM Indicators` → gửi email qua `smtp`.
:::

---
## **📌 Kết Luận**
Workflow **Binance SM Indicators Webhook Tool** là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa **tính toán chỉ số kỹ thuật** trên Binance mà **không cần viết code**. Với chỉ **vài bước cấu hình**, các sếp có thể:
✔ **Tiết kiệm thời gian** so với cách làm thủ công.
✔ **Tăng độ chính xác** với dữ liệu lấy trực tiếp từ API.
✔ **Hoạt động 24/7** mà không cần can thiệp.
✔ **Tích hợp dễ dàng** với bot trading, Telegram, Google Sheets, và nhiều công cụ khác.

**Hãy áp dụng ngay workflow này và nâng cao hiệu quả phân tích thị trường của mình!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Tài liệu chính thức n8n](https://docs.n8n.io/)
- [API Binance Kline](https://binance-docs.github.io/apidocs/spot/en/#kline-candlestick-data)
- [Cách tự host n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-premise/)