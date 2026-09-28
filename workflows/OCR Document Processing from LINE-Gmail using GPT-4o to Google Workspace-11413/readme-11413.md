---
title: "🚀 Tự Động Hóa OCR + Tóm Tắt Tài Liệu từ LINE & Gmail bằng GPT-4o – Lưu Trữ Trọn Bộ Dữ Liệu trên Google Workspace"
description: "Workflow này tự động chụp ảnh, quét PDF từ LINE và Gmail, chuyển đổi thành văn bản bằng OCR, tóm tắt thông minh bằng GPT-4o, và lưu kết quả vào Google Sheets + Gmail Draft. Giúp các sếp không bao giờ mất mát thông tin quan trọng trong tài liệu."
slug: "tieu-dong-hoa-ocr-tom-tat-tai-lieu-tu-line-gmail"
tags: [n8n, automation, no-code, OCR, AI-summarization, google-workspace, openai, line-bot]
keywords: [n8n workflow OCR, tự động hóa tài liệu, GPT-4o tóm tắt văn bản, Google Drive + Sheets, LINE + Gmail tự động hóa, OCR từ ảnh PDF]
---

# 🚀 **Tự Động Hóa OCR + Tóm Tắt Tài Liệu từ LINE & Gmail – Lưu Trữ Trọn Bộ Dữ Liệu trên Google Workspace**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải:
- **Chụp ảnh tài liệu** từ LINE, Gmail, hoặc các ứng dụng khác và **quét thủ công** bằng OCR (Optical Character Recognition).
- **Tìm kiếm văn bản** trong hàng trăm tài liệu PDF/ảnh, mất thời gian và dễ bị lỗi.
- **Lưu trữ rối loạn** giữa Gmail, Google Drive, và LINE, khiến việc theo dõi khó khăn.
- **Không có tóm tắt tự động**, phải đọc toàn bộ tài liệu để rút gọn thông tin.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Chụp ảnh/PDF từ LINE và Gmail** → **Quét OCR** → **Tóm tắt bằng GPT-4o** → **Lưu kết quả vào Google Sheets + Gmail Draft**.
✅ **Không cần code**, chỉ cần cấu hình n8n trên VPS.
✅ **Hoạt động 24/7**, không bỏ sót tài liệu nào.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và độ ổn định cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét OCR thủ công, tóm tắt tài liệu bằng tay.
- **Dữ liệu chính xác**: GPT-4o tóm tắt văn bản với độ chính xác cao, không bỏ sót chi tiết.
- **Lưu trữ thống nhất**: Tất cả tài liệu và tóm tắt được lưu vào **Google Sheets** và **Gmail Draft**, dễ theo dõi.
- **Hoạt động liên tục**: Workflow chạy tự động khi có tài liệu mới từ LINE hoặc Gmail.
- **Cá nhân hóa**: Thêm metadata như **nguồn (LINE/EMAIL)**, **ngày gửi**, và **link tài liệu gốc** vào Sheets.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản và API Keys**:
- **LINE Developer Account** (để kết nối Webhook).
- **Gmail IMAP** (để lấy email mới).
- **Google Drive API** (để lưu tài liệu).
- **Google Sheets API** (để lưu tóm tắt).
- **OpenAI API Key** (để sử dụng GPT-4o cho OCR và tóm tắt).

