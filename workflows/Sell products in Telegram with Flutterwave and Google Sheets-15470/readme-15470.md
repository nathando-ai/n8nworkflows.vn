---
title: "🚀 Tự Động Hóa Bán Hàng Telegram Với Flutterwave & Google Sheets - Không Cần Code"
description: "Workflow này biến Telegram thành cửa hàng e-commerce hoàn chỉnh, tự động quản lý danh mục sản phẩm, giỏ hàng, thanh toán an toàn qua Flutterwave, và theo dõi giao hàng - tất cả thông qua Google Sheets làm cơ sở dữ liệu. Giúp các sếp tiết kiệm 100% thời gian thủ công và nâng cao trải nghiệm khách hàng."
slug: "tieu-dong-hoa-ban-hang-telegram-flutterwave-google-sheets"
tags: [n8n, automation, ecommerce, flutterwave, telegram-bot, google-sheets, no-code]
keywords: [tự động hóa bán hàng telegram, flutterwave n8n, bán hàng qua telegram, google sheets automation, workflow bán hàng không code]
---

# 🚀 **Tự Động Hóa Cửa Hàng E-Commerce Trên Telegram Với Flutterwave & Google Sheets**

## **💡 Giới Thiệu: Giải Pháp "Bán Hàng 24/7" Cho Các Sếp**
Hiện nay, việc bán hàng thủ công qua Telegram hay các kênh khác vẫn còn nhiều hạn chế: **khách hàng phải chờ đợi phản hồi, dễ quên giỏ hàng, quản lý đơn hàng rắc rối, và thanh toán không an toàn**. Workflow này **tự động hóa toàn bộ quy trình bán hàng** từ **hiển thị sản phẩm** đến **thanh toán, giao hàng và theo dõi đơn hàng** - **không cần viết một dòng code nào!**

Với **n8n**, các sếp có thể:
✅ **Hiển thị danh mục sản phẩm** trong Telegram một cách động.
✅ **Quản lý giỏ hàng** và cập nhật trạng thái thực thời.
✅ **Thanh toán an toàn** qua Flutterwave (hỗ trợ cả VNĐ và USD).
✅ **Tự động gửi hóa đơn, file sản phẩm (nếu là sản phẩm số)** hoặc thông báo giao hàng.
✅ **Theo dõi đơn hàng** và cảnh báo khi hàng hết kho.
✅ **Tự động gửi báo cáo đơn hàng** cho quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** quản lý bán hàng thủ công.
- **Khách hàng mua hàng 24/7** mà không cần hỗ trợ trực tiếp.
- **Thanh toán an toàn** với Flutterwave (hỗ trợ cả VNĐ và USD).
- **Quản lý kho hàng tự động** với cảnh báo khi hàng cạn kiệt.
- **Tự động gửi hóa đơn, file sản phẩm (nếu là sản phẩm số)** hoặc thông báo giao hàng.
- **Theo dõi đơn hàng** một cách chuyên nghiệp, không cần phần mềm bên thứ ba.
- **Báo cáo tự động** cho quản lý, giúp theo dõi doanh số dễ dàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân để test.

2. **Google Sheets (Cơ sở dữ liệu)**:
   - **3 bảng chính** cần tạo:
     - **Products** (Danh sách sản phẩm với cột: `name`, `price`, `stock`, `file_url` (nếu là sản phẩm số)).
     - **Orders** (Đơn hàng với cột: `order_id`, `user_id`, `items`, `status`, `total`, `email`, `address`).
     - **Session** (Giỏ hàng tạm thời với cột: `user_id`, `cart`, `state`).
   - **Chia sẻ bảng với n8n** bằng OAuth2 (cài đặt trong n8n dưới **Credentials > Google Sheets OAuth2 API**).

