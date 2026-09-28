---
title: "🚀 Hệ Thống Dự Báo Giá Crypto Tự Động Hàng Ngày với Gemini AI, Decodo & Gmail (N8N)"
description: "Workflow tự động hóa 100% không code giúp các sếp crypto theo dõi giá thị trường live, dự báo xu hướng 24h và nhận báo cáo email định kỳ với độ chính xác cao từ Gemini AI. Giúp tiết kiệm thời gian lên tới 10 giờ/tuần và tối ưu hóa quyết định giao dịch."
slug: "crypto-price-forecasting-pipeline-n8n"
tags: [n8n, crypto, automation, gemini-ai, decodo, gmail, no-code, trading-bot, data-scraping]
keywords: [n8n crypto forecast, tự động hóa dự báo giá crypto, gemini ai n8n, decodo web scraping, email báo cáo crypto, tự động hóa giao dịch crypto]
---

# 🚀 **Hệ Thống Dự Báo Giá Crypto Tự Động Hàng Ngày với Gemini AI, Decodo & Gmail**

## **Giải Pháp Cho Nỗi Đau Của Các Sếp Crypto**
Hàng ngày, các sếp crypto phải:
- **Làm thủ công** theo dõi giá thị trường trên CoinGecko, Binance, hoặc CoinMarketCap.
- **Tốn thời gian** phân tích xu hướng giá, tính toán biến động 1h/24h/7d.
- **Mất cơ hội** vì không nhận được báo cáo dự báo định kỳ (ví dụ: dự báo xu hướng 24h).
- **Không có dữ liệu lịch sử** để so sánh và dự đoán xu hướng dài hạn.

**Workflow này giải quyết tất cả!** Với **Gemini AI**, **Decodo** (scraper web), và **Gmail**, hệ thống sẽ:
✅ **Scrape live** giá crypto từ CoinGecko mỗi **30 phút**.
✅ **Dự báo xu hướng** 24h với **độ chính xác cao** từ Gemini AI.
✅ **Gửi báo cáo email tự động** hàng ngày (18:00) với:
   - Giá hiện tại + biến động 1h/24h/7d.
   - Dự báo xu hướng (tăng/giảm) trong 6h/12h/24h.
   - Thời gian giao dịch tối ưu (trading windows).
   - Market cap & volume 24h.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** (không cần theo dõi thủ công).
