---
title: "🤖 **Hệ Thống Sàng Lọc & Đánh Giá CV Tự Động với AI Gemini, Google Sheets & Drive – Giải Pháp HR Không Code**"
description: "Tự động hóa toàn bộ quy trình sàng lọc CV bằng AI, trích xuất thông tin chi tiết từ CV, so sánh với yêu cầu công việc từ Google Sheets, và lưu kết quả đánh giá để HR dễ dàng review. Giúp tiết kiệm thời gian lên đến 80% so với phương pháp thủ công."
slug: "he-thong-sang-loc-danh-gia-cv-tu-dong-voi-gemini-google-sheets"
tags: [n8n, automation, hr, ai-summarization, google-sheets, google-drive, gemini-ai, no-code]
keywords: [tự động hóa sàng lọc cv, ai đánh giá cv, n8n workflow hr, google sheets + gemini ai, tự động hóa tuyển dụng không code]
---

# 🚀 **Hệ Thống Sàng Lọc CV Tự Động với AI Gemini, Google Sheets & Drive – Giải Pháp HR Không Code**

### **🔍 Nỗi Đau Của Các Sếp Trong Quy Trình Tuyển Dụng**
Mỗi ngày, bộ phận HR phải xử lý **trăm đến nghìn CV** để tìm kiếm ứng viên phù hợp. Quy trình thủ công không chỉ tốn **thời gian dài** (thậm chí mất hàng tuần) mà còn dễ bị **chủ quan** khi đánh giá. Các sếp thường gặp phải:
- **Thời gian chậm**: Phải đọc từng CV một, so sánh với yêu cầu công việc.
- **Chất lượng đánh giá thấp**: Dễ bị ảnh hưởng bởi ấn tượng đầu tiên hoặc thông tin không liên quan.
- **Không thống nhất**: Mỗi người đánh giá có tiêu chí khác nhau, dẫn đến kết quả không nhất quán.
- **Không lưu trữ dữ liệu**: Thông tin đánh giá bị mất hoặc khó theo dõi sau này.

