---
title: "🛒 **Tự Động Hóa Theo Dõi Giá Thương Mại Hàng Hàng Ngày Với Web Scraping, Google Sheets & Telegram** – Giúp Các Sếp Giảm Thiểu Rủi Ro Giá & Tăng Doanh Thu"
description: "Workflow tự động hóa theo dõi giá hàng ngày từ các trang thương mại điện tử, so sánh với giá cũ, gửi cảnh báo qua Telegram và cập nhật lịch sử giá vào Google Sheets – tiết kiệm thời gian và tối ưu hóa chiến lược giá cho doanh nghiệp."
slug: "tu-dong-hoa-theo-doi-gia-thuong-mai-google-sheets-telegram"
tags: [n8n, automation, web-scraping, google-sheets, telegram-bot, ecommerce, marketing, no-code]
keywords: [n8n workflow theo dõi giá, tự động hóa giá hàng, web scraping giá thương mại, cảnh báo giá thay đổi Telegram, Google Sheets tự động hóa, tối ưu chiến lược giá]
---

# 🚀 **Tự Động Hóa Theo Dõi Giá Thương Mại Hàng Ngày – Giúp Các Sếp Tránh Rủi Ro Giá & Tăng Doanh Thu**

## **💡 Nỗi Đau Của Các Sếp Khi Theo Dõi Giá Thương Mại Thủ Công**
Các sếp thường phải:
- **Tốn thời gian** để tra cứu giá hàng ngày trên nhiều trang thương mại điện tử (Shopee, Lazada, Tiki, Amazon...).
- **Mất tập trung** vì phải so sánh giá thủ công, tính toán % thay đổi và ghi chép vào bảng Excel.
- **Không kịp thời** khi giá thay đổi đột ngột, dẫn đến mất cơ hội bán hàng hoặc lỗ lỗ.
- **Không có báo cáo lịch sử** để phân tích xu hướng giá, từ đó điều chỉnh chiến lược giá hiệu quả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động tra cứu giá** từ các trang thương mại điện tử hàng ngày (8h sáng).
✅ **So sánh giá cũ vs. mới** và tính toán % thay đổi.
✅ **Gửi cảnh báo Telegram** khi giá thay đổi (kèm thông tin chi tiết).
✅ **Cập nhật lịch sử giá** vào Google Sheets để phân tích dài hạn.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không phải tra cứu giá thủ công hàng ngày.
- **Giảm rủi ro giá**: Nhận cảnh báo ngay khi giá thay đổi, kịp thời điều chỉnh chiến lược.
- **Dữ liệu chính xác**: Lịch sử giá được tự động cập nhật và sắp xếp logic.
- **Tối ưu hóa doanh thu**: Phân tích xu hướng giá để bán với giá cao nhất.
- **Tích hợp Telegram**: Nhận thông báo tức thời trên điện thoại.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets với **2 tab**:
     - **Master Sheet**: Danh sách sản phẩm (cột `product_url` và `last_price`).
     - **Price_History**: Để lưu lịch sử giá thay đổi.
   - **Chia sẻ quyền truy cập** cho n8n (quyền "Sửa").
   - **API Key Google Sheets OAuth 2.0** (cài đặt trong n8n: `Settings > Credentials > Add Credential > Google Sheets OAuth2`).

2. **Tài khoản Telegram**:
   - Một **chatbot Telegram** (tạo bằng `@BotFather`).
   - **API Token** của bot (để n8n gửi thông báo).
   - **ID Chat** của nhóm hoặc tài khoản cá nhân (để nhận cảnh báo).

3. **VPS cho n8n (khuyến nghị)**:
   - Workflow chạy **mỗi ngày lúc 8h sáng** (theo giờ máy chủ).
   - Để ổn định, các sếp nên **self-host n8n trên VPS** (tránh bị gián đoạn).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

