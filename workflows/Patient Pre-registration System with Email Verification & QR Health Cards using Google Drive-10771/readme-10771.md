---
title: "🏥 **Hệ Thống Đăng Ký Trước Bệnh Nhân Tự Động + Thẻ Sức Khỏe QR + Xác Minh Email (n8n)**"
description: "Tự động hóa toàn bộ quy trình đăng ký trước bệnh nhân cho bác sĩ, từ xác minh email đến tạo thẻ sức khỏe QR chuyên nghiệp, gửi email tự động và ghi chép dữ liệu vào Google Sheets - hoàn thành trong 15-20 giây!"
slug: "he-thong-dang-ky-truoc-benh-nhan-tu-dong-voi-thong-bao-qr"
tags: [n8n, tự động hóa y tế, xác minh email, thẻ sức khỏe QR, Google Drive, Gmail, Slack, Google Sheets]
keywords: [n8n workflow y tế, tự động hóa đăng ký bệnh nhân, thẻ sức khỏe QR tự động, xác minh email VerifiEmail, tự động hóa bác sĩ]
---

# 🚀 **Tự Động Hóa Đăng Ký Trước Bệnh Nhân + Thẻ Sức Khỏe QR (n8n)**

Bạn là một **bác sĩ, nhân viên y tế hoặc quản lý phòng khám** đang phải chịu đựng những **quá trình đăng ký bệnh nhân thủ công, rắc rối, mất thời gian**? Hay phải **ghi chép dữ liệu vào nhiều hệ thống khác nhau** như Google Sheets, Slack và Gmail? Hãy tưởng tượng một **hệ thống tự động hóa hoàn toàn** chỉ trong **15-20 giây** có thể:
✅ **Xác minh email** của bệnh nhân để đảm bảo thông tin chính xác
✅ **Tạo thẻ sức khỏe QR** chuyên nghiệp với thông tin cá nhân, triệu chứng và mã QR check-in
✅ **Gửi email tự động** với thẻ QR và hướng dẫn check-in
✅ **Ghi chép dữ liệu** vào Google Sheets và thông báo cho đội ngũ tiếp nhận trên Slack
✅ **Tạo liên kết Google Drive** để bệnh nhân và nhân viên y tế truy cập dễ dàng

