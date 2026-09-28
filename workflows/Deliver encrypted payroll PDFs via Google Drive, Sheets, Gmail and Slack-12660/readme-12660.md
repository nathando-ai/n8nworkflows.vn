---
title: "🔒 Tự Động Hóa Phân Phối Bảng Lương Máy Móc - PDF Bị Mã Hóa qua Google Drive, Sheets, Gmail & Slack"
description: "Giải pháp tự động hóa 100% không code để phân phối bảng lương an toàn, mã hóa AES-128 và tự động gửi qua email + Slack. Giảm thiểu rủi ro rò rỉ thông tin và tiết kiệm 10+ giờ công mỗi tháng cho bộ phận HR."
slug: "tieu-dong-hoa-phan-phoi-bang-luong-ma-hoa"
tags: [n8n, automation, payroll, google-drive, gmail, slack, encryption, no-code]
keywords: [tự động hóa bảng lương, phân phối PDF mã hóa, n8n workflow payroll, tự động hóa HR, mã hóa AES-128, Google Sheets + Gmail]
---

# 🚀 **Tự Động Hóa Phân Phối Bảng Lương Máy Móc - An Toàn & Tiết Kiệm Thời Gian**

### **Nỗi Đau Của Các Sếp HR**
Hàng tháng, bộ phận HR phải:
✅ **Tải xuống** hàng trăm bảng lương từ Google Drive.
✅ **Mã hóa thủ công** từng file PDF bằng mật khẩu riêng cho mỗi nhân viên (để bảo mật thông tin cá nhân).
✅ **Gửi email** một cách cá nhân hóa cho từng nhân viên (với nội dung khác nhau cho từng quốc gia/đơn vị).
✅ **Xác minh** rằng tất cả file đã được gửi thành công và **lưu log** cho việc kiểm tra sau.

**Kết quả?** Thời gian mất từ **5-10 giờ/ngày** (tùy theo số lượng nhân viên), dễ xảy ra **lỗi nhân sự** (quên gửi, gửi sai email) và **rủi ro bảo mật** (PDF chưa được mã hóa).

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quá trình**: Từ tải file đến mã hóa và gửi email, **không cần can thiệp thủ công**.
- **Bảo mật cao**: Tất cả file PDF được **mã hóa AES-128** với mật khẩu động (tự động lấy từ Google Sheets).
- **Gửi email cá nhân hóa**: Nội dung email tự động thay đổi theo **quốc gia, đơn vị** của nhân viên.
- **Báo cáo lỗi tự động**: Nếu mã hóa thất bại (do thiếu mật khẩu hoặc lỗi hệ thống), **Slack sẽ cảnh báo ngay** và lưu log cho kiểm tra.
- **Hoạt động 24/7**: Workflow chạy liên tục, **không phụ thuộc vào giờ làm việc** của nhân viên HR.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Google Drive**:
   - **Folder chứa bảng lương chưa mã hóa** (các file PDF mới sẽ được theo dõi tự động).
   - **Thư mục OAuth2** đã cấu hình cho n8n (để truy cập Google Drive).
2. **Google Sheets**:
   - **Bảng dữ liệu nhân viên** với các cột:
     - `Email` (địa chỉ email của nhân viên).
     - `National ID` (mã số nhân viên, dùng làm mật khẩu mã hóa).
     - `Country` (để cá nhân hóa nội dung email).
     - `Department` (đơn vị làm việc).
   - **Thư mục OAuth2** đã cấu hình cho n8n (để truy cập Google Sheets).
3. **Gmail**:
   - **Tài khoản email chính thức của bộ phận HR** (để gửi bảng lương).
   - **OAuth2** đã cấu hình cho n8n.
4. **Slack**:
   - **Channel dành cho cảnh báo lỗi** (ví dụ: `#payroll-alerts`).
   - **OAuth2** đã cấu hình cho n8n.
