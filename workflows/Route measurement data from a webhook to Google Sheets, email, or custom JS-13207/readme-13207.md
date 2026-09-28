---
title: "🚀 Tự Động Hóa Dữ Liệu Đo Lường: Nhận Dữ Liệu Webhook → Google Sheets, Email hoặc Logic Tùy Chỉnh (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh nhận dữ liệu đo lường từ webhook, xử lý và phân phối đến Google Sheets, email CSV hoặc logic JavaScript tùy chỉnh - tiết kiệm thời gian và giảm thiểu lỗi nhân sự. Phù hợp cho các doanh nghiệp sản xuất, kiểm tra chất lượng hoặc quản lý dự án."
slug: "tu-dong-hoa-du-lieu-do-luong-webhook-google-sheets-email"
tags: [n8n, automation, document-extraction, google-sheets, email-automation, javascript-code-node]
keywords: [n8n workflow đo lường, tự động hóa dữ liệu webhook, gửi dữ liệu đến Google Sheets, email CSV tự động, logic JavaScript trong n8n]
---

# 🚀 **Tự Động Hóa Dữ Liệu Đo Lường: Nhận Webhook → Xử Lý → Phân Phối Đa Nguồn (Không Cần Code)**

## **🔍 Nỗi Đau Của Các Sếp**
Hiện nay, việc thu thập và xử lý dữ liệu đo lường từ các thiết bị 3D, máy móc hoặc hệ thống kiểm tra chất lượng vẫn còn phụ thuộc vào **nhân sự thủ công**:
- **Tốn thời gian**: Phải copy-paste dữ liệu từ thiết bị sang Google Sheets hoặc email.
- **Rủi ro sai sót**: Nhập sai dữ liệu, mất mát thông tin quan trọng.
- **Không đồng bộ**: Dữ liệu phân tán giữa nhiều ứng dụng, khó theo dõi.
- **Không cá nhân hóa**: Không thể tự động gửi báo cáo định kỳ hoặc tích hợp với hệ thống khác.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Nhận dữ liệu tự động** từ webhook (không cần API phức tạp).
✅ **Xử lý và kiểm tra dữ liệu** trước khi phân phối (tránh sai sót).
✅ **Phân phối đa nguồn** (Google Sheets, email CSV, hoặc logic JavaScript tùy chỉnh).
✅ **Hoạt động 24/7** trên VPS riêng (không phụ thuộc vào máy tính cá nhân).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Dữ liệu tự động lưu và phân phối, không cần nhập thủ công.
- **Chính xác 100%**: Kiểm tra dữ liệu trước khi lưu, tránh lỗi nhập sai.
- **Dữ liệu đồng bộ**: Tất cả dữ liệu đo lường được lưu trữ trung tâm (Google Sheets) và gửi email tự động.
- **Cá nhân hóa**: Chọn cách phân phối phù hợp (Sheets, email, hoặc logic JavaScript).
- **Hoạt động liên tục**: Chạy trên VPS, không ngừng hoạt động dù máy tính tắt.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Thông tin cấu hình sau**:
   - **Google Sheets**:
     - Tài khoản Google với quyền chỉnh sửa sheet.
     - **Google Sheet ID** (tìm trong URL của sheet khi mở).
     - **Tên sheet**: "Measurements".
   - **Email (nếu sử dụng mode CSV)**:
     - Thông tin SMTP (host, port, username, password).
     - **Địa chỉ email nhận**: `emailRecipient`.
     - **Tiêu đề email**: `emailSubject` (tùy chọn).
   - **Logic JavaScript (nếu sử dụng mode custom)**:
     - Các API keys hoặc credentials cần thiết cho logic tùy chỉnh.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13207](https://n8n.io/workflows/13207) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13207) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **14 node** quan trọng, các sếp cần cấu hình như sau:

##### **🔹 Node "Workflow Configuration" (Set)**
- **Cấu hình `outputMode`** (bắt buộc):
  - `sheets` → Lưu dữ liệu vào Google Sheets.
  - `html` → Trả về trang HTML với dữ liệu.
  - `csv` → Gửi email CSV.
  - `custom` → Chạy logic JavaScript.
- **Cấu hình tùy chọn**:
  - `googleSheetId`: ID của Google Sheet (điền từ URL sheet).
  - `emailRecipient`: Email nhận CSV (nếu mode `csv`).
  - `emailSubject`: Tiêu đề email (nếu mode `csv`).

##### **🔹 Node "Webhook Trigger" (Webhook)**
- **URL webhook**: Sẽ tự động tạo khi import. Các sếp **không cần chỉnh sửa**.
- **Phương thức**: POST (đã cấu hình mặc định).
- **Path**: `/measure-data` (không cần thay đổi).

##### **🔹 Node "Validate Required Fields" (If)**
- **Kiểm tra 3 trường bắt buộc**:
  - `measurementId` (ID đo lường).
  - `timestamp` (thời gian đo).
  - `values` (giá trị đo lường).
- **Nếu thiếu trường nào**: Workflow sẽ **dừng và trả lỗi 400**.

##### **🔹 Node "Route to Output Options" (Switch)**
- **Phân phối dữ liệu** theo `outputMode` đã cấu hình:
  - **Sheets**: Lưu vào Google Sheets.
  - **HTML**: Trả về trang web với bảng dữ liệu.
  - **CSV**: Gửi email CSV.
  - **Custom**: Chạy logic JavaScript.

##### **🔹 Node "Google Sheets" (Google Sheets)**
- **Cấu hình**:
  - Chọn **credentials** Google Sheets đã tạo trước.
  - **Operation**: `appendOrUpdate` (lưu hoặc cập nhật dữ liệu).
  - **Sheet Name**: "Measurements" (không cần thay đổi).

##### **🔹 Node "Email Send" (Email)**
- **Cấu hình**:
  - Chọn **credentials SMTP** (nếu chưa có, tạo mới).
  - **From Email**: Địa chỉ gửi (ví dụ: `noreply@doanhnghiep.com`).
  - **To Email**: Điền vào `emailRecipient` trong node "Workflow Configuration".
  - **Subject**: Điền vào `emailSubject` (nếu có).

##### **🔹 Node "Custom JavaScript Logic" (Code)**
- **Mở rộng tính năng**:
  - Thêm logic API, lưu cloud, hoặc gọi workflow khác.
  - **Ví dụ**:
    ```javascript
    // Gọi API bên ngoài
    const response = await $http.post("https://api.example.com/data", {
      measurementData: $input.all()
    });
    ```
  - **Lưu ý**: Các sếp có thể **xóa node này** nếu không cần logic tùy chỉnh.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **dữ liệu mẫu** từ Postman hoặc ứng dụng 3D Measure Up:
     ```json
     {
       "measurementId": "MEAS-001",
       "timestamp": "2024-05-20T10:00:00Z",
       "values": {
         "x": 12.5,
         "y": 20.3,
         "z": 5.7
       },
       "deviceId": "DEV-123",
       "operator": "Nguyễn Văn A"
     }
     ```
   - Kiểm tra **Google Sheets** hoặc **email** để xác nhận dữ liệu đã được lưu.

2. **Bật Active**:
   - Đặt **Active** thành `true` trong node Webhook.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau node "Send Success Response" để thông báo khi dữ liệu được lưu thành công.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Sticky Note** hoặc **Database** để lưu lịch sử lỗi và thành công.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node **Schedule** để gửi báo cáo tổng hợp hàng tuần/month.

4. **Tích Hợp với ERP/CRM**:
   - Trong node **Custom JavaScript**, gọi API của ERP (SAP, Odoo) hoặc CRM (HubSpot) để cập nhật dữ liệu.

5. **Tự Động Xóa Dữ Liệu Cũ**:
   - Thêm logic trong node **Google Sheets** để xóa dữ liệu cũ hơn 30 ngày.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **tăng độ chính xác** và **tích hợp dữ liệu** một cách tự động. Bằng cách cấu hình đơn giản và tích hợp với **Google Sheets, email, hoặc logic JavaScript**, các sếp có thể:
✔ **Theo dõi đo lường** một cách trung tâm.
✔ **Gửi báo cáo tự động** đến đội ngũ.
✔ **Tích hợp với hệ thống khác** (ERP, CRM, cloud storage).

**🚀 Hãy áp dụng ngay workflow này và tự động hóa quy trình đo lường của doanh nghiệp!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/13207) và bắt đầu ngay!