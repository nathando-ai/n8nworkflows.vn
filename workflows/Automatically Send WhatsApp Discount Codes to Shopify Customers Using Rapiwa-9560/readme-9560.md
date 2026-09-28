---
title: "🚀 Tự Động Gửi Mã Giảm Giá WhatsApp Cho Khách Hàng Shopify Với Rapiwa - Không Cần Code!"
description: "Workflow này tự động gửi mã giảm giá qua WhatsApp cho khách hàng Shopify có số điện thoại hợp lệ, tiết kiệm thời gian và tối ưu hóa chuyển đổi. Hỗ trợ theo dõi tất cả các lần gửi và phân loại khách hàng đã xác thực."
slug: "tu-dong-gui-ma-giam-gia-whatsapp-cho-khach-hang-shopify"
tags: [n8n, automation, shopify, whatsapp, rapiwa, no-code, ecommerce]
keywords: [n8n workflow shopify, tự động hóa whatsapp shopify, gửi mã giảm giá tự động, rapiwa api, tự động hóa bán hàng online]
---

# 🚀 **Tự Động Gửi Mã Giảm Giá WhatsApp Cho Khách Hàng Shopify Với Rapiwa**

### **Giải pháp hoàn hảo cho các sếp bán hàng muốn:**
- **Tiết kiệm 100% thời gian** gửi mã giảm giá thủ công qua WhatsApp.
- **Tăng tỷ lệ chuyển đổi** bằng cách tự động liên lạc với khách hàng có số điện thoại hợp lệ.
- **Theo dõi toàn bộ quá trình** gửi mã giảm giá qua Google Sheets.
- **Tối ưu hóa chi phí** bằng cách chỉ gửi mã cho khách hàng có số WhatsApp xác thực.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi có mã giảm giá mới.
✅ **Chỉ gửi cho khách hàng có WhatsApp hợp lệ**: Tránh lãng phí tin nhắn cho số điện thoại không hoạt động.
✅ **Theo dõi chi tiết**: Báo cáo tất cả khách hàng đã gửi và chưa gửi qua Google Sheets.
✅ **Tối ưu hóa API**: Throttling (chậm lại) giữa các yêu cầu để tránh bị chặn API.
✅ **Cá nhân hóa tin nhắn**: Gửi mã giảm giá riêng cho từng khách hàng.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Shopify** với quyền API access.
✔ **API Key của Shopify** (tìm tại **Settings > Apps and Sales Channels > API credentials**).
✔ **Tài khoản Rapiwa** ([Đăng ký miễn phí](https://rapiwa.com/)) và **API Key** (tìm tại **Settings > API Keys**).
✔ **Google Sheets** với cấu trúc mẫu ([Download mẫu](https://docs.google.com/spreadsheets/d/1Zx_WXQW29NsITFPJ-SnjHgOlouvzG_sBNGzSA_B8cSA/edit?usp=sharing)).
✔ **Webhook URL** từ n8n (sẽ được tạo tự động khi import workflow).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/9560](https://n8n.io/workflows/9560) và import vào n8n Editor.
- **Copy/Paste JSON** từ trang trên vào n8n Editor (đảm bảo đã chọn **Import from JSON**).

:::note[Lưu ý]
- **Không thay đổi cấu trúc node** trừ khi hiểu rõ logic.
- **Không xóa node `Wait`** để tránh bị chặn API.
:::

---

### **2. Các bước cấu hình bắt buộc 📌**

#### **🔹 Node 1: Webhook (Nhận Webhook từ Shopify)**
- **Không cần cấu hình thêm**, workflow sẽ tự động nhận HTTP POST từ Shopify khi có mã giảm giá mới.
- **Lưu ý**: Đảm bảo **Webhook URL** trong Shopify trùng khớp với `path` trong node Webhook (`a9b6a936-e5f2-4d4c-9cf9-182de0a970d5`).

#### **🔹 Node 2: Clean Webhooks Response Data (Lọc dữ liệu từ Shopify)**
- **Không cần chỉnh sửa**, node này tự động trích xuất:
  - `title` (tên mã giảm giá)
  - `status` (trạng thái)
  - `created_at` (thời gian tạo)
  - `shop_domain` (domain Shopify)

#### **🔹 Node 3: Get All Customer Data In Shopify Store (Lấy dữ liệu khách hàng)**
- **Cấu hình API Key**:
  - Trong node `httpRequest`, điền:
    - **URL**: `https://{{shop_domain}}/admin/api/2024-01/customers.json`
    - **Headers**:
      ```
      Content-Type: application/json
      X-Shopify-Access-Token: {{API_KEY_SHOPIFY}}
      ```
  - **Tham số query**:
    - `fields=email,phone,total_spent`

#### **🔹 Node 4: Clean Customer Data In Shopify Store (Lọc khách hàng có tổng tiêu dùng > 5000)**
- **Không cần chỉnh sửa**, node này tự động:
  - Lọc khách hàng có `total_spent > 5000`.
  - Trích xuất: `name`, `phone`, `email`, `totalSpent`.

#### **🔹 Node 5: Clean WhatsApp Number (Làm sạch số điện thoại)**
- **Không cần chỉnh sửa**, node này:
  - Loại bỏ ký tự đặc biệt (ví dụ: `+84`, `0`, `-`, ` `).
  - Chuyển thành số nguyên (ví dụ: `84381234567` → `381234567`).

#### **🔹 Node 6: Check Valid WhatsApp Number Using Rapiwa (Xác thực số WhatsApp)**
- **Cấu hình API Key**:
  - Trong node `httpRequest`, điền:
    - **URL**: `https://app.rapiwa.com/api/verify-whatsapp`
    - **Headers**:
      ```
      Content-Type: application/json
      Authorization: Bearer {{API_KEY_RAPIWA}}
      ```
    - **Body (JSON)**:
      ```json
      {
        "phone": "{{cleaned_phone_number}}"
      }
      ```
- **Kiểm tra phản hồi**:
  - Nếu `data.exists === true` → Số WhatsApp hợp lệ.
  - Nếu `data.exists === false` → Số không hợp lệ.

#### **🔹 Node 7: Send Message Using Rapiwa (Gửi tin nhắn WhatsApp)**
- **Cấu hình API Key**:
  - Trong node `httpRequest`, điền:
    - **URL**: `https://app.rapiwa.com/api/send-message`
    - **Headers**:
      ```
      Content-Type: application/json
      Authorization: Bearer {{API_KEY_RAPIWA}}
      ```
    - **Body (JSON)**:
      ```json
      {
        "phone": "{{cleaned_phone_number}}",
        "message": "🎉 Mã giảm giá {{discount_code}} dành riêng cho bạn! Sử dụng tại: {{shop_domain}} 🛒"
      }
      ```

#### **🔹 Node 8 & 9: Save Data in Google Sheets (Lưu log)**
- **Cấu hình Google Sheets OAuth2**:
  - Đăng nhập vào n8n và kết nối tài khoản Google Sheets.
  - Chọn **Google Sheets OAuth2 API** trong credentials.
- **Cấu hình Sheet**:
  - Điền **Sheet Name** (ví dụ: `Khách hàng đã gửi`, `Khách hàng chưa gửi`).
  - **Headers** trong Google Sheets phải trùng khớp với dữ liệu được append:
    ```
    Customer Name | Email | Phone | Total Spent | Discount Code | Verify | Status
    ```

#### **🔹 Node 10: Wait (Throttling)**
- **Cấu hình thời gian chờ**:
  - Đặt **delay** từ **2-5 giây** để tránh bị chặn API.

---

### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Tạo một **mã giảm giá mới** trong Shopify để kích hoạt webhook.
  - Kiểm tra **Google Sheets** xem dữ liệu đã được append chưa.
- **Bật Active**:
  - Chuyển workflow sang **Active** trong n8n Dashboard.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
🔹 **Kết hợp với Slack/Telegram**:
  - Thêm node `httpRequest` để gửi thông báo khi có khách hàng mới được gửi mã giảm giá.
  - Ví dụ:
    ```json
    {
      "text": "🚀 Mã giảm giá đã được gửi cho: {{customer_name}} (Số điện thoại: {{phone}})"
    }
    ```
    → Gửi đến **Webhook Slack/Telegram**.

🔹 **Gửi báo cáo định kỳ**:
  - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp hàng tuần qua email.
  - Ví dụ: "Tổng số khách hàng đã nhận mã giảm giá: 50, Tổng giá trị: 20M VND".

🔹 **Tối ưu hóa mã giảm giá**:
  - Thêm node `code` để **lọc khách hàng theo tiêu chí khác** (ví dụ: khách hàng chưa mua trong 30 ngày).
  - Ví dụ:
    ```javascript
    // Lọc khách hàng chưa mua trong 30 ngày
    const thirtyDaysAgo = new Date();
    thirtyDaysAgo.setDate(thirtyDaysAgo.getDate() - 30);
    const filteredCustomers = $input.all().filter(customer =>
      customer.last_order_date < thirtyDaysAgo.toISOString()
    );
    return { json: { customers: filteredCustomers } };
    ```

🔹 **Lưu log chi tiết hơn**:
  - Thêm cột `timestamp` và `attempt_count` vào Google Sheets để theo dõi số lần gửi thất bại.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc gửi mã giảm giá qua WhatsApp cho khách hàng Shopify, **tiết kiệm thời gian và tăng tỷ lệ chuyển đổi**. Các sếp chỉ cần **cấu hình API và Google Sheets**, sau đó workflow sẽ hoạt động **24/7** mà không cần can thiệp.

:::success[🚀 **Áp dụng ngay!**]
1. **Import workflow** từ [n8n.io/workflows/9560](https://n8n.io/workflows/9560).
2. **Cấu hình API Key** theo hướng dẫn.
3. **Bật Active** và chờ Shopify tạo mã giảm giá mới.
4. **Theo dõi kết quả** trên Google Sheets!

**Nếu gặp vấn đề**, liên hệ [Rapiwa Support](https://wa.me/8801322827799) hoặc tham gia **Facebook Group SpaGreen** để được hỗ trợ!
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::