- **Dự báo chính xác** với AI Gemini (cập nhật live).
- **Báo cáo email tự động** (HTML + văn bản) với thiết kế chuyên nghiệp.
- **Dữ liệu lịch sử** được lưu trữ trong Data Table của n8n (dùng để phân tích dài hạn).
- **Hoạt động 24/7** (không cần can thiệp người dùng).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Decodo** (đăng ký [tại đây](https://visit.decodo.com/discount) với mã giảm giá).
2. **Tài khoản Gmail** (để gửi báo cáo email).
3. **API Key Gemini AI** (từ [Google AI Studio](https://aistudio.google.com/)).
4. **n8n Self-hosted** (không thể chạy trên n8n.cloud do node Decodo là **community node**).
5. **Data Table** trong n8n với schema chuẩn:
   ```json
   {
     "coin": "string",       // Ví dụ: "bitcoin", "ethereum"
     "ts": "string",         // Thời gian scrape (format ISO)
     "price": "number",      // Giá hiện tại
     "change_1h": "number",  // Biến động 1h (%)
     "change_24h": "number", // Biến động 24h (%)
     "change_7d": "number",  // Biến động 7d (%)
     "market_cap": "number", // Market cap (USD)
     "volume_24h": "number"  // Volume 24h (USD)
   }
   ```
6. **Thời gian múi giờ** của máy chủ n8n phải khớp với múi giờ của bạn (do lịch trình email dựa trên server time).
:::

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9964](https://n8n.io/workflows/9964) (ấn "Download").
- **Trên n8n Editor**:
  - Nhấn **"Import"** > Chọn file JSON vừa tải.
  - **Hoặc** copy toàn bộ JSON vào ô **"Import from JSON"** và nhấn **"Import"**.

### **2. Các Bước Cấu Hình BẮT BUỘC**
:::warning[LƯU Ý QUAN TRỌNG]
Các node sau **phải được cấu hình chính xác** để workflow hoạt động:
:::

#### **A. Cấu Hình Credentials (Tài Khoản)**
| Node | Credential | Tham Số Cần Điền |
|------|------------|-------------------|
| **Decodo** | `decodoApi` | API Key từ Decodo (tạo tại [Decodo Dashboard](https://decodo.com/dashboard)). |
| **Gemini AI** | `googlePalmApi` | API Key từ [Google AI Studio](https://aistudio.google.com/). |
| **Gmail** | `gmailOAuth2` | OAuth 2.0 từ tài khoản Gmail (cấu hình trong **n8n Credentials**). |

#### **B. Cấu Hình Data Table**
1. **Tạo Data Table mới** trong n8n với **schema** như trên.
2. **Ghi nhớ ID của Data Table** (sử dụng trong node **"Load Data Last 48h"** và **"Insert Data"**).
3. **Node "Insert Data"** (trong workflow) cần:
   - **Operation**: `upsert` (để cập nhật dữ liệu mới mà không trùng lặp).
   - **Data Table ID**: Điền ID vừa ghi nhớ.

#### **C. Cấu Hình Coin List (Configure Coins)**
- Mở node **"Configure Coins"** (type: `set`).
- **Thay đổi giá trị** trong `coinItems` thành danh sách coin bạn muốn theo dõi (ví dụ):
  ```json
  [
    { "coin": "bitcoin", "slug": "bitcoin" },
    { "coin": "ethereum", "slug": "ethereum" },
    { "coin": "solana", "slug": "solana" }
  ]
  ```
  - **Slug** phải khớp với CoinGecko (kiểm tra tại [CoinGecko API](https://www.coingecko.com/en/api)).
  - **Ghi chú**: Nếu không thay đổi, workflow sẽ scrape mặc định là Bitcoin, Ethereum, Solana.

#### **D. Cấu Hình Email Recipient**
- Mở node **"Recipient Email + Timezone"** (type: `set`).
- **Thay đổi**:
  - `email`: Địa chỉ email của bạn (để nhận báo cáo).
  - `timezone`: Múi giờ của bạn (ví dụ: `"Asia/Ho_Chi_Minh"`).

#### **E. Kiểm Tra Lịch Trình (Schedule)**
- **Scrape & Log (30 phút/lần)**: Node **"Schedule: Every 30m"** sẽ chạy tự động.
- **Forecast Email (18:00 hàng ngày)**: Node **"Schedule: 18:00 Daily"** sẽ gửi báo cáo.
  - **Lưu ý**: Thời gian này dựa trên **server time** của n8n. Nếu khác với múi giờ của bạn, hãy điều chỉnh trong node `set` của **"Recipient Email + Timezone"**.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run Workflow"** và chọn **1 coin** (ví dụ: Bitcoin).
   - Kiểm tra:
     - Dữ liệu scrape từ CoinGecko có đúng không?
     - Gemini AI có dự báo xu hướng hợp lý không?
     - Email test có được gửi thành công không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Dữ Liệu Lịch Sử**
- **Xóa dữ liệu cũ**: Nếu Data Table quá lớn, thêm node **"Filter"** trước **"Insert Data"** để giữ chỉ **7 ngày dữ liệu mới nhất**.
- **Tạo Dashboard**: Sử dụng **n8n Data Table Viewer** hoặc kết nối với **Google Sheets** để visualize dữ liệu.

### **2. Kết Nối Với Slack/Telegram**
- Thêm node **Slack** hoặc **Telegram Bot** sau **"Send Email"** để nhận thông báo tức thời khi có dự báo mới.

### **3. Cập Nhật Coin List Tự Động**
- Sử dụng **node `httpRequest`** để lấy danh sách coin từ CoinGecko API và tự động cập nhật trong **"Configure Coins"**.

### **4. Lưu Log Hoạt Động**
- Thêm node **`stickyNote`** sau **"Send Email"** để ghi log thành công/thất bại vào **n8n Logs**.

### **5. Dự Báo Xu Hướng Dài Hạn**
- Thêm node **`agent`** mới sau **"Forecast Next 24h"** để dự báo xu hướng **7 ngày** với Gemini AI.

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp crypto muốn:
✔ **Tự động hóa** theo dõi giá và dự báo xu hướng.
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược giao dịch.
✔ **Nhận báo cáo email chuyên nghiệp** hàng ngày.

**Bắt đầu ngay!**
1. **Cài đặt n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận báo cáo tự động!

---
:::success[CHÚC MỪNG]
Bạn đã có một **hệ thống dự báo crypto tự động hoàn chỉnh**! Hãy chia sẻ kết quả với cộng đồng n8n tại [n8n Community](https://community.n8n.io/) nếu workflow này giúp ích cho bạn.
:::