5. **HTML to PDF Node** (n8n-nodes-htmlcsstopdf):
   - **API Key** từ [HTML to PDF](https://html-to-pdf.net/) (dùng để mã hóa PDF).
   - **Mã hóa AES-128** sẽ được áp dụng tự động.
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/12660](https://n8n.io/workflows/12660) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào n8n Editor (tab `Import`).

:::note[LƯU Ý]
- **Không** cần chỉnh sửa cấu trúc workflow, chỉ cần **điền thông tin credentials** (OAuth2, API Key) như hướng dẫn dưới đây.
- **Không** cần cài đặt node `htmlcsstopdf` nếu đã có sẵn trong phiên bản n8n mới nhất (n8n 1.30+).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **A. Node "Watch Secure Inbox" (Google Drive)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
- **Folder ID**: Nhập **ID của folder chứa bảng lương chưa mã hóa** (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
- **File Types**: Chọn `PDF` (để theo dõi chỉ file PDF mới được upload).

##### **B. Node "Lookup Employee Password" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Sheet Name**: Nhập tên **bảng Google Sheets chứa dữ liệu nhân viên**.
- **Range**: Chọn **tất cả dữ liệu** (ví dụ: `Sheet1!A:D`).
- **Key Parameters**:
  - `lookupKey`: Chọn cột `National ID` (để tìm kiếm nhân viên).
  - `returnKey`: Chọn cột `Email` (để lấy email của nhân viên).

##### **C. Node "Encrypt PDF (AES-128)" (HTML to PDF)**
- **Credentials**: Nhập `htmlcsstopdfApi` (API Key từ [HTML to PDF](https://html-to-pdf.net/)).
- **Key Parameters**:
  - `operation`: Để là `encrypt`.
  - `resource`: Để là `pdfManipulation`.
  - **Mật khẩu động**: Sử dụng **`{{$node["Lookup Employee Password"].json["email"]}}`** (động từ cột `National ID` trong Google Sheets).

##### **D. Node "IF: Encryption Success?"**
- **Condition**: Kiểm tra `json["status"] === "success"` (nếu mã hóa thành công).
- **Nếu thành công**: Chuyển sang node `Deliver Secure Email`.
- **Nếu thất bại**: Chuyển sang node `Alert Admin (Slack)` (cảnh báo lỗi).

##### **E. Node "Deliver Secure Email" (Gmail)**
- **Credentials**: Chọn `gmailOAuth2`.
- **To**: Sử dụng **`{{$node["Lookup Employee Password"].json["email"]}}`** (email động từ Google Sheets).
- **Subject**: Ví dụ: `📄 Bảng lương tháng {{$node["Download PDF Binary"].json["fileName"].split("_")[1]}} - {{$node["Lookup Employee Password"].json["country"]}}`.
- **Body**: Nội dung email cá nhân hóa (ví dụ: `Xin chào {{$node["Lookup Employee Password"].json["name"]}}, đây là bảng lương của bạn...`).

##### **F. Node "Alert Admin (Slack)"**
- **Credentials**: Chọn `slackOAuth2Api`.
- **Channel**: Nhập `#payroll-alerts` (hoặc channel khác).
- **Message**: Nội dung cảnh báo lỗi (ví dụ: `⚠️ Lỗi mã hóa bảng lương cho nhân viên: {{$node["Download PDF Binary"].json["fileName"]}}. Lỗi: {{$node["Encrypt PDF (AES-128)"].json["error"]}}`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 file PDF mẫu**:
   - Upload một file PDF vào folder Google Drive đã chỉ định.
   - Kiểm tra **Slack** và **Gmail** để xác nhận workflow hoạt động.
2. **Bật Active**:
   - Chuyển **switch Active** sang `ON` trong n8n Editor.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Lưu Log Lỗi Chi Tiết**:
   - Thêm node **`n8n-nodes-base.stickyNote`** để lưu **log lỗi** vào Google Sheets (cột `Error Log`).
   - Ví dụ: `{{$node["Encrypt PDF (AES-128)"].json["error"]}}`.

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để gửi **báo cáo tổng hợp** (số lượng file đã gửi, lỗi,...) qua email hàng tuần.

3. **Kết Nối với CRM (Zoho/HubSpot)**:
   - Sau khi gửi bảng lương thành công, **cập nhật trạng thái** trong CRM (ví dụ: `Bảng lương đã gửi`).

4. **Mã Hóa Giữa File**:
   - Nếu cần **mã hóa thêm** (ví dụ: tên file), thêm node **`n8n-nodes-base.code`** để đổi tên file thành `payroll_2024_12_<NationalID>.pdf.enc`.

5. **Bảo Mật API Key**:
   - **Không** chia sẻ `htmlcsstopdfApi` với bất kỳ ai. Sử dụng **environment variables** trong n8n để bảo mật.
:::

---
### **📌 Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề phân phối bảng lương an toàn, tự động hóa và tiết kiệm thời gian cho bộ phận HR. **Không cần code**, chỉ cần **cấu hình OAuth2 và Google Sheets** là có thể áp dụng ngay.

**Hành động ngay**:
1. **Đăng ký VPS** để chạy n8n 24/7 (tránh gián đoạn):
   👉 [VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và **bắt đầu tự động hóa** ngay!

---
**💡 Chia sẻ ý kiến**: Các sếp có thể **cải tiến workflow** thêm các tính năng như gửi SMS (via Twilio) hoặc tích hợp với **ERP** (SAP, Oracle). Hãy **like và chia sẻ** nếu bài viết hữu ích! 🚀