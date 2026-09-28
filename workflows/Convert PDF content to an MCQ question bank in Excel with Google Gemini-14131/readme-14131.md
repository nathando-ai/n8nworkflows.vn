---
title: "🎓 **Tự Động Hóa Chuyển PDF Sang Trang Đề Trắc Nghiệm Excel Với AI Google Gemini (N8n)**"
description: "Workflow tự động hóa hoàn toàn không cần code chuyển đổi nội dung PDF thành cơ sở dữ liệu câu hỏi trắc nghiệm (MCQ) với đáp án và giải thích, xuất ra Excel và gửi kết quả qua Email/Telegram. Giúp giáo viên, nhà đào tạo tiết kiệm thời gian lên đến 80% trong việc tạo đề thi."
slug: "tuy-dong-hoa-chuyen-pdf-sang-trang-de-trac-nghiem-excel-voi-ai-gemini"
tags: [n8n, automation, no-code, google-gemini, ai, google-drive, telegram, email, excel, doc-extraction]
keywords: [n8n workflow pdf sang excel, tự động hóa câu hỏi trắc nghiệm, google gemini ai, convert pdf to mcq, giáo viên tự động hóa, n8n google drive, n8n telegram bot]
---

# 🎓 **Tự Động Hóa Chuyển PDF Sang Trang Đề Trắc Nghiệm Excel Với AI Google Gemini**

## 🔍 **Nỗi Đau Của Giáo Viên & Nhà Đào Tạo**
Giáo viên và nhà đào tạo thường phải tốn **giờ đồng hồ** để:
- **Tách nội dung** từ tài liệu PDF phức tạp (sách giáo khoa, bài giảng, tài liệu nghiên cứu).
- **Tạo câu hỏi trắc nghiệm** (MCQ) từ nội dung dài, đảm bảo độ chính xác và đa dạng.
- **Sắp xếp đáp án** và **giải thích** cho từng câu hỏi.
- **Xuất dữ liệu** sang Excel để quản lý và chia sẻ với học viên.

**Kết quả?** Thời gian và năng lượng bị "chôn vùi" trong công việc thủ công, trong khi AI có thể **tự động hóa 80% quá trình này** chỉ với một cú nhấp chuột!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Đảm bảo độ chính xác cao** nhờ AI Google Gemini phân tích và tạo câu hỏi logic.
✅ **Xuất dữ liệu sang Excel** với cấu trúc chuẩn (câu hỏi, đáp án, giải thích).
✅ **Gửi kết quả tự động** qua **Email** hoặc **Telegram** cho học viên/đội ngũ.
✅ **Lưu trữ an toàn** trên **Google Drive** với quyền truy cập dễ dàng.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys:**
- **Google Gemini API Key** (để sử dụng AI tạo câu hỏi).
- **Google Drive OAuth 2.0** (để upload file Excel).
- **SMTP hoặc Gmail** (để gửi Email tự động).
- **Telegram Bot Token** (để gửi file qua Telegram, *nếu cần*).

