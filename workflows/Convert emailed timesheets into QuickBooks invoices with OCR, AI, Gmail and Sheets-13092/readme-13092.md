---
title: "🚀 Tự Động Hóa Chuyển Đổi Bảng Thời Gian Làm Việc (Timesheet) Sang Hoá Đơn QuickBooks Với OCR, AI & Gmail – Không Cần Code!"
description: "Workflow này tự động chuyển đổi các email bảng thời gian làm việc (PDF/ảnh) thành hóa đơn QuickBooks chính xác, tiết kiệm 10+ giờ/tháng cho bộ phận kế toán. Sử dụng OCR, AI (OpenAI/Gemini) và Google Sheets để xử lý dữ liệu, tránh sai sót thủ công và đồng bộ hóa đơn 24/7."
slug: "tieu-dong-hoa-chuyen-doi-timesheet-sang-hoa-don-quickbooks"
tags: [n8n, automation, no-code, quickbooks, google-sheets, ai-summarization, ocr, gmail-trigger]
keywords: [n8n workflow timesheet, tự động hóa hóa đơn QuickBooks, OCR chuyển đổi PDF thành text, AI phân tích bảng thời gian, tự động hóa kế toán, Google Sheets + QuickBooks]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Bảng Thời Gian Làm Việc (Timesheet) Sang Hoá Đơn QuickBooks – Không Cần Code!**

### **Giải pháp cho bộ phận kế toán: Từ email PDF/ảnh → Hóa đơn QuickBooks chính xác chỉ trong vài giây!**
Hàng ngày, bộ phận kế toán của các sếp phải mất **tối thiểu 10-15 giờ** để:
- **Quét** các email bảng thời gian làm việc (timesheet) từ nhân viên (được gửi dưới dạng PDF, ảnh, hoặc Excel).
- **Nhập liệu thủ công** vào QuickBooks, dễ dẫn đến **sai sót, mất thời gian và rủi ro vi phạm thuế**.
- **Quản lý tệp** trên Google Drive: Tìm kiếm, tạo thư mục theo khách hàng/nhân viên/năm/month, và đảm bảo không trùng lặp.

