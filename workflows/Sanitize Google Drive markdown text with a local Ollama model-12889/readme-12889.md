---
title: "🔍 **Tự Động Xóa Thông Tin Cá Nhân (PII) Trong Tệp Markdown Google Drive Với Ollama Local AI**"
description: "Workflow tự động hóa hoàn toàn không cần code để quét, phân tích và xóa thông tin cá nhân (PII) trong các tài liệu Markdown trên Google Drive, sử dụng mô hình AI Ollama 3.1 cài đặt trên máy chủ riêng. Giúp các sếp bảo mật dữ liệu trước khi chia sẻ hoặc xử lý với các mô hình LLM công khai."
slug: "tieu-doi-thong-tin-pii-trong-markdown-google-drive-ollama"
tags: [n8n, automation, no-code, ai-summarization, google-drive, ollama, pii-redaction, self-hosted]
keywords: [n8n workflow google drive, xóa thông tin cá nhân tự động, ollama n8n, bảo mật dữ liệu markdown, tự động hóa xử lý văn bản, mô hình AI local]
---

# 🚀 **Tự Động Xóa Thông Tin Cá Nhân (PII) Trong Tệp Markdown Google Drive Với Ollama Local AI**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải xử lý hàng loạt tài liệu Markdown chứa thông tin nhạy cảm như số điện thoại, địa chỉ email cá nhân, hoặc mã số bảo hiểm xã hội trong Google Drive. Khi chia sẻ hoặc xử lý dữ liệu này với các mô hình LLM công khai (chẳng hạn như ChatGPT), rủi ro bị rò rỉ thông tin cá nhân (PII) là rất cao. **Làm thủ công không chỉ tốn thời gian mà còn dễ gây lỗi và vi phạm bảo mật.**

