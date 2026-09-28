---
title: "📲 Tự Động Hóa SMS Xác Nhận, Nhắc Nhở & Lập Lại Hẹn Cho Bác Sĩ - Giảm 90% Công Việc Lặp Lại"
description: "Workflow này tự động gửi SMS xác nhận, nhắc nhở trước giờ hẹn và lập lại hẹn cho khách hàng không đến (no-show) trên Aloware, tiết kiệm thời gian quản lý lên đến 10 giờ/tuần cho các sếp y tế. Hỗ trợ tất cả hệ thống đặt lịch như Calendly, Acuity, Jane App..."
slug: "tieu-dong-hoa-sms-xac-nhan-nhac-nho-no-show-aloware"
tags: [n8n, automation, no-code, aloware, y-te, booking-system, sms-automation]
keywords: [tự động hóa SMS y tế, workflow n8n cho bác sĩ, giảm no-show, nhắc nhở trước hẹn, Aloware API, tự động hóa đặt lịch y tế]
---

# 🚀 **Tự Động Hóa SMS Xác Nhận, Nhắc Nhở & Lập Lại Hẹn Cho Khách Hàng Y Tế**

### **Giải Phóng Thời Gian Quản Lý Hẹn Cho Các Sếp Y Tế**
Các sếp y tế và nhân viên hành chính tại phòng khám, bệnh viện hay trung tâm chăm sóc sức khỏe thường phải mất **từ 5-10 giờ/tuần** để:
- Xác nhận lại thông tin hẹn với khách hàng qua SMS/email.
- Gửi nhắc nhở trước giờ hẹn (48h, 24h, 2h trước).
- Xử lý trường hợp khách hàng **không đến (no-show)** và lập lại hẹn mới.
- Theo dõi và cập nhật thông tin liên lạc của bệnh nhân trong hệ thống Aloware.

**Workflow này tự động hóa toàn bộ quy trình trên chỉ với một dòng mã tự động hóa n8n**, giúp:
✅ **Tiết kiệm 90% thời gian** quản lý hẹn.
✅ **Tăng tỷ lệ khách hàng đến hẹn** nhờ nhắc nhở tự động.
✅ **Giảm công việc lặp lại** với SMS xác nhận và lập lại hẹn no-show.
✅ **Cập nhật tự động** thông tin bệnh nhân trong Aloware.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không phụ thuộc vào dịch vụ cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động xác nhận SMS** ngay khi khách hàng đặt lịch (gồm ngày giờ, địa điểm, tên bác sĩ).
- **Nhắc nhở tự động** 48h, 24h và 2h trước giờ hẹn (có thể kết hợp SMS + gọi điện).
- **Lập lại hẹn tự động** cho khách hàng không đến (no-show) với lịch trình nhắc nhở mới.
- **Cập nhật thông tin bệnh nhân** trong Aloware một cách chính xác và liên tục.
- **Giảm tỷ lệ no-show** lên đến 30-40% nhờ nhắc nhở kịp thời.
- **Hỗ trợ tất cả hệ thống đặt lịch** như Calendly, Acuity, Jane App, Setmore,...
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** (đã tích hợp API) và các thông tin sau:
   - `ALOWARE_API_TOKEN` (API Key của Aloware).
   - `ALOWARE_LINE_PHONE` (số điện thoại của Aloware để gửi SMS).
   - `ALOWARE_REMINDER_SEQUENCE_ID` (ID của chuỗi nhắc nhở tự động).
   - `ALOWARE_NOSHOW_SEQUENCE_ID` (ID của chuỗi lập lại hẹn cho no-show).