📌 **File PDF đầu vào:**
- Kích thước **không quá 5MB** (do giới hạn của workflow).
- Nội dung **phù hợp** với mục đích tạo câu hỏi (ví dụ: sách giáo khoa, bài giảng).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/14131](https://n8n.io/workflows/14131) và import vào **n8n Editor**.
- **Copy/Paste** JSON từ file vào **n8n** (đảm bảo không có lỗi syntax).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần **cấu hình kỹ** các phần sau:

##### **🔹 Node "Webhook" (Nhận File PDF)**
- **Path:** `06f418df-1e24-45a9-87dd-7e67e3274633` (không thay đổi).
- **HTTP Method:** `POST`.
- **Lưu ý:** Đảm bảo **file PDF** được gửi cùng với **email** (nếu muốn gửi kết quả qua Email) và **telegram_chat_id** (nếu muốn gửi qua Telegram).

##### **🔹 Node "Extract from File" (Trích Xuất Text từ PDF)**
- **Operation:** `pdf` (không cần thay đổi).
- **Lưu ý:** Nếu PDF có **bảng biểu** hoặc **hình ảnh**, hiệu quả trích xuất có thể giảm. Các sếp nên **kiểm tra trước** file đầu vào.

##### **🔹 Node "Message a model" (Google Gemini AI)**
- **Credentials:** `googlePalmApi` (đã cấu hình trước khi import).
- **Prompt:** Workflow đã **cấu hình sẵn** để tạo **câu hỏi trắc nghiệm (MCQ)** từ text.
- **Lưu ý:**
  - Nếu **API Key** hết hạn, workflow sẽ **báo lỗi** và dừng lại.
  - **Tối ưu hóa Prompt** (nếu cần) bằng cách chỉnh sửa node **Code** (`Cleaner` và `Chunk`).

##### **🔹 Node "Convert to File" (Xuất Excel)**
- **Operation:** `xlsx`.
- **Lưu ý:**
  - File Excel sẽ có **cấu trúc chuẩn** với các cột:
    - `Question` (Câu hỏi)
    - `Option A` (Đáp án A)
    - `Option B` (Đáp án B)
    - `Option C` (Đáp án C)
    - `Option D` (Đáp án D)
    - `Correct Answer` (Đáp án đúng)
    - `Explanation` (Giải thích).

##### **🔹 Node "Upload file" (Google Drive)**
- **Credentials:** `googleDriveOAuth2Api`.
- **Lưu ý:**
  - File sẽ được upload vào **thư mục mặc định** của tài khoản Google Drive.
  - Các sếp có thể **cấu hình thư mục cụ thể** bằng cách chỉnh sửa node này.

##### **🔹 Node "Send email" & "Send a document" (Telegram)**
- **Email:** Sử dụng **SMTP** hoặc **Gmail** (cấu hình trước khi import).
- **Telegram:** Sử dụng **Bot Token** và **chat_id** của người nhận.
- **Lưu ý:**
  - Nếu không muốn gửi qua Telegram, **bỏ qua node này**.
  - **Kiểm tra lại địa chỉ Email** và **chat_id Telegram** để tránh lỗi gửi.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Gửi một **file PDF mẫu** (ví dụ: một trang sách giáo khoa) để kiểm tra workflow.
- **Bật Active:** Sau khi **không có lỗi**, bật workflow để hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu hóa Prompt cho Gemini:**
   - Chỉnh sửa node **Code** (`Cleaner` và `Chunk`) để **tách nội dung thành các đoạn nhỏ hơn**, giúp AI tạo câu hỏi **đơn giản và chính xác hơn**.

2. **Lưu Log & Theo Dõi:**
   - Sử dụng **Sticky Note** trong workflow để ghi lại **lịch sử chạy** và **lỗi** (nếu có).

3. **Gửi Báo Cáo Định Kỳ:**
   - Kết hợp với **Google Sheets** để **lưu trữ tất cả đề thi** và **theo dõi tiến độ**.

4. **Tích Hợp Slack:**
   - Thay vì Telegram, các sếp có thể **gửi kết quả qua Slack** bằng cách thêm node **Slack Webhook**.

5. **Xử Lý File Lớn:**
   - Nếu PDF **lớn hơn 5MB**, các sếp có thể **tách file** trước khi gửi vào workflow.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho giáo viên, nhà đào tạo và content creator muốn **tự động hóa việc tạo đề thi** mà không cần viết code. Với **Google Gemini**, AI sẽ **phân tích và tạo câu hỏi logic**, trong khi **n8n** đảm bảo **tất cả quá trình chạy tự động** từ trích xuất PDF đến xuất Excel và gửi kết quả.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các API Key** và **tài khoản** cần thiết.
3. **Test với một file PDF** và **nhận kết quả trong vòng vài giây!**

🚀 **Tiết kiệm thời gian, nâng cao hiệu quả giảng dạy – chỉ với một cú nhấp chuột!**