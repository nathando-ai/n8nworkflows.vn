---
title: "📜 Tự Động Hoá Sinh Lập & Kiểm Tra Chứng Nhận Số Hóa (PDF) Cho Khóa Học - N8n"
description: "Workflow tự động hóa hoàn toàn không cần code để sinh tạo, lưu trữ và kiểm tra chứng nhận số hóa (PDF) cho học viên. Giúp tiết kiệm thời gian, giảm thiểu lỗi thủ công và cung cấp chứng nhận cá nhân hóa ngay lập tức."
slug: "tieu-dong-hoa-chung-nhan-so-hoa-pdf"
tags: [n8n, automation, document-generation, pdf, gmail, webhook, no-code]
keywords: [n8n workflow chứng nhận, tự động hóa chứng nhận số hóa, sinh PDF chứng nhận, kiểm tra chứng nhận, n8n document automation]
---

# 🚀 **Tự Động Hoá Sinh Lập & Kiểm Tra Chứng Nhận Số Hóa (PDF) Cho Khóa Học**

### **Giải Pháp Tự Động Hoá 100% Không Code Cho Chứng Nhận Số Hóa**
Bạn đã bao giờ phải mất hàng giờ để thủ công sinh tạo chứng nhận cho học viên, kiểm tra tính hợp lệ của chúng, hoặc gửi PDF qua email? Với **Automated Digital Certificate Creator & Validator**, các sếp có thể **tự động hóa toàn bộ quy trình** từ nhận thông tin học viên đến sinh PDF cá nhân hóa và kiểm tra chứng nhận chỉ bằng một cú nhấp chuột.

Workflow này không chỉ tiết kiệm **thời gian lên đến 90%** mà còn **giảm thiểu lỗi thủ công**, **cung cấp chứng nhận nhanh chóng** và cho phép **kiểm tra hợp lệ chứng nhận một cách dễ dàng** thông qua API.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp sự cố, các sếp nên **self-host n8n** trên một VPS ổn định. N8n chạy tốt nhất trên máy chủ có **RAM 4GB trở lên** và **ổ cứng SSD** để đảm bảo tốc độ sinh PDF và xử lý webhook nhanh chóng.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo ổn định cho workflow)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công nhập liệu hay sinh PDF cho từng học viên.
- **Chứng nhận cá nhân hóa**: Sinh PDF với logo, thông tin học viên và mã chứng nhận duy nhất.
- **Kiểm tra hợp lệ tự động**: API `/certificationscheck` trả về trạng thái chứng nhận (hợp lệ/không hợp lệ) cho frontend.
- **Hoạt động liên tục**: Webhook nhận dữ liệu 24/7, không phụ thuộc vào nhân viên.
- **Giảm thiểu lỗi**: Tránh trùng mã chứng nhận và đảm bảo dữ liệu chính xác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản PDF Generator API** (để sinh PDF từ template HTML).
   - Đăng ký tại: [https://pdfgeneratorapi.com/](https://pdfgeneratorapi.com/)
   - Lưu **API Key** để cấu hình trong node `Generate_PDF`.
2. **Tài khoản Gmail/SMTP** (để gửi email chứng nhận cho học viên).
   - Cấu hình OAuth2 cho Gmail trong **Email_Certification**.
3. **Bảng dữ liệu (Data Table) trong n8n** để lưu trữ thông tin chứng nhận.
   - Tên bảng: **Certifications** (cần các cột: `Name`, `Surname`, `CertificationID`, `Email`, `Course`).
4. **Webhook URLs** (sẽ được tạo tự động khi deploy workflow).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/11097) hoặc sử dụng mã JSON dưới đây:
  ```json
  // (Mã JSON sẽ được cung cấp sau khi hoàn thiện)
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Sinh Chứng Nhận** (`/certifications` POST)
- **Phần 2: Kiểm Tra Chứng Nhận** (`/certificationscheck` POST)

##### **A. Cấu Hình Node `Generate_PDF` (PDF Generator API)**
- **Bước 1**: Tạo **credentials** mới trong n8n:
  - **Node**: `@pdfgeneratorapi/n8n-nodes-pdf-generator-api.pdfGeneratorApi`
  - **Tên credentials**: `pdfGeneratorApi`
  - **API Key**: Nhập key từ tài khoản PDF Generator API.
- **Bước 2**: Cấu hình **HTML Template**:
  - Trong node `Generate_PDF`, chỉnh sửa **`template`** để phù hợp với branding của doanh nghiệp.
  - Ví dụ:
    ```html
    <h1>Chứng Nhận Hoàn Thành Khóa Học</h1>
    <p>Tên: {{Name}}</p>
    <p>Họ: {{Surname}}</p>
    <p>Mã Chứng Nhận: {{CertificationID}}</p>
    <p>Khóa Học: {{Course}}</p>
    ```
- **Bước 3**: Chỉnh `resource` thành `"conversion"` (để chuyển HTML thành PDF).

##### **Bước 3: Cấu Hình Node `Email_Certification` (Gmail)**
- **Bước 1**: Tạo **credentials OAuth2** cho Gmail:
  - **Node**: `gmail`
  - **Tên credentials**: `gmailOAuth2`
  - **Chọn OAuth2** và đăng nhập tài khoản Gmail.
- **Bước 2**: Cấu hình email:
  - **Subject**: `"Chứng Nhận Số Hóa - {{Course}}"`
  - **Body**: Thêm link download PDF hoặc nội dung HTML (nếu muốn gửi trực tiếp).

##### **Bước 4: Cấu Hình Webhook (`/certifications` và `/certificationscheck`)**
- **Node `Webhook_Creation`**:
  - **Path**: `/certifications` (để nhận dữ liệu sinh chứng nhận).
  - **HTTP Method**: `POST`.
  - **Expected Data**:
    ```json
    {
      "name": "Tên Học Viên",
      "surname": "Họ Học Viên",
      "course": "Khóa Học ABC",
      "email": "email@example.com"
    }
    ```
- **Node `Webhook_Check`**:
  - **Path**: `/certificationscheck` (để kiểm tra chứng nhận).
  - **HTTP Method**: `POST`.
  - **Expected Data**:
    ```json
    {
      "certificationId": "ABC123XYZ"
    }
    ```

##### **Bước 5: Cấu Hình Node `Insert_Certification` (Data Table)**
- **Bảng dữ liệu**: Tạo bảng `Certifications` với các cột:
  - `Name` (Tên học viên)
  - `Surname` (Họ học viên)
  - `CertificationID` (Mã duy nhất)
  - `Course` (Khóa học)
  - `Email` (Email liên lạc)
- **Node `Generate_Certification_ID`**:
  - Chỉnh sửa **code JavaScript** để sinh mã duy nhất (nếu cần thay đổi logic).

##### **Bước 6: Kiểm Tra Node `Certification_ID_Exists`**
- Node này **kiểm tra trùng mã** trước khi lưu.
- Nếu mã đã tồn tại, workflow sẽ **lặp lại** cho đến khi tìm được mã mới.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **POST request** đến `/certifications` với dữ liệu mẫu:
    ```bash
    curl -X POST https://tên-domain-n8n.com/certifications \
    -H "Content-Type: application/json" \
    -d '{"name":"Nguyễn Văn A","surname":"B","course":"Marketing Digital","email":"a@example.com"}'
    ```
  - Kiểm tra email của học viên có nhận được PDF không.
- **Kiểm Tra Kiểm Tra Chứng Nhận**:
  - Gửi **POST request** đến `/certificationscheck` với mã chứng nhận:
    ```bash
    curl -X POST https://tên-domain-n8n.com/certificationscheck \
    -H "Content-Type: application/json" \
    -d '{"certificationId":"ABC123XYZ"}'
    ```
  - Nếu chứng nhận hợp lệ, trả về:
    ```json
    {"ok": true, "name": "Nguyễn Văn A", "surname": "B"}
    ```
  - Nếu không hợp lệ:
    ```json
    {"ok": false}
    ```
- **Bật Active Workflow**: Sau khi test thành công, bật **Active** để workflow hoạt động 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Hợp Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi sinh thành công/chứng nhận hợp lệ.
2. **Lưu Log**:
   - Sử dụng node `stickyNote` hoặc `file` để lưu lịch sử sinh chứng nhận.
3. **Báo Cáo Định Kỳ**:
   - Tạo workflow riêng để gửi báo cáo tổng hợp số lượng chứng nhận sinh ra hàng tháng.
4. **Cá Nhân Hóa Thêm**:
   - Thêm trường `Company` hoặc `Date` vào template PDF để tăng tính chuyên nghiệp.
5. **Cấu Hình SMTP**:
   - Nếu không dùng Gmail, cấu hình SMTP khác (ví dụ: SendGrid) trong node `Email_Certification`.

---
### 📌 **Kết Luận**
Workflow **Automated Digital Certificate Creator & Validator** là **giải pháp hoàn hảo** cho các doanh nghiệp cần tự động hóa quy trình chứng nhận số hóa. Với **n8n**, các sếp không chỉ tiết kiệm thời gian mà còn **cung cấp trải nghiệm chuyên nghiệp** cho học viên.

**Hãy áp dụng ngay để:**
✅ **Tự động hóa sinh chứng nhận** chỉ trong vài giây.
✅ **Kiểm tra hợp lệ chứng nhận** thông qua API.
✅ **Gửi PDF qua email tự động** mà không cần can thiệp thủ công.

**Bắt đầu ngay với n8n và nâng cao hiệu suất của doanh nghiệp!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/11097)**
**📌 [Hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**