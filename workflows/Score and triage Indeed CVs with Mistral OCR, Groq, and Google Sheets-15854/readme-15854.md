---
title: "🚀 Tự Động Học Viện CV Trên Indeed Với OCR Mistral, Groq & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa đánh giá và phân loại CV từ Indeed với OCR thông minh, mô hình AI Groq (Llama 3.3 70B) và Google Sheets, giúp các sếp tiết kiệm 10+ giờ/tháng trong tuyển dụng, đồng thời đảm bảo độ chính xác cao và cá nhân hóa thông báo cho đội ngũ tuyển dụng."
slug: "tieu-dong-hoa-danh-gia-cv-indeed-ocr-groq-google-sheets"
tags: [n8n, automation, hr, ai-summarization, groq, mistral-ocr, google-sheets, email-automation]
keywords: [tự động hóa tuyển dụng, đánh giá cv bằng ai, groq llama 3.3, ocr mistral, google sheets tuyển dụng, workflow n8n hr]
---

# 🚀 **Tự Động Học Viện CV Trên Indeed: Từ Email Đến Đề Xuất Tuyển Dụng Chỉ Với 1 Clic**

Hiện nay, việc đánh giá hàng trăm CV mỗi ngày là một công việc mệt mỏi và dễ gây sai sót cho các sếp HR. Thay vì phải mở từng email, đọc CV một cách thủ công và phân loại theo tiêu chí chủ quan, **workflow này tự động hóa toàn bộ quy trình từ nhận email ứng tuyển đến đề xuất tuyển dụng với độ chính xác cao nhờ AI**.

