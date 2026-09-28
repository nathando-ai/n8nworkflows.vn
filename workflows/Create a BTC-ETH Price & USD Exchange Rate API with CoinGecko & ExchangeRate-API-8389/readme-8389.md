---
title: "🚀 Tạo API BTC-ETH + Tỷ Giá Hối Độ USD→EUR/USD→NGN Tự Động Hóa (CoinGecko + ExchangeRate-API)"
description: "Workflow tự động hóa lấy giá BTC/ETH 24h + tỷ giá ngoại tệ USD→EUR/USD→NGN, trả về JSON sạch trong 10 giây. Giúp doanh nghiệp crypto/finance có API nhanh chóng, không cần code backend."
slug: "tao-api-btc-eth-ty-gia-usd-eur-ngn-coingecko-exchange-api"
tags: [n8n, automation, crypto-trading, api-development, no-code]
keywords: [n8n workflow crypto, tự động hóa API giá crypto, tỷ giá ngoại tệ tự động, API BTC ETH, CoinGecko API, ExchangeRate-API]
---

# 🚀 **API Crypto + FX Micro: Lấy Giá BTC/ETH + Tỷ Giá USD→EUR/USD→NGN Trong 10 Giây**

### **Nỗi Đau Của Các Sếp**
Các sếp trong lĩnh vực **crypto, trading, hoặc fintech** thường phải:
- **Tìm kiếm thủ công** giá BTC/ETH và tỷ giá ngoại tệ từ nhiều nguồn khác nhau.
- **Chờ đợi lâu** khi phải gọi API từ nhiều dịch vụ khác nhau (CoinGecko, ExchangeRate-API...).
- **Không có API riêng** để tích hợp vào ứng dụng của mình, phải phụ thuộc vào các API công khai có giới hạn gọi.
- **Mất thời gian** để xây dựng backend để lấy dữ liệu và trả về JSON sạch.

