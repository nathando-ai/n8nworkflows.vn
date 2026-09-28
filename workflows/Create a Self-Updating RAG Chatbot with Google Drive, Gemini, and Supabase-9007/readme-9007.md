---
title: "🤖 Tự Động Hóa AI Chatbot RAG Cập Nhật Tự Động với Google Drive, Gemini & Supabase - Khóa Chìa Cho Content Marketing & Trí Tuệ Nhân Tạo"
description: "Workflow này tự động xây dựng và cập nhật một AI Chatbot RAG (Retrieval-Augmented Generation) dựa trên tài liệu trong Google Drive, kết hợp với Gemini AI và Supabase để trả lời câu hỏi chính xác, tự động đồng bộ khi có thay đổi file mới/được cập nhật. Giúp các sếp tiết kiệm 100% thời gian nghiên cứu và trả lời khách hàng."
slug: "tieu-dong-hoa-chatbot-rag-google-drive-gemini-supabase"
tags: [n8n, automation, no-code, ai-chatbot, content-creation, google-drive, supabase, google-gemini, langchain, retrieval-augmented-generation]
keywords: [n8n workflow chatbot RAG, tự động hóa AI trả lời câu hỏi, đồng bộ Google Drive với Supabase, Gemini API tự động cập nhật, chatbot dựa trên tài liệu, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa AI Chatbot RAG Cập Nhật Tự Động với Google Drive, Gemini & Supabase**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa 100% Không Code**
Hiện nay, khi các sếp phải trả lời hàng trăm câu hỏi liên quan đến tài liệu nội bộ (bao gồm hợp đồng, báo cáo, tài liệu pháp lý, hoặc kiến thức chuyên ngành), việc này thường tốn thời gian và dễ gây sai sót. Thậm chí, khi tài liệu được cập nhật, các sếp phải **tìm kiếm và cập nhật thủ công** để đảm bảo thông tin mới nhất.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động xây dựng một AI Chatbot RAG** dựa trên tất cả tài liệu trong Google Drive (PDF/Doc).
✅ **Cập nhật tự động** khi có file mới, file được chỉnh sửa hoặc xóa.
✅ **Trả lời câu hỏi chính xác** bằng Gemini AI, kết hợp với cơ sở dữ liệu vector Supabase.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu tài liệu thủ công, AI trả lời ngay lập tức.
- **Chính xác 100%**: Dữ liệu luôn cập nhật từ Google Drive, không sai sót như con người.
- **Cá nhân hóa**: AI hiểu ngữ cảnh và trả lời dựa trên nội dung cụ thể của tài liệu.
- **Hoạt động liên tục**: Cập nhật tự động khi có thay đổi file, không cần restart.
- **Dễ dàng mở rộng**: Thêm tài liệu mới chỉ cần upload lên Google Drive.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Drive API** (để đọc/đồng bộ file).
   - **Supabase** (để lưu trữ vector store và metadata).
   - **PostgreSQL** (để lưu trữ bộ nhớ chat).
   - **Google Gemini API** (để xử lý RAG và trả lời câu hỏi).
   - **Cohere Reranker API** (để cải thiện chất lượng kết quả tìm kiếm).
   - **Tài khoản Cohere** (để lấy API Key của Reranker).

2. **Cấu trúc Google Drive**:
   - Một **folder cụ thể** chứa tất cả tài liệu (PDF/Doc) cần được AI phân tích.
   - **Quyền truy cập** cho n8n đọc/ghi file trong folder đó.

3. **Cấu hình Supabase**:
   - **Bảng `documents`** (lưu trữ nội dung vector).
   - **Bảng `document_metadata`** (lưu trữ metadata của file).
   - **Bảng `chat_history`** (nếu sử dụng bộ nhớ chat).
   - **Cấu hình Connection Pooling** trong Supabase (xem hướng dẫn dưới đây).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/9007](https://n8n.io/workflows/9007).
2. Trong **n8n Editor**, nhấn **"Import"** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **"Import from JSON"** trong menu.

:::note[LƯU Ý]
- **Không thay đổi cấu trúc** của workflow, chỉ cần **điền các credential** như hướng dẫn dưới đây.
- **Không xóa node** nào, trừ khi các sếp biết rõ tác dụng của nó.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Bước 1: Cấu Hình Credentials Cho Tất Cả Các Node**
Workflow sử dụng **7 loại credentials chính**, các sếp cần thiết lập như sau:

| **Node**               | **Credential Cần Thiết**       | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------|--------------------------------|----------------------------------------------------------------------------------------|
| **Google Drive**       | `Google Drive`                 | Tạo credential trong **n8n** với quyền **Read & Write** cho folder mục tiêu.          |
| **Supabase**           | `Supabase`                     | Thiết lập trong **Supabase Dashboard** > **API** > **Settings** và copy `URL` + `Key`.   |
| **PostgreSQL**         | `Postgres`                     | Cấu hình trong **Supabase** > **Connection Pooling** (chọn `Transaction` pooler).      |
| **Google Gemini**      | `Google Gemini API Key`        | Mở [Google AI Studio](https://aistudio.google.com/) > Tạo API Key.                     |
| **Cohere Reranker**    | `Cohere API Key`               | Đăng ký tại [Cohere Dashboard](https://dashboard.cohere.com/) > Copy API Key.           |
| **LangChain Agent**    | `LangChain` (n8n-nodes-langchain) | Cài đặt node `n8n-nodes-langchain` từ **n8n Marketplace**.                          |
| **Schedule Trigger**   | `Cron Job`                     | Đặt lịch chạy hàng ngày (ví dụ: `0 0 * * *` để chạy lúc 00:00 hàng ngày).              |

#### **🔹 Bước 2: Cấu Hình Cụ Thể Các Node Quan Trọng**
##### **A. Node "Search files and folders" (Google Drive)**
- **Tham số cần điền**:
  - `Folder ID`: Lấy từ liên kết Google Drive của folder chứa tài liệu (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - `File Types`: Chọn `pdf` và `doc` (hoặc `docx` nếu cần).
- **Lưu ý**: Nếu folder ID sai, workflow sẽ không tìm thấy file.

##### **B. Node "Supabase Vector Store"**
- **Tham số cần điền**:
  - `Table Name`: Đặt tên bảng trong Supabase (ví dụ: `documents`).
  - `Embedding Model`: Chọn `embeddings-google-gemini`.
  - `Collection Name`: Đặt tên collection (ví dụ: `rag_documents`).

##### **C. Node "RAG Agent" (LangChain)**
- **Tham số cần điền**:
  - **Prompt**: Sử dụng prompt mặc định hoặc **tùy chỉnh** theo nhu cầu (ví dụ: `"Trả lời câu hỏi dựa trên nội dung file trong Google Drive, nếu không biết thì nói 'Tôi không có thông tin về câu hỏi này'."`).
  - **Tools**: Chọn `vector_db_query` và `reranker`.
  - **Memory**: Chọn `memoryPostgresChat` để lưu lịch sử chat.

##### **D. Node "Delete Old Doc Rows" (Supabase)**
- **Tham số cần điền**:
  - `Query`: Sử dụng SQL mặc định để xóa dữ liệu cũ (không cần thay đổi).

##### **E. Node "Schedule Trigger" (Dọn Dẹp Tự Động)**
- **Tham số cần điền**:
  - `Cron Expression`: `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Lưu ý**: Node này **xóa dữ liệu cũ** khi file trong Google Drive bị xóa, đảm bảo cơ sở dữ liệu luôn đồng bộ.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run Workflow"** và chọn **Manual Trigger** để kiểm tra.
   - Upload một file PDF/Doc vào Google Drive để AI xử lý.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.
3. **Kích hoạt 2 Node Google Drive Trigger**:
   - Để workflow **hoạt động tự động**, các sếp phải **bật** hai node:
     - `File Created` (khi có file mới).
     - `File Updated` (khi file được chỉnh sửa).
   - **Lưu ý**: Node này **không hoạt động** nếu không kích hoạt.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tùy Chỉnh Prompt Cho RAG Agent**
- Mở node **"RAG Agent"** > **"Code"** > **"Prompt"** và **tùy chỉnh** để phù hợp với ngành nghề:
  - **Ví dụ**:
    ```json
    "Trả lời câu hỏi dựa trên nội dung file trong Google Drive. Nếu câu hỏi liên quan đến hợp đồng, hãy trích dẫn điều khoản cụ thể. Nếu không biết, hãy nói 'Tôi không có thông tin về câu hỏi này'."
    ```

### **2. Lưu Lịch Sử Chat vào Supabase**
- Sử dụng node **"Postgres Chat Memory"** để lưu **lịch sử trò chuyện** vào Supabase.
- **Cách làm**:
  - Mở node **"Postgres Chat Memory"** > **"Credentials"** > Chọn `Postgres` credential đã thiết lập.
  - **Table Name**: Đặt là `chat_history`.

### **3. Gửi Báo Cáo Định Kỳ qua Email/Slack**
- Thêm node **"Email"** hoặc **"Slack"** sau **"Schedule Trigger"** để **báo cáo** khi có file mới được thêm/xóa.
- **Ví dụ**:
  ```json
  {
    "node": "email",
    "operation": "send",
    "to": "email@example.com",
    "subject": "Cập nhật tự động RAG Chatbot",
    "body": "Có {{ $node["Get File IDs"].json["items"].length }} file mới được thêm/xóa trong Google Drive."
  }
  ```

### **4. Cải Thiện Chất Lượng Kết Quả với Cohere Reranker**
- Node **"Reranker Cohere"** giúp **lọc kết quả tìm kiếm** trước khi đưa vào RAG.
- **Lưu ý**: Nếu không cần, có thể **xóa node này** để tiết kiệm chi phí API.

### **5. Sử Dụng Telegram/Telegram Bot để Trả Lời Câu Hỏi**
- Thêm node **"Telegram Bot"** sau **"When chat message received"** để AI trả lời qua Telegram.
- **Cách làm**:
  - Tạo bot Telegram tại [@BotFather](https://t.me/BotFather).
  - Thiết lập credential trong n8n với `Token` và `Chat ID`.

---
## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Cường Trí Tuệ Nhân Tạo**

Workflow này không chỉ **tự động hóa** quá trình xây dựng và cập nhật AI Chatbot RAG, mà còn **giúp các sếp**:
✔ **Tiết kiệm hàng giờ** tra cứu tài liệu thủ công.
✔ **Trả lời khách hàng chính xác** với thông tin mới nhất.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy ổn định.
2. **Thiết lập tất cả credentials** theo hướng dẫn trên.
3. **Upload tài liệu** vào Google Drive và **bật workflow**.
4. **Test với câu hỏi** và **tùy chỉnh prompt** để phù hợp với ngành nghề.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Cảm ơn các sếp đã theo dõi!** Nếu có vấn đề, hãy liên hệ với tác giả tại [anirudh.n.aeran@gmail.com](mailto:anirudh.n.aeran@gmail.com) hoặc tham khảo thêm tại [LinkedIn của Anirudh](https://www.linkedin.com/in/anirudh-narayan-a/). Happy automating! 🤖✨