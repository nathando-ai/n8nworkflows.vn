---
title: "🚀 Tự Động Hóa Thông Báo Sản Phẩm & Voucher Magento 2 Sang Telegram (Với Bảo Vệ Trùng Lặp)"
description: "Workflow tự động hóa 100% không code để theo dõi sản phẩm mới và voucher trên Magento 2, gửi thông báo ngay lập tức đến Telegram (và Twitter/X) với chức năng bảo vệ chống trùng lặp. Giúp các sếp tiết kiệm thời gian theo dõi thủ công và tránh mất thông tin quan trọng."
slug: "tieu-dong-hoa-thong-bao-magento-2-sang-telegram"
tags: [n8n, automation, magento-2, ecommerce, telegram-bot]
keywords: [tự động hóa magento 2, alert sản phẩm mới telegram, bảo vệ trùng lặp voucher, workflow n8n magento, tự động hóa ecommerce]
---

# 🚀 **Tự Động Hóa Thông Báo Sản Phẩm & Voucher Magento 2 Sang Telegram (Với Bảo Vệ Trùng Lặp)**

## **🔥 Nỗi Đau Của Các Sếp Trong Ecommerce**
Giờ đây, việc theo dõi sản phẩm mới, voucher khuyến mại và cập nhật giá trên Magento 2 hoàn toàn có thể được tự động hóa! Thay vì phải **quét thủ công hàng ngày**, **lo ngại bỏ lỡ thông tin quan trọng**, hoặc **mất thời gian kiểm tra trùng lặp**, các sếp chỉ cần **cài đặt workflow này một lần** và **nhận thông báo tức thì** trên Telegram (và Twitter/X) khi có sự thay đổi.

