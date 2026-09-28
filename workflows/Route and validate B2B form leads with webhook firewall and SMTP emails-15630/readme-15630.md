---
title: "🚀 Tự Động Hóa & Lọc Lọc Lead B2B Tối Ưu: Webhook + Email Tự Động Hóa (N8n)"
description: "Workflow này tự động nhận, lọc và phân loại lead từ form B2B qua webhook, loại bỏ email sai định dạng, và gửi email phản hồi cá nhân hóa theo cấp độ dịch vụ. Giúp doanh nghiệp tiết kiệm 80% thời gian xử lý lead thủ công."
slug: "tu-dong-hoa-loc-lead-b2b-webhook-email"
tags: [n8n, automation, lead-generation, smtp-email, webhook-firewall]
keywords: [n8n workflow lead B2B, tự động hóa form webhook, lọc email regex, email tự động hóa theo cấp độ dịch vụ, n8n self-hosted]
---

# 🚀 **Tự Động Hóa & Lọc Lead B2B: Webhook + Email Tự Động Hóa (N8n)**

### **Nỗi Đau Của Các Sếp**
Các sếp đang mất **giờ đồng hồ** mỗi ngày để:
- **Nhận và kiểm tra** hàng trăm lead từ form B2B trên Tally, Typeform hay các công cụ khác.
- **Lọc bỏ** lead không hợp lệ (email sai định dạng, dữ liệu trống, hoặc không phù hợp).
- **Phân loại** lead theo cấp độ dịch vụ (Basic, Implementation, Managed Services) để gửi email phản hồi phù hợp.
- **Gửi email thủ công** cho từng lead, dẫn đến **sai sót** và **trễ thời gian**.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nhận lead** qua webhook từ Tally.
✅ **Lọc bỏ email sai định dạng** bằng Regex (firewall).
✅ **Phân loại lead** theo cấp độ dịch vụ (Basic → Implementation → Managed Services).
✅ **Gửi email phản hồi tự động** với nội dung cá nhân hóa.
✅ **Gửi thông báo nội bộ** cho team xử lý.
✅ **Trả lời webhook** với status 200 (thành công) hoặc JSON lỗi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và độ tin cậy cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** xử lý lead thủ công.
- **Tăng độ chính xác** với Regex lọc email sai định dạng.
- **Cá nhân hóa email phản hồi** theo cấp độ dịch vụ.
- **Hoạt động liên tục** 24/7, không cần can thiệp người dùng.
- **Giảm sai sót** với logic routing tự động.
- **Báo cáo tự động** thông báo lead mới cho team.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản SMTP** (Gmail, SendGrid, Mailgun, hoặc SMTP của nhà cung cấp email doanh nghiệp).
2. **API Key của Tally** (nếu sử dụng Tally Forms).
3. **Webhook URL** từ Tally (sẽ được copy từ workflow).
4. **Email domain chính thức** (ví dụ: `hello@yourdomain.com` và `admin@yourdomain.com`).
5. **Nội dung email mẫu** cho từng cấp độ dịch vụ (Basic, Implementation, Managed Services).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/15630) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15630) và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **12 node** quan trọng, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **A. Node "Form Webhook" (n8n-nodes-base.webhook)**
- **Cấu hình:**
  - **Path:** `your-form-path` (thay bằng đường dẫn cụ thể của form Tally).
  - **HTTP Method:** `POST`.
  - **Credentials:** Chọn **Tally Webhook** (nếu đã cấu hình).
- **Lưu ý:**
  - **Không cần API Key** nếu chỉ dùng webhook.
  - **Test webhook** bằng cách gửi dữ liệu mẫu từ Tally.

##### **B. Node "Format Tally Data" (n8n-nodes-base.code)**
- **Cấu hình:**
  - **JavaScript Code:** Dùng để **trích xuất dữ liệu nested** từ Tally.
  - **Mẫu code tham khảo:**
    ```javascript
    // Dùng để chuyển đổi dữ liệu từ format nested của Tally thành key-value pairs
    const data = $input.all();
    const output = {
      email: data.email,
      name: data.name,
      serviceTier: data.serviceTier,
      // Thêm các trường khác theo cấu trúc của form
    };
    return output;
    ```
