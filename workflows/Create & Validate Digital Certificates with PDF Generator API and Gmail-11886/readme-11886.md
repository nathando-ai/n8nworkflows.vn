---
title: "📜 Tự Động Hóa Sinh Thành & Kiểm Tra Chứng Nhận Số Hóa (PDF) Với n8n - Giải Pháp Không Code Cho Doanh Nghiệp"
description: "Workflow này tự động tạo chứng nhận số hóa (PDF) từ thông tin học viên, kiểm tra tính hợp lệ và gửi email tự động - tiết kiệm 90% thời gian thủ công. Phù hợp cho các trung tâm đào tạo, trường học, hoặc doanh nghiệp cần chứng nhận điện tử."
slug: "tu-dong-hoa-chung-nhan-so-hoa-voi-n8n"
tags: [n8n, automation, no-code, chứng nhận số hóa, PDF API, Gmail API, webhook, data-table]
keywords: [n8n workflow chứng nhận, tự động hóa chứng nhận số hóa, PDF generator API, kiểm tra chứng nhận điện tử, tự động hóa đào tạo]
---

# 🚀 **Tự Động Hóa Sinh Thành & Kiểm Tra Chứng Nhận Số Hóa (PDF) Với n8n**

### **Giải Pháp Không Code Cho Doanh Nghiệp Đào Tạo**
Hiện nay, việc tạo và quản lý chứng nhận số hóa (PDF) cho học viên thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp phải:
- **Ghi chép thủ công** thông tin học viên vào bảng Excel.
- **Tạo PDF** bằng Canva/Word và gửi email một một.
- **Kiểm tra chứng nhận** bằng cách tra cứu trong danh sách.
- **Lo lắng về tính hợp lệ** của chứng nhận sau khi phát hành.

