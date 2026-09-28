---
title: "🚀 Tự Động Hóa Email Outreach Lạnh & Follow-up Tự Động với Resend, Postgres & HubSpot (Không Cần Code)"
description: "Workflow này tự động gửi email outreach lạnh và follow-up cho leads, theo dõi phản hồi từ Resend, cập nhật dữ liệu vào Postgres, và đồng bộ hóa vào HubSpot CRM. Giúp các sếp tiết kiệm 10-15 giờ/tuần và tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-email-outreach-lanh-va-follow-up"
tags: [n8n, automation, lead-nurturing, resend, postgres, hubspot, no-code, email-marketing]
keywords: [n8n workflow outreach, tự động hóa email lạnh, Resend API, HubSpot CRM tự động, Postgres database, follow-up tự động]
---

# 🚀 **Tự Động Hóa Email Outreach Lạnh & Follow-up Tự Động với Resend, Postgres & HubSpot**

### **🔥 Nỗi Đau Của Các Sếp Hiện Nay**
Gửi email outreach lạnh và theo dõi phản hồi thủ công là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp thường phải:
- **Ghi nhớ** gửi email cho từng lead theo lịch trình cụ thể.
- **Tra cứu** dữ liệu leads trong Excel/CRM để tránh gửi lại email cho người đã phản hồi.
- **Chuyển đổi** dữ liệu phản hồi từ email sang CRM thủ công.
- **Lo lắng** về tỷ lệ mở và phản hồi thấp do thiếu cá nhân hóa.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động gửi email outreach lạnh** theo lịch trình.
✅ **Theo dõi phản hồi** từ Resend và **dừng gửi tiếp** nếu lead đã trả lời.
✅ **Cập nhật dữ liệu** vào Postgres (hoặc Supabase) và HubSpot CRM.
✅ **Tối ưu hóa thời gian** từ 10-15 giờ/tuần xuống còn **0 giờ**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình outreach, giảm thiểu công việc thủ công.
- **Tăng tỷ lệ chuyển đổi**: Gửi email theo lịch trình và cá nhân hóa nội dung.
- **Dữ liệu chính xác**: Cập nhật trạng thái leads (đã gửi, đã phản hồi, đã chặn) vào Postgres và HubSpot.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động theo lịch.
- **Tăng cường mối quan hệ**: Theo dõi phản hồi và gửi follow-up tự động khi cần.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Resend**:
   - Đăng ký tại [Resend](https://resend.com/) và **xác minh domain**.
   - Lấy **API Key** từ Dashboard Resend (để kết nối với node `HTTP Request`).
   - **Thiết lập Webhook** trong Resend để nhận phản hồi email (URL Webhook sẽ được cấu hình trong workflow).

2. **Database Postgres/Supabase**:
   - Tạo một bảng chứa dữ liệu leads (ví dụ: `leads` với các cột: `email`, `status`, `last_contacted_at`, `follow_up_at`).
   - **Cấu hình kết nối Postgres** trong n8n:
     - Sử dụng **Supabase** (gợi ý) hoặc Postgres riêng.
     - Thiết lập **Method: Transaction Pooler** trong credential Postgres.
     - Cung cấp **Host, Port, Username, Password, Database Name**.

3. **Tài khoản HubSpot**:
   - Đăng ký tại [HubSpot](https://www.hubspot.com/).
   - Tạo một **Legacy App** và lấy **App Token** (để kết nối với node `Create or update a contact`).

4. **n8n Workflow**:
   - Cài đặt n8n trên **VPS riêng** (Self-hosted) để workflow chạy 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12810](https://n8n.io/workflows/12810).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
- **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **hai luồng chính**:
- **Luồng 1**: Gửi email outreach lạnh cho leads mới.
- **Luồng 2**: Gửi follow-up cho leads đã được tiếp xúc trước đó.

##### **A. Cấu Hình Node Postgres**
- **Node "Select rows from a table"**:
  - **Query SQL**: `SELECT * FROM leads WHERE status = 'pending' AND follow_up_at <= NOW() ORDER BY follow_up_at ASC LIMIT 100;`
  - **Lưu ý**: Thay đổi tên bảng và cột theo cấu trúc của bảng leads trong Postgres.

- **Node "Update rows in a table"**:
  - **Query SQL**: `UPDATE leads SET status = 'sent', last_contacted_at = NOW() WHERE id = $json[$.id];`
  - **Lưu ý**: Đảm bảo cột `id` trong bảng leads là **primary key**.

##### **B. Cấu Hình Node Resend (HTTP Request)**
- **Headers**:
  - `Authorization: Bearer <API_KEY_RESEND>` (thay `<API_KEY_RESEND>` bằng API Key từ Resend).
  - `Content-Type: application/json`.
- **Body (JSON)**:
  ```json
  {
    "from": "noreply@domain.com",
    "to": ["$json[$.email]"],
    "subject": "$json[$.subject]",
    "html": "$json[$.html_content]"
  }
  ```
  - **Lưu ý**:
    - Thay `noreply@domain.com` bằng domain đã xác minh trên Resend.
    - `$json[$.email]`, `$json[$.subject]`, `$json[$.html_content]` là **dữ liệu động** từ Postgres. Các sếp cần **cấu hình template email** trong Postgres (ví dụ: cột `email_template` chứa HTML cá nhân hóa).

##### **C. Cấu Hình Webhook Resend**
- Trong Resend Dashboard:
  - Tạo **Webhook** với URL: `https://<tên-domain-n8n>/webhook/resend-email`.
  - **Event**: `email.opened`, `email.bounced`, `email.unsubscribed`.
  - **Secret** (nếu cần): Để bảo mật, các sếp có thể thêm **secret key** trong Webhook node n8n.

##### **D. Cấu Hình Node HubSpot**
- **Credentials**: Chọn **hubspotAppToken** và điền **App Token** từ HubSpot.
- **Node "Create or update a contact"**:
  - **Properties**:
    - `email`: `$json[$.email]`.
    - `status`: `$json[$.status]` (ví dụ: `contacted`, `lead`, `customer`).
    - **Thêm các field tùy chỉnh** nếu cần (ví dụ: `last_contacted_at`, `follow_up_at`).

##### **E. Cấu Hình Schedule Trigger**
- **Node "Schedule Trigger"**:
  - **Cron Expression**: `0 0 * * *` (gửi hàng ngày lúc 00:00).
  - **Node "Schedule Trigger1"**:
    - **Cron Expression**: `0 0 * * 1-5` (gửi từ thứ 2 đến thứ 6 hàng tuần).
  - **Lưu ý**: Các sếp có thể điều chỉnh lịch trình theo nhu cầu.

##### **F. Cấu Hình Filter Node**
- **Condition**: Lọc leads đã được tiếp xúc trong **7 ngày qua** để gửi follow-up.
  - **Query**: `$json[$.status] === 'sent' && $json[$.last_contacted_at] >= (new Date(Date.now() - 7 * 24 * 60 * 60 * 1000))`.

##### **G. Cấu Hình Wait Node**
- **Delay**: 5000 ms (5 giây) giữa các email để tránh bị đánh dấu là spam.
- **Lưu ý**: Các sếp có thể điều chỉnh thời gian delay theo nhu cầu.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Test Tab** trong n8n Editor.
   - Nhấn **Run Workflow** với một lead mẫu (ví dụ: `email: test@example.com`).
   - Kiểm tra:
     - Email có được gửi thành công không?
     - Dữ liệu trong Postgres có được cập nhật không?
     - HubSpot có nhận được contact mới không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Cá nhân hóa email**:
   - Trong Postgres, thêm cột `custom_message` để lưu nội dung email cá nhân hóa cho từng lead.
   - Sử dụng **template engine** như Handlebars trong Resend để động hóa email.

2. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để báo cáo khi email được gửi hoặc phản hồi.
   - Ví dụ:
     ```json
     {
       "text": `Email sent to ${email}. Status: ${status}`
     }
     ```

3. **Báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Trigger** kết hợp với **Google Sheets** hoặc **Notion** để tạo báo cáo hàng tuần về:
     - Số email đã gửi.
     - Tỷ lệ mở và phản hồi.
     - Leads mới được tạo trong HubSpot.

4. **Tối ưu hóa tỷ lệ mở**:
   - Thử nghiệm **subject line** khác nhau bằng cách lưu các biến trong Postgres.
   - Sử dụng **A/B Testing** với node **SplitInBatches** để gửi hai phiên bản email khác nhau và so sánh kết quả.

5. **Xử lý email bị phản hồi (bounced)**:
   - Thêm logic trong **Webhook** để cập nhật trạng thái leads thành `bounced` và **không gửi tiếp**.
   - Ví dụ:
     ```sql
     UPDATE leads SET status = 'bounced' WHERE email = '$json[$.email]';
     ```

6. **Kết hợp với CRM khác**:
   - Nếu không dùng HubSpot, có thể thay thế bằng **Salesforce**, **Pipedrive**, hoặc **Airtable** bằng cách thay đổi node `hubspot` thành `salesforce` hoặc `airtable`.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **tăng trưởng kinh doanh** thay vì làm thủ công. Bằng cách tự động hóa **email outreach lạnh và follow-up**, các sếp sẽ:
✔ **Tiết kiệm 10-15 giờ/tuần**.
✔ **Tăng tỷ lệ chuyển đổi lên 30%**.
✔ **Cập nhật dữ liệu chính xác** vào Postgres và HubSpot.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản** Resend, Postgres, và HubSpot.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa outreach của mình.

👉 **Xem video hướng dẫn chi tiết** của tác giả [tại đây](https://youtu.be/ZmN8jMhNJS4).

---
**Chia sẻ và đặt câu hỏi** trong cộng đồng n8n để được hỗ trợ! 🚀