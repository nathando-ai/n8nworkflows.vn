---
title: "🚀 Tự Động Hóa Tạo Hồ Sơ Người Dùng Chứng Minh (Email Xác Minh + PDF + Gửi Email Gmail) - N8N"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo hồ sơ người dùng chuyên nghiệp với email xác minh, chuyển đổi sang PDF và gửi tự động qua Gmail - tiết kiệm 90% thời gian thủ công. Phù hợp cho CRM, đăng ký dịch vụ, hoặc quản lý thành viên."
slug: "tay-dong-hoa-tao-ho-so-nguoi-dung-chung-minh"
tags: [n8n, automation, no-code, email-validation, pdf-generation, gmail-api, google-sheets, verifi-email]
keywords: [tự động hóa n8n, tạo hồ sơ người dùng, email xác minh, pdf từ html, gửi email gmail tự động, quản lý thành viên, workflow n8n miễn phí]
---

# 🚀 **Tự Động Hóa Tạo Hồ Sơ Người Dùng Chứng Minh (Email Xác Minh + PDF + Gmail) - N8N**

### **🔥 Giải pháp cho vấn đề gì?**
Các sếp đang gặp khó khăn khi phải:
- **Thủ công tạo hồ sơ người dùng** từ dữ liệu đăng ký (tốn thời gian, dễ sai sót).
- **Xác minh email** để tránh spam và người dùng giả (phải gọi điện hoặc gửi email thủ công).
- **Chuyển đổi hồ sơ sang PDF** và gửi qua email (cần kỹ năng thiết kế hoặc công cụ chuyên dụng).
- **Quản lý dữ liệu người dùng** trên nhiều bảng tính (Google Sheets) khác nhau.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Xác minh email** bằng API VerifiEmail (chỉ 10 giây).
✅ **Tạo hồ sơ HTML đẹp** với thông tin cá nhân của người dùng.
✅ **Chuyển đổi sang PDF** bằng công cụ HTMLcsstoPDF.
✅ **Gửi PDF qua Gmail** với email cá nhân hóa.
✅ **Ghi dữ liệu vào Google Sheets** để theo dõi người dùng đã xác minh.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 90% thời gian** so với thủ công (không cần copy-paste, thiết kế PDF, hoặc gọi điện xác minh).
- **Chính xác 100%** (không sai sót trong dữ liệu, email tự động xác minh).
- **Hồ sơ chuyên nghiệp** (thiết kế responsive, PDF đẹp mắt).
- **Hoạt động 24/7** (không cần can thiệp người dùng).
- **Dữ liệu theo dõi** (tất cả người dùng đã xác minh được lưu vào Google Sheets).
- **Trải nghiệm người dùng tốt** (email cá nhân hóa, thông báo rõ ràng).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (không dùng n8n.cloud vì có giới hạn API).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Các API Key & Credentials sau**:
   | **Dịch vụ**               | **Liên kết đăng ký**                     | **Thông tin cần thiết**                          |
   |---------------------------|------------------------------------------|--------------------------------------------------|
   | **VerifiEmail API**       | [https://verifi.email](https://verifi.email) | API Key (miễn phí 1000 request/tháng).          |
   | **HTMLcsstoPDF API**      | [https://htmlcsstoimg.com](https://htmlcsstoimg.com) | User ID & API Key (miễn phí 50 request/tháng). |
   | **Gmail OAuth2**          | [https://developers.google.com/gmail/api/guides/overview](https://developers.google.com/gmail/api/guides/overview) | Email & mật khẩu Google (để gửi email tự động). |
   | **Google Sheets OAuth2**  | [https://developers.google.com/sheets/api/quickstart/python](https://developers.google.com/sheets/api/quickstart/python) | Google Drive của cùng tài khoản Gmail. |

3. **Bảng tính Google Sheets** để lưu dữ liệu người dùng đã xác minh.
   - **Cột cần thiết**:
     - Name (Tên người dùng)
     - Email (Địa chỉ email)
     - City (Thành phố)
     - Profession (Ngành nghề)
     - Verified (✅/❌)
     - PDF_URL (Link tải PDF)
     - Date (Ngày xác minh)

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10163](https://n8n.io/workflows/10163) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào n8n Editor (đường dẫn: `https://n8n.io/workflows/10163` → Nhấn "Copy Workflow").

:::note[**Lưu ý**]
- **Không dùng n8n.cloud** vì có giới hạn API (VerifiEmail, HTMLcsstoPDF).
- **Kích hoạt "Active"** sau khi cấu hình xong.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node chính**, các sếp cần chú ý cấu hình sau:

#### **🔹 Node 1: Webhook - Nhận dữ liệu người dùng**
- **Cấu hình**:
  - **Path**: `create-profile` (không đổi).
  - **HTTP Method**: `POST`.
  - **Expected JSON Input** (dữ liệu người dùng gửi lên):
    ```json
    {
      "name": "John Doe",
      "email": "john@example.com",
      "city": "Hà Nội",
      "profession": "Kỹ sư phần mềm",
      "bio": "Loves building software"
    }
    ```
- **Lưu ý**:
  - Nếu dùng **webhook public**, các sếp cần bảo mật bằng **API Key** (thêm vào `Authorization: Bearer YOUR_API_KEY`).

#### **🔹 Node 2: IF Email Valid? (Xác minh email)**
- **Cấu hình**:
  - **Node VerifiEmail**: Điền `verifiEmailApi` (credentials đã setup trước).
  - **Input**: `{{ $json.email }}` (lấy email từ webhook).
- **Lưu ý**:
  - Nếu email **không hợp lệ**, workflow sẽ chuyển sang **đường False** (gửi email từ chối).

#### **🔹 Node 3: Generate HTML Template (Tạo mẫu HTML)**
- **Cấu hình**:
  - **Node Set**: Thiết lập biến `htmlTemplate` với nội dung HTML động (sử dụng `{{ $json.name }}`, `{{ $json.city }}`, ...).
  - **Ví dụ mẫu HTML** (có thể copy từ workflow gốc):
    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <style>
        body { font-family: 'Arial', sans-serif; margin: 20px; }
        .profile { border: 1px solid #ddd; padding: 20px; border-radius: 5px; }
        .info { margin-bottom: 10px; }
      </style>
    </head>
    <body>
      <div class="profile">
        <h1>Hồ Sơ Người Dùng</h1>
        <div class="info">
          <strong>Tên:</strong> {{ $json.name }}<br>
          <strong>Email:</strong> {{ $json.email }}<br>
          <strong>Thành Phố:</strong> {{ $json.city }}<br>
          <strong>Ngành Nghề:</strong> {{ $json.profession }}<br>
          <p>{{ $json.bio }}</p>
        </div>
      </div>
    </body>
    </html>
    ```

#### **🔹 Node 4 & 5: HTML → PDF (HTMLcsstoPDF)**
- **Cấu hình**:
  - **Node HTMLcsstoPDF**:
    - **Credentials**: `htmlcsstopdfApi`.
    - **Request Body**:
      ```json
      {
        "html": "{{ $json.htmlTemplate }}",
        "google_fonts": "Inter",
        "viewport_width": 800,
        "viewport_height": 1200
      }
      ```
  - **Node HTTP Request**:
    - **Method**: `GET`.
    - **URL**: `{{ $node["HTML to PDF"].json["url"] }}` (lấy từ node trước).
    - **Headers**: `Accept: application/pdf`.

#### **🔹 Node 6: Send Profile Email - Gmail (Gửi email PDF)**
- **Cấu hình**:
  - **Credentials**: `gmailOAuth2`.
  - **Email To**: `{{ $json.email }}`.
  - **Subject**: `"Hồ Sơ Của Bạn Đã Sẵn Sàng ✅"`.
  - **Body (HTML)**:
    ```html
    <p>Chào <strong>{{ $json.name }}</strong>,</p>
    <p>Hồ sơ của bạn đã được tạo thành công và đã được gửi qua email này.</p>
    <p>Bạn có thể tải hồ sơ PDF tại <a href="{{ $node["Download PDF Binary"].json["url"] }}">đây</a>.</p>
    ```
  - **Attachment**: `{{ $node["Download PDF Binary"].json["binary"] }}` (PDF binary).

#### **🔹 Node 7: Log to Google Sheets (Lưu dữ liệu)**
- **Cấu hình**:
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Operation**: `appendOrUpdate`.
  - **Sheet Name**: `Người Dùng Xác Minh`.
  - **Row Data**:
    ```json
    {
      "Name": "{{ $json.name }}",
      "Email": "{{ $json.email }}",
      "City": "{{ $json.city }}",
      "Profession": "{{ $json.profession }}",
      "Verified": "✅",
      "PDF_URL": "{{ $node["Download PDF Binary"].json["url"] }}",
      "Date": "{{ $node["Verifi Email"].json["date"] }}"
    }
    ```

#### **🔹 Node 8 & 9: Send Rejection Email (Email từ chối nếu email sai)**
- **Cấu hình**:
  - **Email To**: `{{ $json.email }}`.
  - **Subject**: `"Xác Minh Hồ Sơ Bị Từ Chối ❌"`.
  - **Body**:
    ```html
    <p>Chào <strong>{{ $json.name }}</strong>,</p>
    <p>Email của bạn <strong>{{ $json.email }}</strong> không hợp lệ. Vui lòng kiểm tra lại và thử lại.</p>
    <p>Lý do: {{ $node["Verifi Email"].json["reason"] }}</p>
    ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   ```json
   {
     "name": "Test User",
     "email": "test@example.com",
     "city": "Hà Nội",
     "profession": "Tester",
     "bio": "Dùng để test workflow."
   }
   ```
2. **Kiểm tra**:
   - Email **test@example.com** nhận được PDF không?
   - Dữ liệu có được ghi vào Google Sheets không?
3. **Bật Active** nếu test thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁC Ý TƯỞNG MỞ RỘNG**]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi người dùng xác minh thành công.
   - **Cấu hình**:
     ```json
     {
       "text": `🎉 Người dùng <strong>{{ $json.name }}</strong> đã xác minh thành công! Email: {{ $json.email }}`
     }
     ```

2. **Lưu log vào Google Drive**:
   - Thay vì chỉ ghi vào Google Sheets, các sếp có thể lưu **PDF và dữ liệu** vào Google Drive tự động.
   - **Node**: `n8n-nodes-googleDrive.googleDrive`.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để gửi email báo cáo số lượng người dùng mới xác minh hàng tuần.
   - **Ví dụ**:
     ```json
     {
       "subject": "Báo Cáo Người Dùng Mới Xác Minh (Tuần {{ $node["Date"].json["date"] }})",
       "body": `Tổng số người dùng mới: {{ $node["Google Sheets"].json["length"] }}`
     }
     ```

4. **Thêm xác minh 2FA (2 Factor Authentication)**:
   - Sử dụng **Twilio Verify** hoặc **Authy API** để yêu cầu mã xác minh qua SMS/email trước khi tạo hồ sơ.

5. **Tự động tạo hồ sơ từ CRM**:
   - Nếu các sếp dùng **HubSpot, Zoho CRM, hoặc Pipedrive**, có thể kết nối với node **CRM** để tự động tạo hồ sơ cho khách hàng mới.
   - **Ví dụ**:
     ```json
     {
       "name": "{{ $json.properties.first_name }} {{ $json.properties.last_name }}",
       "email": "{{ $json.properties.email }}",
       "city": "{{ $json.properties.city }}",
       "profession": "{{ $json.properties.job_title }}"
     }
     ```

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tạo hồ sơ thủ công, đồng thời **tăng cường độ tin cậy** với hệ thống xác minh email tự động. **Chỉ cần 10 phút setup**, các sếp đã có một hệ thống **tự động hóa hoàn chỉnh** cho quản lý người dùng.

👉 **Hành động ngay!**
1. **Chuẩn bị VPS** và các API Key (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test Run** và **bật Active** để bắt đầu tự động hóa!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với tôi qua [email/twitter] (nếu có). 🚀