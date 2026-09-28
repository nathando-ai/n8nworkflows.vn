---
title: "🚀 Tự Động Hóa Xác Minh & Tạo Thẻ Press Pass Với QR Code - Phân Phối Multi-Channel (n8n)"
description: "Workflow tự động hóa hoàn toàn không cần code để xác minh nhà báo, tạo thẻ press pass chuyên nghiệp với QR code, gửi email xác nhận và thông báo Slack - tiết kiệm thời gian lên đến 90% so với thủ công."
slug: "tieu-dong-hoa-xac-minh-tao-the-press-pass-qr-code"
tags: [n8n, automation, no-code, press-pass, email-verification, qr-code, google-sheets, slack, gmail]
keywords: [tự động hóa press pass, tạo thẻ press pass tự động, xác minh nhà báo, qr code cho sự kiện, n8n workflow, tự động hóa sự kiện, email xác nhận press pass, slack notification]
---

# 🚀 **Tự Động Hóa Xác Minh & Tạo Thẻ Press Pass Với QR Code - Phân Phối Multi-Channel**

### **Giải pháp cho các sếp tổ chức sự kiện**
Bạn đã bao giờ phải mất **giờ đồng hồ** để thủ công:
- Xác minh thông tin nhà báo?
- Tạo thẻ press pass với logo sự kiện?
- Gửi email xác nhận và thông báo cho ban tổ chức?
- Theo dõi danh sách nhà báo đã được cấp thẻ?

Workflow này **tự động hóa toàn bộ quy trình** trong **vài giây**, giúp bạn:
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Giảm sai sót** với xác minh email và domain chuyên nghiệp.
✅ **Cung cấp trải nghiệm chuyên nghiệp** cho nhà báo với thẻ press pass có QR code và branding sự kiện.
✅ **Theo dõi toàn bộ quá trình** trên Google Sheets và Slack.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **giờ đồng hồ** xuống **vài giây** cho mỗi nhà báo.
- **Xác minh chính xác**: Sử dụng **VerifiEmail API** để kiểm tra email và domain của nhà báo.
- **Thẻ press pass chuyên nghiệp**: Tạo thẻ với **logo sự kiện, QR code, và hình ảnh nhà báo** tự động.
- **Phân phối đa kênh**: Gửi email xác nhận, thông báo Slack và lưu log trên Google Sheets.
- **Theo dõi toàn diện**: Danh sách nhà báo được cập nhật tự động, dễ dàng kiểm tra và báo cáo.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản API & Credentials**:
   - **VerifiEmail API** (để xác minh email và domain).
   - **HTML/CSS to Image API** (để tạo thẻ press pass từ mã HTML/CSS).
   - **Gmail OAuth 2.0** (để gửi email xác nhận).
   - **Slack API** (để thông báo ban tổ chức).
   - **Google Sheets API** (để lưu log và theo dõi).

2. **Google Sheets**:
   - Tạo một bảng mới với **cột tiêu đề** sau:
     ```
     Timestamp | Press ID | Name | Email | Phone | Media Outlet | Verification Status | Event Name | Issued Date | Valid Until | Badge Image URL | QR Code URL | Verification URL | Photo URL | Webhook Execution Mode
     ```

