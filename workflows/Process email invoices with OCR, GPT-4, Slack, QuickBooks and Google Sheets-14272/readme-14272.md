---
title: "💰 **Tự Động Xử Lý Hóa Đơn Email với OCR, GPT-4, Slack & QuickBooks – Không Cần Code!**"
description: "Workflow này tự động nhận, đọc hóa đơn từ email (PDF/ảnh), trích xuất dữ liệu bằng AI, kiểm tra tổng hợp, ẩn thông tin nhạy cảm và đồng bộ hóa đơn vào QuickBooks – tiết kiệm 10+ giờ/tháng cho bộ phận tài chính!"
slug: "tieu-dong-xu-ly-hoa-don-email-voi-ocr-gpt-4-slack-quickbooks"
tags: [n8n, automation, invoice processing, ai-summarization, quickbooks, gmail, slack, ocr, gpt-4]
keywords: [n8n workflow hóa đơn, tự động hóa hóa đơn email, OCR hóa đơn PDF, GPT-4 trích xuất dữ liệu, QuickBooks tự động, Slack thông báo hóa đơn]
---

# 🚀 **Tự Động Xử Lý Hóa Đơn Email: Từ Email → AI → QuickBooks – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Tài Chính**
Hàng ngày, bộ phận tài chính phải:
- **Làm thủ công** mở hàng chục email để tìm hóa đơn.
- **Gõ dữ liệu** vào QuickBooks từ hóa đơn PDF/ảnh.
- **Lo lắng** về sai sót trong tổng hợp hoặc mất thông tin nhạy cảm (PAN, GST).
- **Chờ đợi** đồng nghiệp kiểm tra hóa đơn trước khi ghi sổ.

**Kết quả?** Thời gian và tiền bạc bị "chảy ra" như nước qua lưới!

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận tài chính.
- **Giảm sai sót 90%** nhờ AI kiểm tra tổng hợp tự động.
- **Bảo mật thông tin nhạy cảm** (PAN, GST, số tài khoản) bằng việc ẩn dữ liệu.
- **Dồng bộ hóa đơn vào QuickBooks** trong giây lát.
- **Nhận thông báo Slack** khi hóa đơn cần kiểm tra hoặc đã xử lý thành công.
- **Lưu lịch sử xử lý** trong Google Sheets để tra cứu dễ dàng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy hóa đơn từ email).
2. **API Key OpenAI** (để sử dụng GPT-4 và OCR AI).
3. **Tài khoản Slack** (để thông báo và kiểm tra hóa đơn).
4. **Tài khoản QuickBooks** (để đồng bộ hóa đơn).
5. **Google Sheets** (để lưu log xử lý).
6. **OCR API** (nếu hóa đơn là ảnh, không phải PDF).
   - *Gợi ý:* Sử dụng **Tesseract OCR** (miễn phí) hoặc **Google Vision API**.
