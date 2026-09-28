---
title: "📄 Tự Động Xử Lý Hóa Đơn Quét (OCR + AI) Sang Google Sheets - Giảm 90% Thời Gian Kiểm Tra"
description: "Workflow tự động hóa xử lý hóa đơn PDF/ảnh từ Google Drive sang Google Sheets với OCR và AI (OpenAI), giúp các sếp tiết kiệm hàng giờ kiểm tra thủ công mỗi tháng. Hoàn toàn không cần code!"
slug: "tieu-ly-hoa-don-ocr-ai-google-sheets"
tags: [n8n, automation, invoice processing, OCR, AI, Google Drive, Google Sheets, OpenAI, no-code]
keywords: [tự động hóa hóa đơn, OCR hóa đơn, AI xử lý hóa đơn, Google Drive tự động, Google Sheets tự động, workflow n8n hóa đơn]
---

# 🚀 **Tự Động Xử Lý Hóa Đơn Quét (OCR + AI) Sang Google Sheets**

### **Giải pháp cho nỗi đau "đọc hóa đơn như đọc tiểu thuyết"**
Hóa đơn quét từ CamScanner, PDF bị mờ, hoặc ảnh chụp tay thường khiến các sếp phải mất **30-60 phút/ngày** để nhập liệu thủ công. Kết quả? **Sai sót cao, hiệu suất thấp**, và thời gian có thể dùng để phân tích dữ liệu bị "cướp" đi.

**Workflow này tự động hóa toàn bộ quy trình:**
✅ **Quét hóa đơn** từ Google Drive (PDF/ảnh)
✅ **OCR + AI** (OpenAI) để trích xuất thông tin chính xác
✅ **Ghi dữ liệu** tự động vào Google Sheets
✅ **Báo cáo tự động** qua email (Mailgun) khi có hóa đơn mới

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho OCR + AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/ngày** so với cách làm thủ công.
- **Giảm sai sót 90%** nhờ AI trích xuất thông tin chính xác.
- **Hoạt động tự động** 24/7, không cần can thiệp.
- **Dữ liệu sạch** để phân tích, báo cáo và quyết định nhanh chóng.
- **Kết hợp với Mailgun** để nhận báo cáo hóa đơn mới ngay khi có.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lưu hóa đơn và kích hoạt trigger tự động).
✔ **Tài khoản Google Sheets** (để lưu trữ dữ liệu trích xuất).
✔ **API Key OpenAI** (để sử dụng GPT-4.1-mini trong việc trích xuất thông tin).
✔ **API Key Mailgun** (để gửi báo cáo hóa đơn mới qua email).
✔ **API Key OCR.Space** (để xử lý OCR cho ảnh hóa đơn không đọc được từ PDF).
✔ **Credentials OAuth2** cho Google Drive và Google Sheets (cấu hình trong n8n).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần cài đặt OCR.Space** trên máy chủ, chỉ cần **API Key** là đủ.
- **Workflow hỗ trợ cả PDF và ảnh** (JPG/PNG), nhưng **PDF thường được ưu tiên** vì dễ trích xuất hơn.
- **Nếu hóa đơn từ CamScanner**, workflow sẽ tự động chuyển sang **OCR.Space** để trích xuất chính xác.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/7321](https://n8n.io/workflows/7321) và **import vào n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste vào n8n Editor** (tab "Import").

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **19 node**, nhưng các sếp cần chú ý **cấu hình sau**:

##### **A. Cấu hình Google Drive Trigger**
- Node **"Check for new invoices"** (Google Drive Trigger) cần:
  - **Chọn folder** chứa hóa đơn (ví dụ: `Hóa Đơn Quét`).
  - **Lọc file type**: `PDF` và `JPG/PNG` (để tránh file khác).
  - **Thiết lập trigger tự động** (nếu muốn workflow chạy khi có file mới).

##### **B. Cấu hình OpenAI (Information Extractor)**
- Node **"OpenAI Chat Model"** (lmChatOpenAi):
  - **Chọn model**: `gpt-4.1-mini` (đủ mạnh để trích xuất hóa đơn).
  - **Prompt mẫu** (nếu cần chỉnh sửa):
    ```plaintext
    Trích xuất thông tin từ hóa đơn dưới dạng JSON:
    {
      "invoice_number": "",
      "vendor_name": "",
      "date": "",
      "total_amount": "",
      "items": []
    }
    ```
- Node **"Information Extractor"** (langchain.informationExtractor):
  - **Chọn model**: `gpt-4.1-mini`.
  - **Cấu hình schema** để AI biết trích xuất những trường nào (ví dụ: `invoice_number`, `total_amount`).

##### **C. Cấu hình OCR.Space (nếu cần)**
- Node **"Analyze Image"** (httpRequest):
  - **Điền API Key** từ [OCR.Space](https://ocr.space/OCRAPI).
  - **Tham số request**:
    ```json
    {
      "apikey": "{{$node["Analyze Image"].httpHeaderAuth.apiKey}}",
      "language": "eng",
      "file": "{{$json.base64}}"
    }
    ```
- **Switch Mime Type**: Node này **lựa chọn đường đi** cho file:
  - **Nếu là PDF** → Trích xuất trực tiếp.
  - **Nếu là ảnh (CamScanner)** → Sử dụng OCR.Space.

##### **D. Cấu hình Google Sheets**
- Node **"Append row in sheet"** (googleSheets):
  - **Chọn sheet** muốn lưu dữ liệu (ví dụ: `Hóa Đơn Trích Xuất`).
  - **Cấu hình header** để trùng khớp với dữ liệu từ AI:
    ```
    Invoice Number | Vendor Name | Date | Total Amount | Items
    ```

##### **E. Cấu hình Mailgun (Báo cáo tự động)**
- Node **"Mailgun"**:
  - **Điền API Key** từ Mailgun.
  - **Cấu hình email template** (HTML) trong node **"Prepare a table"**:
    ```html
    <table>
      <tr><th>Invoice Number</th><td>{{$json.invoice_number}}</td></tr>
      <tr><th>Total Amount</th><td>{{$json.total_amount}}</td></tr>
    </table>
    ```
  - **Gửi email** cho người quản lý khi có hóa đơn mới.

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với **1-2 hóa đơn mẫu** để kiểm tra:
   - AI trích xuất đúng không?
   - Dữ liệu ghi vào Sheets có chính xác không?
   - Email báo cáo có được gửi không?
2. **Bật Active workflow** và **đặt lịch trigger tự động** (nếu cần).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo hóa đơn mới ngay khi có.

2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** để ghi lại lỗi hoặc thông tin debug.

3. **Tự động xóa file sau xử lý**:
   - Thêm node **Google Drive (Delete)** sau khi dữ liệu đã được trích xuất.

4. **Báo cáo định kỳ**:
   - Sử dụng **Google Sheets + Apps Script** để tự động gửi báo cáo tổng hợp hàng tháng.

5. **Cập nhật AI prompt**:
   - Nếu AI trích xuất sai, **cập nhật prompt** trong node `Information Extractor` để chính xác hơn.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc nhàn tẻ** và giúp họ tập trung vào **quyết định chiến lược** thay vì nhập liệu. **Chỉ cần 10 phút setup**, sau đó **tự động hóa hoàn toàn**!

**Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** (Google Drive, OpenAI, Mailgun).
3. **Test với 1-2 hóa đơn** và **bật tự động hóa**!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để có môi trường ổn định và **mã giảm giá VPSN8N** để tiết kiệm chi phí!

---
**#TựĐộngHóa #N8N #InvoiceProcessing #AI #GoogleSheets**