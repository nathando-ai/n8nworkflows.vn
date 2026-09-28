---
title: "🚀 Tự Động Hóa Pipeline Lead → Client với Email Thông Báo & Theo Dõi Thời Gian (Google Sheets + Gmail)"
description: "Workflow tự động hóa 100% không code chuyển đổi lead thành khách hàng, gửi email tự động khi stage thay đổi, và theo dõi thời gian hoàn thành dự án. Giúp doanh nghiệp tiết kiệm 10+ giờ/ngày và tăng cường quản lý CRM hiệu quả."
slug: "tieu-dong-hoa-pipeline-lead-to-client-google-sheets-gmail"
tags: [n8n, automation, crm, google-sheets, gmail, no-code, time-tracking, sales-pipeline]
keywords: [n8n workflow lead to client, tự động hóa CRM, email tự động khi stage thay đổi, theo dõi thời gian dự án, google sheets + gmail, pipeline sales automation]
---

# 🚀 **Tự Động Hóa Pipeline Lead → Client: Từ Lead Đến Khách Hàng Với Email & Theo Dõi Thời Gian**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Lặp đi lặp lại** gửi email thông báo thay đổi stage cho lead?
- **Tốn thời gian** theo dõi thủ công thời gian chuyển đổi từ lead đến khách hàng?
- **Mất kiểm soát** quá trình chuyển đổi khi stage thay đổi (từ Screening → Proposal → Won)?
- **Không biết** thời gian thực tế để hoàn thành dự án của khách hàng?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Gửi email thông báo** khi stage lead thay đổi (ví dụ: từ "Screening" → "Proposal").
✅ **Cập nhật Google Sheets** khi lead được xác nhận ("Qualified") hoặc chuyển sang stage "Won".
✅ **Theo dõi thời gian** từ khi lead được xác nhận đến khi dự án hoàn thành.
✅ **Tự động gửi email mời lịch hẹn** (Cal.com) khi lead được xác nhận.
✅ **Cập nhật trạng thái dự án** khi khách hàng hoàn thành dự án.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** không phải gửi email thủ công.
- **Tăng độ chính xác** với cập nhật tự động trên Google Sheets.
- **Theo dõi thời gian dự án** một cách minh bạch.
- **Tự động hóa pipeline sales** từ lead đến khách hàng.
- **Cập nhật trạng thái dự án** khi khách hàng hoàn thành.
- **Gửi email mời lịch hẹn** tự động khi lead được xác nhận.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với 2 tab:
   - **"Leads"** (để quản lý lead và stage).
   - **"Clients"** (để quản lý khách hàng và thời gian dự án).