**Workflow này giải quyết tất cả!** Sử dụng **OCR (chuyển đổi PDF/ảnh thành text)**, **AI (OpenAI/Gemini)** để phân tích dữ liệu, và **Google Sheets** để chuẩn hóa trước khi đồng bộ hóa đơn lên QuickBooks. **Kết quả:**
✅ **Tiết kiệm 80% thời gian** so với nhập liệu thủ công.
✅ **Tránh sai sót** nhờ AI và kiểm tra trùng lặp tự động.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
✅ **Dữ liệu sạch** với cấu trúc thư mục Google Drive logic.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn** quá trình chuyển đổi timesheet → hóa đơn QuickBooks.
- **AI phân tích chính xác** thông tin từ PDF/ảnh (tên nhân viên, khách hàng, giờ làm, ngày bắt đầu/kết thúc tuần).
- **Kiểm tra trùng lặp** trước khi tạo hóa đơn, tránh double billing.
- **Cấu trúc thư mục Google Drive** tự động: `01-ClientInvoices/ClientName/EmployeeName/Năm/Tháng`.
- **Đồng bộ hóa đơn lên QuickBooks** một cách chính xác, bao gồm thông tin khách hàng, số PO, và ngày hạn thanh toán.
- **Báo cáo tự động** trên Google Sheets, dễ dàng theo dõi và xuất báo cáo.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
| Dịch vụ               | API Key / Credentials          | Ghi chú                                                                 |
|-----------------------|--------------------------------|-------------------------------------------------------------------------|
| **QuickBooks**        | OAuth 2.0 API Key              | [Cài đặt QuickBooks API](https://developer.intuit.com/app/developer/qbo/docs/start) |
| **Google Sheets**     | OAuth 2.0 API Key              | [Cài đặt Google Sheets API](https://developers.google.com/sheets/api/quickstart/python) |
| **Google Drive**      | OAuth 2.0 API Key              | [Cài đặt Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Gmail**            | OAuth 2.0 API Key              | [Cài đặt Gmail API](https://developers.google.com/gmail/api/quickstart/python) |
| **OpenAI (GPT-4)**   | API Key                        | [Mua API Key OpenAI](https://platform.openai.com/account/api-keys)       |
| **Google Gemini**     | API Key (Google Palm API)      | [Cài đặt Google Vertex AI](https://cloud.google.com/vertex-ai/docs/generative-ai/make-requests) |

### **2. Cấu trúc dữ liệu cần chuẩn bị**
- **Google Sheet "Customer POs"** (mẫu trong workflow):
  - Cột: `Customer Name`, `PO Number`, `Account Number`, `Item Name`, `Invoice Range`, `Due Date Offset`.
- **Google Drive**:
  - Thư mục gốc: `01-ClientInvoices` (sẽ tự động tạo các thư mục con theo khách hàng/nhân viên/năm/tháng).
- **Email Gmail**:
  - Các email timesheet được gửi đến **địa chỉ email đã cấu hình trong Gmail Trigger**.

### **3. Hệ thống n8n**
- **Self-hosted n8n** (khuyến nghị) để workflow hoạt động 24/7.
- **N8n Community Edition** (miễn phí) hoặc **n8n Enterprise** (nếu cần tính năng nâng cao).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13092](https://n8n.io/workflows/13092) (chọn "Export as JSON").
2. **Mở n8n Editor** (trên trang web hoặc self-hosted).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** → **Nhấn "Import"** → **Chọn "Paste JSON"** và dán nội dung file vào.
3. **Xác nhận import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với **45 nodes**, nhưng chỉ cần chú ý đến các phần sau:

#### **A. Cấu hình Credentials (API Keys)**
| Node                     | Credentials cần thiết               | Hướng dẫn cấu hình                                                                 |
|--------------------------|--------------------------------------|------------------------------------------------------------------------------------|
| **QuickBooks**           | `quickBooksOAuth2Api`                | Cài đặt OAuth 2.0 từ QuickBooks Developer Portal.                                  |
| **Google Sheets**        | `googleSheetsOAuth2Api`             | [Cài đặt OAuth 2.0 Google Sheets](https://developers.google.com/sheets/api/quickstart/python). |
| **Google Drive**         | `googleDriveOAuth2Api`              | [Cài đặt OAuth 2.0 Google Drive](https://developers.google.com/drive/api/v3/quickstart/python). |
| **Gmail**                | `gmailOAuth2`                        | [Cài đặt OAuth 2.0 Gmail](https://developers.google.com/gmail/api/quickstart/python). |
| **OpenAI (GPT-4)**       | Không cần credentials riêng (n8n nodes LangChain sẽ tự động lấy từ biến môi trường). | Thiết lập biến môi trường `OPENAI_API_KEY` trong n8n. |
| **Google Gemini**        | `googlePalmApi`                     | Thiết lập API Key từ [Google Cloud Console](https://console.cloud.google.com/).     |

#### **B. Cấu hình Google Sheet Master**
1. **Tạo Google Sheet "Customer POs"** với cấu trúc:
   | Customer Name | PO Number | Account Number | Item Name | Invoice Range | Due Date Offset |
   |---------------|-----------|----------------|-----------|---------------|-----------------|
   | ABC Corp      | PO-2024-01| 123456         | Service   | 1-31/01/2024  | 14 days         |
2. **Chia sẻ sheet với tài khoản n8n** (quyền "Sửa").
3. **Điền ID Sheet** vào node **"Set: Spreadsheet (ID & Name)"** (tìm ID trong URL của sheet).

#### **C. Cấu hình Gmail Trigger**
1. **Tạo filter Gmail**:
   - **Nhận từ**: Email của nhân viên gửi timesheet.
   - **Tiêu đề**: Có từ khóa như "Timesheet", "Report", "Weekly".
2. **Cấu hình node "Gmail Trigger"**:
   - Chọn **credentials `gmailOAuth2`**.
   - Thiết lập **filter** (ví dụ: `from:nhanvien@doanhnghiep.com AND subject:"Timesheet"`).

#### **D. Cấu hình OCR API**
Workflow sử dụng **HTTP Request** để gửi file đến OCR API. Nếu không muốn sử dụng API OCR mặc định, các sếp có thể:
- **Thay thế node "Extract Text"** bằng API OCR khác (ví dụ: Tesseract, AWS Textract).
- **Cập nhật URL API** trong node `httpRequest` (mặc định là `https://api.ocr.space/parse/image`).

#### **E. Cấu hình QuickBooks**
1. **Tạo OAuth 2.0 App** trong [QuickBooks Developer Portal](https://developer.intuit.com/app/developer/qbo/docs/develop/apps/create-an-app).
2. **Cấu hình node "QuickBooks Find Customer"**:
   - Chọn `quickBooksOAuth2Api`.
   - Kiểm tra **operation = "getAll"** để lấy danh sách khách hàng.
3. **Kiểm tra node "QuickBooks Create Invoice"**:
   - Đảm bảo **resource = "invoice"** và các trường bắt buộc (`CustomerRef`, `Line`, `DueDate`) được định nghĩa.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Gửi **email mẫu** (có file timesheet PDF/ảnh) đến địa chỉ email đã cấu hình.
   - **Chạy workflow** và kiểm tra:
     - Dữ liệu được OCR thành text.
     - AI (Gemini/OpenAI) phân tích chính xác.
     - Hóa đơn được tạo trên QuickBooks.
     - Thư mục Google Drive được tạo/cập nhật.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **đặt chế độ "Active"**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa AI Parsing**
- **Cập nhật Prompt** trong node `OpenAI Chat Model1` và `Google Gemini Chat Model` để phù hợp với định dạng timesheet của doanh nghiệp.
- **Ví dụ Prompt cho OpenAI**:
  ```json
  "You are an expert timesheet parser. Extract the following fields from the text:
  - Employee Name: [Name]
  - Client Name: [Client]
  - Week Start Date: [DD/MM/YYYY]
  - Week End Date: [DD/MM/YYYY]
  - Total Hours: [X.XX]
  - PO Number: [PO-XXXX]
  Return the data in JSON format."
  ```

### **2. Tự động tạo báo cáo hàng tháng**
- **Thêm node "Google Sheets: Append Row1"** để ghi lịch sử vào sheet báo cáo.
- **Cấu hình cron job** (n8n Enterprise) để chạy workflow hàng tháng và gửi báo cáo qua email.

### **3. Kết hợp với Slack/Telegram**
- **Thêm node "Slack Webhook"** để thông báo khi workflow hoàn thành.
- **Cấu hình alert** cho các trường hợp lỗi (ví dụ: OCR thất bại, QuickBooks reject).

### **4. Lưu log và theo dõi lỗi**
- **Thêm node "Set"** để lưu `json` của workflow vào Google Sheets với cột `Status`, `Error`, `Timestamp`.
- **Sử dụng n8n Dashboard** để theo dõi hoạt động của workflow.

### **5. Xử lý timesheet nhiều trang**
- **Cập nhật node "Split Binary Attachments"** để xử lý file PDF có nhiều trang.
- **Thêm logic split** trong node `code` để xử lý từng trang riêng biệt.

---
## 📌 **Kết luận**
Workflow này **giải phóng bộ phận kế toán** khỏi công việc nhập liệu mòn mỏi, đồng thời **giảm thiểu sai sót** nhờ AI và tự động hóa. **Các sếp chỉ cần:**
1. **Cấu hình API Keys** và Google Sheet.
2. **Test với email mẫu**.
3. **Bật workflow** và **quên đi việc nhập liệu thủ công**.

**🚀 Hành động ngay!**
- **Cài đặt n8n trên VPS** (khuyến nghị) để workflow hoạt động 24/7.
- **Tạo Google Sheet "Customer POs"** và cấu hình thư mục Google Drive.
- **Import workflow** và bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📩 Liên hệ hỗ trợ:**
Nếu có vấn đề, liên hệ với **Digital Biz Tech** qua:
- Email: [shilpa.raju@digitalbiz.tech](mailto:shilpa.raju@digitalbiz.tech)
- Website: [digitalbiz.tech](https://digitalbiz.tech)
- LinkedIn: [Digital Biz Tech](https://linkedin.com/company/digital-biz-tech)