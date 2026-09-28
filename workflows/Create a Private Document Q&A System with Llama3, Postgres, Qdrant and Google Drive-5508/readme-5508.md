---
title: "🤖 Hệ Thống Trả Lời Câu Hỏi Tự Động Cho Tài Liệu Nội Bộ (RAG + Llama3 + Qdrant) - Tự Động Hóa Wiki Doanh Nghiệp"
description: "Workflow tự động hóa hoàn toàn để tạo hệ thống trả lời câu hỏi thông minh cho tài liệu nội bộ từ Google Drive, sử dụng Llama3, Qdrant và Postgres. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin, tăng độ chính xác và cá nhân hóa hỗ trợ cho đội ngũ."
slug: "he-thong-qa-llama3-qdrant-google-drive"
tags: [n8n, automation, ai-rag, llama3, qdrant, google-drive, no-code, ai-agent]
keywords: [n8n workflow tự động hóa, hệ thống trả lời câu hỏi AI, RAG với Llama3, tự động hóa wiki nội bộ, vector database Qdrant, Ollama API]
---

# 🚀 **Tạo Hệ Thống Trả Lời Câu Hỏi Tự Động Cho Tài Liệu Nội Bộ (RAG + Llama3 + Qdrant)**

## **🔍 Nỗi Đau Của Các Sếp Khi Tìm Kiếm Thông Tin Nội Bộ**
Hiện nay, nhiều doanh nghiệp phải đối mặt với những thách thức sau khi làm việc với tài liệu nội bộ:
- **Tốn thời gian**: Tìm kiếm thông tin trong hàng trăm tài liệu PDF, Word hay Google Docs thủ công.
- **Không chính xác**: Thông tin phân tán, dễ bị lỗi hoặc lỗi thời.
- **Không cá nhân hóa**: Trả lời câu hỏi chung chung, không phù hợp với ngữ cảnh cụ thể của từng người dùng.
- **Không cập nhật tự động**: Khi tài liệu mới được thêm hoặc sửa, hệ thống không tự động đồng bộ.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** việc xây dựng và cập nhật hệ thống trả lời câu hỏi (RAG) từ Google Drive.
✅ **Sử dụng Llama3** (mô hình AI tiên tiến) để trả lời chính xác và logic.
✅ **Qdrant** (vector database) để lưu trữ và tìm kiếm thông tin một cách hiệu quả.
✅ **Postgres** để lưu trữ lịch sử trò chuyện và nhớ ngữ cảnh.
✅ **Cập nhật tự động** khi tài liệu mới được thêm hoặc sửa trên Google Drive.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công, AI trả lời ngay lập tức.
- **Chính xác cao**: Dựa trên kiến thức từ tài liệu chính thức, không sai lệch.
- **Cá nhân hóa**: Nhớ ngữ cảnh trò chuyện qua các lần tương tác.
- **Hoạt động 24/7**: Hệ thống tự động cập nhật và hoạt động liên tục.
- **Dễ dàng mở rộng**: Thêm tài liệu mới mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Drive OAuth 2.0**: Để truy cập và tải tài liệu từ Google Drive.
   - **Ollama API**: Để sử dụng mô hình Llama3.2 (cài đặt Ollama trên máy chủ hoặc máy chủ cloud).
   - **Qdrant API**: Để lưu trữ và tìm kiếm vector embeddings.
   - **PostgreSQL**: Để lưu trữ lịch sử trò chuyện và nhớ ngữ cảnh.

2. **Dữ liệu đầu vào**:
   - Một **thư mục Google Drive** chứa tất cả tài liệu cần xây dựng hệ thống Q&A (PDF, Word, Text,...).
   - **Mô hình Llama3.2** đã được cài đặt trên Ollama (cần cài đặt trước trên máy chủ).

3. **Hệ thống hosting**:
   - **n8n Self-hosted** (không dùng phiên bản cloud) để workflow hoạt động 24/7.

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow này có **17 node** và được chia thành **3 phần chính**:
- **Local RAG AI Agent** (trả lời câu hỏi bằng Llama3).
- **Qdrant Vector Store** (lưu trữ và tìm kiếm embeddings).
- **Workflow tự động từ Google Drive** (tải và cập nhật tài liệu).