**Workflow này giải quyết tất cả những vấn đề trên với 100% tự động hóa, không cần viết code!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 30-50% thời gian** của nhân viên tiếp nhận bệnh nhân
- **Giảm sai sót** nhờ xác minh email tự động
- **Cải thiện trải nghiệm bệnh nhân** với thẻ sức khỏe QR chuyên nghiệp
- **Dữ liệu thống nhất** trên Google Sheets, Slack và Gmail
- **Hoạt động 24/7** mà không cần can thiệp thủ công
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - [VerifiEmail API](https://www.verifiemail.com/) (để xác minh email)
   - [HTMLCSSToImg API](https://htmlcsstoimg.com/) (chuyển HTML thành ảnh PNG)
   - **Google OAuth 2.0** cho:
     - Google Drive (để lưu thẻ sức khỏe)
     - Google Sheets (để ghi chép dữ liệu)
     - Gmail (để gửi email tự động)
   - **Slack API** (để thông báo cho đội ngũ tiếp nhận)
   - **Webhook URL** (để nhận dữ liệu từ form đăng ký bệnh nhân)

2. **Cấu trúc Google Drive & Sheets**:
   - **Thư mục "Patients record"** trong Google Drive (để lưu thẻ sức khỏe)
   - **Google Sheet** với các cột:
     - Timestamp, Patient ID, Name, Email, Phone, Email Verified, Appointment DateTime, Symptoms, Drive Link, Email Sent, Status

3. **Slack Channel**:
   - Tạo **#clinic-reception** để nhận thông báo từ workflow

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10771](https://n8n.io/workflows/10771) và import vào n8n Editor.
- **Copy/Paste JSON** từ link trên vào n8n Editor (đường dẫn: `https://n8n.io/workflows/10771/raw`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **14 node** với các chức năng chính sau. Các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node 1: Webhook Trigger (n8n-nodes-base.webhook)**
- **Path**: `patient-checkin`
- **HTTP Method**: `POST`
- **Lưu ý**:
  - Các sếp cần **cấu hình webhook** để nhận dữ liệu từ form đăng ký bệnh nhân (có thể sử dụng **Google Form**, **Typeform** hoặc **custom form**).
  - **Test webhook** bằng cách gửi dữ liệu mẫu (ví dụ: JSON dưới đây):
    ```json
    {
      "name": "Nguyễn Văn A",
      "email": "patient@example.com",
      "phone": "0123456789",
      "appointmentDateTime": "2024-12-25T10:00:00",
      "symptoms": "Đau đầu, sốt nhẹ",
      "address": "123 Đường ABC, Quận 1, TP.HCM"
    }
    ```

##### **🔹 Node 2: Validate Input Data (n8n-nodes-base.code)**
- **Chức năng**: Kiểm tra dữ liệu đầu vào có đầy đủ không (name, email, appointmentDateTime).
- **Lưu ý**:
  - Sử dụng **JavaScript** để kiểm tra và **bổ sung Patient ID** tự động (ví dụ: `PAT-{timestamp}-{randomString}`).
  - **Định dạng lại thời gian** theo **múi giờ Việt Nam** (12-hour format, ví dụ: "10:00 AM, 25/12/2024").

##### **🔹 Node 3: Check Email Valid (n8n-nodes-base.if)**
- **Chức năng**: Kiểm tra email có hợp lệ không.
- **Lưu ý**:
  - Nếu email **không hợp lệ**, workflow sẽ **dừng lại** và gửi **lỗi đến bệnh nhân** (node `Stop and Error`).

##### **🔹 Node 4: Verifi Email (n8n-nodes-verifiemail.verifiEmail)**
- **Chức năng**: Xác minh email bằng **VerifiEmail API**.
- **Cấu hình**:
  - Điền **API Key** từ VerifiEmail vào `verifiEmailApi` (tạo trong n8n Credentials).
  - **Lưu ý**:
    - Nếu email **không xác minh được**, workflow sẽ **dừng lại** và thông báo lỗi.
    - Nếu xác minh thành công (`valid = true`), workflow tiếp tục.

##### **🔹 Node 5: Generate QR Code & Build Health Card HTML (n8n-nodes-base.code)**
- **Chức năng**: Tạo **mã QR** và **HTML thẻ sức khỏe**.
- **Lưu ý**:
  - **Node `Generate QR Code`** sử dụng **QR Server API** (miễn phí) để tạo mã QR cho check-in.
  - **Node `Build Health Card HTML`** xây dựng **HTML thẻ sức khỏe** với:
    - **Header gradient** (đầu trang)
    - **Grid thông tin bệnh nhân** (tên, email, triệu chứng)
    - **Section QR code** (mã QR check-in)
    - **Footer** (hướng dẫn check-in)

##### **🔹 Node 6: HTML/CSS to Image (n8n-nodes-htmlcsstoimage.htmlCssToImage)**
- **Chức năng**: Chuyển **HTML thẻ sức khỏe** thành **ảnh PNG**.
- **Cấu hình**:
  - Điền **API Key** từ HTMLCSSToImg vào `htmlcsstoimgApi`.
  - **Lưu ý**:
    - **Kích thước ảnh**: 800x500px (đủ để in hoặc xem trên điện thoại).
    - **CSS**: Sử dụng **gradient header**, font **Roboto**, và **màu sắc chuyên nghiệp**.

##### **🔹 Node 7: Upload PNG to Google Drive (n8n-nodes-base.googleDrive)**
- **Chức năng**: Tải **thẻ sức khỏe PNG** lên Google Drive.
- **Cấu hình**:
  - Chọn **thư mục "Patients record"** (đã tạo trước).
  - **Tên file**: `PAT-{patientId}_health_card.png` (ví dụ: `PAT-1762965729048-E5BPPW4T4_health_card.png`).
  - **Lưu ý**:
    - **Cài đặt quyền**: Cho phép **bệnh nhân và nhân viên y tế** truy cập.

##### **🔹 Node 8: Email Health Card to Patient (n8n-nodes-base.gmail)**
- **Chức năng**: Gửi **email tự động** với thẻ sức khỏe và hướng dẫn.
- **Cấu hình**:
  - Chọn **gmailOAuth2** (đã cấu hình trước).
  - **Nội dung email**:
    ```html
    <h1>Thẻ Sức Khỏe Của Bạn</h1>
    <p>Xin chào {{ $node["Validate Input Data"].json["$.name"] }},</p>
    <p>Dưới đây là thẻ sức khỏe của bạn cho cuộc hẹn vào {{ $node["Validate Input Data"].json["$.appointmentDateTime"] }}:</p>
    <img src="cid:health_card" width="800" />
    <p><strong>Hướng dẫn check-in:</strong></p>
    <ol>
      <li>Quét mã QR trên thẻ sức khỏe bằng điện thoại</li>
      <li>Điền thông tin cá nhân nếu yêu cầu</li>
      <li>Chờ nhân viên y tế gọi tên</li>
    </ol>
    <p>Liên kết Google Drive: <a href="{{ $node["Upload PNG to Drive"].json["$.webViewLink"] }}">Truy cập thẻ sức khỏe</a></p>
    ```
  - **Đính kèm**: Thẻ sức khỏe PNG (tải từ Google Drive).

##### **🔹 Node 9: Notify Reception Team (n8n-nodes-base.slack)**
- **Chức năng**: Gửi **thông báo Slack** cho đội ngũ tiếp nhận.
- **Cấu hình**:
  - Chọn **slackApi** (đã cấu hình trước).
  - **Nội dung thông báo**:
    ```json
    {
      "text": "🚨 Bệnh nhân mới đăng ký: {{ $node["Validate Input Data"].json["$.name"] }}",
      "attachments": [
        {
          "title": "Thông tin bệnh nhân",
          "fields": [
            { "title": "Email", "value": "{{ $node["Validate Input Data"].json["$.email"] }}", "short": true },
            { "title": "Số điện thoại", "value": "{{ $node["Validate Input Data"].json["$.phone"] }}", "short": true },
            { "title": "Cuộc hẹn", "value": "{{ $node["Validate Input Data"].json["$.appointmentDateTime"] }}", "short": true },
            { "title": "Triệu chứng", "value": "{{ $node["Validate Input Data"].json["$.symptoms"] }}", "short": false }
          ],
          "footer": "Liên kết thẻ sức khỏe: {{ $node["Upload PNG to Drive"].json["$.webViewLink"] }}",
          "ts": "{{ $node["Validate Input Data"].json["$.timestamp"] }}"
        }
      ]
    }
    ```

##### **🔹 Node 10: Log to Patient Database (n8n-nodes-base.googleSheets)**
- **Chức năng**: Ghi **dữ liệu bệnh nhân** vào Google Sheets.
- **Cấu hình**:
  - Chọn **googleSheetsOAuth2Api**.
  - **Cột cần ghi**:
    - `Timestamp`, `Patient ID`, `Name`, `Email`, `Phone`, `Email Verified`, `Appointment DateTime`, `Symptoms`, `Drive Link`, `Email Sent`, `Status`.

##### **🔹 Node 11: Respond to Webhook (n8n-nodes-base.respondToWebhook)**
- **Chức năng**: Trả lời **webhook** khi workflow hoàn thành.
- **Cấu hình**:
  - **Trả về JSON** thành công:
    ```json
    {
      "status": "success",
      "patientId": "{{ $node["Validate Input Data"].json["$.patientId"] }}",
      "message": "Thẻ sức khỏe đã được tạo và gửi thành công!"
    }
    ```

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu (như ở trên).
2. **Bật Active** workflow.
3. **Monitor** trên Slack và Google Sheets để kiểm tra.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cải Thiện & Mở Rộng**]
1. **Kết nối với CRM**:
   - Sử dụng **Zoho CRM** hoặc **HubSpot** để đồng bộ dữ liệu bệnh nhân.

2. **Tự động gửi nhắc nhở**:
   - Sử dụng **n8n-nodes-base.googleCalendar** để gửi **nhắc nhở email** trước ngày hẹn.

3. **Lưu log hoạt động**:
   - Sử dụng **n8n-nodes-base.stickyNote** để ghi chép **lịch sử hoạt động** của workflow.

4. **Tích hợp với Telegram**:
   - Sử dụng **n8n-nodes-base.telegram** để gửi **thông báo bệnh nhân** qua Telegram.

5. **Tạo báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.googleSheets** để **tính toán thống kê** số lượng bệnh nhân, triệu chứng phổ biến.

6. **Tự động tạo form đăng ký**: