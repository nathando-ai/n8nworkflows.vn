---
title: "🚀 **Hệ Thống Theo Dõi Giá Hàng Tự Động Với AI + Cảnh Báo Thông Minh (N8n) - Giúp Các Sếp Tiết Kiệm Ngàn Tỷ Mỗi Tháng**"
description: "Workflow tự động hóa theo dõi giá hàng từ Amazon, Best Buy, Target với AI phân tích và cảnh báo giá giảm thông minh qua Slack - Giúp các sếp ra quyết định mua sắm thông minh, tiết kiệm chi phí và cạnh tranh hiệu quả."
slug: "he-thong-theo-doi-gia-hang-voi-ai-canh-bao-thong-minh"
tags: [n8n, automation, market-research, ai-summarization, price-tracking, scrapegraphai, google-sheets, slack-integration]
keywords: [n8n workflow theo dõi giá, tự động hóa giá hàng, AI phân tích giá, cảnh báo giá giảm Slack, n8n self-hosted, tự động hóa mua sắm thông minh]
---

# 🚀 **Hệ Thống Theo Dõi Giá Hàng Tự Động Với AI + Cảnh Báo Thông Minh (N8n)**

## **🔍 Nỗi Đau Của Các Sếp Khi Theo Dõi Giá Hàng Thủ Công**
Các sếp thường phải:
- **Tốn thời gian hàng giờ** để tra cứu giá hàng trên Amazon, Best Buy, Target mỗi ngày.
- **Mất nhiều công sức** để so sánh giá giữa các cửa hàng và cập nhật thủ công vào bảng Excel.
- **Bỏ lỡ cơ hội mua sắm** khi giá giảm đột ngột mà không được cảnh báo kịp thời.
- **Không có dữ liệu phân tích** để ra quyết định mua sắm thông minh, dẫn đến chi phí không cần thiết.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100%** theo dõi giá hàng từ 3 nền tảng lớn hàng ngày.
✅ **AI phân tích giá** để cảnh báo các giảm giá có ý nghĩa thực sự.
✅ **Cảnh báo thông minh** qua Slack khi giá xuống dưới ngưỡng mong muốn.
✅ **Lưu lịch sử giá** vào Google Sheets để phân tích dài hạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** lên đến **5-10 giờ/tuần** (giá trị ~5-10 triệu/tháng).
- **Mua sắm thông minh** với dữ liệu giá chính xác từ 3 cửa hàng lớn.
- **Cảnh báo giá giảm kịp thời** qua Slack, không bỏ lỡ bất kỳ cơ hội nào.
- **Phân tích thị trường** từ lịch sử giá để ra quyết định mua sắm chiến lược.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (không dùng phiên bản cloud).
2. **API Key ScrapeGraphAI** (dùng để trích xuất dữ liệu từ trang web).
3. **Credentials Google Sheets** (để lưu lịch sử giá).
4. **Credentials Slack OAuth2** (để gửi cảnh báo).
5. **URL sản phẩm** (các sếp cần nhập vào để theo dõi).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6428](https://n8n.io/workflows/6428) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không sử dụng phiên bản n8n cloud** vì không hỗ trợ các node như `scrapegraphAI` và `scheduleTrigger` 24/7.
- **Không cần code** - workflow đã sẵn sàng, chỉ cần cấu hình credentials.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Daily Price Check Trigger (scheduleTrigger)**
- **Cấu hình:**
  - **Frequency:** `Every 24 hours` (khuyến nghị chạy vào sáng sớm).
  - **Timezone:** Chọn theo giờ Việt Nam (`Asia/Ho_Chi_Minh`).
  - **Active:** Bật để workflow chạy tự động.

#### **🔹 Node 2: Manual Price Check Webhook (webhook)**
- **Cấu hình:**
  - **Path:** `price-check-webhook` (không đổi).
  - **HTTP Method:** `GET`.
  - **Active:** Bật để có thể gọi từ bên ngoài (nếu cần kiểm tra thủ công).

#### **🔹 Node 3-5: Amazon Price Scraper, Best Buy Price Scraper, Target Price Scraper (httpRequest)**
- **Cấu hình chung:**
  - **URL:** Điền vào **URL Product** (ví dụ: `https://www.amazon.com/dp/B08K5J1L2M`).
  - **Headers:** Đảm bảo có `User-Agent` để tránh bị chặn.
  - **Active:** Bật tất cả 3 node này.

#### **🔹 Node 6: AI Price Data Extractor (scrapegraphAI)**
- **Cấu hình:**
  - **Credentials:** Chọn `scrapegraphAIApi` (đã cấu hình trước).
  - **Input Data:** Chọn `json` từ node `httpRequest`.
  - **Active:** Bật để AI trích xuất dữ liệu.

#### **🔹 Node 7: Price Analysis & Intelligence (code)**
- **Cấu hình:**
  - **Code mẫu (sửa nếu cần):**
    ```javascript
    // Kiểm tra giá giảm và phân loại
    const priceChange = {
      trend: "down", // hoặc "up", "stable"
      significance: "high", // hoặc "medium", "low"
      alert: false
    };

    // Cập nhật giá trị vào JSON
    $input.all().forEach(item => {
      item.priceAnalysis = priceChange;
      if (priceChange.significance === "high") {
        item.priceAnalysis.alert = true;
      }
    });

    return $input.all();
    ```
  - **Active:** Bật để phân tích dữ liệu.

#### **🔹 Node 8: Google Sheets Price Log (googleSheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Điền tên sheet (ví dụ: `Price_Log`).
  - **Range:** `A1` (để ghi dữ liệu từ hàng 1).
  - **Active:** Bật để lưu lịch sử giá.

#### **🔹 Node 9: Price Change Alert Filter (if)**
- **Cấu hình:**
  - **Condition:** Chọn `priceAnalysis.alert === true`.
  - **Active:** Bật để lọc cảnh báo.

#### **🔹 Node 10: Slack Price Alert (slack)**
- **Cấu hình:**
  - **Credentials:** Chọn `slackOAuth2Api`.
  - **Message:** Sử dụng template mặc định (có thể sửa để cá nhân hóa).
  - **Active:** Bật để gửi cảnh báo.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Chọn **Run Workflow** và nhập URL sản phẩm mẫu.
   - Kiểm tra kết quả trên **Google Sheets** và **Slack**.
2. **Bật Active:**
   - Sau khi kiểm tra thành công, bật **Active** cho cả workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM ĐẸP HƠN**]
- **Thêm Telegram Bot:** Sử dụng node `telegram` để cảnh báo qua Telegram thay vì Slack.
- **Lưu Log Lịch Sử:** Tạo một sheet mới trong Google Sheets để lưu tất cả các cảnh báo.
- **Báo Cáo Định Kỳ:** Sử dụng node `email` để gửi báo cáo tuần/month về giá hàng.
- **Tự động Mua Sắm:** Kết hợp với node `amazon` hoặc `shopee` để tự động đặt hàng khi giá xuống ngưỡng.
- **Duyệt Dữ Liệu:** Sử dụng node `code` để tính toán giá trung bình và đề xuất mua.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong việc theo dõi giá hàng.
✔ **Mua sắm thông minh** với dữ liệu chính xác từ 3 cửa hàng lớn.
✔ **Cảnh báo giá giảm kịp thời** qua Slack/Telegram.
✔ **Phân tích thị trường** từ lịch sử giá để ra quyết định mua sắm chiến lược.

**👉 Hãy import workflow này ngay và bắt đầu tiết kiệm từ hôm nay!**

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::