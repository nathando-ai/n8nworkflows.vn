---
title: "🚀 Tự Động Hóa Hẹn Làm Việc Luật Sư Với Thanh Toán Stripe, Lịch Google & Telegram - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn hẹn lịch luật sư từ yêu cầu đặt lịch, thanh toán qua Stripe, xác nhận lịch Google, gửi thông báo đến khách hàng và luật sư, đến ghi chép lịch sử và nhắc nhở 24h trước - Giúp tiết kiệm 100% thời gian hành chính cho văn phòng luật."
slug: "tieu-dong-hoa-he-len-luat-su-stripe-google-telegram"
tags: [n8n, automation, no-code, legal, stripe, google-calendar, gmail, telegram, workflow]
keywords: [tự động hóa đặt lịch luật sư, n8n workflow luật sư, thanh toán Stripe tự động, lịch Google tự động, gửi thông báo Telegram, ghi chép Google Sheets]
---

# 🚀 **Tự Động Hóa Hẹn Làm Việc Luật Sư Với Thanh Toán Stripe, Lịch Google & Telegram**

## **🔥 Nỗi Đau Của Các Sếp Luật Sư**
Hàng ngày, văn phòng luật phải chịu gánh nặng **quản lý hẹn lịch thủ công**, từ nhận yêu cầu đặt lịch, kiểm tra lịch Google, gửi thông báo, đến xử lý thanh toán và nhắc nhở khách hàng. Quá trình này không chỉ **tiêu tốn thời gian** mà còn dễ xảy ra **lỗi nhầm lẫn** (ví dụ: lịch trùng, quên nhắc nhở, hoặc không xác nhận thanh toán kịp thời). **Workflow này giải quyết tất cả vấn đề đó bằng cách tự động hóa 100% quy trình từ đầu đến cuối.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** không phải quản lý lịch thủ công.
- **Không còn lỗi lịch trùng** nhờ kiểm tra tự động trên Google Calendar.
- **Thanh toán tự động** qua Stripe, giảm rủi ro khách hàng bỏ qua.
- **Gửi thông báo chính xác** đến khách hàng và luật sư qua Email & Telegram.
- **Ghi chép lịch sử** tất cả các hẹn lịch vào Google Sheets.
- **Nhắc nhở 24h trước** để khách hàng không quên hẹn.
- **Cá nhân hóa thông báo** với tên, thời gian, và chi tiết hẹn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Calendar** (để kiểm tra và tạo sự kiện).
2. **Tài khoản Gmail** (để gửi Email thông báo).
3. **Tài khoản Stripe** (để tạo liên kết thanh toán).
4. **Bot Telegram** (để gửi thông báo đến khách hàng và luật sư).
5. **Google Sheets** (để ghi chép lịch sử hẹn).
6. **Webhook URL** từ hệ thống đặt lịch của bạn (để nhận yêu cầu đặt lịch).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16080](https://n8n.io/workflows/16080) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **18 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node "When Booking Requested" (Webhook)**
- **Cấu hình Webhook**:
  - **Path**: `lawyer-booking` (không đổi).
  - **HTTP Method**: `POST`.
  - **URL**: Sử dụng URL Webhook từ n8n (cần copy từ tab **Webhooks** trong n8n).
  - **Lưu ý**: Cần **cấu hình trong hệ thống đặt lịch** của bạn (ví dụ: Form Google, website, hoặc CRM) để gửi yêu cầu đặt lịch qua URL này.

##### **🔹 Node "Check Calendar for Open Slot" (Google Calendar)**
- **Chọn tài khoản Google Calendar** (nên là tài khoản chính của luật sư).
- **Chọn lịch** (nên là lịch riêng cho luật sư).
- **Cấu hình quyền truy cập**:
  - Chọn **Lịch** → **Cấp quyền truy cập** cho n8n (nếu chưa có).
  - **Thời gian kiểm tra**: Đặt theo giờ làm việc của luật sư (ví dụ: 8h-17h).

##### **🔹 Node "Post to Stripe Payment API" (HTTP Request)**
- **Cấu hình Stripe**:
  - **API Key**: Copy từ **Stripe Dashboard** → **Developers** → **API Keys**.
  - **Product ID & Price ID**: Tạo trong **Stripe Dashboard** → **Products** và **Prices** (ví dụ: `price_123456789`).
  - **URL**: `https://api.stripe.com/v1/checkout/sessions` (không đổi).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_STRIPE_SECRET_KEY",
      "Content-Type": "application/x-www-form-urlencoded"
    }
    ```
  - **Body**:
    ```json
    {
      "line_items": [
        {
          "price": "YOUR_PRICE_ID",
          "quantity": 1
        }
      ],
      "mode": "payment",
      "success_url": "YOUR_SUCCESS_URL", // Ví dụ: `https://tinodoc.vn/success?booking_id={{$node["Set Booking Details"].json["bookingId"]}}`
      "cancel_url": "YOUR_CANCEL_URL" // Ví dụ: `https://tinodoc.vn/cancel`
    }
    ```

##### **🔹 Node "Email Payment Link to Client" & "Email Booking Confirmation" (Gmail)**
- **Cấu hình Gmail**:
  - **Tài khoản Email**: Sử dụng Email chính của luật sư.
  - **Mã xác minh 2FA**: Bật **Mã ứng dụng không an toàn** trong Gmail (nếu cần).
  - **Template Email**:
    - Sử dụng **HTML template** để cá nhân hóa (ví dụ: `Xin chào {{$node["Set Booking Details"].json["clientName"]}},...`).
    - **Lưu ý**: Cần **mapping các biến** như `clientName`, `appointmentTime`, `paymentLink`, `bookingId`.

##### **🔹 Node "Telegram Payment Link" & "Telegram Lawyer Notification" (Telegram)**
- **Cấu hình Bot Telegram**:
  - **Token Bot**: Tạo bot từ [@BotFather](https://t.me/BotFather) và copy `API Token`.
  - **Chat ID**:
    - **Khách hàng**: Cần **lấy Chat ID** từ Telegram (gửi tin nhắn cho bot, sau đó copy ID từ URL).
    - **Luật sư**: Sử dụng Chat ID của luật sư (nếu có).
  - **Template Telegram**:
    - Sử dụng **Markdown** để định dạng tin nhắn (ví dụ: `*Thông báo:* Hẹn lịch đã được xác nhận!`).

##### **🔹 Node "Append Booking to Sheets" (Google Sheets)**
- **Chọn Google Sheets**:
  - **Tài khoản Google Drive**: Nên là tài khoản chung của văn phòng.
  - **Sheet Name**: Đặt tên như `Booking_Log`.
  - **Columns**: Cần **định nghĩa cột** phù hợp với dữ liệu (ví dụ: `BookingID`, `ClientName`, `AppointmentTime`, `Status`).
  - **Operation**: `Append` (thêm mới).

##### **🔹 Node "When Stripe Payment Confirmed" (Webhook)**
- **Cấu hình Webhook Stripe**:
  - Trong **Stripe Dashboard** → **Developers** → **Webhooks** → **Add Endpoint**.
  - **URL**: URL Webhook từ n8n (tab **Webhooks**).
  - **Events**: Chọn `checkout.session.completed`.
  - **Signing Secret**: Copy từ Stripe và điền vào **n8n Webhook** (node này).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một **yêu cầu đặt lịch mẫu** qua Webhook (node `When Booking Requested`).
  - Kiểm tra **Stripe Payment Link** có được tạo không.
  - Sau khi thanh toán, kiểm tra **Google Calendar** có sự kiện mới không.
  - Xem **Google Sheets** có ghi chép lịch sử không.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack**:
   - Thêm node **Slack** để thông báo cho team khi có hẹn mới.
   - Cấu hình trong **Slack App** và điền **Webhook URL** vào node Slack.

2. **Lưu Log Lịch Sử**:
   - Thêm node **Sticky Note** để ghi chép lỗi hoặc thông tin debug.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động tạo báo cáo số lượng hẹn/lượt thanh toán.

4. **Cá Nhân Hóa Thông Báo**:
   - Sử dụng **LLM (n8n-nodes-ai)** để tự động tạo nội dung Email/Telegram dựa trên yêu cầu của khách hàng.

5. **Xử Lý Trùng Lịch**:
   - Thêm **node If** để kiểm tra lại lịch nếu có nhiều yêu cầu cùng thời gian.

---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian hành chính** cho các sếp luật sư, giúp tập trung vào **công việc tư vấn và giải quyết vụ án** thay vì quản lý lịch. **Chỉ cần import, cấu hình và bật Active**, hệ thống sẽ tự động xử lý tất cả quy trình từ đặt lịch đến nhắc nhở.

**🚀 Hãy áp dụng ngay và tiết kiệm 10+ giờ/tuần cho văn phòng của mình!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/16080)**
**💬 Có thắc mắc? Đăng ký tư vấn miễn phí tại [TinoHost](https://tino.vn/vps-n8n?affid=388)**