**Workflow này tự động hóa toàn bộ quy trình** từ nhận thông tin học viên đến tạo PDF, gửi email và kiểm tra hợp lệ - **giúp tiết kiệm 90% thời gian thủ công** và giảm thiểu lỗi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo và gửi chứng nhận trong giây lát.
- **Chứng nhận duy nhất**: Hệ thống tự động sinh ID chứng nhận không trùng lặp.
- **Kiểm tra nhanh chóng**: API trả về kết quả hợp lệ/không hợp lệ cho chứng nhận.
- **Gửi email tự động**: Chứng nhận PDF được gửi ngay sau khi tạo.
- **Bảo mật cao**: Tất cả dữ liệu lưu trữ trong Data Table riêng của n8n.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để gửi email chứng nhận).
2. **Tài khoản PDF Generator API** ([pdfgeneratorapi.com](https://pdfgeneratorapi.com/)) để tạo PDF từ template HTML.
3. **Bảng Data Table** trong n8n với các cột:
   - `Name` (Tên học viên)
   - `Surname` (Họ học viên)
   - `CertificationID` (ID chứng nhận tự động sinh)
   - `Course` (Khóa học)
   - `Email` (Email học viên)
4. **API Key** của PDF Generator và OAuth2 cho Gmail.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11886) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor.
  2. Nhấn **Import** → **Paste JSON** và dán nội dung từ file.
  3. Chọn **Import** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **2 phần chính**:
- **Phần 1: Tạo chứng nhận** (`/certifications`).
- **Phần 2: Kiểm tra chứng nhận** (`/certificationscheck`).

##### **A. Cấu hình Data Table**
- **Tên bảng**: `Certifications` (hoặc tên tùy chỉnh).
- **Cột bắt buộc**:
  - `Name` (Text)
  - `Surname` (Text)
  - `CertificationID` (Text)
  - `Course` (Text)
  - `Email` (Text)

##### **B. Cấu hình Webhook**
- **Webhook Creation** (`/certifications`):
  - **HTTP Method**: `POST`.
  - **Payload Example**:
    ```json
    {
      "name": "Nguyễn Văn A",
      "surname": "B",
      "course": "Khóa Học SEO",
      "email": "a@example.com"
    }
    ```
- **Webhook Check** (`/certificationscheck`):
  - **HTTP Method**: `POST`.
  - **Payload Example**:
    ```json
    {
      "certificationId": "ABC123"
    }
    ```

##### **C. Cấu hình PDF Generator API**
- **Node**: `Generate a PDF document`.
- **Tham số cần thiết**:
  - **API Key**: Điền từ tài khoản PDF Generator.
  - **Template HTML**: Sử dụng template mẫu hoặc tự viết (ví dụ dưới đây):
    ```html
    <h1>Chứng Nhận Thành Công</h1>
    <p>Chúng tôi xin chứng nhận rằng:</p>
    <h2>{{name}} {{surname}}</h2>
    <p>Đã hoàn thành khóa học: <strong>{{course}}</strong></p>
    <p>Ngày: {{date}}</p>
    <p>ID Chứng Nhận: <strong>{{certificationId}}</strong></p>
    ```
  - **Variables**:
    - `{{name}}`, `{{surname}}`, `{{course}}`, `{{certificationId}}`, `{{date}}` (sử dụng node **Code** để sinh ngày hiện tại).

##### **D. Cấu hình Gmail**
- **Node**: `Email_Certification`.
- **Credentials**: Chọn `gmailOAuth2` (cần cấu hình OAuth2 trong n8n).
- **Tham số email**:
  - **Subject**: `Chứng nhận thành công - {{course}}`.
  - **Body**: Nội dung email bao gồm link download PDF và thông tin chứng nhận.

##### **E. Cấu hình Node Code (Generate Certification ID)**
- **Node**: `Generate_Certification_ID`.
- **Mã JavaScript**:
  ```javascript
  // Sinh ID chứng nhận ngẫu nhiên (ví dụ: ABC123)
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
  let id = '';
  for (let i = 0; i < 6; i++) {
    id += chars.charAt(Math.floor(Math.random() * chars.length));
  }
  return { json: { CertificationID: id } };
  ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi request POST đến `/certifications` với dữ liệu mẫu:
     ```bash
     curl -X POST https://your-n8n-url/certifications \
     -H "Content-Type: application/json" \
     -d '{"name":"Nguyễn Văn A","surname":"B","course":"SEO","email":"a@example.com"}'
     ```
   - Kiểm tra email của học viên đã nhận chứng nhận PDF chưa.
   - Gửi request POST đến `/certificationscheck` với `certificationId` để kiểm tra:
     ```bash
     curl -X POST https://your-n8n-url/certificationscheck \
     -H "Content-Type: application/json" \
     -d '{"certificationId":"ABC123"}'
     ```
     - **Trả về `ok: true`** nếu chứng nhận hợp lệ.
     - **Trả về `ok: false`** nếu không tìm thấy.

2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi chứng nhận được tạo thành công.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** để ghi lại lịch sử hoạt động của workflow.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule** để gửi báo cáo tổng hợp số lượng chứng nhận tạo ra hàng tháng.

4. **Tùy chỉnh template PDF**:
   - Thêm logo doanh nghiệp vào template HTML để tăng tính chuyên nghiệp.

5. **Bảo mật thêm**:
   - Sử dụng **JWT** để xác thực API trước khi gọi webhook.

---

### 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc thủ công tạo và quản lý chứng nhận. Với **n8n**, doanh nghiệp có thể:
✅ **Tự động hóa 100%** quy trình chứng nhận.
✅ **Kiểm tra hợp lệ chứng nhận** một cách nhanh chóng.
✅ **Gửi email tự động** trong giây lát.
✅ **Bảo mật dữ liệu** với Data Table riêng.

**Hãy áp dụng ngay workflow này cho doanh nghiệp của các sếp!** Nếu có bất kỳ câu hỏi, hãy để lại comment dưới đây. 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/11886)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**