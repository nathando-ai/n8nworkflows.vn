---
title: "📊 Tự Động Hóa Báo Cáo Đơn Hàng Shopify Hàng Ngày Với Streamline Connector & Gmail (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho doanh nghiệp bán hàng online để nhận báo cáo tổng hợp đơn hàng Shopify hàng ngày qua email, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Workflow chạy tự động mỗi đêm, kết hợp với Streamline Connector để lấy dữ liệu chính xác từ Shopify."
slug: "tieu-dong-hoa-bao-cao-don-hang-shopify-hang-ngay"
tags: [n8n, automation, shopify, ecommerce, gmail, streamline-connector]
keywords: [tự động hóa shopify, báo cáo đơn hàng hàng ngày, n8n workflow shopify, gửi email tự động từ shopify, streamline connector n8n]
---

# 🚀 **Tự Động Hóa Báo Cáo Đơn Hàng Shopify Hàng Ngày Với Streamline Connector & Gmail**

### **Giải pháp cho doanh nghiệp bán hàng online: Dừng việc kiểm tra đơn hàng thủ công hàng ngày!**
Hàng ngày, các sếp phải mất thời gian quét qua hàng chục đơn hàng trên Shopify để tổng hợp, phân tích và gửi báo cáo cho quản lý hoặc khách hàng. **Công việc này không chỉ tốn thời gian mà còn dễ xảy ra lỗi do con người**. Với workflow này, **n8n sẽ tự động lấy tất cả đơn hàng mới trong 24 giờ qua, chuẩn bị báo cáo và gửi qua email mỗi đêm** – **không cần code, không cần can thiệp thủ công!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra đơn hàng thủ công hàng ngày.
- **Dữ liệu chính xác**: Lấy trực tiếp từ API Shopify qua Streamline Connector, tránh sai sót.
- **Báo cáo tự động**: Email được gửi tự động mỗi đêm với nội dung chuẩn bị sẵn.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
- **Dễ dàng mở rộng**: Có thể thêm logic phân tích, phân loại đơn hàng hoặc gửi báo cáo đến nhiều người nhận.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** và **Shop ID** (để kết nối với Streamline Connector).
2. **Tài khoản Gmail** (để gửi email báo cáo).
3. **API Key của Streamline Connector** (nếu chưa có, đăng ký tại [Streamline](https://streamline.com/)).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/14228) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14228) và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **7 node chính**, các sếp cần chú ý cấu hình như sau:

##### **A. Thiết lập Credential Streamline Connector**
- **Bước 1**: Tạo **credential mới** cho Streamline Connector:
  - Vào **Credentials** → **Add Credential** → Chọn **Streamline**.
  - Nhập **Shop ID** của Shopify (có thể tìm thấy trong **Shopify Admin → Settings → Plan and Permissions**).
  - Lưu credential và chọn credential này trong node **Streamline Connector1**.

- **Bước 2**: Xóa **sticky note** "Create your Streamline credential first" sau khi hoàn tất.

##### **B. Cấu hình Node ScheduleTrigger (Chạy hàng ngày)**
- Node **every_24h** (ScheduleTrigger) được cấu hình mặc định chạy **mỗi ngày lúc 00:00** (giờ UTC).
- **Lưu ý**:
  - Nếu muốn chạy ở giờ Việt Nam (UTC+7), các sếp cần chỉnh **timezone** trong node này thành `Asia/Ho_Chi_Minh`.
  - Nếu muốn chạy ở giờ khác, chỉnh **cron expression** (ví dụ: `0 0 12 * * ?` để chạy lúc 12h trưa hàng ngày).

##### **C. Chỉnh sửa Node Gmail (Địa chỉ nhận email)**
- Node **send_email** (Gmail) mặc định gửi đến địa chỉ `your-email@gmail.com`.
- **Bước 1**: Vào node này và chỉnh **To** thành email của mình hoặc email của quản lý.
- **Bước 2**: Kiểm tra **credentials Gmail** đã được thiết lập chưa (nếu chưa, tạo mới trong **Credentials** → **Add Credential** → **Gmail**).

##### **D. Node Code (Chuẩn bị nội dung email)**
- Node **prepare_email** sử dụng JavaScript để chuẩn bị nội dung email.
- **Lưu ý**:
  - Nếu muốn thay đổi **tiêu đề email** hoặc **nội dung mặc định**, các sếp có thể chỉnh sửa code trong node này.
  - Ví dụ: Thay `Subject: "Daily Shopify Orders Report"` thành `Subject: "Báo cáo đơn hàng Shopify - [Ngày tháng]`.
  - **Không chỉnh sửa nếu không biết code** (n8n sẽ tự động lấy dữ liệu từ đơn hàng và format thành email).

##### **E. Node Filter (Lọc đơn hàng trong 24h)**
- Node **last_24_hours** (Filter) được cấu hình mặc định để lấy đơn hàng trong **24 giờ qua**.
- **Lưu ý**:
  - Nếu muốn thay đổi khoảng thời gian (ví dụ: 48h), chỉnh **condition** trong node này:
    ```json
    "condition": {
      "jsonPath": "$[*]",
      "operator": "dateIsAfter",
      "value": "2 days ago"
    }
    ```

##### **F. Node ManualTrigger (Test trước khi chạy tự động)**
- Node **daily_order_report** (ManualTrigger) được sử dụng để **test workflow trước khi bật chạy tự động**.
- **Bước 1**: Click vào node này để chạy **test run** với dữ liệu mẫu.
- **Bước 2**: Kiểm tra email đã nhận được báo cáo chưa.

---

#### **3. Kích hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active workflow**.
- Workflow sẽ tự động chạy **mỗi ngày** theo lịch trình đã thiết lập (mặc định là 00:00 UTC).
- **Kiểm tra email** vào sáng hôm sau để nhận báo cáo!

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Gửi báo cáo đến nhiều người nhận**:
   - Trong node **send_email**, thay vì chỉ gửi đến 1 email, các sếp có thể thêm nhiều địa chỉ vào trường **To** (ví dụ: `manager@company.com, sales@company.com`).

2. **Thêm logo hoặc header vào email**:
   - Trong node **prepare_email**, các sếp có thể thêm HTML để định dạng email đẹp hơn (ví dụ: thêm logo của shop).
   - **Ví dụ code HTML**:
     ```javascript
     const html = `
       <html>
         <body>
           <h1>Báo cáo đơn hàng Shopify</h1>
           <img src="https://tinothost.com/logo.png" width="200">
           <table>
             <!-- Dữ liệu đơn hàng -->
           </table>
         </body>
       </html>
     `;
     ```

3. **Lưu log đơn hàng vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **prepare_email** để lưu dữ liệu đơn hàng vào bảng tính.
   - **Cách làm**:
     - Tạo một bảng Google Sheets mới.
     - Thêm node **Google Sheets** và chọn **credentials** đã thiết lập.
     - Chỉnh **operation** thành `createRow`.

4. **Gửi báo cáo qua Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** sau node **send_email** để gửi báo cáo đồng thời qua kênh chat.
   - **Cách làm**:
     - Tạo **credentials** cho Slack/Telegram.
     - Thêm node **Slack Bot** hoặc **Telegram Bot** và cấu hình để gửi tin nhắn với nội dung email.

5. **Phân tích đơn hàng theo sản phẩm/người mua**:
   - Sử dụng node **Code** để phân tích dữ liệu và thêm logic phân loại (ví dụ: tính tổng doanh thu theo sản phẩm).
   - **Ví dụ**:
     ```javascript
     const ordersByProduct = {};
     data.forEach(order => {
       order.line_items.forEach(item => {
         const product = item.product_title;
         if (!ordersByProduct[product]) {
           ordersByProduct[product] = 0;
         }
         ordersByProduct[product] += item.quantity * item.price;
       });
     });
     ```

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng online muốn **tự động hóa báo cáo đơn hàng hàng ngày** mà không cần can thiệp thủ công. Với **Streamline Connector**, dữ liệu được lấy chính xác từ Shopify, và **Gmail** giúp gửi báo cáo tự động mỗi đêm.

**Hành động ngay hôm nay**:
1. Import workflow và cấu hình credential.
2. Chỉnh sửa email nhận và lịch trình chạy.
3. Bật **Active workflow** và **ngủ yên** – báo cáo sẽ tự động đến mỗi sáng!

---
**Cần hỗ trợ?** Đừng ngần ngại comment bên dưới hoặc liên hệ với Streamline Connector qua [đây](https://streamline.com/). 🚀