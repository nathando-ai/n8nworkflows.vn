---
title: "📄 **Tự Động Hóa Xử Lý Tài Liệu Lớn với OCR bằng SubworkflowAI + Gemini (N8N) – Không Cần Code!**"
description: "Giải pháp tự động hóa xử lý tài liệu PDF/đồ họa lớn (từ 100MB trở lên) với OCR thông minh bằng SubworkflowAI và Gemini API, tiết kiệm thời gian và giảm tải cho hệ thống. Workflow này phân tích, trích xuất và chuyển đổi tài liệu thành markdown tự động, phù hợp cho doanh nghiệp cần xử lý hàng ngàn trang một cách hiệu quả."
slug: "tieu-ly-ta-lieu-lon-ocr-subworkflowai-gemini-n8n"
tags: [n8n, automation, document-extraction, OCR, AI-multimodal, google-gemini, subworkflowai]
keywords: [tự động hóa xử lý tài liệu lớn, OCR tự động hóa, n8n workflow document, Gemini API xử lý PDF, SubworkflowAI API, tự động hóa văn phòng không code]
---

# 🚀 **Tự Động Hóa Xử Lý Tài Liệu Lớn với OCR bằng SubworkflowAI + Gemini (N8N)**

### **Nỗi Đau Của Các Sếp Khi Xử Lý Tài Liệu Lớn**
Các sếp thường gặp phải những vấn đề sau khi xử lý tài liệu thủ công hoặc bằng cách truyền thống:
- **Tài liệu quá lớn (trên 100MB)**: Khó upload vào các API OCR truyền thống (ví dụ: Google Vision, AWS Textract) vì giới hạn kích thước.
- **Thời gian chờ dài**: Xử lý hàng trăm trang PDF hoặc hình ảnh thủ công mất nhiều giờ, thậm chí ngày.
- **Chất lượng trích xuất kém**: Các công cụ OCR cơ bản thường bỏ lỡ nội dung trong bảng biểu, đồ thị hoặc văn bản phức tạp.
- **Tốn tài nguyên hệ thống**: Chạy OCR trên máy chủ nội bộ hoặc cloud tiêu tốn CPU/memory cao, ảnh hưởng đến hiệu suất.

