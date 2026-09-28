---
title: "📄 [Tự Động Chuyển Đổi Batch PDF → Markdown Siêu Nhanh Với AI + Google Drive (Không Cần Code)]"
description: "Workflow tự động hóa chuyển đổi hàng loạt file PDF thành Markdown bằng trí tuệ nhân tạo (LLM) từ PDF Vector, lưu kết quả lên Google Drive và thông báo kết quả qua Slack. Giúp tiết kiệm thời gian lên đến 90% cho việc xử lý tài liệu kỹ thuật, báo cáo, hoặc nội dung dài."
slug: "tieu-dong-chuyen-doi-batch-pdf-den-markdown"
tags: [n8n, automation, pdf-to-markdown, google-drive, ai-llm, content-creation, no-code]
keywords: [n8n workflow pdf markdown, tự động hóa chuyển đổi pdf, pdf vector n8n, lưu file markdown google drive, ai chuyển đổi tài liệu]
---

# 🚀 **Tự Động Chuyển Đổi Batch PDF → Markdown Với AI + Google Drive (Không Cần Code)**

### **🔍 Nỗi Đau Của Các Sếp Khi Xử Lý Tài Liệu PDF**
Các sếp thường phải mất **giờ đồng hồ** để chuyển đổi hàng loạt file PDF thành định dạng Markdown (vì sao?):
- **Tài liệu kỹ thuật** (sách, báo cáo, nghiên cứu) cần được chuyển sang Markdown để dễ dàng chỉnh sửa, chia sẻ hoặc tích hợp vào trang web.
- **Báo cáo định kỳ** (quyết định, thống kê) phải được chuyển đổi để dễ dàng phân tích dữ liệu.
- **Nội dung dài** (sách, bài giảng) cần được chuyển sang Markdown để tối ưu SEO hoặc tạo nội dung blog.