3. **Tài khoản Flutterwave**:
   - **Secret Key** (lấy từ [Dashboard Flutterwave](https://dashboard.flutterwave.com/)).
   - **Webhook URL** (sẽ được tạo tự động từ node `Flutterwave Webhook` trong workflow).

4. **Google Drive (Nếu bán sản phẩm số)**:
   - Đảm bảo cột `file_url` trong bảng **Products** chứa liên kết **công khai** đến file Google Drive.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15470](https://n8n.io/workflows/15470).
- Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON tải xuống.
- **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** từ menu.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần cấu hình **các node quan trọng** sau:

##### **🔹 Cấu Hình Telegram Bot**
- **Tất cả node Telegram** (`📱 Telegram Trigger`, `💬 Send Welcome Menu`, `📤 Send Products List`,...) cần **credentials `telegramApi`**.
  - Đi đến **Credentials > Add Credential > Telegram API**.
  - Nhập **Token Bot** từ `@BotFather`.
  - **Lưu ý**: Thay thế `YOUR_TELEGRAM_BOT_TOKEN` trong các node `HTTP Request` (ví dụ: `📤 Send Products List`) bằng token của bạn.

##### **🔹 Cấu Hình Google Sheets**
- **Tất cả node Google Sheets** (`📋 Get User Session`, `📦 Get Product Detail`,...) cần **credentials `googleSheetsOAuth2Api`**.
  - Đi đến **Credentials > Add Credential > Google Sheets OAuth2 API**.
  - Chọn **Google Account** và cấp quyền truy cập.
  - **Điền Document ID** của 3 bảng (**Products**, **Orders**, **Session**) vào các node tương ứng.
    - **Lấy Document ID**:
      1. Mở bảng Google Sheets.
      2. URL bảng sẽ có dạng: `https://docs.google.com/spreadsheets/d/[DOCUMENT_ID]/edit`.
      3. Copy phần `[DOCUMENT_ID]` và dán vào node.

##### **🔹 Cấu Hình Flutterwave**
- **Node `💳 Flutterwave Init Transaction`**:
  - Thay thế **`YOUR_FLUTTERWAVE_SECRET_KEY`** trong **Authorization Header** bằng **Secret Key** từ Flutterwave.
  - Thay thế **`redirect_url: http://t.me/YOUR_BOT_URL`** trong **Body JSON** bằng URL của bot Telegram (ví dụ: `http://t.me/ten_bot_cua_bạn`).
- **Node `🔐 Verify Flutterwave Signature`**:
  - Thay thế **`flutterwave_secret_hash`** trong **URL** bằng **hash key** từ Flutterwave (thường là `FLWSECK-...`).

##### **🔹 Cấu Hình Webhook Flutterwave**
- Sau khi import, node **`💳 Flutterwave Webhook`** sẽ tự động tạo **URL webhook**.
- Đi đến **Dashboard Flutterwave > Settings > Webhooks** và thêm:
  - **URL**: `https://[URL_VPS_CỦA_BẠN]/webhook/flutterwave-payment` (thay `[URL_VPS_CỦA_BẠN]` bằng URL VPS của bạn).
  - **Events**: Chọn tất cả events (`charge.success`, `charge.failed`,...).

##### **🔹 Cấu Hình Node Code (JavaScript)**
- Các node **`🔄 Extract Telegram Data`**, **`📝 Format Products List`**, **`📊 Check Stock for Qty`**,... sử dụng **JavaScript**.
- **Không cần chỉnh sửa** nếu cấu hình Google Sheets và Flutterwave đúng.
- Nếu gặp lỗi, kiểm tra **log trong node Code** để debug.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn `/start` đến bot Telegram.
   - Kiểm tra các bước:
     - Hiển thị danh sách sản phẩm.
     - Thêm sản phẩm vào giỏ hàng.
     - Thanh toán qua Flutterwave.
     - Xác nhận đơn hàng.
2. **Bật Active** workflow sau khi test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram Admin Alerts**:
   - Thêm node **`🔔 Admin: Low Stock Alert`** và **`🔔 Admin: New Order Notification`** để gửi thông báo cho quản lý qua Slack hoặc Telegram.

2. **Lưu Log Tất Cả Các Hoạt Động**:
   - Thêm node **Google Sheets** để ghi log tất cả các hành động của khách hàng (ví dụ: `user_id`, `action`, `timestamp`).

3. **Gửi Báo Cáo Doanh Số Hàng Tháng**:
   - Sử dụng node **`📊 Fetch User Orders`** và **`📤 Send Orders List`** để tự động gửi báo cáo doanh số cho quản lý vào cuối tháng.

4. **Hỗ Trợ Nhiều Ngôn Ngữ**:
   - Sử dụng node **Code** để chuyển đổi ngôn ngữ trong bot (ví dụ: tiếng Việt, tiếng Anh) dựa trên `language_code` của khách hàng.

5. **Tích Hợp Google Analytics**:
   - Thêm node **HTTP Request** để gửi dữ liệu giao dịch đến Google Analytics để theo dõi hiệu suất bán hàng.

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Bán Hàng Ngay Hôm Nay!**
Workflow này **giải phóng các sếp khỏi công việc thủ công**, giúp **bán hàng 24/7** mà không cần hỗ trợ trực tiếp. **Khách hàng có trải nghiệm mua sắm chuyên nghiệp**, trong khi các sếp **tiết kiệm thời gian và giảm thiểu lỗi**.

👉 **Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi kích hoạt.
3. **Bắt đầu bán hàng tự động** và theo dõi kết quả!

**Nếu gặp vấn đề**, các sếp có thể liên hệ với tác giả [Afigo Sam](https://n8n.io/workflows/15470) để hỗ trợ 1:1 hoặc tham gia **community n8n** để trao đổi.

---
**Chúc các sếp thành công với việc tự động hóa bán hàng trên Telegram!** 🚀