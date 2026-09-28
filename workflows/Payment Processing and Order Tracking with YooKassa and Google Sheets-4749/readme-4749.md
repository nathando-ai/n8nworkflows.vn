---
title: "💳 Tự Động Hóa Thanh Toán & Theo Dõi Đơn Hàng với YooKassa + Google Sheets (Không Code)"
description: "Workflow này giúp các sếp chấp nhận thanh toán trực tuyến qua YooKassa và ghi chép tất cả đơn hàng, giao dịch vào Google Sheets một cách tự động, hoàn toàn không cần viết code. Phù hợp cho cửa hàng online, bán sản phẩm số hoặc khóa học."
slug: "tieu-dong-hoa-thanh-toan-voi-yookassa-google-sheets"
tags: [n8n, automation, finance, ecommerce, yookassa, google-sheets, no-code]
keywords: [n8n workflow thanh toán, tự động hóa thanh toán online, yookassa google sheets, checkout tự động, theo dõi đơn hàng]
---

# 🚀 **Tự Động Hóa Thanh Toán & Theo Dõi Đơn Hàng với YooKassa + Google Sheets**

### **Giải pháp hoàn hảo cho các sếp bán hàng online không muốn mất thời gian với backend**
Hãy tưởng tượng: Khách hàng chọn sản phẩm, thanh toán một cách nhanh chóng, và tất cả thông tin đơn hàng, giao dịch tự động được ghi vào Google Sheets — **không cần viết một dòng code nào!** Workflow này giúp các sếp:
- **Chấp nhận thanh toán trực tuyến** qua YooKassa (ngân hàng uy tín tại Nga và các quốc gia CIS).
- **Theo dõi toàn bộ quá trình** từ chọn sản phẩm đến hoàn thành giao dịch.
- **Ghi chép tự động** tất cả đơn hàng và giao dịch vào Google Sheets để phân tích dễ dàng.
- **Xử lý webhook** của YooKassa để cập nhật trạng thái thanh toán và hoàn tiền.

Không cần là kỹ sư, các sếp chỉ cần **cấu hình vài bước** là có thể triển khai hệ thống thanh toán chuyên nghiệp!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản cloud. Với VPS, các sếp có thể:
✅ **Tùy chỉnh** và mở rộng không giới hạn.
✅ **Bảo mật cao** (không phụ thuộc vào nhà cung cấp cloud).
✅ **Tiết kiệm chi phí dài hạn** so với các gói premium.

