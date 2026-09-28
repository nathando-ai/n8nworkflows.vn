---
title: "🚀 Tự Động Hóa Shop Online Trên Telegram Với Paystack & Google Sheets - Không Cần Code"
description: "Workflow này chuyển đổi Telegram thành cửa hàng e-commerce hoàn chỉnh, tự động hóa quản lý sản phẩm, giỏ hàng, thanh toán Paystack và theo dõi đơn hàng - tất cả thông qua Google Sheets làm cơ sở dữ liệu. Giúp các sếp tiết kiệm 100% thời gian thủ công trong bán hàng 24/7."
slug: "tieu-dong-hoa-shop-online-telegram-paystack-google-sheets"
tags: [n8n, automation, ecommerce, telegram-bot, paystack, google-sheets, no-code, crm]
keywords: [tự động hóa bán hàng telegram, paystack n8n, shop online trên telegram, quản lý giỏ hàng tự động, google sheets ecommerce, workflow n8n bán hàng]
---

# 🚀 **Tự Động Hóa Shop Online Trên Telegram Với Paystack & Google Sheets**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ mệt mỏi với việc:
- **Quản lý sản phẩm thủ công** trên Telegram, mất nhiều thời gian để cập nhật danh sách hàng hóa?
- **Không thể tự động hóa thanh toán** mà phải nhờ nhân viên theo dõi từng đơn hàng?
- **Không biết cách theo dõi đơn hàng** một cách chuyên nghiệp, dẫn đến trải nghiệm khách hàng kém?
- **Mất thời gian phản hồi** khi khách hàng hỏi về giỏ hàng, đơn hàng hoặc thanh toán?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tạo cửa hàng e-commerce hoàn chỉnh trên Telegram** (không cần website)
✅ **Quản lý sản phẩm, giỏ hàng và thanh toán Paystack tự động**
✅ **Theo dõi đơn hàng từ thanh toán đến giao hàng**
✅ **Tự động gửi thông báo** khi đơn hàng được đặt, thanh toán, giao hàng
✅ **Hỗ trợ khách hàng 24/7** thông qua Telegram

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công** trong bán hàng, quản lý đơn hàng và thanh toán.
- **Tăng trải nghiệm khách hàng** với giao diện Telegram thân thiện và thanh toán an toàn Paystack.
- **Quản lý sản phẩm và tồn kho** một cách tự động từ Google Sheets.
- **Theo dõi đơn hàng chi tiết** từ thanh toán đến giao hàng, giảm thiểu lỗi.
- **Tự động hóa báo cáo** và thông báo cho quản trị viên khi có đơn hàng mới hoặc hàng tồn kho thấp.
- **Không cần code** – chỉ cần cấu hình và chạy ngay!
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **Token API**.
   - Cài đặt bot vào nhóm hoặc chat cá nhân với khách hàng.

2. **Google Sheets**:
   - **3 bảng dữ liệu** cần thiết:
     - **Products** (danh sách sản phẩm với tên, giá, mã sản phẩm, tồn kho, link Google Drive nếu là sản phẩm số).
     - **Orders** (đơn hàng với trạng thái, thời gian, chi tiết sản phẩm).
     - **Session** (quản lý trạng thái giỏ hàng của khách hàng).
   - **Cấu trúc cột tiêu chuẩn** (cần tham khảo file mẫu trong workflow).
   - **Chia sẻ quyền truy cập** cho n8n với vai trò "Editor".

3. **Paystack**:
   - **Tài khoản Paystack** (test hoặc live).
   - **Secret Key** của Paystack (để cấu hình thanh toán).
   - **Webhook URL** từ node `Paystack Webhook` trong workflow (cần đăng ký trên Paystack).

