---
title: "🚀 **Tự Động Hóa Theo Dõi Chuyến Bay Thực Tế với API Hàng Không, Slack & Thông Báo SMS/Email (n8n)**"
description: "Giải pháp tự động hóa 24/7 theo dõi thay đổi lịch bay từ API hàng không, so sánh với cơ sở dữ liệu nội bộ, và gửi thông báo tức thời đến đội ngũ vận hành qua Slack, email (SendGrid) và SMS (Twilio) cho hành khách bị ảnh hưởng. Tiết kiệm thời gian, giảm thiểu lỗi và nâng cao trải nghiệm hành khách."
slug: "tu-dong-hoa-theo-doi-chuyen-bay-real-time"
tags: [n8n, automation, aviation, no-code, real-time-tracking, sendgrid, twilio, slack, postgres]
keywords: [tự động hóa theo dõi chuyến bay, n8n workflow aviation, API hàng không tự động, gửi thông báo SMS email cho hành khách, Slack alert, SendGrid Twilio n8n]
---

# 🚀 **Tự Động Hóa Theo Dõi Chuyến Bay Thực Tế với API Hàng Không, Slack & Thông Báo SMS/Email**

### **Giải pháp cho nỗi đau của các sếp hàng không:**
Hàng ngày, đội ngũ vận hành hàng không phải mất **giờ đồng hồ** để thủ công kiểm tra và cập nhật lịch bay từ các API hàng không, so sánh với cơ sở dữ liệu nội bộ, và gửi thông báo cho hành khách khi có thay đổi (đổi cổng, hủy chuyến, chậm trễ). **Kết quả?** Thông tin không kịp thời, hành khách bất mãn, và rủi ro pháp lý tăng cao.

**Workflow này tự động hóa toàn bộ quy trình trong 30 phút/lần**, so sánh dữ liệu thực tế với cơ sở dữ liệu, và gửi thông báo **tức thời** đến:
- Đội ngũ vận hành qua **Slack**.
- Hành khách bị ảnh hưởng qua **email (SendGrid)** và **SMS (Twilio)** (chỉ cho trường hợp khẩn cấp).
- Cập nhật đồng bộ với **hệ thống nội bộ** và **lưu log** cho giám sát.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và độ tin cậy cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công mỗi giờ, giảm **90% công việc lặp lại**.
- **Chính xác 100%**: So sánh tự động giữa API và cơ sở dữ liệu, loại bỏ sai sót con người.
- **Cá nhân hóa thông báo**: Gửi SMS chỉ cho trường hợp **khẩn cấp** (hủy chuyến, chậm trễ >3h), email cho thông tin chi tiết.
- **Hoạt động liên tục**: Chạy tự động **mỗi 30 phút**, không cần can thiệp người dùng.
- **Giảm rủi ro pháp lý**: Thông báo kịp thời cho hành khách tránh tranh chấp.
- **Dữ liệu theo dõi**: Log tất cả hoạt động để **giám sát và phân tích** hiệu suất.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key của Aviation API** (ví dụ: FlightAware, OpenFlights, hoặc API hàng không khác) để **Fetch Airline Data**.
2. **Thông tin kết nối cơ sở dữ liệu PostgreSQL**:
   - Host, Port, Database Name, Username, Password.
   - Bảng dữ liệu chứa lịch bay hiện tại (cấu trúc tùy chỉnh, nhưng workflow sử dụng `executeQuery`).
3. **Credentials cho Slack**:
   - Webhook URL của kênh Slack (để **Notify Slack Channel**).
4. **Credentials cho SendGrid (Email)**:
   - API Key và từ khóa bảo mật (để **Send Email Notifications**).
5. **Credentials cho Twilio (SMS)**:
   - Account SID và Auth Token (để **Send SMS (Critical Only)**).
