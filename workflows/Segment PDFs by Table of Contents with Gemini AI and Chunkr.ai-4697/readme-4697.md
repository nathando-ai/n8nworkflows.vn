---
title: "📄 **Tự Động Xây Dự Table of Contents (TOC) cho PDF bằng AI Gemini + Chunkr.ai – Không Cần Code!**"
description: "Workflow tự động hóa phân tích và xây dựng Table of Contents (TOC) chính xác từ PDF, kết hợp AI Gemini và công nghệ OCR Chunkr.ai. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc tổ chức nội dung tài liệu, đồng thời đảm bảo cấu trúc logic và phân cấp chính xác cho từng phần."
slug: "tieu-dong-xay-dung-table-of-contents-pdf-ai-gemini-chunkr"
tags: [n8n, automation, ai-gemini, chunkr-ai, pdf-processing, no-code, structured-data]
keywords: [tự động hóa pdf, table of contents ai, gemini api n8n, chunkr ai workflow, phân tích pdf bằng ai, tự động hóa văn phòng]
---

# 🚀 **Tự Động Xây Dự Table of Contents (TOC) cho PDF bằng AI Gemini + Chunkr.ai**

## **Giới thiệu: Tiết kiệm thời gian và nâng cao hiệu quả tổ chức tài liệu**
Các sếp đã bao giờ phải mất **giờ đồng hồ** để thủ công phân tích, sắp xếp và xây dựng **Table of Contents (TOC)** cho các tài liệu PDF dài hàng trăm trang? Hay phải đối mặt với **cấu trúc không logic**, **nhân viên khác hiểu khác** khi chia sẻ tài liệu? Đây chính là **nỗi đau thực tế** của nhiều doanh nghiệp khi làm việc với tài liệu kỹ thuật, báo cáo, hoặc sách điện tử.