4. **Google Drive (nếu bán sản phẩm số)**:
   - Đảm bảo các sản phẩm số có **link Google Drive công khai** trong cột `file_url` của bảng `Products`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15388](https://n8n.io/workflows/15388).
- **Import vào n8n Editor**:
  - Trên giao diện n8n, nhấn `Import` → Chọn file JSON vừa tải.
  - Hoặc copy toàn bộ JSON và dán vào `Import Workflow` trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với 98 node, nhưng chỉ cần chú ý đến các phần sau:

##### **🔑 Cấu hình Telegram**
- **Tất cả node liên quan đến Telegram** (`Telegram Trigger`, `Send Welcome Menu`, `Ask Quantity`,...) đều cần **credentials `telegramApi`**.
  - Đi đến **Credentials** → Tạo mới `Telegram API` → Nhập **Token API** từ @BotFather.
  - **Cấu hình Webhook**:
    - Trong node `📱 Telegram Trigger`, đảm bảo `path` là `/` (hoặc tùy chỉnh).
    - Trong node `💳 Paystack Webhook`, cập nhật `path` thành `paystack-payment` (để Paystack gửi callback về).

##### **📊 Cấu hình Google Sheets**
- **Tất cả node Google Sheets** (`Get User Session`, `Create New Session`, `Fetch All Products`,...) cần **credentials `googleSheetsOAuth2Api`**.
  - Đi đến **Credentials** → Tạo mới `Google Sheets OAuth2` → Đăng nhập Google và cho phép truy cập.
  - **Cập nhật Document ID**:
    - Mở bảng `Products`, `Orders`, `Session` trên Google Sheets.
    - Copy **ID của bảng** (phần sau `https://docs.google.com/spreadsheets/d/[ID]/edit`) và điền vào các node tương ứng.
    - Ví dụ: Nếu URL là `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/...`, thì **ID = `1AbCdEfGhIjKlMnOpQrStUvWxYz`**.

##### **💳 Cấu hình Paystack**
- Trong node `💳 Paystack Init Transaction`:
  - Đi đến **Headers** → Thêm `Authorization` với giá trị:
    ```
    Bearer YOUR_PAYSTACK_SECRET_KEY
    ```
  - Thay `YOUR_PAYSTACK_SECRET_KEY` bằng **Secret Key** của Paystack.
- **Cấu hình Webhook Paystack**:
  - Trong node `💳 Paystack Webhook`, sao chép **URL Webhook** (đường dẫn sau khi import).
  - Đăng ký URL này trên **Paystack Dashboard** → **Webhooks** → **Add Webhook** với `event` là `charge.success`, `charge.failed`.

##### **📝 Cấu hình URL Telegram cho HTTP Request**
- Trong các node `📤 Send Products List`, `🛒 Send Cart Display`, `📤 Send Payment Link`,...:
  - Đi đến **URL** → Thay thế `YOUR_TELEGRAM_BOT_TOKEN` bằng **Token API** của bot.
  - **Cấu trúc URL mẫu**:
    ```
    https://api.telegram.org/bot<YOUR_TELEGRAM_BOT_TOKEN>/sendMessage
    ```
  - Đối với `Send Payment Link`, URL sẽ là:
    ```
    https://api.telegram.org/bot<YOUR_TELEGRAM_BOT_TOKEN>/sendMessage
    ```
    với **payload** bao gồm inline keyboard chứa nút "Pay Now".

##### **🔄 Cấu hình Session & Trạng thái**
- Bảng `Session` trên Google Sheets cần **cấu trúc cột chuẩn**:
  - `chat_id`, `user_id`, `state`, `cart`, `email`, `address`, `payment_link`, `order_id`.
- Các node như `💾 Set State: Selecting Qty`, `💾 Set State: Entering Email`,... sẽ **cập nhật trạng thái** của khách hàng trong quá trình mua hàng.

##### **🛠️ Cấu hình sản phẩm số (nếu có)**
- Nếu bán **sản phẩm số**, cần đảm bảo:
  - Cột `file_url` trong bảng `Products` chứa **link Google Drive công khai**.
  - Node `📁 Send Digital File` sẽ tự động gửi file khi đơn hàng được thanh toán.

---

#### **3. Kích hoạt ⚡️**
- **Test run dữ liệu mẫu**:
  - Gửi tin nhắn `/start` đến bot Telegram.
  - Kiểm tra các bước:
    - Danh sách sản phẩm được gửi.
    - Giỏ hàng hoạt động.
    - Thanh toán Paystack được kiểm tra.
    - Đơn hàng được cập nhật trạng thái.
- **Bật Active workflow**:
  - Sau khi kiểm tra thành công, chuyển workflow từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động gửi báo cáo hàng ngày**:
   - Sử dụng **n8n Cron Trigger** để gửi báo cáo tổng hợp đơn hàng qua Telegram hoặc email cho quản trị viên.

2. **Kết hợp với Slack/Email**:
   - Thêm node `Slack` hoặc `Email` để thông báo đơn hàng mới cho team quản lý.

3. **Cập nhật tồn kho tự động**:
   - Sử dụng **Google Sheets API** để cập nhật tồn kho khi đơn hàng được thanh toán thành công.

4. **Hỗ trợ khách hàng đa ngôn ngữ**:
   - Sử dụng node `Code` để chuyển đổi ngôn ngữ trong tin nhắn Telegram dựa trên `language_code` của khách hàng.

5. **Tích hợp với Google Analytics**:
   - Theo dõi hành vi mua hàng của khách hàng để tối ưu chiến lược marketing.

6. **Xóa dữ liệu cũ**:
   - Thêm node `Code` để xóa các session cũ (ví dụ: sau 30 ngày không hoạt động).

---

### 📌 **Kết luận**
Workflow này **chuyển Telegram thành một cửa hàng e-commerce hoàn chỉnh**, tự động hóa toàn bộ quy trình từ bán hàng đến giao hàng, **không cần code**. Các sếp chỉ cần:
✔ **Cấu hình Telegram, Google Sheets và Paystack** theo hướng dẫn.
✔ **Import và chạy workflow** trên n8n.
✔ **Kiểm tra và kích hoạt** để bắt đầu bán hàng 24/7!

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian, tăng doanh thu cho doanh nghiệp!**

---
**💬 Cần hỗ trợ?**
- **Trao đổi 1:1** với tác giả Afigo Sam: [Tư vấn video](https://afigo.dev/consultation) (6+ năm kinh nghiệm tự động hóa).
- **Hỏi đáp cộng đồng**: [n8n Community](https://community.n8n.io/) hoặc [Facebook Group](https://www.facebook.com/groups/n8nworkflow/).