4. **Danh sách sản phẩm**:
   - Các sếp cần **điền danh sách sản phẩm** vào tab `Master Sheet` của Google Sheets, với cột:
     - `product_url` (link trang sản phẩm trên thương mại điện tử).
     - `last_price` (giá cũ để so sánh).
     - `product_name` (tên sản phẩm, tùy chọn).

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON**
:::note[**Bước 1: Tải workflow từ n8n.io**]
- Truy cập [link workflow gốc](https://n8n.io/workflows/4640).
- Nhấn **"Export"** để tải file `.json` về máy.
:::

:::note[**Bước 2: Import vào n8n Editor**]
1. Mở **n8n Editor** (trang chủ của n8n).
2. Nhấn **"Import"** (góc trên bên phải).
3. Chọn file `.json` vừa tải và nhấn **"Import"**.
4. Workflow sẽ xuất hiện trên canvas.
:::

:::note[**Bước 3: Chọn Credentials**]
- Khi import xong, các node **Google Sheets** và **Telegram** sẽ yêu cầu chọn **credentials**:
  - **Google Sheets**: Chọn `googleSheetsOAuth2Api` (đã cài đặt trước).
  - **Telegram**: Chọn `telegramApi` (đã cài đặt API Token).
:::

---

### **2. Các Lưu Ý Quan Trọng (BẮT BUỘC Chỉnh)**
:::info[**📌 Node "Fetch Product List from Sheet"**]
- **Chọn tab "Master Sheet"** trong Google Sheets.
- **Cấu hình cột**:
  - `product_url`: Link trang sản phẩm.
  - `last_price`: Giá cũ để so sánh.
  - `product_name`: Tên sản phẩm (tùy chọn).
:::

:::info[**📌 Node "Load Product Page HTML"**]
- **Thay đổi URL mẫu** nếu cần:
  - Nếu trang thương mại điện tử có **URL khác nhau**, chỉnh sửa trong **HTTP Request** (ví dụ: `{{$node["Fetch Product List from Sheet"].json[0].product_url}}`).
- **Thêm Header** (nếu trang yêu cầu):
  - Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).
:::

:::info[**📌 Node "Extract Current Price from HTML"**]
- **Chỉnh CSS Selector** để trích xuất giá:
  - Mở trang sản phẩm trong trình duyệt, **inspect element** (phím `F12`) để tìm thẻ HTML chứa giá.
  - Ví dụ: Nếu giá nằm trong thẻ `<span class="price">`, chọn `span.price`.
  - Nếu giá có **dạng text** (ví dụ: `"Giá: 500.000 VNĐ"`), chỉnh sửa **expression** trong node `html` để trích xuất số:
    ```javascript
    $json["price"].replace(/[^\d]/g, '') // Loại bỏ ký tự không phải số
    ```
:::

:::info[**📌 Node "Normalize Price Values" (Code)**]
- **Chỉnh logic chuyển đổi giá thành số**:
  - Nếu giá có **đơn vị tiền tệ** (VND, USD), chỉnh sửa code để loại bỏ ký tự:
    ```javascript
    const priceString = $json["price"].toString().replace(/[^\d]/g, '');
    $json["price"] = parseFloat(priceString);
    ```
:::

:::info[**📌 Node "Compute Price Change" (Code)**]
- **So sánh giá cũ vs. mới**:
  - Code hiện tại so sánh `last_price` (trong Sheet) vs. `price` (trích xuất).
  - Nếu cần **định dạng % thay đổi**, chỉnh sửa:
    ```javascript
    const priceChange = ((($json["price"] - $json["last_price"]) / $json["last_price"]) * 100).toFixed(2);
    $json["price_change_percent"] = priceChange;
    $json["price_changed"] = priceChange !== "0.00";
    ```
:::

:::info[**📌 Node "Is Price Changed?" (If)**]
- **Chỉnh điều kiện**:
  - Nếu giá không thay đổi (`price_changed = false`), workflow **dừng** cho sản phẩm đó.
  - Nếu giá thay đổi, tiếp tục các node sau.
:::

:::info[**📌 Node "Build Telegram Alert Message" (Code)**]
- **Chỉnh nội dung cảnh báo**:
  - Thay đổi format để phù hợp với Telegram:
    ```javascript
    $node["Build Telegram Alert Message"].json = {
      text: `🚨 GIÁ THAY ĐỔI: ${$json["product_name"]}\n` +
            `🔗 Link: ${$json["product_url"]}\n` +
            `💰 Giá cũ: ${$json["last_price"]} VND\n` +
            `💰 Giá mới: ${$json["price"]} VND\n` +
            `📈 % Thay đổi: ${$json["price_change_percent"]}\n` +
            `⏰ Thời gian: ${new Date().toLocaleString()}`
    };
    ```
:::

:::info[**📌 Node "Log Price History to Sheet"**]
- **Chọn tab "Price_History"** trong Google Sheets.
- **Cấu hình cột**:
  - `timestamp`, `product_name`, `product_url`, `last_price`, `current_price`, `price_change_percent`.