- **Lưu ý:**
  - **Không thay đổi logic** nếu không hiểu code, chỉ cần **đảm bảo dữ liệu đầu vào đúng format**.

##### **C. Node "Validate Lead" (n8n-nodes-base.if)**
- **Cấu hình:**
  - **Condition:** Kiểm tra email bằng Regex:
    ```regex
    ^[^\s@]+@[^\s@]+\.[^\s@]+$
    ```
  - **Nếu email hợp lệ:** Tiếp tục xử lý.
  - **Nếu email sai:** Gửi **Email - Error Response** (node `respondToWebhook`).
- **Lưu ý:**
  - **Regex này lọc bỏ email không hợp lệ** (ví dụ: `test@`, `@gmail.com`, `test@`).

##### **D. Node "Switch by Service Tier" (n8n-nodes-base.switch)**
- **Cấu hình:**
  - **Key:** `serviceTier` (trường được chọn trong form).
  - **Các case:**
    - `Basic` → Gửi **Email - Generic/Fallback**.
    - `Implementation` → Gửi **Email - Implementation**.
    - `Managed Services` → Gửi **Email - Managed Services**.
    - **Default (Fallback):** Gửi **Email - Generic/Fallback**.
- **Lưu ý:**
  - **Đảm bảo trường `serviceTier` trong form** được chọn đúng (Basic/Implementation/Managed Services).

##### **E. Các Node Email (n8n-nodes-base.emailSend)**
- **Cấu hình chung:**
  - **SMTP Credentials:** Chọn **SMTP của bạn** (Gmail, SendGrid...).
  - **From Email:** `hello@yourdomain.com` (thay bằng email chính thức).
  - **To Email:** `$json["email"]` (địa chỉ email của lead).
  - **Subject & Body:** Sử dụng **HTML template** cá nhân hóa.
- **Lưu ý:**
  - **Tải template email** từ [đây](https://n8n.io/workflows/15630) và **chỉnh sửa** theo brand của doanh nghiệp.
  - **Test email** trước khi kích hoạt workflow.

##### **F. Node "Success Response" & "Error Response" (n8n-nodes-base.respondToWebhook)**
- **Cấu hình:**
  - **Status Code:** `200` (thành công) hoặc `400` (lỗi).
  - **Body:**
    - **Success:**
      ```json
      { "status": "success", "message": "Lead received and processed." }
      ```
    - **Error:**
      ```json
      { "status": "error", "message": "Invalid email format." }
      ```
- **Lưu ý:**
  - **Không cần thay đổi** nếu không muốn custom.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một lead mẫu từ Tally để kiểm tra workflow.
   - Kiểm tra **email đã được gửi** và **webhook trả về status 200**.
2. **Bật Active workflow** sau khi test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối Slack/Telegram:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để **báo cáo lead mới** ngay khi nhận được.
2. **Lưu Log vào Google Sheets:**
   - Sử dụng node **Google Sheets** để **ghi lại tất cả lead** và **theo dõi tiến trình**.
3. **Gửi Báo Cáo Định Kỳ:**
   - Tạo một workflow **daily report** để gửi tổng hợp lead mới cho team.
4. **Cập Nhật Email Templates:**
   - **Chỉnh sửa HTML email** để phù hợp với **branding** và **các chương trình khuyến mãi** mới.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp cần:
✔ **Tự động hóa lead B2B** từ form webhook.
✔ **Lọc bỏ lead không hợp lệ** bằng Regex.
✔ **Phân loại và gửi email phản hồi tự động** theo cấp độ dịch vụ.
✔ **Giảm thời gian xử lý lead** từ **giờ đồng hồ xuống còn giây phút**.

**Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả team Sales!** 🚀

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/15630) | 📧 [Liên hệ tác giả](mychel.garzon@gmail.com)**