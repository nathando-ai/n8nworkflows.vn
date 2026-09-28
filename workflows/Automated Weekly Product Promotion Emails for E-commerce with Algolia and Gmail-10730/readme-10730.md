---
title: "🚀 Tự Động Hóa Email Quảng Cáo Tuần Hàng Cho E-commerce Với Algolia & Gmail (Không Cần Code)"
description: "Workflow tự động hóa gửi email quảng cáo hàng tuần cho khách hàng với sản phẩm khuyến mãi từ Algolia, chạy tự động vào mỗi Chủ Nhật 8h sáng. Giúp tiết kiệm thời gian, tăng hiệu quả marketing và cá nhân hóa nội dung cho từng khách hàng."
slug: "tieu-dong-hoa-email-quang-cao-tuan-hang-voi-algolia-gmail"
tags: [n8n, automation, e-commerce, email-marketing, algolia, google-sheets, gmail, no-code]
keywords: [tự động hóa email quảng cáo, n8n workflow, algolia api, gửi email hàng tuần tự động, marketing e-commerce, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Email Quảng Cáo Tuần Hàng Cho E-commerce Với Algolia & Gmail**

### **Giải pháp hoàn hảo cho các sếp e-commerce muốn tiết kiệm thời gian và tăng doanh số!**
Hãy tưởng tượng: **Không cần viết email thủ công, không cần nhắc nhở khách hàng về khuyến mãi, và không cần lo lắng về việc quên gửi email** – tất cả đều được tự động hóa chỉ với một workflow n8n đơn giản! Đây là giải pháp **100% không cần code**, giúp bạn gửi **email quảng cáo hàng tuần** với sản phẩm khuyến mãi từ Algolia, **tự động tính toán ngày hiệu lực khuyến mãi**, và **gửi đến tất cả khách hàng đăng ký** qua Gmail.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần viết email thủ công hàng tuần.
✅ **Tăng doanh số** – Khuyến mãi được gửi chính xác đến khách hàng đúng thời điểm.
✅ **Cá nhân hóa nội dung** – Email bao gồm sản phẩm khuyến mãi + ngày hiệu lực khuyến mãi.
✅ **Hoạt động liên tục** – Workflow chạy tự động vào **mỗi Chủ Nhật 8h sáng**.
✅ **Dễ dàng tùy chỉnh** – Thay đổi sản phẩm, ngày gửi, hoặc nội dung email chỉ với vài cú nhấp chuột.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Algolia** với:
   - **Application ID** và **Search API Key** (để truy cập sản phẩm).
   - **Index tên** (`dogtreats_prod_products` – các sếp cần thay đổi thành tên index của mình).
   - **Trường dữ liệu** trong index phải có: `on_sale`, `price_eur`, `original_price_eur`, `image`, `name`, `description`.

✔ **Google Sheet** chứa danh sách **khách hàng đăng ký nhận email** (cột tên phải là **"Email"**).

✔ **Tài khoản Gmail** để gửi email (cần **OAuth 2.0** để kết nối với n8n).

✔ **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
1. Tải file JSON từ [n8n.io/workflows/10730](https://n8n.io/workflows/10730).
2. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **"Import from JSON"** trong Editor.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Algolia (Node: "Request products from Algolia")**
- **Credentials**: Chọn `"httpCustomAuth"` và điền:
  - **URL**: `https://YOUR_APP_ID-dsn.algolia.net/1/indexes/YOUR_INDEX_NAME/query`
  - **Headers**:
    ```
    {
      "X-Algolia-API-Key": "YOUR_SEARCH_API_KEY",
      "X-Algolia-Application-Id": "YOUR_APP_ID"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "params": "filters=on_sale:true&hitsPerPage=6"
    }
    ```
  - **Lưu ý**:
    - Thay `YOUR_APP_ID`, `YOUR_INDEX_NAME`, và `YOUR_SEARCH_API_KEY` bằng thông tin của Algolia.
    - Nếu muốn lấy sản phẩm theo **danh mục khác** (ví dụ: `category:shoes`), thay `filters=on_sale:true` thành `filters=category:shoes`.

#### **B. Cấu hình Google Sheets (Node: "Get row(s) in sheet")**
- **Credentials**: Chọn `"googleSheetsOAuth2Api"`.
- **Sheet Name**: Đặt tên là **"Khách hàng Email"** (hoặc tên sheet chứa danh sách email).
- **Range**: Đặt là `"Sheet1!A:B"` (giả sử cột A là tên, cột B là email).

#### **C. Cấu hình Gmail (Node: "Send newsletter")**
- **Credentials**: Chọn `"gmailOAuth2"` và kết nối tài khoản Gmail.
- **To**: `$$.json["email"]` (đây là email của khách hàng từ Google Sheets).
- **Subject**: `"Khuyến mãi tuần này - Sản phẩm hot chỉ còn lại!"`.
- **HTML Body**: Sử dụng nội dung từ node **"Newsletter Generation (HTML Format)"**.

#### **D. Cấu hình Schedule Trigger (Node: "On sundays 8.00 am")**
- **Time Zone**: Chọn **múi giờ** phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Active**: Bật để workflow chạy tự động **mỗi Chủ Nhật 8h sáng**.

#### **E. Cấu hình HTML Template (Node: "Newsletter Generation (HTML Format)")**
- **Nội dung mẫu**:
  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <style>
          .product-tile { border: 1px solid #ddd; padding: 10px; margin: 10px; }
          .price { color: red; font-weight: bold; }
      </style>
  </head>
  <body>
      <h1>🎉 Khuyến mãi tuần này!</h1>
      <p>Khuyến mãi hiệu lực từ <span id="start-date"></span> đến <span id="end-date"></span>.</p>
      <div id="products"></div>
  </body>
  </html>
  ```
- **Thay thế `{{products}}` và `{{start-date}}`, `{{end-date}}`** bằng dữ liệu từ node **"Merge data for newsletter"**.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute"** trên node **"On sundays 8.00 am"**.
   - Kiểm tra email đã được gửi đến **một khách hàng mẫu** trong Google Sheets.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node đều **hoạt động** và không có lỗi.
   - Nhấn **"Active"** trên tab **"Workflow"**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Gửi email cho nhiều danh sách khách hàng**
- Nếu có **nhiều sheet Google Sheets** (ví dụ: khách hàng VIP, khách hàng mới), các sếp có thể:
  - **Tạo nhiều node "Get row(s) in sheet"** và **sử dụng node "Merge"** để kết hợp danh sách.
  - **Lọc email** bằng node **"If"** trước khi gửi.

### **2. Thêm Slack/Telegram để báo lỗi**
- Sử dụng node **"Slack Webhook"** hoặc **"Telegram Bot"** để **báo lỗi** nếu workflow gặp vấn đề.
- Ví dụ:
  ```json
  {
    "type": "slack",
    "credentials": "slackWebhookUrl",
    "message": "🚨 Workflow gửi email khuyến mãi gặp lỗi! Vui lòng kiểm tra."
  }
  ```

### **3. Lưu log hoạt động**
- Sử dụng node **"Sticky Note"** để **ghi lại lịch sử** của workflow.
- Ví dụ:
  ```json
  {
    "type": "stickyNote",
    "content": "Email đã gửi cho {{$.json.length}} khách hàng vào ngày {{$.json.date}}."
  }
  ```

### **4. Gửi báo cáo định kỳ**
- Sử dụng node **"Schedule Trigger"** để **gửi báo cáo thống kê** (ví dụ: số email đã gửi, sản phẩm bán chạy nhất) vào **cuối tháng**.

---

## 📌 **Kết luận**
Workflow này **giúp các sếp e-commerce tự động hóa hoàn toàn quá trình gửi email quảng cáo**, tiết kiệm **thời gian và tăng hiệu quả marketing** mà không cần viết code. **Chỉ cần cấu hình một lần**, workflow sẽ **chạy tự động hàng tuần** và **cập nhật sản phẩm khuyến mãi** từ Algolia.

**Hãy áp dụng ngay và bắt đầu tự động hóa email của mình!** 🚀
Nếu có vấn đề, các sếp có thể liên hệ với tác giả **Emir Belkahia** qua [LinkedIn](https://www.linkedin.com/in/emirbelkahia/) hoặc email: **emir.belkahia@gmail.com**.

---
**💡 Lưu ý cuối cùng**:
- **Không dùng tài khoản Gmail cá nhân** để gửi email bulk (có thể bị khóa).
- **Sử dụng VPS** để đảm bảo workflow **không bị ngắt kết nối**.
- **Test trước khi bật Active** để tránh gửi email sai hoặc lỗi.