#### **Bước 1: Tải workflow từ n8n.io**
1. Truy cập [workflow gốc](https://n8n.io/workflows/5508).
2. Nhấp vào **"Import"** để tải file JSON.
3. Trong n8n Editor, chọn **"Import"** và chọn file JSON vừa tải.

#### **Bước 2: Import từ JSON (nếu copy/paste)**
Nếu muốn copy/paste JSON:
1. Mở n8n Editor và chọn **"Import"** > **"Paste JSON"**.
2. Dán toàn bộ JSON từ [tại đây](https://n8n.io/workflows/5508) (hoặc file JSON đã tải).
3. Nhấp **"Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Google Drive Trigger (File Created/Updated)**
- **Mục đích**: Khi có file mới hoặc file được sửa trên Google Drive, workflow sẽ tự động kích hoạt.
- **Cấu hình**:
  - Chọn **thư mục Google Drive** chứa tài liệu cần xử lý.
  - Chọn **loại file** (PDF, DOCX, TXT,...) cần theo dõi.
  - **Credentials**: Đảm bảo đã cấu hình `googleDriveOAuth2Api` trong n8n.

#### **🔹 Node 2: Download File & Extract Text**
- **Mục đích**: Tải file từ Google Drive và trích xuất văn bản.
- **Cấu hình**:
  - **Node "Download File"**: Đảm bảo `fileId` được truyền từ node `Set File ID`.
  - **Node "Extract Document Text"**: Chọn **operation = "text"** để trích xuất toàn bộ văn bản.

#### **🔹 Node 3: Default Data Loader & Text Splitter**
- **Mục đích**: Chia văn bản thành các chunk nhỏ để xử lý hiệu quả.
- **Cấu hình**:
  - **Node "Default Data Loader"**: Đảm bảo dữ liệu văn bản được truyền từ node `Extract Document Text`.
  - **Node "Recursive Character Text Splitter"**: Cấu hình **chunk size** phù hợp (ví dụ: 500-1000 ký tự).

#### **🔹 Node 4: Ollama Embeddings (Llama3.2)**
- **Mục đích**: Chuyển văn bản thành embeddings để lưu vào Qdrant.
- **Cấu hình**:
  - **Credentials**: Chọn `ollamaApi`.
  - **Model**: Đảm bảo chọn `llama3.2:latest`.
  - **Input**: Dữ liệu từ node `Recursive Character Text Splitter`.

#### **🔹 Node 5: Qdrant Vector Store Insert**
- **Mục đích**: Lưu embeddings vào Qdrant để tìm kiếm sau này.
- **Cấu hình**:
  - **Credentials**: Chọn `qdrantApi`.
  - **Collection Name**: Đặt tên collection (ví dụ: `company_knowledge`).
  - **Vector Size**: Đảm bảo khớp với mô hình Llama3 (768).

#### **🔹 Node 6: Chat Trigger (When chat message received)**
- **Mục đích**: Kích hoạt khi người dùng gửi câu hỏi.
- **Cấu hình**:
  - **Credentials**: Đảm bảo `ollamaApi` và `postgres` đã cấu hình.
  - **Model**: Chọn `llama3.2:latest`.

#### **🔹 Node 7: Postgres Chat Memory**
- **Mục đích**: Lưu trữ lịch sử trò chuyện để AI nhớ ngữ cảnh.
- **Cấu hình**:
  - **Credentials**: Chọn `postgres`.
  - **Table Name**: Đặt tên bảng (ví dụ: `chat_history`).

#### **🔹 Node 8: Tool Vector Store (Answer questions)**
- **Mục đích**: Tìm kiếm embeddings trong Qdrant để trả lời câu hỏi.
- **Cấu hình**:
  - **Credentials**: Chọn `qdrantApi`.
  - **Collection Name**: Khớp với collection đã tạo ở Node 5.

#### **🔹 Node 9: AI Agent (Llama3)**
- **Mục đích**: Trả lời câu hỏi bằng Llama3, kết hợp với vector store.
- **Cấu hình**:
  - **Model**: `llama3.2:latest`.
  - **Input**: Dữ liệu từ node `Tool Vector Store`.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **node "When chat message received"** và nhấp **"Run Workflow"**.
   - Gửi một câu hỏi mẫu (ví dụ: *"Tôi muốn biết về chính sách mới của công ty?"*).
   - Kiểm tra kết quả trả lời.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Slack/Telegram**
- Sử dụng **node Slack Webhook** hoặc **Telegram Bot** để người dùng gửi câu hỏi qua Slack/Telegram.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
  - Kết nối với node `When chat message received`.

### **2. Lưu Log Trò Chuyện**
- Sử dụng **node `n8n-nodes-base.telegram`** hoặc **Google Sheets** để lưu lịch sử câu hỏi và trả lời.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.googleSheets` sau node `Postgres Chat Memory`.
  - Lưu dữ liệu vào một sheet mới.

### **3. Gửi Báo Cáo Định Kỳ**
- Sử dụng **node `n8n-nodes-base.email`** hoặc **Slack Notification** để báo cáo số lượng câu hỏi được trả lời hàng ngày.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.cron` để kích hoạt hàng ngày.
  - Gửi email hoặc thông báo Slack với thống kê.

### **4. Cập Nhật Tự Động Tài Liệu**
- Nếu có nhiều tài liệu, có thể chia thành **nhiều thư mục Google Drive** và tạo **workflow riêng** cho mỗi thư mục.
- **Cách làm**:
  - Sử dụng **node `n8n-nodes-base.if`** để kiểm tra thư mục và kích hoạt workflow tương ứng.

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa hệ thống trả lời câu hỏi cho tài liệu nội bộ, giúp các sếp:
✔ **Tiết kiệm thời gian** tìm kiếm thông tin.
✔ **Tăng độ chính xác** với AI Llama3.
✔ **Cập nhật tự động** khi tài liệu thay đổi.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay workflow này và biến tài liệu nội bộ của doanh nghiệp thành một hệ thống thông minh, tự động trả lời mọi câu hỏi!** 🚀

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp khó khăn trong quá trình cấu hình, hãy liên hệ với **David Olusola** qua [david@daexai.com](mailto:david@daexai.com) để hỗ trợ.
- Để tối ưu hiệu suất, các sếp nên **optimize chunk size** và **vector dimension** phù hợp với mô hình Llama3.2.