**Giải pháp?** Một **workflow tự động hóa 100% không code** sử dụng **trí tuệ nhân tạo (LLM)** để:
✅ **Chuyển đổi PDF → Markdown** với độ chính xác cao.
✅ **Lưu kết quả tự động** lên Google Drive.
✅ **Thông báo kết quả** qua Slack (hoặc Telegram, Email).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho PDF Vector)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
- **Chuyển đổi chính xác** nhờ trí tuệ nhân tạo (LLM) từ **PDF Vector** (độ chính xác cao hơn so với OCR truyền thống).
- **Lưu trữ tự động** lên Google Drive, dễ dàng chia sẻ hoặc tích hợp vào CMS.
- **Thông báo kết quả** qua Slack (hoặc Email/Telegram) để theo dõi tiến trình.
- **Hoạt động liên tục** mà không cần can thiệp, thậm chí khi các sếp **ngủ ngon**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lấy danh sách PDF và lưu Markdown).
✔ **API Key của PDF Vector** (miễn phí cho 1000 request/tháng, [đăng ký tại đây](https://pdfvector.com/)).
✔ **Credentials Slack** (để nhận thông báo kết quả).
✔ **Folder Google Drive** để lưu file Markdown (cần chia sẻ cho n8n).

---
:::note[Lưu ý quan trọng]
- **PDF Vector** hỗ trợ **chuyển đổi từ URL, Google Drive, Dropbox hoặc file local**.
- **Workflow này chỉ hoạt động với file PDF** (không hỗ trợ DOCX, PPT, JPG).
- **Nếu sử dụng Google Drive**, cần **chia sẻ folder** cho n8n để có quyền đọc/thêm file.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/7355](https://n8n.io/workflows/7355) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **dán vào n8n Editor** (tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **7 node chính**, các sếp cần **cấu hình kỹ** các phần sau:

##### **🔹 Node 1: Google Drive - List PDFs**
- **Chọn credentials**: Tạo mới hoặc chọn **Google Drive OAuth 2.0** đã có.
- **Folder để lấy PDF**: Chọn **folder chứa file PDF** (nên là folder có quyền chia sẻ cho n8n).
- **Lọc file**: Workflow sẽ tự động **lọc chỉ file PDF** (không cần cấu hình thêm).

##### **🔹 Node 2: PDF Vector - Convert to Markdown**
- **Chọn credentials**: Tạo mới **PDF Vector API Key** (đăng ký tại [pdfvector.com](https://pdfvector.com/)).
- **Operation**: Đặt là **"parse"** (chuyển đổi PDF thành Markdown).
- **Resource**: Đặt là **"document"** (chuyển đổi từ file PDF).
- **Lưu ý**:
  - Nếu file PDF **có nhiều trang**, PDF Vector sẽ **tự động chia thành các phần** và lưu thành nhiều file Markdown.
  - **Không cần cấu hình thêm** nếu muốn sử dụng mặc định.

##### **🔹 Node 3: Prepare Output (Code Node)**
- **Không cần chỉnh sửa** (n8n tự động chuẩn bị dữ liệu cho node sau).
- **Nếu muốn tùy chỉnh**, các sếp có thể mở node này và **sửa logic** (ví dụ: thêm prefix/suffix cho tên file).

##### **🔹 Node 4: Save Markdown Files (Google Drive Upload)**
- **Chọn credentials**: Sử dụng **Google Drive OAuth 2.0** cùng node 1.
- **Folder để lưu**: Chọn **folder muốn lưu Markdown** (nên là folder khác với folder lấy PDF).
- **Tên file**: Workflow sẽ **tự động đặt tên** theo định dạng:
  ```
  {tên_file_original}.md
  ```
  (Ví dụ: `báo_cáo_2024.pdf` → `báo_cáo_2024.md`).

##### **🔹 Node 5: Conversion Summary (Set Node)**
- **Không cần chỉnh sửa** (n8n tự động tổng hợp số lượng file đã chuyển đổi).

##### **🔹 Node 6: Send Notification (Slack)**
- **Chọn credentials**: Tạo mới **Slack Webhook** (tạo tại [api.slack.com/apps](https://api.slack.com/apps)).
- **Message**: Workflow sẽ gửi **tin nhắn thông báo** như:
  ```
  🚀 **Bulk PDF to Markdown Conversion Complete!**
  - Total PDFs processed: 5
  - Total Markdown files saved: 5
  - Check Google Drive folder: [LINK]
  ```

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy **test run** với **1-2 file PDF** để kiểm tra kết quả.
- **Bật Active**: Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Telegram/Email**:
   - Thay vì Slack, các sếp có thể **thêm node Email** (n8n-nodes-base.email) hoặc **Telegram Bot** (n8n-nodes-base.telegram) để nhận thông báo.

2. **Lưu Log Lịch Sử**:
   - Thêm **node Sticky Note** (n8n-nodes-base.stickyNote) để ghi lại **lịch sử chuyển đổi** (ngày giờ, số file, tên file).

3. **Chuyển Đổi Từ URL**:
   - Nếu các sếp muốn **chuyển đổi từ URL** (không phải Google Drive), thay node **Google Drive List** bằng **HTTP Request** (n8n-nodes-base.http) để lấy danh sách URL PDF.

4. **Tự Động Chuyển Đổi Định Kỳ**:
   - Sử dụng **node Schedule** (n8n-nodes-base.schedule) để **chạy workflow hàng ngày/tuần** (ví dụ: chuyển đổi tất cả PDF mới trong Google Drive).

5. **Tối Ưu Hiệu Suất**:
   - Nếu chuyển đổi **hàng trăm file**, các sếp nên **tăng RAM VPS** (4GB+ để tránh lag).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nhiệt nhọc chuyển đổi PDF → Markdown**, đồng thời **tự động hóa toàn bộ quy trình** với độ chính xác cao nhờ **AI từ PDF Vector**.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình Google Drive, PDF Vector và Slack**.
3. **Bật Active** và **nghỉ ngơi** trong khi n8n làm việc!

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ [PDF Vector](https://pdfvector.com/) để biết thêm chi tiết về API!

---
**#TựĐộngHóa #N8N #PDFtoMarkdown #AIContentCreation #NoCodeAutomation**