2. **Tài khoản Gmail** (để gửi email tự động).
3. **API Key Google Sheets** (để n8n có thể cập nhật dữ liệu).
4. **API Key Gmail OAuth2** (để gửi email tự động).
5. **Google Apps Script** (để kết nối Google Sheets với n8n).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7514](https://n8n.io/workflows/7514).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste** JSON từ file vào n8n Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Google Sheets**
- **Tạo 2 tab** trong Google Sheets:
  - **Tab "Leads"** (cột: Tên, Email, Nguồn, Stage, Người phụ trách, Checkbox "Qualified?").
  - **Tab "Clients"** (cột: Tên, Email, Loại dự án, Trạng thái dự án, Thời gian bắt đầu, Thời gian kết thúc, Thời gian thực hiện).
- **Cập nhật Google Apps Script**:
  - Mở **Extensions → Apps Script** trong Google Sheets.
  - **Dán mã script** từ [đoạn hướng dẫn trên canvas](https://n8n.io/workflows/7514).
  - **Thay thế URL webhook** trong `WEBHOOKS` bằng URL của n8n:
    ```javascript
    const WEBHOOKS = {
      STAGE_CHANGED: 'https://TEN_DOMAIN_N8N_CỦA_BẠN/webhook/lead-stage-changed',
      LEAD_QUALIFIED: 'https://TEN_DOMAIN_N8N_CỦA_BẠN/webhook/lead-qualified',
      CLIENT_STATUS_CHANGED: 'https://TEN_DOMAIN_N8N_CỦA_BẠN/webhook/client-status-changed',
    };
    ```
  - **Chạy script** để kích hoạt trigger tự động.

##### **B. Cấu Hình Gmail**
- **Tạo credential Gmail OAuth2** trong n8n:
  - Mở **Credentials → Add** → Chọn **Gmail OAuth2**.
  - Đăng nhập tài khoản Gmail và cấp quyền.
- **Kiểm tra node "Gmail: Send Stage-Change Email"** và **"Gmail: Send Cal.com Invite"**:
  - Chọn credential `gmailOAuth2` đã tạo.
  - Cấu hình **chủ đề email** và **nội dung email** phù hợp với doanh nghiệp.

##### **C. Cấu Hình Webhook**
- **Kiểm tra các node Webhook**:
  - **Webhook: Lead Stage Changed** → Path: `lead-stage-changed`, HTTP Method: `POST`.
  - **Webhook: Lead Qualified?** → Path: `lead-qualified`, HTTP Method: `POST`.
  - **Webhook: Client Status Changed** → Path: `client-status-changed`, HTTP Method: `POST`.
  - **Webhook: Meeting Booked** → Path: `cal-booked`, HTTP Method: `POST`.

##### **D. Cấu Hình Google Sheets API**
- **Tạo credential Google Sheets OAuth2 API** trong n8n:
  - Mở **Credentials → Add** → Chọn **Google Sheets OAuth2 API**.
  - Đăng nhập tài khoản Google và cấp quyền.
- **Kiểm tra các node Google Sheets**:
  - **GS: Clients Append (On Won)** → Chọn credential `googleSheetsOAuth2Api`.
  - **GS: Leads Update Stage to Meeting Booked** → Chọn credential `googleSheetsOAuth2Api`.
  - **GS: Clients Lookup by Email** → Chọn credential `googleSheetsOAuth2Api`.
  - **GS: Clients Update End & Duration** → Chọn credential `googleSheetsOAuth2Api`.

##### **E. Cấu Hình Node "Format Start Timestamp" và "Format End Timestamp"**
- **Chọn định dạng ngày giờ** phù hợp (ví dụ: `YYYY-MM-DD HH:mm:ss`).

##### **F. Kiểm Tra Node "Code"**
- **Node này** được sử dụng để xử lý logic phức tạp (nếu có). Nếu không cần chỉnh sửa, **bỏ qua**.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - **Chuyển đổi stage lead** trong Google Sheets từ "Screening" → "Proposal".
  - **Xác nhận lead** bằng cách đánh dấu checkbox "Qualified?".
  - **Cập nhật trạng thái dự án** trong tab "Clients" từ "In Progress" → "Delivered".
- **Kiểm tra email** đã được gửi tự động.
- **Kiểm tra Google Sheets** đã được cập nhật.
- **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi lead được xác nhận hoặc dự án hoàn thành.
   - Ví dụ: Khi stage chuyển sang "Won", gửi tin nhắn Slack: *"🎉 Lead [Tên] đã được chuyển sang khách hàng!"*.

2. **Lưu Log Hoạt Động**:
   - Thêm node **Set** hoặc **Code** để lưu lịch sử hoạt động vào Google Sheets hoặc một bảng khác.
   - Ví dụ: Tạo tab **"Logs"** để ghi lại thời gian và người thực hiện các thay đổi.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần/monthly để gửi báo cáo tổng hợp về pipeline lead và thời gian dự án.
   - Ví dụ: Gửi email tổng hợp hàng tháng với dữ liệu từ Google Sheets.

4. **Tích Hợp với CRM Khác**:
   - Nếu đang sử dụng **HubSpot, Salesforce, hoặc Zoho CRM**, có thể kết nối n8n với API của CRM để tự động đồng bộ dữ liệu.

5. **Tự Động Gửi Email Cảm Ơn**:
   - Khi dự án hoàn thành, thêm node **Gmail** để gửi email cảm ơn khách hàng.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **tăng cường quản lý pipeline lead** một cách chuyên nghiệp. Bằng cách tự động hóa:
✔ **Gửi email thông báo stage thay đổi**
✔ **Cập nhật Google Sheets**
✔ **Theo dõi thời gian dự án**
✔ **Gửi email mời lịch hẹn**

**Các sếp có thể tập trung vào việc phát triển doanh nghiệp thay vì làm thủ công!**

👉 **Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!** 🚀

---
**Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow 24/7 mà không lo gián đoạn!