✔ **Tham số cấu hình**:
- **Folder ID Google Drive** (để lưu tài liệu tạm).
- **Sheet ID Google Sheets** (để lưu tóm tắt).
- **Prompt tóm tắt** (có thể chỉnh sửa trong node `Message a model`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11413](https://n8n.io/workflows/11413) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **17 node**, các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu Hình Khởi Động (Triggers)**
- **LINE Webhook**:
  - Đăng ký **Webhook URL** từ n8n (ví dụ: `https://tên-vps-của-bạn.com/webhook/line-webhook`).
  - Cấu hình trên **LINE Developer Console** để nhận tin nhắn ảnh/PDF.
- **Gmail IMAP Trigger**:
  - Thiết lập **IMAP Server** (ví dụ: `imap.gmail.com`).
  - Sử dụng **OAuth 2.0** để kết nối với Gmail.

##### **B. Cấu Hình Chia Sẻ (Workflow Configuration)**
- Node này lưu **Folder ID Google Drive** và **Sheet ID Google Sheets**.
  - **Lấy Folder ID**:
    - Mở Google Drive → Chọn folder muốn lưu → URL sẽ có dạng `https://drive.google.com/drive/folders/ID_FOLDER`.
    - Copy `ID_FOLDER` vào node `Workflow Configuration`.
  - **Lấy Sheet ID**:
    - Mở Google Sheets → URL sẽ có dạng `https://docs.google.com/spreadsheets/d/ID_SHEET/edit`.
    - Copy `ID_SHEET` vào node `Append row in sheet`.

##### **C. Chuyển Đổi File & OCR**
- **Upload to Google Drive**:
  - Chọn **Folder ID** đã cấu hình ở trên.
- **Convert to Base64**:
  - Node này chuyển file thành định dạng Base64 để OCR xử lý.
- **Analyze image (OpenAI)**:
  - Điền **API Key OpenAI** và chọn **model Vision API** (ví dụ: `gpt-4o`).
  - Cấu hình **prompt OCR** (nếu cần):
    ```json
    {
      "prompt": "Extract all text from this image and return as plain text.",
      "temperature": 0
    }
    ```

##### **D. Tóm Tắt Bằng GPT-4o**
- **Message a model (OpenAI)**:
  - Sử dụng **model GPT-4o** để tóm tắt văn bản.
  - Cấu hình **prompt tóm tắt** (ví dụ):
    ```json
    {
      "prompt": "Summarize this document in 3 bullet points: {text}",
      "temperature": 0.3
    }
    ```
  - **Lưu ý**: Thay `{text}` bằng `$json["text"]` (trong node `Analyze image`).

##### **E. Lưu Trữ Kết Quả**
- **Append row in sheet (Google Sheets)**:
  - Chọn **Sheet ID** và **tab** (ví dụ: `Tóm Tắt Tài Liệu`).
  - Cấu hình **cột** để lưu:
    - `Source` (LINE/EMAIL)
    - `Date` (ngày gửi)
    - `Summary` (tóm tắt)
    - `Link Drive` (đường dẫn tài liệu gốc)
- **Create Gmail Draft**:
  - Chọn **Gmail Account** và cấu hình **tiêu đề/nhân vật** cho email draft.

##### **F. Node Quá Trình (Optional)**
- **Wait (1-2 giây)**: Giúp tránh bị rate limit khi gọi API.
- **Code (JavaScript)**: Normalize file từ Gmail và LINE để cùng định dạng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một **tài liệu ảnh/PDF** từ LINE hoặc Gmail.
   - Kiểm tra **Google Sheets** và **Gmail Draft** xem kết quả có xuất hiện không.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và nó sẽ hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi có tài liệu mới được xử lý.
2. **Lưu Log Chi Tiết**:
   - Thêm node **Google Drive** để lưu **log chi tiết** (ví dụ: thời gian xử lý, lỗi nếu có).
3. **Tự Động Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng **Google Apps Script** kết hợp với n8n để gửi **báo cáo tổng hợp** về tài liệu đã xử lý.
4. **Chỉnh Sửa Prompt Tóm Tắt**:
   - Nếu muốn tóm tắt chi tiết hơn, thay đổi **prompt** trong node `Message a model`:
     ```json
     {
       "prompt": "Summarize this document in 5 bullet points with key details: {text}",
       "temperature": 0.5
     }
     ```
5. **Kết Nối với Notion/Confluence**:
   - Thay vì Google Sheets, có thể lưu tóm tắt vào **Notion** hoặc **Confluence** bằng node **HTTP Request**.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa OCR** từ LINE và Gmail.
✔ **Tóm tắt tài liệu** bằng GPT-4o với độ chính xác cao.
✔ **Lưu trữ thống nhất** trên Google Workspace.
✔ **Tiết kiệm thời gian** và tránh mất mát thông tin.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test với tài liệu mẫu** và bật workflow.

**Không còn cần quét OCR thủ công nữa!** 🚀
---
**Cần hỗ trợ?** Đăng ký **hỗ trợ kỹ thuật** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với chúng tôi qua **LINE/Telegram** để được tư vấn chi tiết!