Với **OCR Mistral** để quét và extraxt nội dung từ file PDF/DOCX, **mô hình Groq (Llama 3.3 70B)** để phân tích và đánh giá CV theo schema chuẩn, và **Google Sheets** để lưu trữ và theo dõi, bạn sẽ tiết kiệm **10+ giờ/tháng** và giảm thiểu sai sót trong tuyển dụng.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Tự động xử lý hàng trăm CV/ngày mà không cần can thiệp thủ công.
- **Độ chính xác cao**: AI Groq đánh giá CV theo schema chuẩn (16 trường dữ liệu) với kết quả nhất quán.
- **Cá nhân hóa thông báo**: Email tự động gửi cho đội ngũ tuyển dụng với nội dung chi tiết, bao gồm điểm số, đánh giá và liên kết CV.
- **Quản lý trung tâm**: Tất cả dữ liệu ứng viên được lưu trữ trên Google Sheets với khả năng lọc, sắp xếp và phân tích dễ dàng.
- **Tuân thủ GDPR**: CV được tổ chức theo folder riêng trên Google Drive, dễ dàng xóa hoặc bảo mật theo yêu cầu pháp lý.
- **Chi phí thấp**: ~500 VNĐ/1 CV (OCR + AI), phù hợp với ngân sách của các doanh nghiệp vừa và nhỏ.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động ổn định, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
- **Email IMAP (Indeed)**: Một địa chỉ email riêng biệt để nhận email ứng tuyển từ Indeed (ví dụ: `applications@company.com`).
- **Google Drive OAuth2**: Tài khoản Google với quyền truy cập vào một folder cụ thể để lưu trữ CV.
- **Google Sheets OAuth2**: Tài khoản Google với quyền chỉnh sửa một bảng Google Sheets để lưu trữ dữ liệu ứng viên.
- **Mistral AI API**: [Đăng ký API Mistral](https://console.mistral.ai/) (dùng cho OCR).
- **Groq API**: [Đăng ký API Groq](https://console.groq.com/) (mô hình `llama-3.3-70b-versatile`).
- **SMTP (Gửi Email)**: Tài khoản email (Gmail, Outlook, hoặc SMTP riêng) để gửi thông báo tự động.

### **2. Hệ Thống & Hạ Tầng**
- **n8n Self-hosted**: Để workflow chạy 24/7, các sếp nên cài đặt n8n trên **VPS** (không dùng phiên bản cloud).
  :::info[**Gợi ý hạ tầng cho n8n**]
  Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
  :::
- **PostgreSQL + Redis**: Để hỗ trợ chế độ queue và xử lý song song (nếu scale lớn).

### **3. Cấu Hình Email IMAP**
- **Tên miền email**: Sử dụng một địa chỉ email chuyên dụng (ví dụ: `applications@company.com`).
- **Lọc email**: Chỉ lấy email có chủ đề chứa từ khóa `"application"` (Indeed thường dùng định dạng này).
- **Cài đặt polling**: Kiểm tra email mỗi **1 phút** để không bỏ lỡ ứng tuyển.
- **Tải kèm**: Bật `downloadAttachments: true` để tự động tải file CV (PDF/DOCX) từ email.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/15854) hoặc copy JSON từ link trên.
2. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/15854](https://n8n.io/workflows/15854).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON** và dán mã.
3. Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **17 node** và cần cấu hình chi tiết như sau:

#### **🔹 Node "⚙️ Configuration" (Set)**
- **Cấu hình biến môi trường**:
  | Biến | Mô Tả | Ví Dụ |
  |------|--------|-------|
  | `DRIVE_ROOT_FOLDER_ID` | ID folder Google Drive để lưu CV | `1AbCdEfGhIjKlMnOpQrStUvWxYz` |
  | `SHEET_ID` | ID Google Sheets để lưu dữ liệu ứng viên | `1AbCdEfGhIjKlMnOpQrStUvWxYz` |
  | `RECRUITER_EMAIL` | Email của người tuyển dụng nhận thông báo | `recruiter@company.com` |
  | `OPS_EMAIL` | Email của team Ops nhận thông báo lỗi | `ops@company.com` |
  | `SENDER_EMAIL` | Email gửi thông báo (phải khớp với SMTP) | `noreply@company.com` |
  | `SCORE_THRESHOLD` | Ngưỡng điểm để gửi email cho tuyển dụng (mặc định: 75) | `75` |
  | `IMAP_SUBJECT_FILTER` | Từ khóa lọc email từ Indeed | `application` |

- **Lấy ID folder/Sheet**:
  - Mở folder/Sheet trên Google Drive/Sheets → URL sẽ có dạng:
    ```
    https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz
    ```
    → **ID** là phần sau `/folders/` hoặc `/d/` trong URL.

#### **🔹 Node "IMAP Email Trigger (Indeed)" (emailReadImap)**
- **Cấu hình IMAP**:
  - **Host**: `imap.gmail.com` (nếu dùng Gmail) hoặc host của nhà cung cấp email.
  - **Port**: `993` (SSL).
  - **Username/Password**: Tài khoản email ứng tuyển.
  - **Subject Filter**: `subjectContains: application` (để chỉ lấy email từ Indeed).
  - **Download Attachments**: `true` (để tải file CV tự động).

#### **🔹 Node "🧠 Mistral OCR" (httpRequest)**
- **API Key Mistral**: Đăng ký tại [Mistral Console](https://console.mistral.ai/) và điền vào `Authorization: Bearer YOUR_API_KEY`.
- **Endpoint**: `https://api.mistral.ai/v1/models/mistral-ocr-latest/ocr`.
- **Body Request**:
  ```json
  {
    "image": "base64_encoded_pdf",
    "model": "mistral-ocr-latest"
  }
  ```
  - File PDF sẽ được chuyển thành base64 và gửi trong body request.

#### **🔹 Node "Groq Chat Model" (lmChatGroq)**
- **API Key Groq**: Đăng ký tại [Groq Console](https://console.groq.com/) và điền vào `Authorization: Bearer YOUR_API_KEY`.
- **Model**: `llama-3.3-70b-versatile` (mặc định).
- **Prompt**: Workflow đã cấu hình sẵn prompt để phân tích CV theo schema. **Không cần chỉnh sửa** trừ khi cần thay đổi logic đánh giá.

#### **🔹 Node "Append row in sheet" (googleSheets)**
- **Sheet ID**: Điền ID bảng Google Sheets từ biến `SHEET_ID`.
- **Range**: `Sheet1!A1` (hoặc tên sheet cụ thể).
- **Operation**: `append` (thêm hàng mới).

#### **🔹 Node "📁 Upload Drive" (googleDrive)**
- **Folder ID**: Điền `DRIVE_ROOT_FOLDER_ID` từ biến cấu hình.
- **File**: File CV đã được OCR và xử lý.
- **Folder Name**: Tự động tạo folder theo vị trí công việc (ví dụ: `CV_Senior_Backend_Developer`).

#### **🔹 Node "✅ Validate & Build Email" (code)**
- **Lưu ý**: Node này kiểm tra tính hợp lệ của output JSON từ Groq và xây dựng email thông báo.
- **Không cần chỉnh sửa** trừ khi cần thay đổi logic kiểm tra.

#### **🔹 Node "Has Error?" & "Score >= 75?" (if)**
- **Điều kiện**:
  - Nếu `error: true` → gửi email lỗi (`⚠️ Notify Error`).
  - Nếu `score >= 75` → gửi email cho tuyển dụng (`📧 Notify Recruiter`).
  - Nếu `score < 75` → chỉ append vào Google Sheets.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**: Nhấn **Run Workflow** và gửi một email mẫu từ Indeed để kiểm tra.
   - Kiểm tra email IMAP có nhận được file CV không.
   - Kiểm tra Google Drive có lưu file CV không.
   - Kiểm tra Google Sheets có thêm hàng mới không.
   - Kiểm tra email thông báo cho tuyển dụng/ops.
2. **Bật Active**: Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cải Thiện & Tối Ưu Hóa**]
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node `slackSend` hoặc `telegramSend` để gửi thông báo ngay khi có ứng viên mới.
   - Ví dụ: Khi `score >= 75`, gửi tin nhắn Slack với link CV và điểm số.

2. **Lưu Log & Audit**:
   - Thêm node `set` hoặc `code` để lưu log vào Google Sheets hoặc PostgreSQL.
   - Ví dụ: Lưu thời gian xử lý, trạng thái (success/error), và nguyên nhân lỗi.

3. **Gửi Báo Cáo Định Kỳ**:
   - Tạo một workflow mới để gửi báo cáo hàng tuần/tháng cho CEO/HR Manager.
   - Dùng node `googleSheets` để lấy dữ liệu từ bảng và `emailSend` để gửi báo cáo HTML.

4. **Xử Lý CV Bị Lỗi**:
   - Thêm một queue Redis để lưu CV bị lỗi và xử lý lại sau.
   - Sử dụng node `set` để lưu CV bị lỗi vào một folder riêng trên Google Drive.

5. **Tối Ưu Hóa Chi Phí**:
   - Nếu chi phí Groq cao, thử mô hình `gpt-oss-120b` hoặc `mixtral-8x7b` (đổi trong node `Groq Chat Model`).
   - Sử dụng **Mistral Extract from File** (miễn phí) cho CV đơn giản trước khi gửi đến OCR.

6. **Tuân Thủ GDPR**:
   - Thêm một workflow định kỳ để xóa CV đã bị loại sau 6-12 tháng.
   - Sử dụng node `googleDrive` với `operation: delete` và `googleSheets` để xóa hàng trong bảng.

7. **Kết Nối Với ATS**:
   - Nếu dùng Greenhouse/Workable, kết nối với node `httpRequest` để tự động chuyển ứng viên từ n8n sang ATS.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc mệt mỏi là đánh giá CV thủ công, đồng thời **tăng độ chính xác** nhờ AI Groq và OCR Mistral. Với chi phí thấp (~500 VNĐ/1 CV) và khả năng tự động hóa hoàn toàn, đây là **giải pháp lý tưởng** cho các doanh nghiệp muốn tối ưu quy trình tuyển dụng.

**Bắt đầu ngay hôm nay!**
1. Cài đặt n8n trên VPS.
2. Cấu hình email IMAP và API keys.
3. Import workflow và test với email mẫu.
4. Bật workflow và theo dõi kết quả trên Google Sheets.

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với team n8n tại [n8n.io/community](https://n8n.io/community). Chúc các sếp thành công! 🚀