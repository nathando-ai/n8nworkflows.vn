---
title: "🎁 Tự Động Hóa Phiếu Giảm Giá Tự Động Cho Khách Hàng Giá Trị Cao Magento 2 - Gmail + API"
description: "Workflow tự động hóa gửi phiếu giảm giá cá nhân hóa cho khách hàng có đơn hàng lớn trên Magento 2, tiết kiệm thời gian và tăng doanh số. Hoạt động 24/7, không cần code."
slug: "tieu-dong-hoa-phieu-giam-gia-magento-2-gmail"
tags: [n8n, automation, ecommerce, magento-2, gmail-api, no-code]
keywords: [tự động hóa magento 2, phiếu giảm giá tự động, n8n workflow, giảm giá khách hàng giá trị cao, api magento 2]
---

# 🚀 **Tự Động Hóa Phiếu Giảm Giá Cho Khách Hàng Giá Trị Cao Magento 2 - Gmail + API**

### **Nỗi Đau Của Các Sếp Ecommerce**
Các sếp Magento 2 thường phải **làm thủ công** việc:
- **Xem xét đơn hàng** của khách hàng giá trị cao.
- **Tạo phiếu giảm giá** riêng cho từng khách hàng.
- **Gửi email cá nhân hóa** thông báo phiếu giảm giá.
- **Quản lý thời gian** để không bỏ lỡ khách hàng tiềm năng.

Kết quả? **Thời gian bị lãng phí**, khách hàng không nhận được sự chăm sóc kịp thời, và doanh số có thể bị bỏ lỡ. **Workflow này giải quyết tất cả bằng tự động hóa 100% không cần code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần làm thủ công cho từng khách hàng.
- **Tăng doanh số**: Khách hàng giá trị cao nhận phiếu giảm giá kịp thời.
- **Cá nhân hóa**: Phiếu giảm giá được tạo riêng cho từng khách hàng.
- **Hoạt động liên tục**: Workflow chạy tự động hàng tháng, không cần can thiệp.
- **Tăng trải nghiệm khách hàng**: Email thông báo chuyên nghiệp, logo cửa hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Magento 2 Admin API**:
   - API Key và Secret Key từ **Admin Panel** (System → Web Services → OAuth).
   - URL API của Magento 2 (ví dụ: `https://domain.com/rest`).
2. **Tài khoản Gmail**:
   - Email từ Gmail (không phải Google Workspace) để gửi phiếu giảm giá.
   - **App Password** (nếu sử dụng 2FA).
3. **Logo cửa hàng**:
   - Đường dẫn đến file logo (được lưu trên server hoặc URL trực tiếp).
4. **Thông tin cấu hình**:
   - **Sales Rule Name** (tên quy tắc giảm giá).
   - **Coupon Code Prefix** (ví dụ: `DISCOUNT_`).
   - **Coupon Code Length** (ví dụ: 8 ký tự).
   - **Discount Percentage** (ví dụ: 10%).
   - **Coupon Usage Limit** (ví dụ: 1 lần/một khách hàng).
   - **Coupon Usage Start Date** (ngày bắt đầu sử dụng).
   - **Coupon Usage End Date** (ngày kết thúc sử dụng).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6982) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** → Nhấn **Import** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **API Magento 2** và **Gmail** để tự động hóa. Dưới đây là các bước **cấu hình bắt buộc**:

##### **A. Cấu Hình Node "Cron" (Đặt Lịch Trình)**
- **Cron Expression**: `0 0 1 * * *` (Chạy vào ngày 1 hàng tháng, lúc 00:00).
- **Lưu ý**: Nếu muốn chạy khác, chỉnh sửa biểu thức theo [format cron](https://crontab.guru/).

##### **B. Cấu Hình Node "Get Completed Orders" (Lấy Đơn Hàng Hoàn Thành)**
- **Method**: `GET`
- **URL**: `{{ $json["apiUrl"] }}/V1/orders?searchCriteria[pageSize]=1000`
  - Thay `{{ $json["apiUrl"] }}` bằng URL API của Magento 2 (ví dụ: `https://domain.com/rest`).
- **Headers**:
  - `Authorization: Bearer {{ $json["apiToken"] }}`
    - Thay `{{ $json["apiToken"] }}` bằng **Access Token** từ OAuth Magento 2.
  - `Content-Type: application/json`

##### **C. Cấu Hình Node "Create New Sales Rule" (Tạo Quy Tắc Giảm Giá)**
- **Method**: `POST`
- **URL**: `{{ $json["apiUrl"] }}/V1/carts-rules`
- **Body (JSON)**:
  ```json
  {
    "code": "AUTOMATED_DISCOUNT_${{ $node["Get Customer Order Value"].json["customer_email"] | slice(0, 8) }}",
    "name": "Automated Discount for {{ $node["Get Customer Order Value"].json["customer_email"] }}",
    "from_date": "{{ $json["startDate"] }}",
    "to_date": "{{ $json["endDate"] }}",
    "is_active": 1,
    "customer_group_ids": [],
    "coupon_type": "no_coupon",
    "uses_per_coupon": 1,
    "uses_per_customer": 1,
    "discount_amount": "{{ $json["discountPercentage"] }}",
    "discount_qty_steps": 1,
    "discount_step": 0,
    "apply_to_shipping": 0,
    "times_used": 0,
    "is_rss": 0,
    "simple_action": "by_percent",
    "stop_rules_processing": 0,
    "from_time": "00:00:00",
    "to_time": "23:59:59",
    "customer_emails": "{{ $node["Get Customer Order Value"].json["customer_email"] }}",
    "product_ids": [],
    "category_ids": []
  }
  ```
  - Thay `{{ $json["discountPercentage"] }}` bằng **lệ phí giảm giá** (ví dụ: `10` cho 10%).
  - Thay `{{ $json["startDate"] }}` và `{{ $json["endDate"] }}` bằng ngày bắt đầu/kết thúc sử dụng phiếu.

##### **D. Cấu Hình Node "Generate Coupon for Each Customer" (Tạo Mã Phiếu Giảm Giá)**
- **Method**: `POST`
- **URL**: `{{ $json["apiUrl"] }}/V1/carts-rules/coupons`
- **Body (JSON)**:
  ```json
  {
    "rule_id": "{{ $node["Create New Sales Rule"].json["id"] }}",
    "code": "DISCOUNT_${{ $node["Get Customer Order Value"].json["customer_email"] | slice(0, 8) }}_${{ $node["Get 3 Month Dates"].json["currentMonth"] }}",
    "times_used": 0
  }
  ```
  - **Lưu ý**: Node này tự động tạo **mã phiếu giảm giá** từ email khách hàng.

##### **E. Cấu Hình Node "Send Voucher" (Gửi Email Phiếu Giảm Giá)**
- **Credentials**: Chọn tài khoản Gmail đã cấu hình trước.
- **To**: `{{ $node["Get Customer Order Value"].json["customer_email"] }}`
- **Subject**: `🎁 Phiếu Giảm Giá 10% Cho Bạn - {{ $node["Get Customer Order Value"].json["customer_name"] }}`
- **HTML Body**:
  ```html
  <h2>🎉 Chúc Mừng Bạn!</h2>
  <p>Bạn đã được chọn là khách hàng giá trị cao của chúng tôi!</p>
  <p>Để cảm ơn sự tin tưởng, chúng tôi gửi tặng phiếu giảm giá <strong>10%</strong> cho đơn hàng tiếp theo của bạn.</p>

  <h3>Mã Phiếu Giảm Giá:</h3>
  <p><strong>{{ $node["Generate Coupon for Each Customer"].json["code"] }}</strong></p>

  <h3>Điều Kiện:</h3>
  <ul>
    <li>Giá trị áp dụng: <strong>10%</strong></li>
    <li>Sử dụng được: <strong>1 lần</strong></li>
    <li>Hết hạn: <strong>{{ $node["Get 3 Month Dates"].json["endDate"] }}</strong></li>
  </ul>

  <p>Chúng tôi rất vui khi phục vụ bạn!</p>
  <p><img src="{{ $node["SetOrGet Logo"].json["logoPath"] }}" alt="Logo Cửa Hàng" width="200"></p>
  ```
  - **Lưu ý**:
    - Node **"SetOrGet Logo"** sẽ lấy đường dẫn logo từ **Node "Get Media Path"**.
    - Nếu logo không tồn tại, **cấu hình Node "Get Media Path"** để lấy từ URL hoặc server.

##### **F. Cấu Hình Node "Send Report" (Gửi Báo Cáo Định Kỳ)**
- **To**: Email của quản trị viên (ví dụ: `admin@domain.com`).
- **Subject**: `📊 Báo Cáo Phiếu Giảm Giá Tháng {{ $node["Get 3 Month Dates"].json["currentMonth"] }}`
- **HTML Body**:
  ```html
  <h2>📊 Báo Cáo Phiếu Giảm Giá Tháng {{ $node["Get 3 Month Dates"].json["currentMonth"] }}</h2>
  <p>Tổng số phiếu giảm giá đã gửi: <strong>{{ $node["If"].json["true"].length }}</strong></p>
  <p>Tổng giá trị đơn hàng của khách hàng nhận phiếu: <strong>{{ $node["Get Customer Order Value"].json["total_order_value"] }}</strong> VND</p>
  ```

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi workflow chạy thành công/thất bại.
2. **Lưu Log**:
   - Sử dụng node **Sticky Note** để lưu lịch sử phiếu giảm giá đã gửi.
3. **Gửi Báo Cáo Hàng Tuần**:
   - Chỉnh sửa **Node Cron** để chạy tuần thay vì tháng.
4. **Tăng Cường Cá Nhân Hóa**:
   - Thêm thông tin từ **Magento Customer API** (tên, địa chỉ) vào email.
5. **Kiểm Tra API Magento**:
   - Nếu API Magento không trả về dữ liệu, kiểm tra **Access Token** và **URL API**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp Magento 2 bằng cách tự động hóa việc tạo và gửi phiếu giảm giá cho khách hàng giá trị cao. **Không cần code**, chỉ cần cấu hình API và Gmail là xong!

**Hành động ngay**:
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình API Magento** và **Gmail**.
3. **Bật Active** và để workflow làm việc!

**Cảm ơn các sếp đã đọc đến cuối!** Nếu có vấn đề, hãy để lại comment dưới đây. 🚀