Workflow này **giải quyết vấn đề đó bằng cách tự động quét, phân tích và xóa thông tin nhạy cảm** trong các tệp Markdown, đồng thời lưu kết quả đã được "sạch hóa" lại vào Google Drive. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 với hiệu suất tối ưu, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) với Ollama chạy cục bộ.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ để chạy n8n + Ollama 3.1)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối**: Xóa tự động tất cả thông tin cá nhân (PII) trong Markdown trước khi chia sẻ.
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công từng tệp.
- **Hoạt động liên tục**: Workflow chạy tự động khi có tệp mới được thêm vào Google Drive.
- **Kết quả sạch sẽ**: Tệp Markdown đã được "sạch hóa" được lưu lại với tên mới (ví dụ: `tên_tệp_cleaned.md`).
- **Dữ liệu theo dõi**: (Tùy chọn) Ghi log vào Google Sheets để biết tệp nào có PII và đã được xử lý như thế nào.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền truy cập vào thư mục chứa tệp Markdown cần xử lý.
2. **Credentials OAuth 2.0 cho Google Drive** (cấu hình trong n8n).
3. **Credentials OAuth 2.0 cho Google Sheets** (nếu muốn ghi log).
4. **Mô hình Ollama 3.1** đã cài đặt trên máy chủ n8n (cập nhật bằng lệnh `ollama pull llama3.1`).
5. **Thư mục Google Drive** được cấu hình để **n8n có thể theo dõi sự kiện tạo thư mục mới** (để workflow kích hoạt).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không hoạt động** nếu không có mô hình Ollama 3.1 cài đặt.
- Các tệp Markdown phải nằm trong **thư mục con** mới được tạo trong Google Drive để workflow kích hoạt.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/12889](https://n8n.io/workflows/12889).
2. Trong n8n Dashboard, nhấn **"Import"** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **"Import from JSON"** trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình **các node quan trọng** như sau:

##### **A. Cấu Hình Google Drive Trigger (`on_subfolder_created`)**
- **Credentials**: Chọn `"googleDriveOAuth2Api"` (đã cấu hình trước).
- **Folder ID**: Điền **ID của thư mục cha** chứa các thư mục con mới được tạo (để workflow kích hoạt).
  *Lấy ID thư mục từ liên kết Google Drive (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp` → `1AbCdEfGhIjKlMnOp`).
- **Event Type**: Chọn **"folder.create"** để theo dõi khi có thư mục mới được tạo.

##### **B. Cấu Hình Ollama Model (`Ollama Model`)**
- **Credentials**: Chọn `"ollamaApi"` (n8n sẽ tự động kết nối đến Ollama chạy cục bộ).
- **Model**: Đảm bảo chọn `"llama3.1:latest"` (đã cài đặt trước).
- **Prompt**: Workflow đã cấu hình sẵn prompt để Ollama phát hiện PII. Các sếp có thể **tùy chỉnh** ở node `Basic LLM Chain` (node `chainLlm`) nếu cần thêm loại PII mới.

##### **C. Cấu Hình Google Sheets (Tùy Chọn - `log_text_with_pii_flag`)**
- **Credentials**: Chọn `"googleSheetsOAuth2Api"`.
- **Sheet Name**: Điền tên **Google Sheet** để ghi log (ví dụ: `"Chunk_Logs"`).
- **Range**: Điền `"A1"` (để ghi từ ô A1).
- **Headers**: Bật để tự động tạo tiêu đề cột (`"Chunk Text"`, `"Has PII"`).

##### **D. Node `chunk_text_for_local_llm` (Code)**
- Workflow đã cấu hình sẵn **lógica chia text thành chunks** (mỗi chunk ~500 từ) để Ollama xử lý hiệu quả.
- **Không cần chỉnh sửa** trừ khi các sếp muốn thay đổi kích thước chunk.

##### **E. Node `create_cleaned_text_file`**
- **File Name**: Workflow sẽ tự động đặt tên tệp mới là `"[tên_gốc]_cleaned.md"` (ví dụ: `draft_cleaned.md`).
- **Folder ID**: Chọn **thư mục con mới** (đã được tạo bởi trigger) để lưu tệp đã xử lý.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một tệp Markdown mẫu:
   - Tạo một **thư mục con mới** trong Google Drive (đã cấu hình trong trigger).
   - Đặt một tệp Markdown vào thư mục đó (ví dụ: `test.md` chứa thông tin như `Email: tobi@example.com`).
   - Chạy workflow và kiểm tra:
     - Tệp `test_cleaned.md` đã được tạo trong thư mục con.
     - Nếu có PII, nó sẽ được xóa; nếu không, tệp giữ nguyên.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Prompt Ollama**:
   - Mở node `Basic LLM Chain` và chỉnh sửa **prompt** để Ollama phát hiện thêm loại PII (ví dụ: số điện thoại quốc tế, mã số thuế).
   - Ví dụ:
     ```json
     "prompt": "You are a PII redaction expert. Your task is to identify and redact the following sensitive information in the text: emails, phone numbers, national IDs, and credit card numbers. Return the cleaned text in JSON format with a 'has_pii' flag. Example: {{ 'has_pii': true, 'cleaned_text': '...' }}"
     ```

2. **Ghi Log Chi Tiết**:
   - Sử dụng Google Sheets để **theo dõi tất cả các tệp** đã được xử lý, bao gồm:
     - Tên tệp gốc.
     - Ngày giờ xử lý.
     - Có PII không.
     - Link tệp đã sạch.

3. **Kết Hợp Với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để **báo cáo kết quả** khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Tệp [tên] đã được sạch hóa thành công! [Link]"` khi tệp đã được xử lý.

4. **Xử Lý Nhiều Loại File**:
   - Thay đổi node `select_markdown_files` (node `filter`) để **lọc các loại file khác** (ví dụ: `.txt`, `.docx`) bằng cách chỉnh sửa điều kiện:
     ```json
     "$.mimeType": "text/markdown"
     ```
     → Thay thành:
     ```json
     "$.name.endsWith('.txt')"
     ```

5. **Lưu Trữ Tệp Gốc**:
   - Thêm node `googleDrive` với **operation: "copy"** để sao lưu tệp gốc vào thư mục khác trước khi xóa PII.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc thủ công bảo mật dữ liệu, đồng thời **giảm thiểu rủi ro vi phạm bảo mật** khi chia sẻ tài liệu với các mô hình AI công khai. **Chỉ cần import, cấu hình credentials và kích hoạt – không cần kỹ năng code!**

**Hành động ngay hôm nay:**
1. Cài đặt n8n + Ollama trên VPS (dùng mã giảm giá **VPSN8N**).
2. Import workflow và cấu hình Google Drive.
3. Test với một tệp Markdown mẫu và **bắt đầu tự động hóa bảo mật dữ liệu!**

---
**💡 Cần hỗ trợ?**
- Trên [n8n Community](https://community.n8n.io/) hoặc [Discord n8n](https://discord.gg/n8n).
- Liên hệ với TinoHost/BNIX để hỗ trợ cài đặt VPS n8n + Ollama.