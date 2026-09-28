---
title: "🚀 Tự Động Hồi Phục Giỏ Hàng Bỏ Qua Shopify: Email Follow-up + HubSpot CRM + Theo Dõi Google Sheets"
description: "Giải pháp 100% tự động hóa để phục hồi giỏ hàng bỏ qua trên Shopify, gửi email nhắc nhở cá nhân hóa, cập nhật CRM HubSpot và theo dõi hiệu suất trong Google Sheets - tăng doanh thu lên tới 30% cho các sếp bán hàng."
slug: "tieu-dong-hoi-phuc-gio-hang-bo-qua-shopify"
tags: [n8n, automation, no-code, shopify, hubspot, google-sheets, email-marketing, lead-nurturing]
keywords: [tự động hóa shopify, hồi phục giỏ hàng bỏ qua, email follow-up, hubspot automation, google sheets tracking, tăng doanh thu ecommerce]
---

# 🚀 **Hồi Phục Giỏ Hàng Bỏ Qua Shopify: Từ 0% → 30% Doanh Thu Thêm**

### **Nỗi Đau Của Các Sếp Ecommerce**
Bạn đã từng mất hàng chục nghìn đồng mỗi tháng vì khách hàng bỏ giỏ hàng không mua? Theo thống kê, **tỷ lệ giỏ hàng bỏ qua trên Shopify dao động từ 60% đến 80%**! Điều này không chỉ làm hao tổn doanh thu mà còn khiến các sếp phải mất thời gian thủ công theo dõi và gửi email nhắc nhở.