**Workflow này giải quyết tất cả!** Nó tự động hóa việc lấy **giá BTC/ETH + tỷ giá USD→EUR/USD→NGN** từ 2 API uy tín và trả về **JSON sạch** trong **10 giây**, chỉ với **một request GET đơn giản**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **API riêng** để tích hợp vào ứng dụng của bạn (không phụ thuộc vào API công khai).
- **Dữ liệu chính xác** từ CoinGecko (giá crypto) và ExchangeRate-API (tỷ giá ngoại tệ).
- **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
- **Hoạt động liên tục 24/7** trên VPS của bạn (self-hosted).
- **JSON sạch** với cấu trúc thống nhất, dễ tích hợp vào frontend/backend.
- **Miễn phí** (n8n Community Edition) hoặc **rẻ** (n8n Enterprise).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản API từ 2 dịch vụ**:
   - [CoinGecko API](https://www.coingecko.com/en/api) (miễn phí, cần **API Key**).
   - [ExchangeRate-API](https://www.exchangerate-api.com/) (miễn phí cho 1000 request/ngày, cần **API Key**).
2. **VPS hoặc máy chủ** để chạy n8n (self-hosted) để workflow hoạt động 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
3. **Cài đặt n8n** trên VPS (hướng dẫn [đây](https://docs.n8n.io/hosting/installation/)).
4. **Thiết lập Webhook** trong n8n với **path = `crypto-fx`** và **HTTP Method = GET**.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8389) (chọn "Export").
- **Copy JSON** từ [dưới đây](https://gist.githubusercontent.com/...) (nếu có).
- **Paste vào n8n Editor** và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình như sau:

| **Node**               | **Loại Node**       | **Cấu Hình Cần Thiết**                                                                 | **Lưu Ý**                                                                                     |
|------------------------|---------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Webhook**            | `n8n-nodes-base.webhook` | - **Path**: `crypto-fx` <br> - **HTTP Method**: `GET` <br> - **Credentials**: Không cần | Nếu không có Webhook, workflow sẽ không nhận được request.                                |
| **Get Fiat Exchange Rates** | `n8n-nodes-base.httpRequest` | - **URL**: `https://v6.exchangerate-api.com/v6/YOUR_API_KEY/latest/USD` <br> - **Headers**: `Accept: application/json` | Thay `YOUR_API_KEY` bằng API Key từ [ExchangeRate-API](https://www.exchangerate-api.com/). |
| **Get Crypto Prices**  | `n8n-nodes-base.httpRequest` | - **URL**: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin%2Cethereum&vs_currencies=usd&api_key=YOUR_API_KEY` <br> - **Headers**: `Accept: application/json` | Thay `YOUR_API_KEY` bằng API Key từ [CoinGecko](https://www.coingecko.com/en/api).          |
| **Merge**              | `n8n-nodes-base.merge` | - **Merge by**: `$` (default)                                                                 | Kết hợp dữ liệu từ 2 node HTTP Request.                                                     |
| **Build JSON**         | `n8n-nodes-base.code` | - **Code**: Sử dụng template dưới đây (không cần chỉnh sửa nếu import từ file JSON). | Node này chuyển đổi dữ liệu thành JSON sạch.                                               |
| **Respond**            | `n8n-nodes-base.respondToWebhook` | - **Response Type**: `JSON`                                                                 | Trả về JSON cho client gọi API.                                                             |

**Mẫu Code trong Node "Build JSON" (nếu cần chỉnh sửa):**
```javascript
// Dữ liệu đầu vào từ node Merge
const { json: { bitcoin, ethereum, rates } } = $input.all();

// Xây dựng JSON cuối cùng
const response = {
  btc: {
    price: bitcoin.usd,
    change_24h: bitcoin.usd_24h_change_percentage,
  },
  eth: {
    price: ethereum.usd,
    change_24h: ethereum.usd_24h_change_percentage,
  },
  usd_eur: rates.EUR,
  usd_ngn: rates.NGN,
  ts: new Date().toISOString(),
};

return { json: response };
```

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gọi endpoint: `https://YOUR_N8N_URL/webhook/crypto-fx` (thay `YOUR_N8N_URL` bằng URL của n8n).
   - Kết quả nên trả về JSON như ví dụ dưới đây:
     ```json
     {
       "btc": { "price": 112417, "change_24h": 1.22 },
       "eth": { "price": 4334.57, "change_24h": 1.33 },
       "usd_eur": 0.854,
       "usd_ngn": 1524.54,
       "ts": "2025-09-08T08:00:00.000Z"
     }
     ```
2. **Bật Active** workflow trong n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Log Lịch Sử**:
   - Sử dụng node **n8n-nodes-base.terminate** để lưu log vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử gọi API.
   - Cài đặt node **n8n-nodes-base.googleSheets** và cấu hình để ghi dữ liệu mỗi khi workflow chạy.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để gửi báo cáo giá crypto và tỷ giá hàng ngày qua email/Slack.
   - Ví dụ: Gửi báo cáo lúc 8h sáng hàng ngày với dữ liệu từ ngày hôm trước.

3. **Cập Nhật Tự Động**:
   - Sử dụng **n8n-nodes-base.set** để lưu trữ dữ liệu gần nhất vào **n8n Database** hoặc **n8n Credentials**, tránh gọi API liên tục.

4. **Tích Hợp Với Telegram/Slack**:
   - Khi giá BTC/ETH thay đổi đột biến (>5%), gửi thông báo ngay qua **Telegram** hoặc **Slack**.
   - Sử dụng node **n8n-nodes-base.telegram** hoặc **n8n-nodes-base.slack**.

5. **Bảo Mật API Key**:
   - Đặt **API Key** của CoinGecko và ExchangeRate-API vào **n8n Credentials** thay vì hardcode trong node.
   - Hướng dẫn: [Sử dụng Credentials trong n8n](https://docs.n8n.io/integrations/credentials/).
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tạo API riêng** để lấy **giá BTC/ETH + tỷ giá USD→EUR/USD→NGN** một cách **tự động hóa, nhanh chóng và không cần code backend**. Bằng cách chạy trên **VPS**, workflow sẽ hoạt động **liên tục 24/7**, cung cấp dữ liệu chính xác cho ứng dụng của bạn.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình API Key.
3. **Test API** và tích hợp vào ứng dụng của bạn.

**Nếu cần hỗ trợ**, liên hệ tác giả David Olusola qua email: **david@daexai.com** hoặc tham khảo [n8n Community](https://community.n8n.io/).

---
🚀 **Chúc các sếp thành công với dự án tự động hóa API của mình!** 🚀