7. **Thông tin cấu hình**:
   - **Slack Channel ID** (để gửi thông báo).
   - **Sheet ID Google Sheets** (để lưu log).
   - **QuickBooks OAuth Token** (để tạo hóa đơn).
   - **Ngưỡng kiểm tra** (ví dụ: hóa đơn nào có độ tin cậy < 80% sẽ cần review).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/14272](https://n8n.io/workflows/14272).
2. **Đăng nhập** vào n8n (Self-hosted hoặc n8n.cloud).
3. **Nhấn "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo workflow mới.
2. **Nhấn "Import"** → Chọn "Paste JSON".
3. **Dán JSON** từ [n8n.io/workflows/14272](https://n8n.io/workflows/14272) (đã tải trước).
4. **Nhấn "Import"** để hoàn tất.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **20 node** phức tạp, nhưng chỉ cần chú ý đến **các node quan trọng sau**:

#### **🔹 Node 1: Invoice Email Trigger (gmailTrigger)**
- **Cấu hình**:
  - **Label**: `invoice` (để chỉ định email nào là hóa đơn).
  - **Attachments**: Chọn `Download` để lưu tệp vào n8n.
  - **Credentials**: Sử dụng tài khoản Gmail có quyền truy cập vào thư mục hóa đơn.

#### **🔹 Node 2 & 3: Workflow Configuration & Capture Invoice Metadata (set)**
- **Điền thông tin cấu hình**:
  - `ocrApiUrl`: URL của API OCR (nếu sử dụng Google Vision API, điền `https://vision.googleapis.com/v1/images:annotate`).
  - `slackChannelId`: ID channel Slack (để gửi thông báo).
  - `googleSheetsId`: ID sheet Google Sheets (để lưu log).
  - `quickbooksOAuthToken`: Token OAuth của QuickBooks.
  - `reviewThreshold`: Ngưỡng độ tin cậy (ví dụ: `80`).

#### **🔹 Node 4: Check File Type (if)**
- **Kiểm tra loại file**:
  - Nếu file là **PDF** → Đi đến node `Extract Text from PDF`.
  - Nếu file là **ảnh** → Đi đến node `OCR for Images`.

#### **🔹 Node 5 & 6: Extract Text from PDF & OCR for Images (extractFromFile + httpRequest)**
- **PDF**:
  - Node `extractFromFile` sẽ tự động trích xuất văn bản từ PDF.
- **Ảnh**:
  - Node `httpRequest` gửi yêu cầu đến API OCR (ví dụ: Google Vision API).
  - **Cấu hình API Key** trong `httpRequest`:
    ```json
    {
      "headers": {
        "Authorization": "Bearer YOUR_GOOGLE_VISION_API_KEY"
      }
    }
    ```

#### **🔹 Node 7: Merge OCR Results (merge)**
- **Kết hợp** kết quả từ PDF và OCR thành một chuỗi văn bản duy nhất.

#### **🔹 Node 8 & 9: AI Invoice Extractor & OpenAI GPT-4 (agent + lmChatOpenAi)**
- **Cấu hình GPT-4**:
  - **Model**: `gpt-4o` (đã được cấu hình sẵn).
  - **Prompt**:
    ```json
    "Extract structured invoice data from the following text. Return in JSON format with fields: vendor, invoice_number, date, items, subtotal, tax, total, due_date."
    ```
  - **API Key OpenAI**: Điền vào `Credentials` của node `lmChatOpenAi`.

#### **🔹 Node 10: Invoice Schema Parser (outputParserStructured)**
- **Chuyển** kết quả JSON từ GPT-4 thành dạng dữ liệu chuẩn.

#### **🔹 Node 11: Validate and Recalculate Totals (code)**
- **Mã JavaScript** sẽ kiểm tra tổng hợp và tính lại tổng nếu có sai sót.
- **Lưu ý**: Các sếp có thể **chỉnh sửa mã** này nếu hóa đơn có cấu trúc đặc biệt.

#### **🔹 Node 12: Mask PII Data (code)**
- **Ẩn** thông tin nhạy cảm như:
  - Số PAN (Personal Account Number).
  - Số GST/VAT.
  - Số tài khoản ngân hàng.
- **Mã mẫu**:
  ```javascript
  $input.all().forEach(item => {
    item.data.pan = "****-****-****-1234"; // Ẩn số PAN
    item.data.gst = "****-****-****";
  });
  ```

#### **🔹 Node 13: Check if Review Needed (if)**
- **Điều kiện**:
  - Nếu độ tin cậy < `reviewThreshold` (ví dụ: 80%) → Đi đến node `Send Review Request`.
  - Nếu tổng hợp sai → Đi đến node `Wait for Human Review`.

#### **🔹 Node 14 & 15: Wait for Human Review & Send Review Request (wait + slack)**
- **Slack Notification**:
  - **Message**:
    ```json
    {
      "text": "🚨 Invoice #{{ $node["Capture Invoice Metadata"].json()["invoice_number"] }} needs review!\n\nVendor: {{ $node["Capture Invoice Metadata"].json()["vendor"] }}\nTotal: {{ $node["Capture Invoice Metadata"].json()["total"] }}\n\n[Click here to approve](https://quickbooks.example.com/review)"
    }
    ```
  - **Attachments**: Gửi file hóa đơn kèm theo.

#### **🔹 Node 16: Create QuickBooks Bill (quickbooks)**
- **Cấu hình**:
  - **Resource**: `Bill`.
  - **Operation**: `Create`.
  - **Credentials**: Sử dụng OAuth Token của QuickBooks.
  - **Fields**:
    ```json
    {
      "VendorName": "{{ $node["Invoice Schema Parser"].json()["vendor"] }}",
      "Amount": "{{ $node["Invoice Schema Parser"].json()["total"] }}",
      "DueDate": "{{ $node["Invoice Schema Parser"].json()["due_date"] }}"
    }
    ```

#### **🔹 Node 17 & 18: Log to Audit Trail & Send Success Notification (googleSheets + slack)**
- **Google Sheets**:
  - **Sheet Name**: `Audit Log`.
  - **Columns**: `Invoice Number`, `Vendor`, `Date`, `Status`, `Reviewed By`, `Timestamp`.
- **Slack Success Message**:
  ```json
  {
    "text": "✅ Invoice #{{ $node["Capture Invoice Metadata"].json()["invoice_number"] }} processed successfully!\n\nVendor: {{ $node["Capture Invoice Metadata"].json()["vendor"] }}\nTotal: {{ $node["Invoice Schema Parser"].json()["total"] }}"
  }
  ```

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 hóa đơn mẫu**:
   - Gửi email hóa đơn vào Gmail (đã cấu hình label `invoice`).
   - Kiểm tra:
     - Hóa đơn có được trích xuất dữ liệu không?
     - Slack có thông báo không?
     - QuickBooks có đồng bộ hóa đơn không?
2. **Bật Active** workflow khi đã kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối với Google Drive**
- **Node `googleDrive`** (n8n-nodes-base.googleDrive) để lưu bản sao hóa đơn vào Google Drive thay vì chỉ Slack.

### **2. Gửi Báo Cáo Định Kỳ**
- **Node `set` + `googleSheets`** để tạo báo cáo tổng hợp hóa đơn hàng tháng.

### **3. Thêm Nhận Dạng OCR Tự Động**
- **Node `httpRequest`** kết nối với **AWS Textract** hoặc **Azure Form Recognizer** để nâng cao độ chính xác OCR.

### **4. Thông Báo Violation (Hóa Đơn Sai)**
- **Node `slack`** gửi cảnh báo khi hóa đơn có:
  - Tổng hợp không khớp.
  - Thiếu thông tin quan trọng.
  - Ngày quá hạn.

### **5. Lưu Lịch Sử Review**
- **Node `googleSheets`** thêm cột `Reviewed By` và `Review Date` để theo dõi ai đã kiểm tra hóa đơn.

---
## 📌 **Kết Luận**
Workflow này **giải phóng bộ phận tài chính** khỏi công việc lặp lại, **giảm sai sót**, và **tự động hóa** quy trình từ email đến QuickBooks. **Chỉ cần 1 ngày** để setup và chạy 24/7!

**👉 Hãy thử ngay và tiết kiệm thời gian cho đội ngũ tài chính của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bạn có câu hỏi về setup? Để lại comment bên dưới hoặc liên hệ với ResilNext qua [n8n.io](https://n8n.io)!**