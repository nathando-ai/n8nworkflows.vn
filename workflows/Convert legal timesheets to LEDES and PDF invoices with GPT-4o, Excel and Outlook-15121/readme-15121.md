---
title: "🚀 Tự Động Hóa Bảng Thời Gian Pháp Lý → LEDES + PDF Hóa Đơn Với GPT-4o, Excel & Outlook (Không Cần Code)"
description: "Workflow này tự động chuyển đổi bảng thời gian pháp lý từ email (PDF/Word) thành LEDES 1998B, XML 2.0 và PDF hóa đơn chuyên nghiệp, gửi lại cho khách hàng trong giây lát. Giúp tiết kiệm 10+ giờ công/tháng và giảm thiểu lỗi nhập liệu."
slug: "tieu-dong-hoa-bang-thoi-gian-phap-ly-ledes-pdf"
tags: [n8n, automation, legal-billing, ai-summarization, excel-integration, outlook-automation, gpt-4o]
keywords: [tự động hóa bảng thời gian pháp lý, convert LEDES với AI, n8n workflow legal, tự động hóa hóa đơn luật sư, GPT-4o extraxt time entries, Excel + Outlook automation]
---

# 🚀 **Tự Động Hóa Bảng Thời Gian Pháp Lý → LEDES + PDF Hóa Đơn Với GPT-4o, Excel & Outlook**

### **Giải pháp hoàn hảo cho các sếp luật sư, công ty tư vấn pháp lý và doanh nghiệp cần hóa đơn chuyên nghiệp, chính xác và tự động hóa 100%**

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ công/tháng**: Không cần nhập liệu thủ công từ bảng thời gian PDF/Word.
- **Chính xác 100%**: AI GPT-4o tự động phân loại thời gian theo mã UTBMS (chính xác hơn 95% so với cách làm thủ công).
- **Hóa đơn chuyên nghiệp**: Tự động tạo **LEDES 1998B (txt)**, **LEDES XML 2.0**, và **PDF hóa đơn có logo** của công ty.
- **Hoạt động 24/7**: Workflow chạy tự động khi có email mới với bảng thời gian đính kèm.
- **Cập nhật Excel tự động**: Thời gian và số hóa đơn mới được ghi vào file Excel theo thời gian thực.
- **Gửi hóa đơn lại cho khách hàng**: Tất cả file LEDES và PDF được gửi về email của khách hàng trong 1 lần click.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản email IMAP** (để n8n theo dõi hộp thư mới):
   - Ví dụ: Gmail, Outlook, Yahoo Mail (cần **mật khẩu ứng dụng** nếu sử dụng 2FA).
   - **Lưu ý**: Nếu dùng Gmail, cần bật **"Dùng ứng dụng ít an toàn"** trong cài đặt 2FA.

2. **API Key OpenAI** (để sử dụng GPT-4o và GPT-4o-mini):
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - **Lưu ý**: Workflow này **không** chạy trên n8n Cloud do sử dụng node **n8n-nodes-word2text** (community node).

3. **Tài khoản Microsoft Excel Online** (để cập nhật thời gian và số hóa đơn):
   - File Excel cần có **cấu trúc bảng dữ liệu** với cột: `InvoiceNumber`, `Date`, `TaskCode`, `Description`, `Hours`, `Rate`, `Amount`.
   - **Lưu ý**: Workflow sẽ **tự động tăng số hóa đơn** khi có email mới.

4. **Tài khoản Microsoft Outlook** (để gửi hóa đơn về khách hàng):
   - Nếu không dùng Outlook, có thể thay thế bằng **Gmail SMTP** (cần cấu hình thêm node `emailSend`).

5. **Logo và mẫu hóa đơn** (để tạo PDF hóa đơn chuyên nghiệp):
   - Cần **URL hoặc file logo** của công ty (để hiển thị trên PDF).
   - **Mẫu HTML hóa đơn** có thể chỉnh sửa trong node `Generate — Invoice HTML`.