**Giải pháp này sẽ:**
- **Tự động phát hiện** giỏ hàng bỏ qua trên Shopify.
- **Lọc chọn** những giỏ hàng có giá trị cao (>50k VND) và đã bỏ qua hơn 12 giờ.
- **Gửi email nhắc nhở cá nhân hóa** để khuyến khích khách hàng hoàn tất mua hàng.
- **Cập nhật CRM HubSpot** với thông tin khách hàng và chi tiết giỏ hàng.
- **Ghi log tất cả hoạt động** vào Google Sheets để theo dõi hiệu suất và tối ưu chiến lược.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công giỏ hàng bỏ qua.
- **Tăng doanh thu**: Hồi phục từ 10% đến 30% giỏ hàng bỏ qua thành đơn hàng thực sự.
- **Cá nhân hóa tương tác**: Email nhắc nhở được tự động hóa với nội dung phù hợp.
- **CRM được cập nhật**: Thông tin khách hàng và giỏ hàng được đồng bộ vào HubSpot.
- **Báo cáo chi tiết**: Theo dõi hiệu suất hồi phục qua Google Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Shopify** với quyền API và **Shopify Access Token** (tạo tại [Shopify Partners](https://partners.shopify.com/)).
2. **Tài khoản Gmail** (hoặc Google Workspace) để gửi email nhắc nhở.
3. **Tài khoản HubSpot** với **App Token** (tạo tại [HubSpot Developer](https://developers.hubspot.com/)).
4. **Google Sheet** để lưu log hoạt động (cần chia sẻ quyền chỉnh sửa cho n8n).
5. **API Key** của các dịch vụ trên (nếu cần).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/10818](https://n8n.io/workflows/10818) hoặc copy JSON từ file.
- **Bước 2:** Mở n8n Editor → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create new workflow"** và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Shopify Trigger (Node: Shopify Trigger)**
- **Tham số cần thiết:**
  - **Credentials:** Chọn `shopifyAccessTokenApi` (đã cấu hình trước).
  - **Trigger:** Chọn **"Order Created"** (hoặc **"Checkout Created"** nếu muốn bắt giỏ hàng bỏ qua).
  - **Webhook URL:** Đảm bảo n8n có thể nhận được request từ Shopify (cần mở port 5678 trên VPS nếu self-hosted).

##### **B. Filter Qualified Carts (Node: If)**
- **Cấu hình lọc:**
  - **Điều kiện 1:** `$.age > 12` (giỏ hàng bỏ qua >12 giờ).
  - **Điều kiện 2:** `$.totalPrice > 50000` (giá trị giỏ hàng >50k VND).
  - **Nếu không thỏa mãn:** Workflow sẽ **dừng** (không tiếp tục xử lý).

##### **C. Send a Message (Node: Gmail)**
- **Tham số cần thiết:**
  - **Credentials:** Chọn `gmailOAuth2`.
  - **Email Template:** Sử dụng **n8n Set Node** để động thái hóa email (ví dụ: `{{$json.totalPrice}}`, `{{$json.items}}`).
  - **Gửi từ:** Điền địa chỉ email của bạn hoặc email thương mại.
  - **Địa chỉ nhận:** `$json.customerEmail` (trích xuất từ Shopify).

##### **D. HubSpot CRM Sync (Node: HubSpot & HTTP Request)**
- **Create or Update Contact:**
  - **Credentials:** Chọn `hubspotAppToken`.
  - **Properties:** Cập nhật thông tin khách hàng từ giỏ hàng (ví dụ: `email`, `firstName`, `lastName`).
- **Create HubSpot Note:**
  - **Tham số API:** Sử dụng `POST /crm/v3/objects/notes` với nội dung:
    ```json
    {
      "properties": {
        "subject": "Abandoned Cart Recovery",
        "body": "Customer left cart with {{items}} worth {{totalPrice}}",
        "associationType": "CONTACT",
        "associationId": "{{contactId}}"
      }
    }
    ```
- **Associate Note with Contact:**
  - **Tham số API:** `POST /crm/v3/objects/notes/{{noteId}}/associations` với `associationType: CONTACT` và `associationId: {{contactId}}`.

##### **E. Log to Google Sheets (Node: Google Sheets)**
- **Tham số cần thiết:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Điền tên sheet (ví dụ: `Abandoned_Carts_Log`).
  - **Range:** `Sheet1!A1` (đảm bảo sheet có cột: `Timestamp`, `Customer Email`, `Cart Value`, `Items`, `Status`).
  - **Operation:** Chọn `append` (thêm dữ liệu mới vào cuối).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu:
  - Tạo một giỏ hàng bỏ qua trên Shopify (hoặc sử dụng **n8n Code Node** để mock dữ liệu).
  - Chạy workflow và kiểm tra:
    - Email có được gửi không?
    - HubSpot có cập nhật thông tin không?
    - Google Sheets có log dữ liệu không?
- **Bước 2:** **Bật Active** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu email nhắc nhở:**
   - Sử dụng **n8n Set Node** để động thái hóa email với:
     - **Lời khuyến mãi đặc biệt** (ví dụ: `-10% cho đơn hàng trong 24h`).
     - **Link quay lại giỏ hàng** (`{{$json.checkoutUrl}}`).
   - **Ví dụ template:**
     ```
     Hi {{$json.customerFirstName}},
     Chúng tôi thấy bạn đã bỏ quên giỏ hàng với {{$json.items}} ({{$json.totalPrice}} VND). Để hoàn tất mua hàng, hãy nhấn [QUAY LẠI GIỎ HÀNG]({{$json.checkoutUrl}}).
     ```

2. **Kết hợp với Slack/Telegram:**
   - Thêm **n8n Slack Node** để thông báo khi có giỏ hàng mới được hồi phục thành công.
   - **Cấu hình:**
     ```json
     {
      "text": "🎉 Giỏ hàng của {{$json.customerEmail}} đã được hồi phục thành công! Giá trị: {{$json.totalPrice}} VND"
     }
     ```

3. **Báo cáo định kỳ:**
   - Sử dụng **n8n Google Sheets Node** để tạo **báo cáo hàng tuần** về:
     - Số giỏ hàng hồi phục thành công.
     - Doanh thu từ giỏ hàng hồi phục.
     - Tỷ lệ chuyển đổi.
   - **Cách làm:**
     - Thêm một **n8n Code Node** để tính toán thống kê.
     - Gửi báo cáo qua email hoặc Slack.

4. **Lưu log chi tiết:**
   - Thêm cột `Status` vào Google Sheets để ghi:
     - `Sent Email` (email đã gửi).
     - `Contact Updated` (CRM đã cập nhật).
     - `Note Added` (ghi chú đã tạo).
   - **Ví dụ:**
     ```
     | Timestamp          | Email               | Cart Value | Status                     |
     |--------------------|---------------------|------------|---------------------------|
     | 2024-05-20 10:30   | customer@example.com | 250,000    | Sent Email, Contact Updated |
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp ecommerce tự động hóa quy trình hồi phục giỏ hàng bỏ qua, từ đó **tăng doanh thu lên đến 30%** mà không cần viết code. Bằng cách kết hợp **Shopify, Gmail, HubSpot và Google Sheets**, các sếp có thể:
✅ **Tiết kiệm thời gian** theo dõi thủ công.
✅ **Cá nhân hóa tương tác** với khách hàng.
✅ **Theo dõi hiệu suất** một cách chuyên nghiệp.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình các credentials** (Shopify, Gmail, HubSpot, Google Sheets).
3. **Test và bật workflow** để bắt đầu hồi phục giỏ hàng tự động.

**Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với [iTechNotion](https://itechnotion.com/) - đội ngũ chuyên gia tự động hóa AI của Avkash Kakdiya.

---
**🚀 Chúc các sếp thành công với chiến dịch hồi phục giỏ hàng tự động hóa!** 🛒💨