6. **Webhook URL** của hệ thống nội bộ (nếu có) để **Update Internal Systems**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6227](https://n8n.io/workflows/6227) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và chọn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **13 node**, mỗi node đều cần cấu hình chi tiết. Dưới đây là **hướng dẫn cụ thể** cho từng phần quan trọng:

##### **A. Schedule Trigger**
- **Thời gian chạy**: Đặt **30 phút/lần** (hoặc tùy chỉnh theo nhu cầu).
- **Lưu ý**: Đảm bảo workflow được **Active** và **triggers** hoạt động.

##### **B. Fetch Airline Data (HTTP Request)**
- **Credentials**: Chọn `httpQueryAuth` (đã cấu hình sẵn trong n8n).
- **URL API**: Điền URL của API hàng không (ví dụ: `https://api.flightaware.com/...`).
- **Query Parameters**: Thêm các tham số cần thiết (ví dụ: `flight_number`, `departure_airport`).
- **Headers**: Thêm `Authorization: Bearer {API_KEY}` (điền API Key từ bước **Yêu cầu cần thiết**).

##### **C. Get Current Schedules (PostgreSQL)**
- **Credentials**: Chọn `postgres` (cấu hình sẵn trong n8n).
- **Query**: Sử dụng câu lệnh SQL để lấy dữ liệu lịch bay hiện tại từ bảng (ví dụ):
  ```sql
  SELECT * FROM flight_schedules WHERE status = 'active';
  ```

##### **D. Process Changes (Node Code)**
- **Lưu ý**: Node này **so sánh dữ liệu mới** từ API với dữ liệu cũ trong DB.
- **Không cần chỉnh sửa** nếu API và DB có cấu trúc tương đồng.

##### **E. Check for Changes (If Node)**
- **Condition**: Đặt điều kiện để **lọc ra các thay đổi** (ví dụ: `json["status"] !== "unchanged"`).

##### **F. Update Database (PostgreSQL)**
- **Credentials**: Chọn `postgres`.
- **Query**: Cập nhật bảng `flight_schedules` với dữ liệu mới (ví dụ):
  ```sql
  UPDATE flight_schedules
  SET status = 'delayed', gate = 'B2'
  WHERE flight_number = $1 AND departure_time = $2;
  ```

##### **G. Notify Slack Channel (HTTP Request)**
- **Credentials**: Chọn `httpHeaderAuth`.
- **URL**: Điền Webhook URL của kênh Slack (ví dụ: `https://hooks.slack.com/services/...`).
- **Payload**: Tùy chỉnh nội dung thông báo (ví dụ: `{"text": "Flight {{$node["Fetch Airline Data"].json()["flight_number"]}} delayed by 2 hours!"}`).

##### **H. Check Urgent Notifications (If Node)**
- **Condition**: Chỉ gửi SMS cho trường hợp **khẩn cấp** (ví dụ: `json["severity"] === "critical"`).

##### **I. Get Affected Passengers (PostgreSQL)**
- **Credentials**: Chọn `postgres`.
- **Query**: Lấy danh sách hành khách bị ảnh hưởng (ví dụ):
  ```sql
  SELECT phone, email FROM passengers
  WHERE flight_id = $1;
  ```

##### **J. Send Email Notifications (HTTP Request)**
- **Credentials**: Chọn `httpHeaderAuth`.
- **URL**: Điền URL API của SendGrid (ví dụ: `https://api.sendgrid.com/v3/mail/send`).
- **Headers**: Thêm `Authorization: Bearer {SENDGRID_API_KEY}`.
- **Payload**: Nội dung email (ví dụ: `{"personalizations": [{"to": [{"email": "{{$node["Get Affected Passengers"].json()["email"]}}"}]}], "from": {"email": "no-reply@airline.com"}, "subject": "Update Flight Schedule", "text": "Your flight has been delayed..."}`).

##### **K. Send SMS (Critical Only) (HTTP Request)**
- **Credentials**: Chọn `httpBasicAuth`.
- **URL**: Điền URL API của Twilio (ví dụ: `https://api.twilio.com/2010-04-01/Accounts/{ACCOUNT_SID}/Messages.json`).
- **Headers**: Thêm `Authorization: Basic {ACCOUNT_SID}:{AUTH_TOKEN}`.
- **Payload**: Nội dung SMS (ví dụ: `{"To": "{{$node["Get Affected Passengers"].json()["phone"]}}", "From": "+1234567890", "Body": "URGENT: Your flight has been CANCELLED. Contact customer service."}`).

##### **L. Update Internal Systems (HTTP Request)**
- **URL**: Điền Webhook URL của hệ thống nội bộ (nếu có).
- **Payload**: Gửi dữ liệu thay đổi để đồng bộ (ví dụ: `{"flight_number": "{{$node["Fetch Airline Data"].json()["flight_number"]}}", "status": "{{$node["Fetch Airline Data"].json()["status"]}}"`).

##### **M. Log Sync Activity (PostgreSQL)**
- **Credentials**: Chọn `postgres`.
- **Query**: Ghi log hoạt động (ví dụ):
  ```sql
  INSERT INTO sync_logs (flight_number, action, timestamp)
  VALUES ($1, $2, NOW());
  ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và nhập **dữ liệu mẫu** (ví dụ: một chuyến bay bị hủy).
   - Kiểm tra các **thông báo Slack, email, SMS** và **cập nhật DB**.
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Google Sheets/Excel**:
   - Thay vì PostgreSQL, các sếp có thể sử dụng **Google Sheets** (n8n có node `n8n-nodes-base.googleSheets`) để lưu lịch bay và log.
   - **Lợi ích**: Dễ dàng theo dõi và chia sẻ dữ liệu với đội ngũ.

2. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.scheduleTrigger`** để chạy workflow **mỗi ngày cuối tuần** và gửi **báo cáo tổng hợp** về lịch bay qua email.

3. **Tích hợp với CRM (HubSpot/Salesforce)**:
   - Sử dụng node `httpRequest` để gửi thông báo về **CRM** nếu hành khách bị ảnh hưởng là khách hàng VIP.

4. **Lưu log vào Google Drive**:
   - Thay vì PostgreSQL, các sếp có thể lưu log vào **Google Drive** (n8n có node `n8n-nodes-base.googleDrive`) để dễ dàng truy cập và phân tích.

5. **Cảnh báo tự động cho hành khách qua WhatsApp**:
   - Sử dụng **Twilio WhatsApp API** để gửi thông báo thay vì SMS (nếu hành khách đã đăng ký).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các công ty hàng không, tour du lịch, hoặc bất kỳ doanh nghiệp nào cần **theo dõi lịch bay thực tế và thông báo tức thời** cho hành khách. Với **tự động hóa 100% không cần code**, các sếp sẽ:
✅ **Tiết kiệm thời gian** và giảm thiểu sai sót.
✅ **Nâng cao trải nghiệm hành khách** với thông báo kịp thời.
✅ **Giảm rủi ro pháp lý** bằng cách đảm bảo thông tin được cập nhật chính xác.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** với dữ liệu mẫu.
3. **Active workflow** và bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định 24/7!