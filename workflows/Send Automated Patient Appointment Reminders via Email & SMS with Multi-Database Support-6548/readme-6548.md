---
title: "🚀 Tự Động Gửi Lại Lịch Hẹn Bệnh Nhân qua Email & SMS với Hỗ Trợ Multi-Database (Google Sheets, Airtable, PostgreSQL)"
description: "Giải pháp tự động hóa hoàn toàn không cần code để gửi nhắc nhở lịch hẹn bệnh nhân qua email và SMS với 3 ngày và 1 ngày trước, đồng thời cập nhật trạng thái trong 3 cơ sở dữ liệu khác nhau. Giúp bác sĩ và nhân viên y tế tiết kiệm thời gian lên đến 60% trong quản lý lịch hẹn."
slug: "tieu-dong-gui-lai-lich-hen-benh-nhan-email-sms"
tags: [n8n, automation, no-code, y-te, healthcare, email-sms, google-sheets, airtable, postgresql, twilio]
keywords: [tự động hóa y tế n8n, gửi nhắc nhở lịch hẹn bệnh nhân, multi-database automation, nhắc nhở email sms, tự động hóa không code, lưu trữ dữ liệu bệnh nhân]
---

# 🚀 **Tự Động Gửi Lại Lịch Hẹn Bệnh Nhân qua Email & SMS với Multi-Database**

### **Giải pháp cho bác sĩ và nhân viên y tế: Tiết kiệm 60% thời gian quản lý lịch hẹn!**
Hiện nay, việc nhắc nhở bệnh nhân về lịch hẹn vẫn còn phụ thuộc vào cách thủ công: gọi điện, gửi email hoặc nhắn tin qua ứng dụng. Điều này không chỉ tốn thời gian mà còn dễ bị bỏ sót hoặc trùng lịch. **Workflow này tự động hóa toàn bộ quy trình nhắc nhở lịch hẹn qua email và SMS với 2 thời điểm quan trọng: 3 ngày và 1 ngày trước**, đồng thời cập nhật trạng thái trong **Google Sheets, Airtable và PostgreSQL** để đảm bảo tính nhất quán và dễ theo dõi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần gọi điện hoặc gửi email thủ công, giảm thiểu sai sót và trùng lịch.
- **Tính nhất quán**: Dữ liệu lịch hẹn được đồng bộ hóa trên **3 cơ sở dữ liệu** (Google Sheets, Airtable, PostgreSQL).
- **Tăng tỷ lệ tham dự**: Nhắc nhở kịp thời qua **email và SMS** giúp bệnh nhân nhớ lịch hẹn hơn.
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
- **Dễ theo dõi**: Trạng thái nhắc nhở (đã gửi, chưa gửi) được cập nhật tự động trên tất cả các bảng dữ liệu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Sheets**: API Key và file CSV của sheet (cần tạo sheet mới với các cột: `PatientName`, `AppointmentDate`, `Email`, `Phone`, `Status`).
   - **Airtable**: API Key và Base ID (tạo một Base mới với các trường tương ứng).
   - **PostgreSQL**: Thông tin kết nối (Host, Port, Database Name, Username, Password).
   - **Twilio**: API Key và Auth Token (để gửi SMS).
   - **Email Provider**: Thông tin SMTP (nếu sử dụng node `emailSend`).

2. **Workflow Webhook**:
   - Cần một URL Webhook để nhận dữ liệu lịch hẹn mới từ hệ thống quản lý bệnh viện (hoặc bạn có thể mock dữ liệu mẫu để test).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/6548) (hoặc copy JSON từ link trên).
- **Bước 2**: Mở n8n Editor và chọn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập.
- **Bước 3**: Workflow sẽ hiển thị với 18 node đã sắp xếp theo logic.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook: New Appointment**
- Node này nhận dữ liệu từ bên ngoài (ví dụ: từ hệ thống quản lý bệnh viện).
- **Lưu ý**:
  - Chọn **HTTP Trigger** và cấu hình URL Webhook.
  - Nếu mock dữ liệu, bạn có thể sử dụng **Set Node** để tạo dữ liệu mẫu (ví dụ: `{"PatientName": "Nguyễn Văn A", "AppointmentDate": "2024-12-15", "Email": "a@example.com", "Phone": "+84123456789", "Status": "Pending"}`).

##### **B. Cấu hình Google Sheets**
- Node **"Store in Google Sheets"** và **"Update Google Sheets: 3-Day Sent" / "1-Day Sent"**:
  - **Credentials**: Chọn tài khoản Google đã kết nối với n8n.
  - **Sheet Name**: Điền tên sheet đã tạo trước đó (ví dụ: `Lịch_Hẹn_Bệnh_Nhân`).
  - **Range**: Điền `Sheet1!A1:F1000` (hoặc tùy chỉnh theo cột dữ liệu).
  - **Headers**: Chọn `Use first row as header`.

##### **C. Cấu hình Airtable**
- Node **"Store in Airtable"** và **"Update Airtable: 3-Day Sent" / "1-Day Sent"**:
  - **Credentials**: Chọn API Key đã cấu hình trong n8n.
  - **Base ID**: Điền ID của Base Airtable đã tạo.
  - **Table Name**: Điền tên bảng (ví dụ: `Lịch_Hẹn`).
  - **Fields**: Đảm bảo các trường trong Airtable khớp với dữ liệu input (ví dụ: `PatientName`, `AppointmentDate`, `Email`, `Phone`, `Status`).

