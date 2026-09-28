---
title: "🚀 Tự Động Hoá Tạo Vé Hỗ Trợ HubSpot Từ Đăng Ký Tally Form - Giảm 90% Công Việc Nhập Liệu"
description: "Workflow này tự động chuyển đổi tất cả các form đăng ký từ Tally thành vé hỗ trợ HubSpot, đồng thời cập nhật thông tin liên lạc mới hoặc hiện có. Giúp các sếp tiết kiệm 90% thời gian nhập liệu thủ công và đảm bảo dữ liệu chính xác 100%."
slug: "tay-dong-hoa-tao-ve-hotro-hubspot-tu-tally-form"
tags: [n8n, automation, ticket-management, HubSpot, TallyForms, no-code]
keywords: [tự động hóa HubSpot, Tally Forms, tạo vé hỗ trợ tự động, tích hợp HubSpot Tally, giảm thời gian nhập liệu]
---

# 🚀 **Tự Động Hoá Tạo Vé Hỗ Trợ HubSpot Từ Đăng Ký Tally Form**

### **Giải Phá 90% Công Việc Nhập Liệu Thủ Công Với Tally + HubSpot**
Hãy tưởng tượng: Một khách hàng gửi form đăng ký hỗ trợ trên website của bạn qua **Tally Forms**, nhưng bạn phải **nhập liệu thủ công** vào HubSpot để tạo vé hỗ trợ và cập nhật thông tin liên lạc. **Lặp đi lặp lại hàng ngày?** Với workflow này, **tất cả đều tự động hóa** chỉ trong vài giây!