:::

:::info[**📌 Node "Update Last Price in Master Sheet"**]
- **Chỉnh cột `last_price`** để cập nhật giá mới.
- **Thêm delay 1 phút** (node `Pause Before Updating Sheet`) để tránh xung đột.
:::

---

### **3. Kích Hoạt Workflow**
1. **Test Run** với 1 sản phẩm mẫu:
   - Chọn node **"Daily 8 AM Trigger"** và nhấn **"Run Workflow"**.
   - Kiểm tra kết quả trong **Telegram** và **Google Sheets**.
2. **Bật Active**:
   - Chuyển slider ở góc trên bên phải thành **đỏ (Active)**.
3. **Kiểm tra lịch sử**:
   - Mở tab **Price_History** trong Google Sheets để theo dõi lịch sử giá.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Slack thay vì Telegram**
- Thay node **Telegram** bằng **Slack Webhook**:
  - Cài đặt **Slack App** và lấy **Webhook URL**.
  - Thay đổi node `telegram` thành `httpRequest` với method `POST` và body:
    ```json
    {
      "text": "{{$node["Build Telegram Alert Message"].json.text}}"
    }
    ```
  - Gửi đến URL Slack (ví dụ: `https://hooks.slack.com/services/XXX`).

### **2. Gửi Báo Cáo Định Kỳ qua Email**
- Sử dụng node **Email** (n8n-nodes-base.email) hoặc **SendGrid**:
  - Tạo một **workflow mới** chạy hàng tuần.
  - Trích xuất dữ liệu từ **Price_History** và gửi báo cáo dưới dạng **PDF/Excel**.
  - Ví dụ:
    ```javascript
    // Node Code để tạo nội dung email
    $node["Email Content"].json = {
      subject: "Báo cáo giá hàng tuần",
      html: `<h1>Báo cáo giá từ ${new Date().toLocaleDateString()}</h1>
             <p>Danh sách sản phẩm có giá thay đổi:</p>
             <table>${$json["price_history"].map(item => `
               <tr>
                 <td>${item.product_name}</td>
                 <td>${item.price_change_percent}%</td>
               </tr>
             `).join('')}</table>`
    };
    ```

### **3. Lọc Sản Phẩm Theo Ngưỡng Giá**
- Thêm node **Filter** trước khi so sánh giá:
  - Chỉ so sánh sản phẩm có **giá > 1 triệu** hoặc **giá < 500k**.
  - Ví dụ:
    ```javascript
    // Node Code để lọc
    if ($json["price"] > 1000000) {
      $node["continue"].json = $json;
    } else {
      $node["continue"].json = null;
    }
    ```

### **4. Lưu Log Lỗi vào Google Sheets**
- Thêm node **Error Handling** để ghi lỗi:
  - Sử dụng node **Code** để kiểm tra lỗi:
    ```javascript
    if ($node["Load Product Page HTML"].error) {
      $json["error"] = $node["Load Product Page HTML"].error.message;
      $json["product_url"] = $json["product_url"];
      $node["Log Error"].json = $json;
    }
    ```
  - Gửi lỗi đến **tab "Errors"** trong Google Sheets.

### **5. Tích Hợp với Google Analytics**
- Nếu muốn **phân tích hành vi người dùng** khi giá thay đổi:
  - Sử dụng node **Google Analytics** (n8n-nodes-base.googleAnalytics) để gửi dữ liệu.
  - Ví dụ: Gửi sự kiện `price_change` khi giá thay đổi.

---

## 📌 **Kết Luận: Áp Dụng Ngay để Tối Ưu Hóa Chiến Lược Giá**

Workflow này không chỉ **tự động hóa theo dõi giá hàng ngày** mà còn **giúp các sếp**:
✔ **Tránh rủi ro giá** với cảnh báo Telegram tức thời.
✔ **Tối ưu hóa doanh thu** bằng phân tích lịch sử giá.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược kinh doanh.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 sản phẩm** trước khi áp dụng toàn bộ danh sách.
3. **Tích hợp Telegram/Slack** để nhận cảnh báo.
4. **Phân tích dữ liệu** trong Google Sheets để điều chỉnh chiến lược giá.

**Nếu cần hỗ trợ thêm**, liên hệ với **Tony Paul** (tác giả workflow) qua:
🔗 [Blog Datahut