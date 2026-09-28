---
title: "🚀 Tự Động Gửi Thông Báo Thanh Toán Stripe Trên WhatsApp Mới Chỉ Với 5 Phút - Không Cần Code!"
description: "Giải pháp tự động hóa hoàn toàn miễn phí giúp doanh nghiệp gửi thông báo xác nhận thanh toán Stripe ngay lập tức qua WhatsApp cho khách hàng, tăng trải nghiệm và giảm thời gian phản hồi. Sử dụng MoltFlow để kết nối với API WhatsApp Business API."
slug: "tu-dong-hoa-thong-bao-thanh-toan-stripe-whatsapp"
tags: [n8n, automation, stripe, whatsapp-business-api, lead-nurturing, no-code]
keywords: [tự động hóa stripe whatsapp, gửi thông báo thanh toán qua whatsapp, n8n workflow stripe, tự động hóa bán hàng online, api whatsapp business]
---

# 🚀 **Tự Động Gửi Thông Báo Thanh Toán Stripe Trên WhatsApp - Không Cần Code!**

### **💸 Bạn đã từng gặp tình huống này?**
- Khách hàng thanh toán thành công trên website nhưng không nhận được thông báo xác nhận ngay lập tức.
- Phải tra cứu thủ công mỗi lần khách hàng gọi hỏi: *"Bạn đã thanh toán chưa?"*
- Mất thời gian phản hồi, làm giảm trải nghiệm mua hàng và tăng tỷ lệ hủy đơn.