3. **URL Webhook**:
   - Sau khi import workflow, **copy URL Webhook** từ node `Webhook Trigger` để embed vào form đăng ký của sự kiện.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10793](https://n8n.io/workflows/10793) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (trong tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Webhook Trigger**
- **Path**: `press-application` (không thay đổi).
- **HTTP Method**: `POST`.
- **Test Webhook**: Sau khi import, **test với một request mẫu** (ví dụ bằng Postman) để đảm bảo nhận được dữ liệu.

##### **B. Validate Required Fields (Node `If`)**
- **Cấu hình điều kiện**:
  - Kiểm tra **Name**, **Email**, và **Photo URL** phải **không rỗng**.
  - Nếu thiếu, workflow sẽ **dừng và báo lỗi** (`Stop: Incomplete Data`).

##### **C. Check Domain Verified (Node `If`)**
- **Sử dụng VerifiEmail API** để xác minh domain email.
- **Nếu domain không hợp lệ**, workflow sẽ **dừng và báo lỗi** (`Stop: Domain Not Verified`).

##### **D. Generate Press ID & QR (Node `Code`)**
- **Cấu hình mã JavaScript** để:
  - Tạo **Press ID** duy nhất (ví dụ: `PRESS-2024-001`).
  - Tạo **QR code** liên kết đến thông tin nhà báo.
  - Chuẩn bị dữ liệu cho **HTML/CSS to Image**.

##### **E. HTML/CSS to Image (Node `htmlCsstoImage`)**
- **Cấu hình**:
  - **HTML Template**: Sử dụng mã HTML/CSS để tạo thẻ press pass với:
    - Logo sự kiện.
    - Hình ảnh nhà báo.
    - Press ID và QR code.
    - Thông tin sự kiện (tên, ngày, địa điểm).
  - **Mẫu tham khảo**:
    ```html
    <div style="width: 200px; height: 120px; background: #2c3e50; padding: 10px; border-radius: 5px;">
      <img src="{{photo_url}}" style="width: 60px; height: 60px; border-radius: 50%;">
      <h3 style="color: white; margin: 5px 0;">PRESS PASS</h3>
      <p style="color: white; font-size: 12px;">{{name}}</p>
      <p style="color: white; font-size: 10px;">{{media_outlet}}</p>
      <img src="{{qr_code_url}}" style="width: 50px; height: 50px; margin-top: 10px;">
    </div>
    ```

##### **F. Send Press Pass Email (Node `Gmail`)**
- **Cấu hình**:
  - **Chủ đề email**: `📢 Xác nhận thẻ Press Pass cho sự kiện [Tên Sự Kiện]`.
  - **Nội dung email**: Gồm:
    - Thông tin nhà báo.
    - Thẻ press pass (đính kèm dưới dạng ảnh).
    - QR code để quét và xác minh.
    - Link xác minh email (nếu cần).

##### **G. Notify Organizers (Slack) (Node `Slack`)**
- **Cấu hình**:
  - **Channel**: Chọn kênh Slack để thông báo.
  - **Message Template**:
    ```json
    {
      "text": ":tada: Nhà báo mới được cấp thẻ press pass!",
      "attachments": [
        {
          "title": "{{name}}",
          "title_link": "https://example.com/press-pass/{{press_id}}",
          "text": `Email: {{email}} | Media: {{media_outlet}}`,
          "fields": [
            { "title": "Press ID", "value": "{{press_id}}", "short": true },
            { "title": "QR Code", "value": "<{{qr_code_url}}|Quét QR>", "short": false }
          ]
        }
      ]
    }
    ```

##### **H. Log to Google Sheets (Node `Google Sheets`)**
- **Cấu hình**:
  - **Sheet Name**: Chọn bảng Google Sheets đã tạo trước đó.
  - **Operation**: `append` (thêm dữ liệu mới vào cuối bảng).
  - **Mappings**:
    - `Timestamp`: `{{$node["Webhook Trigger"].json["timestamp"]}}`
    - `Press ID`: `{{$node["Generate Press ID & QR"].json["press_id"]}}`
    - `Name`, `Email`, `Media Outlet`, `Badge Image URL`, `QR Code URL`, ... (đối ứng với dữ liệu từ các node trước).

##### **I. Verifi Email (Node `verifiEmail`)**
- **Cấu hình**:
  - **API Key**: Điền vào `verifiEmailApi` (đã setup trước).
  - **Email Address**: `{{$node["Webhook Trigger"].json["email"]}}`
  - **Domain Check**: Bật tùy chọn `checkDomain`.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một **request mẫu** đến Webhook (ví dụ bằng Postman):
    ```json
    {
      "name": "Nguyễn Văn A",
      "email": "a.nguyen@mediaoutlet.com",
      "photo_url": "https://example.com/photo.jpg",
      "media_outlet": "Vietnam Media Group",
      "event_name": "Tech Summit 2024"
    }
    ```
  - Kiểm tra:
    - Email xác nhận được gửi.
    - Thông báo Slack xuất hiện.
    - Dữ liệu được lưu vào Google Sheets.

- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **đặt URL Webhook** vào form đăng ký của sự kiện.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa xác minh email**:
   - Sử dụng **VerifiEmail API** để gửi **link xác minh** cho nhà báo qua email (nếu cần).

2. **Phân loại nhà báo**:
   - Thêm **cột "Role"** vào Google Sheets (ví dụ: "Photographer", "Reporter") và hiển thị trên thẻ press pass.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo **báo cáo tổng hợp** về số lượng nhà báo đã được cấp thẻ.

4. **Tích hợp với CRM**:
   - Nếu sử dụng **HubSpot, Zoho CRM**, bạn có thể **tự động thêm nhà báo** vào danh sách CRM sau khi xác minh thành công.

5. **Branding sự kiện**:
   - Thay đổi **màu sắc và logo** trong node `HTML/CSS to Image` để phù hợp với chủ đề sự kiện.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp tổ chức sự kiện, đồng thời **cung cấp trải nghiệm chuyên nghiệp** cho nhà báo. Với **tự động hóa 100% không cần code**, bạn có thể:
✔ **Tiết kiệm hàng giờ** mỗi ngày.
✔ **Giảm sai sót** với xác minh email và domain.
✔ **Tăng chuyên nghiệp** với thẻ press pass có QR code và branding.

**Hãy áp dụng ngay và bắt đầu tự động hóa sự kiện của bạn!** 🚀

---
:::note[Lưu ý cuối cùng]
- **Backup dữ liệu**: Đảm bảo **backup Google Sheets** định kỳ.
- **Monitoring**: Sử dụng **n8n Dashboard** để theo dõi status của workflow.
- **Cập nhật API Key**: Nếu API Key hết hạn, **cập nhật ngay** để workflow không bị ngắt.
:::