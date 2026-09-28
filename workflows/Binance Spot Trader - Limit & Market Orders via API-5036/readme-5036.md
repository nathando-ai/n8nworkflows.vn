---
title: "🚀 Tự Động Giao Dịch Binance Spot: Limit & Market Orders qua API với n8n"
description: "Workflow n8n giúp các sếp tự động thực hiện lệnh mua/bán Spot trên Binance (Limit & Market) mà không cần viết code, giảm rủi ro và tăng tốc độ giao dịch."
slug: "tu-dong-giao-dich-binance-spot-limit-market-orders-n8n"
tags: [n8n, automation, no-code, finance, crypto, binance]
keywords: [n8n workflow, tự động hóa, Binance, giao dịch crypto, limit order, market order]
---

# 🚀 Tự Động Giao Dịch Binance Spot: Limit & Market Orders qua API với n8n

Bạn đã từng phải **đăng nhập Binance, kiểm tra số dư, tính toán khối lượng, tạo chữ ký HMAC, rồi mới gửi lệnh**?  
Quá trình này tốn thời gian, dễ sai sót và không thể chạy 24/7.  

**Workflow “Binance Spot Trader - Limit & Market Orders via API”** chính là giải pháp **tự động 100%**, cho phép các sếp:

* Đặt lệnh **Limit BUY/SELL** và **Market BUY/SELL** chỉ bằng một cú click.
* Theo dõi, hủy toàn bộ lệnh mở tự động.
* Tích hợp vào bất kỳ hệ thống nào (Slack, Telegram, Google Sheets…) mà không viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Tự động thực hiện hàng trăm lệnh trong giây.  
- **Độ chính xác 100%**: Chữ ký HMAC được tạo tự động, không còn lỗi nhập tay.  
- **Hoạt động liên tục**: Không cần ngồi trước máy, workflow chạy 24/7.  
- **Dễ mở rộng**: Kết nối Slack/Telegram để nhận thông báo ngay lập tức.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Binance** (có quyền API).  
- **API Key & Secret Key** (được cấp trong Binance > API Management).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Kết nối internet ổn định** để gọi API Binance.  
- (Tùy chọn) **Webhook URL** nếu muốn kích hoạt workflow từ bên ngoài.  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow (được cung cấp ở cuối README) hoặc sao chép toàn bộ JSON.  
2. Vào **n8n Editor → Workflows → Import** → Dán JSON → **Import**.  
3. Đặt tên cho workflow (mặc định: *Binance Spot Trader*).

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chúng:

| Node | Loại | Mục đích | Cấu hình cần chỉnh |
|------|------|----------|--------------------|
| **When clicking ‘Execute workflow’** | manualTrigger | Bắt đầu workflow thủ công hoặc qua webhook. | Nếu muốn trigger tự động, chuyển sang **Webhook** và sao chép URL. |
| **Set Account Query** | set | Định nghĩa query string cho API `/api/v3/account`. | Không cần thay đổi, chỉ kiểm tra `timestamp` được tạo trong node sau. |
| **Signature Get Account** | crypto | Tạo chữ ký HMAC SHA256 cho request account. | **Secret Key**: chọn credential Binance API (tạo mới nếu chưa có). |
| **Account Info Query** | code | Xây dựng payload JSON cho request account. | Kiểm tra `apiKey` và `signature` được truyền đúng. |
| **Get Account Info** | httpRequest | Gửi GET tới `https://api.binance.com/api/v3/account`. | **Authentication**: chọn credential Binance API, **Headers**: `X-MBX-APIKEY`. |
| **LimitBuy Parameter** | set | Tham số cho lệnh Limit BUY (symbol, side, type, quantity, price). | Thay **symbol**, **quantity**, **price** theo chiến lược của bạn. |
| **Signature Limit BUY** | crypto | Chữ ký cho lệnh Limit BUY. | **Secret Key**: credential Binance API. |
| **Execute Limit BUY** | httpRequest | Gửi POST `/api/v3/order` để thực hiện Limit BUY. | **Method**: POST, **Headers**: `X-MBX-APIKEY`, **Body**: JSON từ node trước. |
| **LimitSale Parameter** | set | Tham số cho lệnh Limit SELL. | Thay **symbol**, **quantity**, **price**. |
| **Signature Limit SELL** | crypto | Chữ ký cho lệnh Limit SELL. | Same as above. |
| **Execute Limit SELL** | httpRequest | Gửi POST để thực hiện Limit SELL. | Same as above. |
| **MarketBuy Parameter** | set | Tham số cho Market BUY (symbol, side, type, quantity). | Thay **symbol**, **quantity**. |
| **Signature MarketBuy** | crypto | Chữ ký cho Market BUY. | Same as above. |
| **Execute MarketBuy** | httpRequest | Gửi POST `/api/v3/order` cho Market BUY. | Same as above. |
| **MarketSell Parameter** | set | Tham số cho Market SELL. | Thay **symbol**, **quantity**. |
| **Signature MarketSell** | crypto | Chữ ký cho Market SELL. | Same as above. |
| **Execute MarketSell** | httpRequest | Gửi POST cho Market SELL. | Same as above. |
| **OpenOrder Query** | code | Tạo query để lấy danh sách lệnh mở. | Kiểm tra `timestamp`. |
| **Signature OpenOrder** | crypto | Chữ ký cho request Open Orders. | Same as above. |
| **Get Open Orders** | httpRequest | GET `/api/v3/openOrders`. | **Headers**: `X-MBX-APIKEY`. |
| **Cancel All Order Params** | set | Tham số chung để hủy lệnh (symbol). | Thay **symbol** cần hủy. |
| **CancelAllOrder Query** | code | Tạo query cho hủy toàn bộ lệnh. | Kiểm tra `timestamp`. |
| **Signature Cancel All Order** | crypto | Chữ ký cho hủy lệnh. | Same as above. |
| **Cancell All Order** | httpRequest | DELETE `/api/v3/openOrders`. | **Headers**: `X-MBX-APIKEY`. |

> **Lưu ý:** Tất cả các node **crypto** phải được gắn **credential Binance API** (API Key & Secret). Nếu chưa tạo credential, vào **Credentials → New Credential → Binance API** và nhập thông tin.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** và kiểm tra log ở mỗi node để chắc chắn request trả về `200 OK`.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải).  
3. Đặt **Cron** hoặc **Webhook** nếu muốn tự động chạy theo lịch hoặc khi nhận tín hiệu từ hệ thống khác.

## ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** ngay sau mỗi node `httpRequest` để nhận báo cáo lệnh thành công hoặc lỗi.  
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại thời gian, symbol, side, price, quantity – tiện cho việc audit.  
- **Chiến lược tự động**: Kết hợp node **IF** + **Code** để quyết định mua/bán dựa trên chỉ báo MA, RSI từ API Binance Futures.  
- **Bảo mật**: Đặt **environment variables** cho API Key/Secret và bật **HTTPS** cho n8n để tránh rò rỉ thông tin.  

## 📌 Kết luận
Với workflow này, các sếp có thể **đánh bại thời gian**, **giảm lỗi thủ công** và **tối ưu hoá chiến lược giao dịch** trên Binance chỉ bằng vài cú click. Hãy import ngay, cấu hình API, và để n8n làm việc cho bạn 24/7! 🚀

---

### 📥 File JSON của Workflow
```json
{
  "nodes": [
    { "name": "When clicking ‘Execute workflow’", "type": "n8n-nodes-base.manualTrigger", "typeVersion": 1, "position": [250, 300] },
    { "name": "Set Account Query", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [450, 300] },
    { "name": "Signature Get Account", "type": "n8n-nodes-base.crypto", "typeVersion": 1, "position": [650, 300] },
    { "name": "Account Info Query", "type": "n8n-nodes-base.code", "typeVersion": 1, "position": [850, 300] },
    { "name": "Order Query", "type": "n8n-nodes-base.code", "typeVersion": 1, "position": [1050, 300] },
    { "name": "LimitBuy Parmeter", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [1250, 200] },
    { "name": "Set Credentials", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [1250, 400] },
    { "name": "Get Account Info", "type": "n8n-nodes-base.httpRequest", "typeVersion": 1, "position": [1450, 300] },
    { "name": "LimitSale Parameter", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [1250, 500] },
    { "name": "Sale Query", "type": "n8n-nodes-base.code", "typeVersion": 1, "position": [1050, 500] },
    { "name": "Execute Limit SELL", "type": "n8n-nodes-base.httpRequest", "typeVersion": 1, "position": [1450, 500] },
    { "name": "Execute Limit BUY", "type": "n8n-nodes-base.httpRequest", "typeVersion": 1, "position": [1650, 200] },
    { "name": "Market Buy Query", "type": "n8n-nodes-base.code", "typeVersion": 1, "position": [1050, 100] },
    { "name": "MarketBuy Parameter", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [1250, 100] },
    { "name": "Signature MarketBuy", "type": "n8n-nodes-base.crypto", "typeVersion": 1, "position": [1450, 100] },
    { "name": "Signature Limit BUY", "type": "n8n-nodes-base.crypto", "typeVersion": 1, "position": [1450, 200] },
    { "name": "Signature Limit SELL", "type": "n8n-nodes-base.crypto", "typeVersion": 1, "position": [1450, 500] },
    { "name": "Execute MarketBuy", "type": "n8n-nodes-base.httpRequest", "typeVersion": 1, "position": [1650, 100] },
    { "name": "MarketSell Parameter", "type": "n8n-nodes-base.set", "typeVersion": 1, "position": [1250, 600] },
    { "name":