Workflow này **liên kết Tally Forms với HubSpot** để:
✅ **Tạo vé hỗ trợ tự động** khi khách hàng gửi form.
✅ **Cập nhật hoặc tạo mới contact** trong HubSpot (không trùng lặp).
✅ **Tích hợp hoàn hảo** với pipeline hỗ trợ hiện có của bạn.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **mật mã hóa GDPR-compliant** và tốc độ tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** nhập liệu thủ công (không cần copy-paste từ Tally sang HubSpot).
- **Không trùng lặp contact**: Dữ liệu liên lạc được **tìm kiếm và cập nhật tự động** trong HubSpot.
- **Vé hỗ trợ được tạo ngay lập tức** khi khách hàng gửi form, **giảm thời gian phản hồi** từ 24h xuống **vài giây**.
- **Hoạt động liên tục 24/7** mà không cần can thiệp người dùng.
- **Dữ liệu chính xác 100%**: Không sai sót do nhập liệu sai (ví dụ: email, tên, nội dung yêu cầu).
- **Tích hợp với Slack/Telegram** (nâng cao) để thông báo khi có vé mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Tally Forms** (để lấy **API Key** và **Form ID**).
✔ **Tài khoản HubSpot** (để lấy **API Token** hoặc **OAuth**).
✔ **Dữ liệu mẫu** từ form Tally (để test workflow):
   - Email (bắt buộc)
   - Tên (First Name, Last Name)
   - Nội dung yêu cầu (Message)
   - (Nếu có) Số điện thoại, tên công ty...

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14474](https://n8n.io/workflows/14474) hoặc copy toàn bộ JSON từ **View Code** trên trang workflow.
- **Mở n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node chính**, nhưng **3 node này cần cấu hình kỹ lưỡng**:

##### **🔹 Node 1: When Tally Form Submitted (n8n-nodes-tallyforms.tallyTrigger)**
- **Cấu hình:**
  - **Credentials:** Chọn `tallyApi` (đã tạo trước khi import).
  - **Form ID:** Nhập **ID của form Tally** bạn muốn theo dõi (thường là một chuỗi số hoặc mã form).
  - **Test:** Nhấn **Execute Node** để kiểm tra kết nối.

##### **🔹 Node 2 & 3: Search HubSpot Contacts & Upsert HubSpot Contact (n8n-nodes-base.hubspot)**
- **Credentials:** Chọn `hubspotAppToken` (đã tạo trước khi import).
- **Search Contacts:**
  - **Operation:** Đặt là `search`.
  - **Filter:** Cấu hình để tìm kiếm theo **email** (ví dụ: `email = {{ $json["email"] }}`).
- **Upsert Contact:**
  - **Resource:** Đặt là `contact`.
  - **Fields to Map:**
    - `email` → `email` (tự động từ Tally).
    - `firstName` → `firstName` (tự động từ Tally).
    - `lastName` → `lastName` (tự động từ Tally).
    - **Thêm các field tùy chọn** như `phone`, `company`, `custom properties` nếu cần.

##### **🔹 Node 4: Create HubSpot Ticket (n8n-nodes-base.hubspot)**
- **Credentials:** Chọn `hubspotAppToken`.
- **Resource:** Đặt là `ticket`.
- **Fields Cần Điền:**
  - **Subject:** `{{ $json["subject"] }}` (ví dụ: `"Yêu cầu hỗ trợ: {{ $json["message"] }}"`).
  - **Description:** `{{ $json["message"] }}` (nội dung từ form Tally).
  - **Contact ID:** Sử dụng **Set Contact ID and Name** (node sau) để truyền giá trị.
  - **Status:** Đặt là `open` (hoặc tùy chỉnh theo pipeline của bạn).
  - **Pipeline:** Chọn **Pipeline hỗ trợ** phù hợp (ví dụ: "Support").

##### **🔹 Node 5: If Contact Already Exists (n8n-nodes-base.if)**
- **Cấu hình:**
  - **Condition:** Kiểm tra `{{ $json["contact"] }}` có tồn tại không.
  - **Nếu có:** Sử dụng **Set Contact ID and Name** để lấy `contactId` và `name` từ kết quả tìm kiếm.
  - **Nếu không:** Sử dụng **Upsert Contact** để tạo mới, sau đó lấy `contactId` từ kết quả trả về.

##### **🔹 Node 6: Set Contact ID and Name (n8n-nodes-base.set)**
- **Cấu hình:**
  - **Branch True (Contact tồn tại):**
    - `contactId` → `{{ $json["contactId"] }}` (từ node Search).
    - `contactName` → `{{ $json["firstName"] }} {{ $json["lastName"] }}`.
  - **Branch False (Contact mới):**
    - `contactId` → `{{ $json["contact"]["id"] }}` (từ node Upsert).
    - `contactName` → `{{ $json["firstName"] }} {{ $json["lastName"] }}`.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **Execute Workflow** với dữ liệu mẫu từ Tally.
- **Kiểm tra HubSpot:**
  - Đăng nhập HubSpot → **Contacts** → Kiểm tra contact đã được tạo/ cập nhật.
  - **Tickets** → Kiểm tra vé hỗ trợ đã được tạo.
- **Bật Active:** Sau khi test thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để gửi thông báo khi có vé mới.
   - **Cấu hình:**
     ```json
     {
       "text": "🚨 Vé hỗ trợ mới từ {{ $json["contactName"] }}:\n{{ $json["message"] }}"
     }
     ```

2. **Lưu Log Lịch Sử**
   - Thêm **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.notion** để ghi lại lịch sử vé.
   - **Cấu hình:**
     - Sheet Name: `Vé Hỗ Trợ HubSpot`
     - Fields: `Email, Tên, Nội Dung, Ngày Tạo, Trạng Thái`

3. **Tự Động Gửi Email Xác Nhận**
   - Sử dụng **n8n-nodes-base.email** để gửi email xác nhận cho khách hàng khi vé được tạo.
   - **Nội dung email:**
     ```
     Xin chào {{ $json["firstName"] }},

     Vé hỗ trợ của bạn đã được tạo thành công với nội dung:
     {{ $json["message"] }}

     ID vé: {{ $json["ticketId"] }}
     ```

4. **Tích Hợp với Zapier/Make (Integromat)**
   - Nếu cần thêm tính năng như **gửi SMS** hoặc **cập nhật CRM khác**, có thể kết nối với **Zapier** hoặc **Make** qua **n8n-nodes-base.httpRequest**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng bạn khỏi công việc nhập liệu thủ công**, đồng thời **tăng cường hiệu quả hỗ trợ khách hàng** bằng cách tự động hóa toàn bộ quy trình từ **form đăng ký → vé hỗ trợ → cập nhật contact**. **Chỉ cần import, cấu hình và bật chạy** – **không cần code nào!**

👉 **Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/14474](https://n8n.io/workflows/14474).
2. **Cấu hình Tally API + HubSpot Token**.
3. **Test và bật Active** để workflow hoạt động 24/7.

**Hãy để tự động hóa làm việc cho bạn!** 🚀