**Giải pháp này giúp các sếp:**
✅ **Xử lý tài liệu lớn (từ 100MB đến 5000 trang)** một cách hiệu quả, không giới hạn kích thước.
✅ **Tự động trích xuất văn bản, bảng biểu, và hình ảnh** với độ chính xác cao nhờ Gemini (LLM multimodal).
✅ **Tiết kiệm thời gian**: Từ hàng giờ thủ công xuống còn vài phút tự động hóa.
✅ **Giảm tải hệ thống**: SubworkflowAI xử lý phần lớn công việc trên cloud, giảm thiểu yêu cầu tài nguyên của n8n.
✅ **Kết quả sạch sẽ**: Tài liệu được chuyển đổi thành **Markdown** hoặc JSON, dễ dàng tích hợp vào CRM, ERP, hoặc hệ thống nội bộ.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|-------------------------------------------------------------------------------|
| **Tự động hóa 100%**      | Không cần viết code, chỉ cần cấu hình workflow trong n8n.                     |
| **Chất lượng OCR cao**    | Sử dụng **Gemini (LLM multimodal)** để phân tích văn bản, bảng biểu, và đồ thị. |
| **Dung lượng không giới hạn** | Xử lý tài liệu từ **100MB đến 5000 trang** mà không bị giới hạn.              |
| **Tích hợp dễ dàng**      | Kết nối với **Google Drive**, **Slack**, hoặc **email** để thông báo kết quả. |
| **Giảm chi phí cloud**    | SubworkflowAI xử lý phần lớn công việc, giảm tải cho máy chủ n8n.             |

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản SubworkflowAI**:
   - Đăng ký miễn phí tại [subworkflow.ai](https://subworkflow.ai) và lấy **API Key**.
   - Thêm **API Key** vào n8n dưới dạng **HTTP Header Auth** (cấu hình chi tiết ở phần sau).
2. **Tài khoản Google Drive** (nếu tải tài liệu từ Google Drive):
   - Cấu hình **Google Drive OAuth2** trong n8n để download file.
3. **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) và thêm vào n8n dưới dạng **Google Palm API**.
4. **File tài liệu cần xử lý**:
   - File PDF, image (PNG/JPG), hoặc document lớn (từ 100MB trở lên).

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí trên cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/10566](https://n8n.io/workflows/10566) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
3. Workflow sẽ xuất hiện trên canvas với **10 node** như mô tả.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/10566](https://n8n.io/workflows/10566) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. Nhấn **Import** để hoàn tất.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials (API Keys)**
Các node quan trọng cần cấu hình **credentials** như sau:

| **Node**               | **Loại Credentials**          | **Tham Số Cần Điền**                          | **Hướng Dẫn**                                                                 |
|------------------------|--------------------------------|-----------------------------------------------|-------------------------------------------------------------------------------|
| **Check Job Status**   | `httpHeaderAuth`              | API Key SubworkflowAI                         | Thêm vào **n8n Credentials** → **HTTP Header Auth** → Điền `Authorization: Bearer <API_KEY>`. |
| **Get Dataset Items**  | `httpHeaderAuth`              | API Key SubworkflowAI                         | Giống như trên.                                                             |
| **Get Dataset**        | `httpHeaderAuth`              | API Key SubworkflowAI                         | Giống như trên.                                                             |
| **Download file**      | `googleDriveOAuth2Api`       | OAuth 2.0 Google Drive                         | Cấu hình tại **n8n Credentials** → **Google Drive OAuth2** → Đăng nhập Google Drive. |
| **Document OCR via VLM** | `googlePalmApi`          | API Key Google Gemini                          | Cấu hình tại **n8n Credentials** → **Google Palm API** → Điền API Key từ Google AI Studio. |

#### **B. Cấu Hình Node "Download file" (Google Drive)**
1. Trong node **Download file**, chọn **Google Drive OAuth2** trong **Credentials**.
2. Chọn **Operation**: `download`.
3. Điền **File ID** của tài liệu muốn xử lý (lấy từ liên kết Google Drive, ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
4. Chọn **Folder** để lưu file tạm (n8n sẽ tự động download và xử lý).

#### **C. Cấu Hình Node "Document OCR via VLM" (Google Gemini)**
1. Trong node **Document OCR via VLM**, chọn **Google Palm API** trong **Credentials**.
2. Chọn **Operation**: `analyze`.
3. Chọn **Resource**: `image`.
4. **Prompt** (gợi ý):
   ```json
   {
     "task": "extract_text_and_structure",
     "instructions": "Extract all text, tables, and figures from the document. Return the result in markdown format with clear headings and lists."
   }
   ```
   (Các sếp có thể tùy chỉnh prompt theo nhu cầu.)

#### **D. Cấu Hình Loop Polling (Check Job Status)**
Workflow sử dụng **loop polling** để kiểm tra trạng thái job trên SubworkflowAI:
1. Node **Check Job Status** sẽ gọi API `GET /v1/jobs/:id` để kiểm tra trạng thái.
2. Node **Job Complete?** (type `if`) sẽ kiểm tra:
   - Nếu `status = "SUCCESS"` → Tiến hành OCR.
   - Nếu `status = "ERROR"` → Gửi thông báo lỗi (có thể kết nối với Slack/Email).
   - Nếu `status = "IN_PROGRESS"` → Loop lại (sử dụng node **Wait** để tránh overloading API).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Nhấn **Execute Workflow** (node **Manual Trigger**).
   - Chọn file mẫu (ví dụ: PDF 50MB) từ Google Drive.
   - Kiểm tra kết quả trong node **Document OCR via VLM** (nếu thành công, sẽ trả về Markdown).

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **Active** trên tab **Workflow** để chạy liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối với Slack/Telegram để Thông Báo Kết Quả**
- Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để gửi thông báo khi:
  - Tài liệu được xử lý thành công.
  - Xảy ra lỗi (ví dụ: file quá lớn, API thất bại).
- **Cách làm**:
  1. Tạo **Slack Webhook** hoặc **Telegram Bot Token**.
  2. Thêm node **HTTP Request** (type `httpRequest`) với URL:
     - Slack: `https://hooks.slack.com/services/XXXX/YYYY`
     - Telegram: `https://api.telegram.org/bot<BOT_TOKEN>/sendMessage`
  3. Gửi payload JSON:
     ```json
     {
       "text": "📄 Tài liệu đã xử lý thành công! Kết quả: {{ $json["result"].text }}"
     }
     ```

### **2. Lưu Log Xử Lý vào Google Sheets**
- Sử dụng node **Google Sheets** để ghi lịch sử xử lý:
  - **Sheet Name**: `Log_XuLy_TaiLieu`
  - **Columns**:
    - `File Name`
    - `File Size`
    - `Status` (SUCCESS/ERROR)
    - `Time Processed`
    - `Result` (Markdown hoặc JSON)
- **Cách làm**:
  1. Thêm node **Google Sheets** sau node **Document OCR via VLM**.
  2. Chọn **Operation**: `createRow`.
  3. Điền dữ liệu từ `$json["result"]` vào các cột tương ứng.

### **3. Chỉ Xử Lý Một Số Trang Đặc Trưng**
- Thay vì xử lý toàn bộ tài liệu, các sếp có thể chỉ lấy **trang cụ thể** (ví dụ: trang 10-20) để tiết kiệm thời gian và tài nguyên.
- **Cách làm**:
  1. Trong node **Get Dataset Items**, thêm **query parameters**:
     ```json
     {
       "page": [10, 20]
     }
     ```
  2. Node này sẽ trả về chỉ các trang từ 10 đến 20.

### **4. Tích Hợp với Email để Gửi Kết Quả**
- Sử dụng node **Email** (ví dụ: Gmail) để gửi kết quả OCR về email:
  - **Subject**: `Kết quả xử lý tài liệu: {{ $json["fileName"] }}`
  - **Body**: `{{ $json["result"].markdown }}`
- **Cách làm**:
  1. Thêm node **Gmail** sau node **Document OCR via VLM**.
  2. Cấu hình **Credentials**: OAuth 2.0 Gmail.
  3. Điền **To**, **Subject**, và **Body** từ `$json`.

---

## 📌 **Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian & Tài Nguyên**

Workflow này là **giải pháp hoàn hảo** cho các sếp cần xử lý tài liệu lớn (PDF, image) một cách **tự động hóa, chính xác và hiệu quả**. Bằng cách kết hợp **SubworkflowAI** (xử lý tài liệu lớn) và **Gemini** (OCR thông minh), các sếp có thể:
✔ **Tiết kiệm hàng giờ làm việc thủ công** mỗi tuần.
✔ **Giảm tải cho hệ thống** nhờ xử lý trên cloud.
✔ **Nâng cao chất lượng dữ liệu** với OCR dựa trên AI multimodal.
✔ **Tích hợp dễ dàng** với Slack, Email, hoặc Google Drive.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình API Keys.
3. **Test với file mẫu** và điều chỉnh prompt OCR.
4. **Kết nối với Slack/Email** để nhận thông báo tự động.

👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/10566)** và bắt đầu tự động hóa ngay!

---
**Cần hỗ trợ thêm?**
- **Trang tài liệu chính thức SubworkflowAI**: [https://docs.subworkflow.ai](https://docs.subworkflow.ai)
- **Join Discord SubworkflowAI**: [https://discord.gg/RCHeCPJnYw](https://discord.gg/RCHeCPJnYw)
- **Hỗ trợ n8n**: [https://community.n8n.io](https://community.n8n.io)