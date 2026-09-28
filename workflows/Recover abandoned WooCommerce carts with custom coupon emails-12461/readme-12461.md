---
title: "🛒 **Hồi phục giỏ hàng bị bỏ quên WooCommerce bằng email khuyến mãi tự động hóa (N8N)**"
description: "Tự động hóa việc hồi phục đơn hàng bị bỏ quên trên WooCommerce bằng cách gửi email khuyến mãi cá nhân hóa với mã giảm giá độc quyền, giúp tăng tỷ lệ hoàn thành checkout lên đến 30%. Workflow này hoạt động 24/7 mà không cần viết code."
slug: "hoi-phuc-gio-hang-woocommerce-bang-email-khuyen-mai"
tags: [n8n, automation, woocommerce, email-marketing, lead-nurturing, ecommerce]
keywords: [tự động hóa woocommerce, hồi phục giỏ hàng bỏ quên, email khuyến mãi tự động, n8n workflow woocommerce, tăng doanh thu online]
---

# 🚀 **Hồi phục giỏ hàng bị bỏ quên WooCommerce bằng email khuyến mãi tự động hóa**

## **Nỗi đau thực tế của các sếp**
Bạn đã từng mất hàng chục nghìn đồng mỗi tháng vì khách hàng thêm sản phẩm vào giỏ hàng nhưng **bỏ qua** trước khi thanh toán? Theo thống kê, **tỷ lệ giỏ hàng bị bỏ quên** trên WooCommerce dao động từ **60-80%**, trong khi chỉ **10-20%** khách hàng đó quay lại mua lại nếu được khuyến khích. Với workflow này, các sếp sẽ **tự động hóa việc hồi phục** những cơ hội bán hàng bị bỏ quên bằng cách:
✅ **Gửi email khuyến mãi cá nhân hóa** với mã giảm giá độc quyền trong vòng **30 phút** sau khi khách hàng bỏ giỏ.
✅ **Kiểm tra tự động** xem khách hàng đã mua hàng chưa (tránh gửi email không cần thiết).
✅ **Tạo mã giảm giá tự động** với thời hạn sử dụng ngắn (khuyến khích khách hàng mua ngay).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tỷ lệ hoàn thành checkout lên 30%** (theo nghiên cứu của Baymard Institute).
- **Tiết kiệm thời gian** từ việc theo dõi giỏ hàng thủ công (tự động hóa hoàn toàn).
- **Khách hàng cảm thấy được chăm sóc** với email cá nhân hóa và mã giảm giá độc quyền.
- **Giảm chi phí marketing** so với các chiến dịch email truyền thống.
- **Hoạt động liên tục** ngay cả khi các sếp nghỉ ngơi.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản WooCommerce** với **WooCommerce REST API** được kích hoạt.
✔ **Thông tin API Key** của WooCommerce (được tạo trong **WooCommerce → Settings → Advanced → REST API**).
✔ **Thông tin SMTP** để gửi email (có thể là Gmail, SendGrid, hoặc SMTP của hosting).
✔ **Mã giảm giá mặc định** (ví dụ: `HELLO` cho mã `HELLO123`).
✔ **Thời gian hiệu lực của mã giảm giá** (ví dụ: 30 phút).
✔ **Mã HTML email** đã chuẩn bị (có thể sử dụng template từ [n8n.io](https://n8n.io/) hoặc thiết kế riêng).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/12461](https://n8n.io/workflows/12461) (chọn **Export as JSON**).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
3. **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- Nếu các sếp **self-hosted n8n**, đảm bảo **cài đặt n8n trên VPS ổn định** (không bị ngắt kết nối).
- **Không sử dụng phiên bản n8n Community trên cloud** nếu muốn workflow hoạt động liên tục.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Webhook trong WooCommerce**
1. **Tạo Webhook trong WooCommerce**:
   - Đi đến **WooCommerce → Settings → Advanced → Webhooks**.
   - Nhấn **Add Webhook**.
   - **Topic**: Chọn **Action**.
   - **Action Event**: Chọn **woocommerce_add_to_cart**.
   - **Delivery URL**: Dán URL webhook từ n8n (dạng: `https://tên-domain-n8n.com/webhook/fde986cf-7c26-42e9-885d-cb44ee305863`).
   - **Secret (optional)**: Để trống hoặc nhập một chuỗi ngẫu nhiên để tăng bảo mật.

2. **Cấu hình Webhook trong n8n**:
   - Mở node **"Fetching Cart Contents"** (Webhook).
   - Đảm bảo **HTTP Method** là **POST**.
   - **Path** phải khớp với URL trong WooCommerce (trong ví dụ là `fde986cf-7c26-42e9-885d-cb44ee305863`).

#### **B. Cấu hình WooCommerce API**
1. **Tạo API Key trong WooCommerce**:
   - Đi đến **WooCommerce → Settings → Advanced → REST API**.
   - Nhấn **Add Key** và tạo một **Consumer Key** với quyền **Read/Write**.
   - Lưu **Consumer Key** và **Consumer Secret** để sử dụng trong n8n.

2. **Thêm Credentials trong n8n**:
   - Trong **n8n Editor**, nhấn **Credentials** (góc trên bên phải) → **Add Credentials** → **WooCommerce API**.
   - Điền:
     - **Consumer Key**: Từ WooCommerce.
     - **Consumer Secret**: Từ WooCommerce.
     - **Store URL**: URL của cửa hàng WooCommerce (ví dụ: `https://tên-cửa-hàng.com`).

#### **C. Cấu hình SMTP**
1. **Thêm Credentials SMTP**:
   - Nhấn **Credentials** → **Add Credentials** → **SMTP**.
   - Điền thông tin SMTP của hosting hoặc dịch vụ email (ví dụ Gmail):
     - **Host**: `smtp.gmail.com` (hoặc SMTP của hosting).
     - **Port**: `587` (hoặc `465` nếu SSL).
     - **Username**: Email gửi.
     - **Password**: Mật khẩu ứng dụng (nếu sử dụng Gmail).
     - **From Email**: Email gửi (ví dụ: `no-reply@tên-cửa-hàng.com`).
     - **From Name**: Tên hiển thị (ví dụ: `Cửa hàng Tôi`).

#### **D. Cấu hình Code Nodes (đặc biệt quan trọng!)**
Workflow này sử dụng **3 node Code** để:
1. **Lấy dữ liệu đơn hàng mặc định** (`Set Default Order Data`).
2. **Tạo mã giảm giá duy nhất** (`Generate Unique Coupon Code`).
3. **Tạo nội dung email HTML** (`Generate Email HTML`).

Các sếp **phải chỉnh sửa** các node này để phù hợp với cửa hàng:
- **Node "Generate Unique Coupon Code"**:
  - Thay đổi `COUPON_PREFIX` (ví dụ: `HELLO` → `MAGIC`).
  - Thay đổi `EXPIRY_MINUTES` (ví dụ: `30`).
  - Thay đổi `TIMEZONE` (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Dữ liệu mẫu**:
    ```javascript
    return {
      couponCode: `MAGIC${Math.floor(1000 + Math.random() * 9000)}`,
      expiryDate: new Date(Date.now() + 30 * 60 * 1000).toISOString(),
      discountType: 'fixed_cart',
      amount: '10.00',
      description: 'Mã giảm giá hồi phục giỏ hàng',
      individualUse: true,
      expiryDateEnabled: true,
      usageLimit: 1,
      usageLimitPerUser: 1,
    };
    ```

- **Node "Generate Email HTML"**:
  - Thay đổi `CURRENCY_SYMBOL` (ví dụ: `$` → `₫`).
  - Thay đổi nội dung email để phù hợp với brand (có thể sử dụng template từ [n8n.io](https://n8n.io/)).
  - **Dữ liệu mẫu**:
    ```html
    <html>
      <body>
        <h1>🎁 Mã giảm giá đặc biệt cho bạn!</h1>
        <p>Chúng tôi thấy bạn đã thêm sản phẩm vào giỏ hàng nhưng chưa hoàn tất checkout.</p>
        <p>Để hoàn thành đơn hàng, hãy sử dụng mã giảm giá sau:</p>
        <h2>{{ $json.couponCode }}</h2>
        <p>Mã giảm giá này chỉ áp dụng trong 30 phút và chỉ dùng được 1 lần.</p>
        <p>Tổng giá trị giỏ hàng của bạn: {{ $json.cartTotal }}₫</p>
        <p>Xin cảm ơn!</p>
        <p>Team Cửa hàng Tôi</p>
      </body>
    </html>
    ```

#### **E. Thêm mã PHP vào WooCommerce**
Để workflow nhận được dữ liệu giỏ hàng, các sếp **phải thêm mã PHP** vào WordPress:
1. **Tải mã PHP** từ [Pastebin](https://pastebin.com/tp0yFSRN).
2. **Thêm vào `functions.php`** của theme hoặc sử dụng plugin **Header and Footer Code Manager (HFCM)**.
3. **Chỉnh sửa các biến**:
   - `WEBHOOK_URL`: URL webhook trong n8n (ví dụ: `https://tên-domain-n8n.com/webhook/fde986cf-7c26-42e9-885d-cb44ee305863`).
   - `COUPON_PREFIX`: Khớp với mã trong node Code (ví dụ: `MAGIC`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Thêm một sản phẩm vào giỏ hàng trên WooCommerce.
   - Kiểm tra **n8n Editor** để xem workflow có hoạt động không.
   - Nếu có lỗi, kiểm tra **Logs** trong node tương ứng.

2. **Bật Active Workflow**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi email nhắc lại sau 24 giờ**: Sử dụng node **Wait** và **Webhook** để gửi email thứ 2 nếu khách hàng không mua hàng trong 24 giờ.
- **Lưu log hoạt động**: Sử dụng node **Google Sheets** hoặc **Notion** để theo dõi lịch sử email đã gửi.
- **Kết hợp với Slack/Telegram**: Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có đơn hàng bị bỏ quên.
- **Tối ưu hóa thời gian chờ**: Thay đổi `Waiting Time` trong workflow để phù hợp với chiến lược marketing của các sếp (ví dụ: 15 phút thay vì 30 phút).
- **A/B Testing**: Tạo nhiều phiên bản email khác nhau và sử dụng node **Random** để chọn email ngẫu nhiên gửi cho khách hàng.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để hồi phục giỏ hàng bị bỏ quên trên WooCommerce **một cách tự động hóa 100%**, không cần viết code. Với việc **tự động gửi email khuyến mãi cá nhân hóa**, các sếp sẽ:
✔ **Tăng doanh thu** từ những cơ hội bán hàng bị bỏ quên.
✔ **Tiết kiệm thời gian** so với cách làm thủ công.
✔ **Cải thiện trải nghiệm khách hàng** với email chuyên nghiệp.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để bắt đầu hồi phục đơn hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Happy Automating!** 🚀