**Giải pháp của chúng ta?** Một **workflow tự động hóa hoàn toàn** chỉ với **5 phút setup**, giúp:
✅ Gửi **thông báo xác nhận thanh toán** ngay lập tức qua WhatsApp khi khách hàng thanh toán thành công trên Stripe.
✅ **Không cần code**, chỉ cần kết nối Stripe Webhook với API WhatsApp Business thông qua **MoltFlow**.
✅ **Tăng độ tin cậy** với khách hàng và giảm thời gian phản hồi.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian phản hồi**: Thông báo tự động trong giây lát, không cần nhân viên tra cứu.
- **Tăng trải nghiệm khách hàng**: Khách hàng nhận được thông báo ngay lập tức, giảm lo lắng về thanh toán.
- **Tăng tỷ lệ hoàn thành đơn hàng**: Thông báo xác nhận giúp khách hàng yên tâm hơn khi mua hàng.
- **Hoạt động 24/7**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc của nhân viên.
- **Dễ dàng mở rộng**: Có thể kết hợp với Slack, Email hoặc CRM để theo dõi thêm.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Stripe** (đã cấu hình Webhook cho `checkout.session.completed`).
2. **Tài khoản MoltFlow** ([Đăng ký miễn phí tại đây](https://molt.waiflow.app)) và kết nối với **WhatsApp Business API**.
3. **API Key của MoltFlow** (để cấu hình trong workflow).
4. **Số điện thoại của khách hàng** (được lưu trong Stripe dưới dạng `customer_details.phone`).
5. **VPS hoặc máy chủ n8n** (để lưu trữ workflow 24/7).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow** từ [n8n.io/workflows/13483](https://n8n.io/workflows/13483) hoặc copy JSON từ trang này.
- **Import vào n8n Editor**:
  - Mở **n8n Editor** trên máy chủ của bạn.
  - Nhấn **Import** → Chọn file JSON hoặc **Paste JSON** từ trang workflow.
  - Nhấn **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Stripe Webhook**
- **Tên node**: `Stripe Webhook`
- **Cấu hình**:
  - **Path**: `stripe-payment`
  - **HTTP Method**: `POST`
  - **Credentials**: Không cần (sử dụng Webhook URL mặc định của n8n).
- **Lưu ý**:
  - Sau khi import, **copy URL Webhook** từ node này (được hiển thị ở góc trên bên phải).
  - Trong **Stripe Dashboard** → **Developers** → **Webhooks**, thêm **n8n URL** này với **Event**: `checkout.session.completed`.

##### **🔹 Node 2: Format Receipt (Code)**
- **Tên node**: `Format Receipt`
- **Mã JavaScript**:
  ```javascript
  // Dữ liệu đầu vào từ Stripe Webhook
  const { data } = $input.all();
  const session = data.object;

  // Lấy thông tin cần thiết
  const customerName = session.customer_details.name || "Khách hàng";
  const customerEmail = session.customer_details.email || "";
  const customerPhone = session.customer_details.phone || "";
  const amount = session.amount_total / 100; // Stripe trả về số tiền trong cent
  const currency = session.currency;
  const sessionId = session.id;

  // Định dạng thông điệp WhatsApp
  const message = `📩 **XÁC NHẬN THANH TOÁN**
  👤 Tên: ${customerName}
  📧 Email: ${customerEmail}
  📱 Số điện thoại: ${customerPhone}
  💰 Số tiền: ${amount} ${currency}
  🔗 Mã đơn hàng: ${sessionId}
  👉 **Cảm ơn bạn đã mua hàng!**`;

  // Trả về dữ liệu để gửi qua WhatsApp
  return {
    message: message,
    phone: customerPhone,
    sessionId: sessionId
  };
  ```
- **Lưu ý**:
  - Đảm bảo **`customer_details.phone`** được lưu trong Stripe (nếu không, workflow sẽ không gửi được tin nhắn).

##### **🔹 Node 3: Has Phone? (If)**
- **Tên node**: `Has Phone?`
- **Cấu hình**:
  - **Condition**: `$node["Format Receipt"].json["phone"] != null && $node["Format Receipt"].json["phone"] != ""`
  - **Nếu đúng**: Tiếp tục đến node `Send WhatsApp Receipt`.
  - **Nếu sai**: Bỏ qua (không gửi tin nhắn nếu không có số điện thoại).
- **Lưu ý**:
  - Nếu khách hàng không có số điện thoại, workflow sẽ **bỏ qua** và không gửi tin nhắn.

##### **🔹 Node 4: Send WhatsApp Receipt (HTTP Request)**
- **Tên node**: `Send WhatsApp Receipt`
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://api.molt.waiflow.app/api/v1/send`
  - **Headers**:
    - `Content-Type: application/json`
    - `X-API-Key: YOUR_MOLTFLOW_API_KEY` (thay bằng API Key của bạn).
  - **Body (JSON)**:
    ```json
    {
      "phone": "$node["Format Receipt"].json["phone"]",
      "message": "$node["Format Receipt"].json["message"]"
    }
    ```
- **Lưu ý**:
  - **Thêm API Key của MoltFlow** vào **Header Auth** (nếu không, request sẽ thất bại).
  - Đảm bảo **số điện thoại** được định dạng đúng (ví dụ: `+841234567890` hoặc `0123456789`).

##### **🔹 Node 5: Log Success (Code)**
- **Tên node**: `Log Success`
- **Mã JavaScript** (giống như node `Format Receipt`, nhưng chỉ in log):
  ```javascript
  const { data } = $input.all();
  const session = data.object;

  console.log("📝 **Thanh toán thành công** - Mã đơn hàng: " + session.id);
  console.log("👤 Tên khách hàng: " + (session.customer_details.name || "Khách hàng"));
  console.log("💰 Số tiền: " + (session.amount_total / 100) + " " + session.currency);
  ```
- **Lưu ý**:
  - Node này **không bắt buộc**, nhưng hữu ích để **theo dõi log** trong n8n.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Tạo một **checkout session** trên Stripe (ngay cả là test mode).
  - Kiểm tra **n8n Logs** để xem liệu workflow có hoạt động không.
  - Kiểm tra **WhatsApp** của khách hàng (nếu có số điện thoại) để xác nhận tin nhắn đã được gửi.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO TRONG THỰC TIỆN]
1. **Kết hợp với Slack/Email**:
   - Thêm node **Slack** hoặc **Email** để thông báo cho team khi có đơn hàng mới.
   - Ví dụ: `Send Slack Notification` với nội dung: `📦 Đơn hàng mới: ${sessionId} - ${customerName}`.

2. **Lưu log vào Google Sheets/Notion**:
   - Sử dụng node **Google Sheets** hoặc **Notion** để ghi lại tất cả các đơn hàng thành công.
   - Cấu hình node **HTTP Request** để gửi dữ liệu vào API của Google Sheets.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp số đơn hàng thành công hàng ngày qua Email.

4. **Sử dụng Stripe Test Mode**:
   - Trước khi chuyển sang **Live Mode**, hãy test với **Stripe Test Cards** (ví dụ: `4242 4242 4242 4242`) để đảm bảo workflow hoạt động ổn định.

5. **Cập nhật thông tin khách hàng**:
   - Nếu khách hàng không có số điện thoại, có thể **yêu cầu họ nhập số điện thoại** qua Email hoặc WhatsApp trước khi thanh toán.
:::

---

### 📌 **Kết luận**
Với **workflow này**, các sếp đã tự động hóa **quá trình xác nhận thanh toán Stripe** chỉ trong **5 phút**, giúp:
✔ **Tiết kiệm thời gian phản hồi** cho khách hàng.
✔ **Tăng trải nghiệm mua hàng** và giảm tỷ lệ hủy đơn.
✔ **Hoạt động 24/7** mà không cần nhân viên.

**Bắt đầu ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Stripe Webhook** và **MoltFlow API Key**.
3. **Test và kích hoạt** để bắt đầu tự động hóa!

**🚀 Cần hỗ trợ?** Hãy để lại comment bên dưới hoặc liên hệ với chúng tôi qua [n8n Community](https://community.n8n.io/)!

---