Workflow này **không chỉ tiết kiệm thời gian mà còn đảm bảo chính xác 100%** nhờ chức năng **bảo vệ chống trùng lặp** thông qua cơ sở dữ liệu MySQL.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần theo dõi thủ công hàng ngày.
✅ **Bảo vệ chống trùng lặp** – Tránh gửi thông báo lặp lại cho cùng một sản phẩm/voucher.
✅ **Thông báo tức thì** – Nhận alert ngay khi có sản phẩm mới hoặc voucher mới trên Telegram.
✅ **Hoạt động liên tục** – Workflow chạy tự động theo lịch trình (Schedule Trigger).
✅ **Kết hợp với Twitter/X** – Có thể tự động đăng sản phẩm/voucher lên Twitter (nếu cần).
✅ **Dữ liệu được lưu trữ** – Tất cả thông tin được ghi vào cơ sở dữ liệu MySQL để theo dõi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Magento 2 (Adobe Commerce)** – API Key và URL API của Magento.
✔ **Tài khoản Telegram Bot** – Token API và Chat ID của bot Telegram.
✔ **Tài khoản Twitter/X (nếu sử dụng)** – API Key và Secret Key.
✔ **Cơ sở dữ liệu MySQL** – Để lưu trữ lịch sử sản phẩm/voucher đã được gửi.
✔ **VPS hoặc máy chủ n8n** – Để chạy workflow 24/7 (không dùng phiên bản cloud miễn phí).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/5893](https://n8n.io/workflows/5893) (chọn **Export as JSON**).
2. **Mở n8n Editor** và nhấn **Import** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiển thị trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. **Dán JSON** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "Schedule Trigger" (Lịch Trình Khởi Động)**
- **Cấu hình thời gian chạy**:
  - Thiết lập **thời gian chạy định kỳ** (ví dụ: **mỗi 1 giờ** hoặc **mỗi ngày lúc 8h sáng**).
  - **Lưu ý**: Nếu chạy trên VPS, đảm bảo **n8n đang hoạt động 24/7**.

#### **🔹 Node "Init Database" (Khởi Tạo Cơ Sở Dữ Liệu)**
- **Cấu hình MySQL**:
  - **Host**: `localhost` (nếu chạy trên VPS cùng máy) hoặc IP VPS.
  - **Database**: Tên cơ sở dữ liệu bạn tạo (ví dụ: `magento_alerts`).
  - **User & Password**: Tài khoản MySQL có quyền truy cập.
  - **Query**:
    ```sql
    CREATE TABLE IF NOT EXISTS posted_products (
      id INT AUTO_INCREMENT PRIMARY KEY,
      product_id VARCHAR(255),
      posted_at DATETIME DEFAULT CURRENT_TIMESTAMP
    );

    CREATE TABLE IF NOT EXISTS posted_vouchers (
      id INT AUTO_INCREMENT PRIMARY KEY,
      voucher_id VARCHAR(255),
      posted_at DATETIME DEFAULT CURRENT_TIMESTAMP
    );
    ```
  - **Nếu không có bảng**, workflow sẽ tự động tạo.

#### **🔹 Node "Get Rule Info" & "Fetch New Product" (Lấy Thông Tin Sản Phẩm)**
- **Cấu hình API Magento**:
  - **URL API**: `https://domain.com/rest/V1/products` (thay `domain.com` bằng domain Magento của bạn).
  - **Headers**:
    - `Authorization: Bearer {API_KEY}`
    - `Content-Type: application/json`
  - **Query Parameters**:
    - `searchCriteria[pageSize]=100` (lấy tất cả sản phẩm mới).
    - `searchCriteria[filterGroups][0][filters][0][field]=created_at`
    - `searchCriteria[filterGroups][0][filters][0][value]=2024-01-01` (thay ngày theo yêu cầu).

#### **🔹 Node "Get Latest Offer" (Lấy Voucher Mới)**
- **Cấu hình API Magento**:
  - **URL API**: `https://domain.com/rest/V1/coupons` (hoặc `https://domain.com/rest/V1/promo_catalog_rules` tùy theo phiên bản).
  - **Headers**: Giống như trên.
  - **Query Parameters**:
    - `searchCriteria[pageSize]=100`
    - `searchCriteria[filterGroups][0][filters][0][field]=created_at`
    - `searchCriteria[filterGroups][0][filters][0][value]=2024-01-01`

#### **🔹 Node "Telegram" (Gửi Thông Báo)**
- **Cấu hình Telegram Bot**:
  - **Token API**: Lấy từ [@BotFather](https://t.me/BotFather).
  - **Chat ID**: Lấy bằng cách gửi tin nhắn cho bot và copy ID từ link.
  - **Message Format**:
    - **Sản phẩm mới**:
      ```json
      {
        "photo": "{{$node["Product Alert to Telegram"].json()["media"]}}",
        "caption": "🚀 **Sản phẩm mới trên Magento!**\n\n📌 **Tên:** {{$node["Get Product Info"].json()["name"]}}\n💰 **Giá:** {{$node["Get Product Info"].json()["price"]}}\n🔗 **Link:** {{$node["Get Product Info"].json()["url"]}}"
      }
      ```
    - **Voucher mới**:
      ```json
      {
        "text": "🎁 **Voucher mới trên Magento!**\n\n💰 **Giá trị:** {{$node["Get Latest Offer"].json()["discount_amount"]}}\n📅 **Hết hạn:** {{$node["Get Latest Offer"].json()["end_date"]}}\n🔗 **Link:** {{$node["Get Latest Offer"].json()["url"]}}"
      }
      ```

#### **🔹 Node "Twitter/X" (Nếu Sử Dụng)**
- **Cấu hình Twitter API**:
  - **API Key & Secret Key**: Lấy từ [Developer Portal Twitter](https://developer.twitter.com/).
  - **Message Format**:
    ```json
    {
      "text": "🚀 **Sản phẩm mới!** {{$node["Get Product Info"].json()["name"]}} - {{$node["Get Product Info"].json()["price"]}} 💰\n{{$node["Get Product Info"].json()["url"]}}",
      "media": "{{$node["Product Alert to Telegram"].json()["media"]}}"
    }
    ```

#### **🔹 Node "If" (Bảo Vệ Trùng Lặp)**
- **Cấu hình logic**:
  - **Product Duplication Protection**:
    ```javascript
    // Kiểm tra nếu sản phẩm đã được gửi trước
    const isDuplicate = await $node["Product Duplication Protection"].execute({
      query: "SELECT * FROM posted_products WHERE product_id = ?",
      params: [$node["Get Product Info"].json()["id"]]
    }).then(res => res.json().length > 0);
    return !isDuplicate;
    ```
  - **Voucher Duplication Protection**:
    ```javascript
    const isDuplicate = await $node["Voucher Duplication Protection"].execute({
      query: "SELECT * FROM posted_vouchers WHERE voucher_id = ?",
      params: [$node["Get Latest Offer"].json()["id"]]
    }).then(res => res.json().length > 0);
    return !isDuplicate;
    ```

#### **🔹 Node "Code" (Định Hình Tin Nhắn)**
- **Sản phẩm**:
  ```javascript
  // Trích xuất thông tin sản phẩm
  const product = $node["Get Product Info"].json();
  return {
    media: product.image_url, // URL ảnh sản phẩm
    name: product.name,
    price: product.price,
    url: product.url
  };
  ```
- **Voucher**:
  ```javascript
  const voucher = $node["Get Latest Offer"].json();
  return {
    discount_amount: voucher.discount_amount,
    end_date: voucher.end_date,
    url: voucher.url
  };
  ```

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Schedule Trigger** một lần thủ công để kiểm tra.
   - Kiểm tra **Telegram** và **Twitter/X** (nếu sử dụng) có nhận được thông báo không.
2. **Bật Active workflow**:
   - Nhấn **Active** trên nút trạng thái workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack**:
   - Thay vì chỉ Telegram, có thể **gửi alert lên Slack** bằng node `n8n-nodes-base.slack`.
   - **Cấu hình**:
     ```json
     {
       "text": "🚨 **New Product Alert!** {{$node["Get Product Info"].json()["name"]}}",
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*New Product:* `{{$node["Get Product Info"].json()["name"]}}`\n*Price:* `{{$node["Get Product Info"].json()["price"]}}`"
           }
         }
       ]
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử sản phẩm/voucher đã được gửi.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.googleSheets`.
     - Cấu hình **Sheet Name** và **Range** để ghi dữ liệu.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo hàng tuần về sản phẩm/voucher mới.
   - **Ví dụ**:
     ```json
     {
       "to": "email@example.com",
       "subject": "Báo cáo sản phẩm mới tuần này",
       "html": `
         <h2>Danh sách sản phẩm mới</h2>
         <ul>
           ${products.map(p => `<li>${p.name} - ${p.price}</li>`).join('')}
         </ul>
       `
     }
     ```

4. **Tối Ưu Hóa Query API**:
   - Nếu Magento có nhiều sản phẩm, **optimize query** để tránh timeout.
   - **Ví dụ**:
     ```sql
     -- Thay vì lấy tất cả, chỉ lấy sản phẩm trong khoảng thời gian gần đây
     SELECT * FROM catalog_product_entity WHERE created_at > '2024-01-01'
     ```

---

## 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn vấn đề theo dõi thủ công** cho Magento 2, giúp các sếp:
✔ **Tiết kiệm thời gian** với tự động hóa hoàn toàn.
✔ **Tránh mất thông tin** nhờ bảo vệ chống trùng lặp.
✔ **Cập nhật tức thì** thông qua Telegram và Twitter/X.
✔ **Dễ dàng mở rộng** với Slack, email và báo cáo định kỳ.

**Hãy áp dụng ngay workflow này và tự động hóa eCommerce của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/5893)**
**📌 [Hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-vps/)**