6. **Gotenberg API** (để chuyển HTML → PDF):
   - **Tự động cài đặt** khi import workflow (n8n sẽ tự động tạo credential).
   - Nếu không muốn dùng Gotenberg, có thể thay thế bằng **node `httpRequest`** kết hợp với dịch vụ PDF khác (ví dụ: [PDFShift](https://pdfshift.io/)).

---
## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
:::note[HƯỚNG DẪN CHI TIẾT]
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/15121](https://n8n.io/workflows/15121) hoặc copy toàn bộ JSON từ link trên.
- **Bước 2**: Mở **n8n Editor** (self-hosted) → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.
- **Bước 3**: Chọn **Active** để bật workflow.
:::

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **27 node**, nhưng chỉ có **5 node cần cấu hình chính** (các node khác tự động chạy sau). Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node 1: IMAP — Watch Inbox (Email Trigger)**
- **Cấu hình**:
  - **Credentials**: Chọn `imap` (cần tạo mới trong **Credentials Manager**).
  - **Host**: `imap.gmail.com` (nếu dùng Gmail) hoặc `imap.outlook.com` (nếu dùng Outlook).
  - **Port**: `993` (IMAP).
  - **Username**: Email của bạn.
  - **Password**: **Mật khẩu ứng dụng** (nếu dùng 2FA) hoặc mật khẩu chính.
  - **Folder**: `INBOX` (hoặc folder chứa email khách hàng gửi bảng thời gian).
  - **Filter**: `hasAttachments=true` (chỉ lấy email có file đính kèm).
  - **Polling Interval**: `60` (kiểm tra email mỗi 60 giây).

#### **🔹 Node 2: Excel — Read Invoice Numbers (Lấy số hóa đơn mới nhất)**
- **Cấu hình**:
  - **Credentials**: Chọn `microsoftExcelOAuth2Api` (cần tạo mới).
  - **File**: Chọn file Excel chứa bảng thời gian (ví dụ: `timesheets.xlsx`).
  - **Worksheet**: Chọn sheet chứa dữ liệu (ví dụ: `Sheet1`).
  - **Table**: Chọn bảng dữ liệu (ví dụ: `TimeEntries`).
  - **Operation**: `getRows` (lấy tất cả dòng).
  - **Filter**: `InvoiceNumber` (để lấy số hóa đơn lớn nhất hiện có).

#### **🔹 Node 3: LLM — GPT-4o (Time Entries) & LLM — GPT-4o-mini (Sender Info)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi` (cần tạo mới với API Key OpenAI).
  - **Model**:
    - Node `LLM — GPT-4o (Time Entries)`: Chọn `gpt-4o`.
    - Node `LLM — GPT-4o-mini (Sender Info)`: Chọn `gpt-4o-mini`.
  - **System Prompt** (cần chỉnh sửa để phù hợp với công ty):
    - **Ví dụ cho `GPT-4o (Time Entries)`**:
      ```json
      "You are a legal time tracking assistant. Extract all time entries from the PDF/Word file and assign UTBMS task codes. Return data in JSON format with keys: 'date', 'taskCode', 'description', 'hours', 'rate', 'amount'."
      ```
    - **Ví dụ cho `GPT-4o-mini (Sender Info)`**:
      ```json
      "Extract the 'Remit To' billing information from the email signature. Return JSON with keys: 'companyName', 'address', 'city', 'state', 'zip', 'country', 'email', 'phone'."
      ```

#### **🔹 Node 4: Generate — Invoice HTML (Tạo mẫu PDF hóa đơn)**
- **Cấu hình**:
  - **Logo URL**: Thay thế bằng URL logo của công ty (ví dụ: `https://tinodoc.com/logo.png`).
  - **Màu sắc và font**: Chỉnh sửa trong template HTML (node này sử dụng **code JavaScript** để render HTML).
  - **Dữ liệu động**: Workflow sẽ tự động điền thông tin từ AI (thời gian, số hóa đơn, thông tin khách hàng).

#### **🔹 Node 5: Send a message (Gửi email hóa đơn về khách hàng)**
- **Cấu hình**:
  - **Credentials**: Chọn `microsoftOutlookOAuth2Api` (nếu dùng Outlook) hoặc `emailSend` (nếu dùng Gmail SMTP).
  - **To**: `$json["email"]` (địa chỉ email của khách hàng, được extra từ email gốc).
  - **Subject**: `Invoice #$json["invoiceNumber"] - $json["companyName"]`.
  - **Attachments**: Tất cả file LEDES và PDF hóa đơn (được merge từ node trước).

---
### **3. Kích hoạt ⚡️**
:::note[TEST RUN TRƯỚC KHI CHẠY THỰC SỰ]
- **Bước 1**: Nhấn **Run Workflow** và chọn **Test Run** với một email mẫu (có file PDF/Word đính kèm).
- **Bước 2**: Kiểm tra:
  - AI có extra thời gian và thông tin khách hàng không?
  - Số hóa đơn có tăng lên không?
  - File LEDES và PDF có được tạo thành công không?
- **Bước 3**: Nếu test thành công, chuyển sang **Active** để workflow chạy tự động.
:::

---

## **✍️ Mẹo & gợi ý nâng cao**
### **🔹 1. Tối ưu hóa AI cho công ty**
- **Chỉnh sửa System Prompt** để phù hợp với **mã UTBMS** của công ty.
- **Thêm validation** trong node `Parse Time Entry Output` để loại bỏ thời gian sai (ví dụ: thời gian âm, vượt quá 8 giờ/ngày).

### **🔹 2. Lưu log và báo cáo**
- **Thêm node `stickyNote`** để ghi lại lỗi hoặc thông tin debug.
- **Tạo báo cáo hàng tháng** bằng cách:
  - Dùng node `microsoftExcel` để **tính tổng thời gian theo tháng**.
  - Gửi báo cáo qua **Slack/Telegram** (thêm node `slackSend` hoặc `telegramSend`).

### **🔹 3. Kết hợp với Slack/Telegram**
- Thêm node **`webhook`** để gửi thông báo khi có email mới:
  ```json
  {
    "url": "https://hooks.slack.com/services/YOUR_WEBHOOK_URL",
    "method": "POST",
    "body": {
      "text": "📄 New invoice generated for $json[companyName] (Invoice #$json[invoiceNumber])"
    }
  }
  ```

### **🔹 4. Sử dụng template LEDES chuẩn**
- **Tải template LEDES 1998B và XML 2.0** từ [UTBMS](https://www.utbms.org/) và **chỉnh sửa trong node `Generate — LEDES 1998B`** để đảm bảo chuẩn mực.

### **🔹 5. Backup dữ liệu**
- **Tạo bản sao file Excel** hàng ngày bằng node `microsoftExcel` với **operation: `getRows`** và lưu vào **Google Drive/OneDrive**.
- **Dùng node `httpRequest`** để backup JSON của workflow vào **GitHub/GitLab**.

---
## **📌 Kết luận**
### **🚀 Workflow này giúp các sếp:**
✅ **Tự động hóa hoàn toàn** quá trình chuyển đổi bảng thời gian → hóa đơn.
✅ **Giảm thiểu lỗi** nhờ AI GPT-4o phân loại thời gian chính xác.
✅ **Tiết kiệm thời gian** và tập trung vào công việc có giá trị cao hơn.
✅ **Cập nhật dữ liệu Excel tự động**, không cần nhập liệu thủ công.

### **🎁 Đăng ký VPS để tự động hóa 24/7**
:::info[GỢI Ý HẠT HÀNG]
Để workflow này **chạy liên tục** mà không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Dưới đây là một số gợi ý:
- **VPS TinoHost** (Giảm 39% với mã **VPSN8N**):
  👉 [Đăng ký VPS 4GB/4CPU chỉ 50k/tháng](https://tino.vn/vps-n8n?affid=388)
- **VPS Xeon 4GB** (Tốc độ cao, ổ cứng NVMe):
  👉 [Đăng ký tại BNIX](https://my.bnix.one/aff.php?aff=172) (Giảm 10% với mã **N8N10**).

**Lưu ý**: N8n Cloud **không hỗ trợ** node `n8n-nodes-word2text`, nên phải self-host.
:::

---
### **💡 Bắt đầu ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test run** với email mẫu.
3. **Active workflow** và **nhận hóa đơn tự động** trong giây lát!

**Nếu có vấn đề**, hãy để lại comment bên dưới hoặc liên hệ với [AI Solutions](https://n8n.io/workflows/15121) để hỗ trợ! 🚀