**Workflow này giải quyết hoàn toàn vấn đề đó bằng cách:**
✅ **Tự động hóa 100%** quá trình phân tích PDF, từ việc **đọc nội dung** đến **xây dựng TOC chính xác** với cấu trúc phân cấp.
✅ **Sử dụng AI Gemini** để **hiểu ngữ cảnh** và **tự động phân loại** các phần, chương, và tiểu mục trong tài liệu.
✅ **Kết hợp công nghệ OCR Chunkr.ai** để **trích xuất văn bản** từ PDF, ngay cả khi tài liệu có hình ảnh hoặc bố cục phức tạp.
✅ **Cung cấp nhiều định dạng xuất** (Markdown, HTML, JSON) để **sử dụng linh hoạt** trong các hệ thống khác (Slack, Notion, CRM, hoặc API).

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian lên đến 80%** so với phương pháp thủ công.
- **Đảm bảo tính nhất quán** trong việc phân loại nội dung (không còn "ai cũng hiểu khác").
- **Cấu trúc TOC logic** với phân cấp chính xác (chương → tiểu mục → nội dung).
- **Hoạt động liên tục 24/7** khi tự động hóa trên VPS (không phụ thuộc vào nhân viên).
- **Xuất nhiều định dạng** (Markdown, HTML, JSON) để tích hợp với các công cụ khác.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Chunkr.ai** (để trích xuất văn bản từ PDF):
   - Đăng ký tại: [https://chunkr.ai](https://chunkr.ai)
   - **Lấy API Key** từ Dashboard → API Keys.
2. **Tài khoản Google Drive** (nếu tải PDF từ Google Drive):
   - **OAuth 2.0 Credentials** (cấu hình trong n8n).
3. **API Key Google Gemini** (để sử dụng AI Gemini):
   - **Lấy tại:** [Google AI Studio](https://makersuite.google.com/app/apikey).
4. **VPS tự host n8n** (khuyến nghị để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4697](https://n8n.io/workflows/4697) (chọn **Export as JSON**).
2. **Trên n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Kiểm tra cấu trúc** trước khi kích hoạt.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/4697](https://n8n.io/workflows/4697).
2. **Trên n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. **Lưu ý:** Nếu có lỗi, **xóa và import lại từ đầu**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** do sử dụng **AI + OCR**, nên các bước sau **cần chú ý đặc biệt**:

#### **🔹 Node: POST Chunkr Task (HTTP Request)**
- **Thay thế API Key Chunkr.ai**:
  ```json
  "headers": {
    "Authorization": "Bearer YOUR_CHUNKR_API_KEY"
  }
  ```
  - **Lấy API Key** từ [Chunkr.ai Dashboard](https://chunkr.ai/dashboard/api-keys).
  - **Không để quên** thay thế `<your_api_key>` thành key thực tế!

#### **🔹 Node: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Thiết lập credentials**:
  1. **Tạo credential mới** trong n8n:
     - **Type:** `Google Gemini API`
     - **API Key:** Nhập key từ [Google AI Studio](https://makersuite.google.com/app/apikey).
  2. **Chọn credential** trong node `Google Gemini Chat Model`.

#### **🔹 Node: Download PDF từ Google Drive**
- **Cấu hình OAuth 2.0**:
  1. **Tạo credential mới** trong n8n:
     - **Type:** `Google Drive OAuth2`
     - **Client ID & Secret** lấy từ [Google Cloud Console](https://console.cloud.google.com/).
  2. **Chọn credential** trong node `Download PDF from Google Drive`.
  3. **Điền ID file PDF** (tìm trong liên kết Google Drive).

#### **🔹 Node: Set File Name (set)**
- **Đặt tên file đầu ra**:
  - **Thay đổi `fileNameSnake`** để tên file xuất ra phù hợp (ví dụ: `report_final`).
  - **Lưu ý:** Tên này sẽ được sử dụng trong **Chunkr.ai** và **Google Drive**.

#### **🔹 Node: AI Agent (Agent)**
- **Cấu hình Prompt (nếu cần chỉnh sửa)**:
  - **Mặc định**, AI sẽ tự động phân tích TOC từ đầu tài liệu.
  - **Nếu muốn tùy chỉnh**, chỉnh sửa trong **node `Table of Content Agent`**:
    ```json
    "prompt": "Analyze the document structure and create a nested Table of Contents with chapters, sections, and subsections."
    ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - **Nhấn "Execute workflow"** và chọn **PDF mẫu** (tải từ Google Drive hoặc URL).
   - **Kiểm tra kết quả** trong node `Return each section individually` hoặc `Return the whole document`.
2. **Bật Active workflow**:
   - Sau khi **không có lỗi**, chuyển trạng thái sang **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram để báo cáo kết quả**
- **Sử dụng node `Slack` hoặc `Telegram Bot`** để gửi **TOC đã xây dựng** về nhóm chat.
- **Cách làm**:
  ```json
  "webhookUrl": "https://hooks.slack.com/services/YOUR_WEBHOOK_URL"
  "message": "{{ $json.output }}"
  ```

### **2. Lưu log kết quả vào Google Sheets**
- **Sử dụng node `Google Sheets`** để ghi lại **tên file, ngày xử lý, và kết quả**.
- **Cách làm**:
  - Tạo **credential Google Sheets** trong n8n.
  - Chọn **Sheet Name** và **Range** (ví dụ: `A1`).

### **3. Gửi báo cáo định kỳ qua Email**
- **Sử dụng node `Email`** (SMTP) để gửi **báo cáo TOC** cho team hàng tuần.
- **Cách làm**:
  ```json
  "to": "team@example.com"
  "subject": "Báo cáo TOC tài liệu mới"
  "html": "{{ $htmlDocument }}"
  ```

### **4. Sử dụng với LangChain Agent cho tự động hóa cao**
- **Nếu muốn tích hợp với LangChain**, có thể **trích xuất JSON TOC** và sử dụng trong **Agent khác** để tự động tạo **tóm tắt** hoặc **câu hỏi thường gặp**.

---
## 📌 **Kết luận**
Workflow này **không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng tổ chức tài liệu** cho các sếp. Bằng cách **tự động hóa phân tích PDF** và **xây dựng TOC chính xác**, các sếp có thể:
✔ **Tập trung vào công việc chiến lược** thay vì thủ công phân loại tài liệu.
✔ **Chia sẻ nội dung một cách logic** với team.
✔ **Tích hợp với các hệ thống khác** (CRM, Notion, Slack) một cách dễ dàng.

**🚀 Hãy thử ngay hôm nay!**
1. **Import workflow** và **cấu hình API Key**.
2. **Test với một PDF mẫu**.
3. **Bật Active và tự động hóa 24/7** trên VPS.

**Nếu có vấn đề, hãy để lại comment bên dưới!** Các sếp có thể **tùy chỉnh Prompt AI** hoặc **thêm node mới** để phù hợp với nhu cầu cụ thể. 💡

---
:::note[**Lưu ý cuối cùng**]
- **Không sử dụng workflow này với tài liệu có bản quyền** (vi phạm chính sách Chunkr.ai).
- **Nếu PDF có bảo mật**, Chunkr.ai **không thể trích xuất** được nội dung.
- **Đối với tài liệu có hình ảnh nhiều**, hiệu suất **có thể chậm hơn** do OCR.
:::

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/4697)** | **📌 [Cài đặt VPS cho n8n](https://tino.vn/vps-n8n?affid=388)**