👉 **[Đăng ký VPS TinoHost với mã giảm giá VPSN8N (giảm 39%)](https://tino.vn/vps-n8n?affid=388)**
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng (đảm bảo ổn định)](https://my.bnix.one/aff.php?aff=172)**
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết backend, tự động hóa toàn bộ quy trình thanh toán.
- **Chính xác 100%**: Ghi chép tự động vào Google Sheets, không sai sót như thủ công.
- **Theo dõi toàn diện**: Xem trạng thái đơn hàng, giao dịch, hoàn tiền từ một bảng dữ liệu duy nhất.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không bị ngắt kết nối.
- **Dễ dàng mở rộng**: Thêm logic mới như gửi email xác nhận, tích hợp Telegram, hoặc cập nhật trạng thái sản phẩm.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản YooKassa**
- **Shop ID** và **Secret Key** từ [trang quản trị YooKassa](https://yoomoney.ru/).
- **Domain** để cấu hình `return_url` (ví dụ: `https://tudonghoa.vn`).

### **2. Google Sheets**
- **Bảng `products`** (chứa `product_id`, `title`, `price`).
- **Bảng `orders`** (ghi chép đơn hàng thành công).
- **Bảng `transactions`** (ghi chép tất cả giao dịch, bao gồm hoàn tiền).

### **3. Credentials trong n8n**
- **Google Sheets OAuth2** (cấu hình từ [Google Cloud Console](https://console.cloud.google.com/)).
- **YooKassa Basic Auth** (điền `shopId` và `secretKey`).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4749) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào n8n (đảm bảo không có lỗi syntax).

🔹 **Lưu ý**: Workflow này **không cần code** ngoại trừ phần **Idempotence Key Generation** (sử dụng hàm `uuidv4()` trong node `code`).

---

### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**
#### **A. Cấu hình Google Sheets**
1. **Tạo 3 bảng Google Sheets** với tên:
   - `products` (cấu trúc: `product_id`, `title`, `price`).
   - `orders` (cấu trúc: `order_id`, `product_id`, `email`, `amount`, `created_at`).
   - `transactions` (cấu trúc: `transaction_id`, `order_id`, `amount`, `status`, `created_at`).

2. **Chia sẻ bảng với n8n**:
   - Trong Google Sheets, chọn **Chia sẻ** → **Thêm người dùng** → Điền email của n8n (nếu self-hosted) hoặc **n8n.io**.
   - Cấp quyền **Sửa đổi**.

3. **Cấu hình credentials Google Sheets trong n8n**:
   - Tạo **Google Sheets OAuth2** trong **Credentials** → **Add Credential** → Chọn **Google Sheets**.
   - Đăng nhập và cấp quyền cho n8n.

#### **B. Cấu hình YooKassa**
1. Trong **Credentials** → **Add Credential** → Chọn **HTTP Basic Auth**.
2. Điền:
   - **Username**: `shopId` (mà các sếp lấy từ YooKassa).
   - **Password**: `secretKey` (cũng từ YooKassa).

#### **C. Cấu hình Webhook trong YooKassa**
1. Trong **YooKassa Dashboard**, đi đến **Webhooks**.
2. Thêm **2 URL webhook**:
   - **`/yoomoney`** (để xử lý sự kiện thanh toán/hoàn tiền).
   - **`/status/:id`** (để kiểm tra trạng thái thanh toán).
3. Chọn **Events** cần xử lý:
   - `payment.succeeded`
   - `payment.failed`
   - `refund.succeeded`

#### **D. Cấu hình Node quan trọng**
| **Node**               | **Lưu ý cấu hình**                                                                 |
|------------------------|-----------------------------------------------------------------------------------|
| **Get products**       | Đảm bảo **Google Sheets OAuth2** được chọn và bảng `products` đúng cấu trúc.     |
| **YooKassa Request**   | Kiểm tra `httpBasicAuth` có đúng `shopId` và `secretKey`.                         |
| **Save Order**         | Chọn **Google Sheets OAuth2** và bảng `orders`.                                    |
| **Payment (webhook)**  | Kiểm tra `return_url` trong payload phải đúng domain của các sếp.                |
| **Handle Events (switch)** | Cấu hình các case cho `payment.succeeded`, `refund.succeeded`, `payment.failed`. |
| **Status (webhook)**  | Đảm bảo `YooKassa Request Status` lấy dữ liệu từ API YooKassa.                     |

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi request POST đến `/payment` với payload:
     ```json
     {
       "product_id": "abc123",
       "email": "khachhang@example.com",
       "return_url": "https://tudonghoa.vn/success"
     }
     ```
   - Kiểm tra phản hồi và xem đơn hàng có được ghi vào `orders` không.

2. **Bật Active workflow**:
   - Trong n8n Editor, chuyển trạng thái từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp Email Xác Nhận Thanh Toán**
- Sử dụng **n8n-nodes-base.email** để gửi email xác nhận khi đơn hàng thành công.
- **Cấu hình**:
  - Thêm node **Email** sau `Save Order`.
  - Sử dụng **Template Email** với nội dung:
    ```
    Xin chào {{email}},
    Đơn hàng của bạn đã được xử lý thành công!
    Mã đơn: {{order_id}}
    Sản phẩm: {{product_title}}
    ```

### **2. Theo Dõi Log Giao Dịch**
- Thêm node **Google Sheets** để ghi chép **log lỗi** vào một bảng riêng (`logs`).
- **Cấu hình**:
  - Sau node `Handle Error`, thêm node **Google Sheets** với bảng `logs`.
  - Cấu trúc bảng: `timestamp`, `error_type`, `data`.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n-nodes-base.googleSheets** + **n8n-nodes-base.email** để gửi báo cáo tổng hợp hàng tuần.
- **Cách làm**:
  - Thêm node **Set** để tính tổng doanh thu.
  - Thêm node **Email** để gửi báo cáo cho admin.

### **4. Cập Nhật Trạng Thái Sản Phẩm**
- Sau khi thanh toán thành công, tự động **cập nhật số lượng sản phẩm** trong `products`.
- **Cấu hình**:
  - Sau node `Save Order`, thêm node **Google Sheets** với **operation: update**.
  - Cập nhật cột `quantity` trong `products`.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa thanh toán online **không cần code**, đồng thời theo dõi tất cả đơn hàng và giao dịch trong Google Sheets. Với **YooKassa** và **n8n**, các sếp có thể:
✅ **Chấp nhận thanh toán 24/7** mà không lo gián đoạn.
✅ **Ghi chép tự động** tất cả dữ liệu vào bảng Excel.
✅ **Mở rộng logic** như gửi email, tích hợp Telegram, hoặc cập nhật trạng thái sản phẩm.

**Hãy thử ngay!** Import workflow, cấu hình vài bước, và bắt đầu bán hàng online một cách chuyên nghiệp!

---
**🚀 Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ n8n.io](https://n8n.io/workflows/4749) và cài đặt trên VPS để chạy 24/7.