2. **Hệ thống đặt lịch** (Calendly, Acuity, Jane App,...) đã cấu hình **webhook POST** đến URL của n8n.
3. **Thông tin cơ sở y tế**:
   - `PRACTICE_NAME` (tên phòng khám/bệnh viện).
   - `PRACTICE_ADDRESS` (địa chỉ chi tiết).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15021](https://n8n.io/workflows/15021) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** (trang chủ của n8n) và nhấn **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô nhập liệu.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này bao gồm **10 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Webhook: Nhận Lịch Hẹn Mới**
- **Node**: `Booking System: Appointment Created`
  - **Path**: `appointment-booked` (không thay đổi).
  - **HTTP Method**: `POST` (không thay đổi).
  - **Lưu ý**:
    - Cấu hình **webhook** trong hệ thống đặt lịch (Calendly, Acuity,...) để gửi dữ liệu mới về URL của n8n.
    - Ví dụ: Nếu URL của n8n là `https://tên-máy-vps.com`, thì webhook sẽ POST đến `https://tên-máy-vps.com/appointment-booked`.

##### **B. Normalize Appointment Data**
- **Node**: `Normalize Appointment Data` (type: `set`)
  - **Lưu ý**: Node này **không cần chỉnh sửa** nếu dữ liệu từ hệ thống đặt lịch đã chuẩn. Nếu dữ liệu không đầy đủ, các sếp có thể thêm logic xử lý trong **stickyNote** hoặc **JavaScript** để đảm bảo các trường như `patientName`, `appointmentDate`, `providerName` được trích xuất chính xác.

##### **C. Aloware: Create or Update Patient Contact**
- **Node**: `Aloware: Create or Update Patient Contact` (type: `httpRequest`)
  - **Method**: `POST` (để tạo mới) hoặc `PUT` (để cập nhật).
  - **Headers**:
    - `Authorization`: `Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "phone": "{{ $json["patientPhone"] }}",
      "name": "{{ $json["patientName"] }}",
      "email": "{{ $json["patientEmail"] }}",
      "custom_fields": {
        "practice_name": "{{ $variables.PRACTICE_NAME }}",
        "practice_address": "{{ $variables.PRACTICE_ADDRESS }}"
      }
    }
    ```
  - **Lưu ý**:
    - Thay thế `{{ $json["patientPhone"] }}`, `{{ $json["patientName"] }}`, `{{ $json["patientEmail"] }}` bằng các trường tương ứng trong dữ liệu từ webhook.
    - Nếu Aloware yêu cầu cấu trúc khác, các sếp cần tham khảo [API Documentation của Aloware](https://aloware.com/developers/api-docs).

##### **D. Aloware: Send Booking Confirmation SMS**
- **Node**: `Aloware: Send Booking Confirmation SMS` (type: `httpRequest`)
  - **Method**: `POST`.
  - **Headers**:
    - `Authorization`: `Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "phone": "{{ $json["patientPhone"] }}",
      "message": "Xác nhận hẹn với {{ $variables.PRACTICE_NAME }}:\n\nNgày: {{ $json["appointmentDate"] }}\nGiờ: {{ $json["appointmentTime"] }}\nĐịa chỉ: {{ $variables.PRACTICE_ADDRESS }}\nBác sĩ: {{ $json["providerName"] }}",
      "type": "sms"
    }
    ```
  - **Lưu ý**:
    - Thay thế các biến `{{ $json["..."] }}` bằng dữ liệu từ webhook.
    - Có thể tùy chỉnh nội dung SMS theo yêu cầu (ví dụ: thêm link Google Maps, thông tin bảo hiểm,...).

##### **E. Aloware: Enroll in Reminder Sequence**
- **Node**: `Aloware: Enroll in Reminder Sequence` (type: `httpRequest`)
  - **Method**: `POST`.
  - **Headers**:
    - `Authorization`: `Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "patient_id": "{{ $json["patientId"] }}",
      "sequence_id": "{{ $variables.ALOWARE_REMINDER_SEQUENCE_ID }}"
    }
    ```
  - **Lưu ý**:
    - `patient_id` phải trùng với ID bệnh nhân trong Aloware.
    - `ALOWARE_REMINDER_SEQUENCE_ID` là ID của chuỗi nhắc nhở đã cấu hình trước trong Aloware (ví dụ: chuỗi gồm SMS 48h, 24h, 2h trước).

##### **F. Wait Until After Appointment**
- **Node**: `Wait Until After Appointment` (type: `wait`)
  - **Lưu ý**:
    - Node này sẽ **chờ 1 giờ sau giờ hẹn** trước khi kiểm tra no-show.
    - Thời gian chờ được tính từ `{{ $json["appointmentDate"] }} + 1 hour`.
    - Các sếp có thể điều chỉnh thời gian chờ trong **Expression**:
      ```javascript
      new Date($json["appointmentDate"]) + 1 * 60 * 60 * 1000
      ```

##### **G. Aloware: Check If Appointment Completed**
- **Node**: `Aloware: Check If Appointment Completed` (type: `httpRequest`)
  - **Method**: `GET`.
  - **URL**:
    ```
    https://api.aloware.com/v1/appointments/{{ $json["appointmentId"] }}
    ```
  - **Headers**:
    - `Authorization`: `Bearer {{ $variables.ALOWARE_API_TOKEN }}`
  - **Lưu ý**:
    - Node này sẽ gọi API Aloware để kiểm tra trạng thái của hẹn (đã đến hay no-show).
    - Nếu trạng thái là `no-show`, workflow sẽ chuyển sang node tiếp theo.

##### **H. Was It a No-Show?**
- **Node**: `Was It a No-Show?` (type: `if`)
  - **Condition**:
    ```javascript
    $json["status"] === "no-show"
    ```
  - **Lưu ý**:
    - Node này sẽ **kiểm tra** nếu hẹn có trạng thái `no-show`.
    - Nếu **true**, workflow sẽ gửi yêu cầu lập lại hẹn (`Aloware: Enroll in No-Show Re-booking Sequence`).
    - Nếu **false**, workflow sẽ kết thúc với node `Appointment Completed — No Action`.

##### **I. Aloware: Enroll in No-Show Re-booking Sequence**
- **Node**: `Aloware: Enroll in No-Show Re-booking Sequence` (type: `httpRequest`)
  - **Method**: `POST`.
  - **Headers**:
    - `Authorization`: `Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "patient_id": "{{ $json["patientId"] }}",
      "sequence_id": "{{ $variables.ALOWARE_NOSHOW_SEQUENCE_ID }}"
    }
    ```
  - **Lưu ý**:
    - `ALOWARE_NOSHOW_SEQUENCE_ID` là ID của chuỗi lập lại hẹn cho no-show (cần cấu hình trước trong Aloware).
    - Chuỗi này có thể bao gồm SMS/email mời lập lại hẹn và lịch trình nhắc nhở mới.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Các sếp có thể **test run** với dữ liệu mẫu từ webhook để đảm bảo workflow hoạt động chính xác.
- **Bật Active**: Sau khi kiểm tra, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo lỗi hoặc cập nhật trạng thái hẹn cho đội ngũ quản lý.
   - Ví dụ: Gửi tin nhắn Slack khi có hẹn no-show:
     ```json
     {
       "text": "Khách hàng {{ $json["patientName"] }} ({{ $json["patientPhone"] }}) không đến hẹn! Đã lập lại hẹn tự động."
     }
     ```

2. **Lưu Log Dữ Liệu**:
   - Thêm node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.database` để lưu lịch sử hẹn, no-show và phản hồi của khách hàng.
   - Có thể phân tích dữ liệu để cải thiện tỷ lệ đến hẹn.

3. **Tùy Chỉnh Nội Dung SMS**:
   - Sử dụng **stickyNote** hoặc **JavaScript** để động thái nội dung SMS dựa trên loại hẹn (ví dụ: khám tổng quát, tiêm vaccine,...).
   - Ví dụ:
     ```javascript
     if ($json["appointmentType"] === "vaccine") {
       message = "Xin nhắc nhở: Hẹn tiêm vaccine COVID-19 tại {{ $variables.PRACTICE_NAME }}!";
     } else {
       message = "Xác nhận hẹn khám tổng quát...";
     }
     ```

4. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` để gửi báo cáo tổng hợp no-show hàng tuần cho quản lý.
   - Ví dụ: Báo cáo số lượng no-show, tỷ lệ no-show, và thời gian lập lại hẹn.

5. **Cấu Hình Chuỗi Nhắc Nhở Tùy Chỉnh**:
   - Trong Aloware, các sếp có thể **t