##### **D. Cấu hình PostgreSQL**
- Node **"Store in PostgreSQL"** và **"Update PostgreSQL: 3-Day Sent" / "1-Day Sent"**:
  - **Credentials**: Thêm mới một credential PostgreSQL trong n8n với thông tin kết nối.
  - **Query**: Đối với node lưu trữ, sử dụng:
    ```sql
    INSERT INTO appointments (patient_name, appointment_date, email, phone, status)
    VALUES ($$.json["PatientName"], $$.json["AppointmentDate"], $$.json["Email"], $$.json["Phone"], $$.json["Status"])
    ```
  - Đối với node cập nhật, sử dụng:
    ```sql
    UPDATE appointments
    SET status = '3-Day Reminder Sent'
    WHERE phone = $$.json["Phone"] AND appointment_date = $$.json["AppointmentDate"]
    ```

##### **E. Cấu hình Twilio (SMS)**
- Node **"Send 3-Day SMS Reminder"** và **"Send 1-Day SMS Reminder"**:
  - **Credentials**: Thêm credential Twilio với API Key và Auth Token.
  - **From Number**: Điền số điện thoại Twilio đã mua.
  - **To Number**: Sử dụng `$$.json["Phone"]` để gửi SMS cho bệnh nhân.
  - **Body**: Tùy chỉnh nội dung SMS (ví dụ: `Xin chào {{ $$.json["PatientName"] }}, nhắc nhở lịch hẹn ngày {{ $$.json["AppointmentDate"] }} sắp đến. Xin vui lòng xác nhận.`).

##### **F. Cấu hình Email**
- Node **"Send 3-Day Email Reminder"** và **"Send 1-Day Email Reminder"**:
  - **Credentials**: Thêm credential SMTP của nhà cung cấp email (ví dụ: Gmail, SendGrid).
  - **From**: Điền địa chỉ email gửi (ví dụ: `no-reply@benhvien.com`).
  - **To**: Sử dụng `$$.json["Email"]`.
  - **Subject**: Tùy chỉnh tiêu đề (ví dụ: `Nhắc nhở: Lịch hẹn ngày {{ $$.json["AppointmentDate"] }}`).
  - **HTML Content**: Thêm nội dung HTML (ví dụ:
    ```html
    <p>Xin chào {{ $$.json["PatientName"] }},</p>
    <p>Đây là nhắc nhở lịch hẹn với bác sĩ ngày {{ $$.json["AppointmentDate"] }}.</p>
    <p>Xin vui lòng xác nhận tham dự.</p>
    ```).

##### **G. Cấu hình Wait Nodes**
- Node **"Wait: 3 Days Before"** và **"Wait: 1 Day Before"**:
  - Đảm bảo thời gian chờ được tính từ ngày hẹn (`$$.json["AppointmentDate"]`).
  - Ví dụ: Đối với node `Wait: 3 Days Before`, sử dụng:
    ```javascript
    const appointmentDate = new Date($$.json["AppointmentDate"]);
    const waitTime = new Date(appointmentDate);
    waitTime.setDate(waitTime.getDate() - 3);
    return { waitTime: waitTime };
    ```

---

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Test run với dữ liệu mẫu (ví dụ: một lịch hẹn giả).
- **Bước 2**: Kiểm tra các node:
  - Dữ liệu có được lưu vào Google Sheets, Airtable và PostgreSQL không?
  - Email và SMS có được gửi không?
  - Trạng thái trong các bảng dữ liệu có được cập nhật không?
- **Bước 3**: Nếu test thành công, bật **Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo lỗi hoặc trạng thái workflow.
   - Ví dụ: Nếu gửi SMS thất bại, gửi thông báo đến Slack.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại tất cả hoạt động (thành công/thất bại) của workflow.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Set** và **Email Send** để tự động gửi báo cáo tổng hợp số lượng nhắc nhở đã gửi hàng tháng cho quản lý.

4. **Tùy chỉnh nội dung nhắc nhở**:
   - Sử dụng node **Code** để động thái hóa nội dung email/SMS dựa trên loại lịch hẹn (ví dụ: khám tổng quát, khám chuyên khoa).

5. **Bảo mật dữ liệu**:
   - Masks hoặc xóa các trường nhạy cảm (ví dụ: số điện thoại) trong log hoặc email nếu không cần thiết.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình nhắc nhở lịch hẹn bệnh nhân, giúp bác sĩ và nhân viên y tế **tiết kiệm thời gian, giảm sai sót và tăng tỷ lệ tham dự**. Với hỗ trợ **multi-database**, dữ liệu luôn nhất quán và dễ theo dõi.

**Hành động ngay hôm nay!**
- Import workflow và cấu hình theo hướng dẫn trên.
- Thử nghiệm với dữ liệu mẫu trước khi áp dụng cho sản phẩm thực tế.
- **Tăng hiệu suất quản lý bệnh viện với tự động hóa 100% không cần code!**

---
**Cần hỗ trợ thêm?**
- Liên hệ tác giả David Olusola qua email: [david@daexai.com](mailto:david@daexai.com).
- Hoặc tham gia cộng đồng n8n tại [n8n.io/community](https://n8n.io/community).