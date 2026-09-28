---
title: "🚀 Tự Động Hóa Đơn Hàng, Đăng Ký & Quà Tặng Ko-fi Với Webhook Xác Minh - Không Cần Code"
description: "Workflow này tự động xử lý tất cả các giao dịch từ Ko-fi (đơn hàng, đăng ký, quà tặng) với xác minh webhook an toàn, giúp các sếp tiết kiệm thời gian và tránh lừa đảo. Hỗ trợ tích hợp ngay vào hệ thống quản lý doanh thu."
slug: "tu-dong-hoa-don-hang-dang-ky-qua-tang-ko-fi"
tags: [n8n, automation, ko-fi, finance, webhook-verification]
keywords: [n8n workflow ko-fi, tự động hóa đơn hàng ko-fi, xác minh webhook ko-fi, tự động hóa đăng ký ko-fi, tự động hóa quà tặng ko-fi]
---

# 🚀 Tự Động Hóa Đơn Hàng, Đăng Ký & Quà Tặng Ko-fi Với Webhook Xác Minh

### 🔍 Nỗi Đau Của Các Sếp Khi Quản Lý Ko-fi Thủ Công
Các sếp đang phải:
- **Lặp đi lặp lại** kiểm tra email hoặc dashboard Ko-fi để xác nhận giao dịch.
- **Lo ngại bị lừa đảo** khi không có cơ chế xác minh webhook.
- **Tốn thời gian** để phân loại từng loại giao dịch (đơn hàng, đăng ký, quà tặng) và cập nhật vào hệ thống.
- **Không biết cách tích hợp** với các công cụ quản lý tài chính hoặc CRM hiện có.

Workflow này **giải quyết tất cả** bằng cách tự động nhận và xử lý tất cả các giao dịch từ Ko-fi, **xác minh an toàn** thông qua webhook, và **phân loại chính xác** từng loại giao dịch để các sếp chỉ cần **nhận tiền và làm việc hiệu quả hơn**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính bảo mật và ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra email hoặc dashboard Ko-fi thủ công.
- **An toàn tuyệt đối**: Xác minh webhook ngăn chặn giao dịch giả mạo.
- **Tự động phân loại**: Đơn hàng, đăng ký và quà tặng được xử lý riêng biệt.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào thời gian làm việc.
- **Tích hợp dễ dàng**: Kết nối với Google Sheets, Slack, hoặc các hệ thống tài chính khác.
:::

---