**Giải pháp này giúp các sếp:**
✅ **Tự động hóa 100% quy trình** – Không cần viết code, chỉ cần cài đặt và chạy.
✅ **Đánh giá khách quan** – AI Gemini phân tích CV theo tiêu chí chính xác từ Google Sheets.
✅ **Tiết kiệm thời gian** – Giảm thiểu công việc thủ công xuống **chỉ 20%** so với trước.
✅ **Lưu trữ và theo dõi dễ dàng** – Kết quả được ghi vào Google Sheets và Drive, dễ dàng review sau này.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm thiểu thời gian sàng lọc CV từ **70% xuống chỉ 30%**.
- **Đánh giá chính xác**: AI so sánh ứng viên với yêu cầu công việc theo tiêu chí **cụ thể và khách quan**.
- **Lưu trữ tự động**: CV và kết quả đánh giá được **ghi vào Google Drive và Sheets**, dễ dàng chia sẻ với team.
- **Cá nhân hóa**: Hệ thống cung cấp **báo cáo chi tiết** về phù hợp của ứng viên với từng vị trí.
- **Hoạt động 24/7**: Workflow chạy liên tục, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google** (với quyền quản lý **Google Sheets** và **Google Drive**).
2. **API Key Google Gemini** (miễn phí từ [Google AI Studio](https://makersuite.google.com/)).
3. **Google Sheets** với **2 bảng dữ liệu**:
   - **Bảng "Job Roles"**: Cột `Role` (tên vị trí) và `Profile Wanted` (yêu cầu kỹ năng, kinh nghiệm).
   - **Bảng "Candidate Evaluation"**: Cột `Candidate Name`, `Score`, `Summary`, `Recommendation`.
4. **Google Drive** để lưu trữ CV được upload.
5. **Form Submission** (có thể là Google Form, Typeform, hoặc form tùy chỉnh).
6. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo **privacy và ổn định**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/5453) (hoặc sao chép từ link trên).
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file `.json`.

:::note[Lưu ý]
- **Không dùng phiên bản cloud** của n8n (n8n.io) vì **không hỗ trợ Google Drive API** và **không bảo mật**.
- **Cài n8n trên VPS** để workflow chạy **24/7** mà không bị gián đoạn.
:::

#### **2. Các Bước Cấu Hình Quan Trọng (BẮT BUỘC Chỉnh)**
Workflows này gồm **13 node**, nhưng các sếp chỉ cần chú ý đến **các node sau**:

##### **📌 Node 1: "On form submission" (formTrigger)**
- **Cấu hình**:
  - Chọn **Google Form** hoặc **form tùy chỉnh** (nếu dùng Typeform, cần cấu hình Webhook).
  - **Lưu ý**: Nếu dùng form ngoài Google, cần **cấu hình Webhook** để nhận dữ liệu.

##### **📌 Node 2: "Extract from File" (extractFromFile)**
- **Cấu hình**:
  - **Operation**: Chọn `pdf` (nếu CV là PDF) hoặc `docx` (nếu là Word).
  - **Credentials**: Không cần, chỉ cần **upload file** từ form.

##### **📌 Node 3 & 4: "Qualifications" & "Personal Data" (informationExtractor)**
- **Cấu hình**:
  - **Prompt**: AI sẽ tự động trích xuất thông tin từ CV (không cần chỉnh sửa).
  - **Lưu ý**: Nếu muốn **cải thiện độ chính xác**, các sếp có thể **tùy chỉnh prompt** trong node `informationExtractor`.

##### **📌 Node 5: "Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Cấu hình**:
  - **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước khi import).
  - **API Key**: Nhập **API Key Google Gemini** (miễn phí từ [Google AI Studio](https://makersuite.google.com/)).
  - **Model**: Chọn `gemini-pro` (mô hình mạnh nhất hiện nay).

##### **📌 Node 6 & 7: "Summarization Chain" & "HR Expert" (chainSummarization & chainLlm)**
- **Cấu hình**:
  - **Prompt**: AI sẽ **tóm tắt CV** và **đánh giá phù hợp** với yêu cầu công việc.
  - **Lưu ý**: Nếu muốn **tùy chỉnh tiêu chí đánh giá**, các sếp cần chỉnh sửa **prompt** trong node `chainLlm`.

##### **📌 Node 8 & 9: "Google Sheets" (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Operation**: Chọn `append` (thêm dữ liệu mới vào bảng).
  - **Sheet Name**:
    - `Job Roles` (để lưu yêu cầu công việc).
    - `Candidate Evaluation` (để lưu kết quả đánh giá).
  - **Range**: Chọn `A1:D1000` (hoặc tùy chỉnh theo số lượng dữ liệu).

##### **📌 Node 10: "Upload CV" (googleDrive)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder**: Chọn **thư mục lưu CV** trong Google Drive.
  - **File Name**: Tự động đặt tên theo `Candidate Name + Date`.

##### **📌 Node 11 & 12: "Merge" (merge)**
- **Cấu hình**:
  - **Liên kết dữ liệu** giữa các node (không cần chỉnh sửa, n8n tự động merge).

##### **📌 Node 13: "Structured Output Parser" (outputParserStructured)**
- **Cấu hình**:
  - **Schema**: AI sẽ **định dạng kết quả** thành JSON (không cần chỉnh sửa).

---

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**: Nhấn **Run Workflow** với **dữ liệu mẫu** (CV PDF/Word) để kiểm tra.
- **Active Workflow**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi có CV mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo tự động**:
   - Kết hợp với **Slack/Telegram** để thông báo khi có **candidate phù hợp**.
   - **Cách làm**: Thêm node `slack` hoặc `telegram` sau node `googleSheets`.

2. **Lưu log hoạt động**:
   - Sử dụng **Google Sheets Logging** để ghi lại **lịch sử hoạt động** của workflow.
   - **Cách làm**: Thêm node `googleSheets` mới để ghi log.

3. **Báo cáo định kỳ**:
   - Tự động gửi **báo cáo tổng hợp** về số lượng CV, tỷ lệ phù hợp, và ứng viên top.
   - **Cách làm**: Sử dụng **n8n Scheduler** để chạy workflow hàng tuần.

4. **Dịch vụ đa ngôn ngữ**:
   - Nếu công ty tuyển dụng quốc tế, thêm **node translation** (ví dụ: `deepL` hoặc `Google Translate`) để dịch CV.

5. **Kết hợp với CRM**:
   - Lưu kết quả vào **HubSpot, Salesforce** hoặc **Airtable** để quản lý ứng viên.
   - **Cách làm**: Thêm node `hubspot` hoặc `airtable` sau node `googleSheets`.
:::

---

### 📌 **Kết Luận**
Hệ thống **sàng lọc CV tự động với AI Gemini** không chỉ **giải phóng thời gian** cho bộ phận HR mà còn **tăng chất lượng tuyển dụng** với tiêu chí đánh giá **khách quan và nhất quán**. Các sếp không cần **viết code** hay **hiểu sâu về AI**, chỉ cần **cài đặt và chạy** là có thể tự động hóa **tất cả quy trình tuyển dụng** trong vài phút.

**🚀 Hãy thử ngay và tiết kiệm thời gian cho team HR của mình!**

---
:::tip[CHÚC MỪNG]
- **Đã có hệ thống tự động hóa tuyển dụng** – không cần lo lắng về việc đọc CV thủ công nữa!
- **AI Gemini đánh giá chính xác** – giảm thiểu sai sót so với phương pháp truyền thống.
- **Lưu trữ và theo dõi dễ dàng** – tất cả kết quả đều được ghi vào Google Sheets và Drive.
:::

---
:::info[CHÚ Ý CUỐI CUNG]
- **Nếu gặp khó khăn trong quá trình cài đặt**, các sếp có thể liên hệ với tác giả:
  - **Email**: [tharwat.elsayed2000@gmail.com](mailto:tharwat.elsayed2000@gmail.com)
  - **WhatsApp**: [+20106 180 3236](tel:+201061803236)
- **Để workflow chạy ổn định**, các sếp nên **cài n8n trên VPS** (không dùng phiên bản cloud).
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::