### 🔧 Yêu Cầu Cần Thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Ko-fi** và quyền quản lý webhook.
2. **Token xác minh** từ [cài đặt webhook Ko-fi](https://ko-fi.com/manage/webhooks).
3. **URL Webhook** để đăng ký trong Ko-fi (sẽ được tạo trong workflow).
4. **N8n Self-hosted** (không dùng phiên bản miễn phí trên cloud).

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
```bash
# Cách 1: Import từ file JSON
1. Tải file workflow từ [n8n.io/workflows/3186](https://n8n.io/workflows/3186).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON.
3. Chọn **Create Workflow** để bắt đầu.

# Cách 2: Copy/Paste JSON
1. Trên n8n Editor, nhấn **Create Workflow**.
2. Chọn **Import** và chọn **Paste JSON**.
3. Dán toàn bộ mã JSON từ [n8n.io/workflows/3186](https://n8n.io/workflows/3186) vào ô.
4. Nhấn **Import** và tiếp tục cấu hình.
```

#### 2. Các Lưu Ý **BẮT BUỘC** Phải Chỉnh 📌
Workflow này gồm **9 node** chính, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **A. Node "Webhook" (Xác nhận giao dịch từ Ko-fi)**
- **Cấu hình**:
  - **HTTP Method**: Đặt là `POST` (không thay đổi).
  - **Path**: Giá trị mặc định `83f4e1de-2011-487c-a9f7-be6ccbac0782` (không cần thay đổi).
  - **Credentials**: Chọn **None** (không cần API key).
- **Lưu ý**:
  - Sau khi import, **copy URL Webhook** từ node này và **đăng ký trong Ko-fi**:
    1. Đi đến [cài đặt webhook Ko-fi](https://ko-fi.com/manage/webhooks).
    2. Nhấn **Add Webhook** và dán URL từ node Webhook vào.
    3. Chọn **All Events** để nhận tất cả giao dịch.

##### **B. Node "Prepare" (Điền Token Xác Minh)**
- **Cấu hình**:
  - Trong tab **Credentials**, chọn **New Credentials** và đặt tên (ví dụ: `Ko-fi-Verification`).
  - Trong tab **Main**, tìm **Verification Token** và **điền token** từ Ko-fi:
    1. Trên trang [cài đặt webhook Ko-fi](https://ko-fi.com/manage/webhooks), mở phần **Advanced**.
    2. Copy **Verification Token** và dán vào node này.
  - **Lưu ý**: Nếu không điền đúng token, **tất cả giao dịch sẽ bị từ chối** và workflow sẽ không hoạt động.

##### **C. Node "Check type" (Switch - Phân loại giao dịch)**
- **Cấu hình**:
  - Node này sử dụng **JSONPath** để phân loại giao dịch thành:
    - **Donation** (quà tặng).
    - **Subscription** (đăng ký).
    - **Shop Order** (đơn hàng).
  - **Không cần thay đổi** cấu hình mặc định, nhưng các sếp có thể **thêm node sau** để xử lý từng loại riêng biệt (ví dụ: gửi thông báo Slack, cập nhật Google Sheets).

#### 3. Kích Hoạt ⚡️
1. **Test Run** với dữ liệu mẫu:
   - Trên Ko-fi, tạo một **giao dịch mẫu** (ví dụ: một quà tặng nhỏ).
   - Trong n8n, nhấn **Run Workflow** và kiểm tra **log** để đảm bảo workflow nhận và xử lý giao dịch.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **Donation**, **Subscription**, hoặc **Shop Order** để **nhận thông báo tức thời** khi có giao dịch mới.
   - Ví dụ:
     ```json
     {
       "node": "slack",
       "operation": "sendMessage",
       "text": "💰 New Ko-fi Donation: {{$json.body.amount}} from {{$json.body.user.name}}",
       "channel": "#ko-fi-alerts"
     }
     ```

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** sau node **Prepare** để **lưu tất cả giao dịch** vào một bảng Excel.
   - Cấu hình:
     - **Sheet Name**: `Ko-fi-Transactions`.
     - **Columns**: `Date`, `Type`, `Amount`, `User`, `Status`.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node **Set** để tính tổng doanh thu hàng tháng và gửi báo cáo qua **email** hoặc **Slack**.
   - Ví dụ:
     ```json
     {
       "node": "email",
       "to": "sếp@example.com",
       "subject": "Báo cáo doanh thu Ko-fi Tháng {{$date.format('MMMM YYYY')}}",
       "body": "Tổng doanh thu: {{$json.totalAmount}}"
     }
     ```

4. **Xử Lý Lỗi Hiệu Quả**:
   - Node **Stop and Error** sẽ **dừng workflow** nếu có lỗi. Các sếp có thể **thêm node Email** trước node này để **nhận thông báo lỗi** qua email.

---

### 📌 Kết Luận
Workflow này **giải phóng thời gian** của các sếp khỏi việc quản lý Ko-fi thủ công, đồng thời **tăng cường an toàn** bằng xác minh webhook. Với **cấu hình đơn giản**, các sếp có thể:
✅ **Tự động nhận tất cả giao dịch** (đơn hàng, đăng ký, quà tặng).
✅ **Phân loại và xử lý riêng biệt** từng loại giao dịch.
✅ **Tích hợp với Slack, Google Sheets, hoặc email** để quản lý hiệu quả.

**Hành động ngay hôm nay**:
1. **Import workflow** và **cấu hình Webhook** trong Ko-fi.
2. **Điền token xác minh** vào node **Prepare**.
3. **Bật Active** và **test với giao dịch mẫu**.
4. **Tích hợp thêm** Slack, Google Sheets, hoặc email để quản lý thông minh.

**💡 Mẹo cuối**: Nếu các sếp muốn **tự động hóa thêm**, có thể **mở rộng workflow** để kết nối với **Stripe, PayPal, hoặc hệ thống CRM** để quản lý toàn bộ doanh thu từ nhiều nguồn!

---
**🚀 Chúc các sếp thành công!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với tác giả [Audun](https://xqus.com) qua Ko-fi.