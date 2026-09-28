---
title: "🚀 Tự Động Hóa Chia Tách & Lưu Trữ Tài Liệu Google Drive vào Pinecone với AI (RAG + Gemini + OpenRouter)"
description: "Workflow tự động hóa 100% không code để tải tài liệu từ Google Drive, chia nhỏ thành các chunk thông minh, tạo embedding bằng Gemini và lưu vào Pinecone cho ứng dụng RAG (Retrieval-Augmented Generation). Giúp các sếp tiết kiệm thời gian xử lý dữ liệu và nâng cao hiệu suất AI."
slug: "tieu-dong-hoa-chia-tach-tai-lieu-google-drive-ve-pinecone"
tags: [n8n, automation, no-code, ai, machine-learning, google-drive, pinecone, openrouter, gemini, rag]
keywords: [n8n workflow google drive pinecone, tự động hóa chia nhỏ tài liệu, embedding text với gemini, lưu trữ vector pinecone, rag với openrouter, tự động hóa ai không code]
---

# 🚀 **Tự Động Hóa Chia Tách & Lưu Trữ Tài Liệu Google Drive vào Pinecone với AI (RAG + Gemini + OpenRouter)**

---

### **🔍 Nỗi Đau Của Các Sếp Khi Xử Lý Tài Liệu Thông Minh**
Các sếp thường phải:
- **Tải xuống và xử lý hàng trăm tài liệu** từ Google Drive một cách thủ công.
- **Chia nhỏ tài liệu thành các chunk** phù hợp để phân tích, nhưng không có công cụ tự động hóa.
- **Tạo embedding và lưu trữ vào Pinecone** để sử dụng trong hệ thống RAG (Retrieval-Augmented Generation), nhưng phải viết code hoặc sử dụng nhiều công cụ khác nhau.
- **Mất thời gian và dễ sai sót** khi làm thủ công, đặc biệt với lượng dữ liệu lớn.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tải tự động** tất cả tài liệu từ Google Drive.
✅ **Chia nhỏ tài liệu** thành các chunk thông minh (Context-Aware Chunking).
✅ **Tạo embedding** bằng Google Gemini và OpenRouter.
✅ **Lưu vào Pinecone** để sử dụng trong các mô hình AI như RAG, chatbot hay search thông minh.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tải và xử lý tài liệu thủ công.
- **Chia nhỏ thông minh**: Chunking tự động theo logic Context-Aware, tránh mất mát thông tin.
- **Embedding cao cấp**: Sử dụng Google Gemini và OpenRouter để tạo embedding chất lượng.
- **Lưu trữ hiệu quả**: Tất cả dữ liệu được lưu vào Pinecone, sẵn sàng cho các ứng dụng AI như RAG, chatbot hay search thông minh.
- **Hoạt động liên tục**: Workflow tự động chạy khi có tài liệu mới được upload vào Google Drive.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Drive OAuth 2.0 API Key** (để tải tài liệu từ Google Drive).
   - **Google Palm API Key** (để sử dụng Gemini Embeddings).
   - **OpenRouter API Key** (để sử dụng mô hình chat).
   - **Pinecone API Key** (để lưu trữ embedding).
2. **Dữ liệu mẫu**:
   - Một hoặc nhiều tài liệu (PDF, DOCX, TXT) đã được upload vào Google Drive.
3. **Cài đặt Node LangChain**:
   - Các sếp cần cài đặt **n8n-nodes-langchain** để sử dụng các node như `embeddingsGoogleGemini`, `vectorStorePinecone`, `lmChatOpenRouter`, và `textSplitterRecursiveCharacterTextSplitter`.

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/2871).
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (hoặc paste JSON vào ô Import).
- **Bước 3**: Chọn **Create Workflow** để tạo workflow mới.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**, các sếp cần chú ý cấu hình các node sau:

##### **📌 Phần 1: Prepare Document (Tải và Chia Nhỏ Tài Liệu)**
- **Node "Get Document From Google Drive"**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Folder ID**: Điền ID của thư mục Google Drive chứa tài liệu.
  - **File ID**: Nếu chỉ muốn tải một file cụ thể, điền ID file đó.
- **Node "Extract Text Data From Google Document"**:
  - **Operation**: Chọn `text` để trích xuất nội dung văn bản.
- **Node "Split Document Text Into Sections" (Code Node)**:
  - **Mã JavaScript**:
    ```javascript
    // Chia nhỏ văn bản thành các chunk theo logic Context-Aware
    const chunkSize = 1000; // Kích thước chunk mặc định
    const chunkOverlap = 200; // Trùng lặp giữa các chunk

    const chunks = [];
    let currentChunk = "";

    for (const line of $input.all().text.split("\n")) {
      if (currentChunk.length + line.length + 1 <= chunkSize) {
        currentChunk += line + "\n";
      } else {
        chunks.push(currentChunk.trim());
        currentChunk = line + "\n";
      }
    }

    if (currentChunk.trim().length > 0) {
      chunks.push(currentChunk.trim());
    }

    return chunks.map(chunk => ({
      json: { text: chunk }
    }));
    ```
- **Node "Prepare Sections For Looping"**:
  - Chọn `text` từ node trước để chuẩn bị cho vòng lặp.

##### **📌 Phần 2: Prepare Context (Chuẩn Bị Bối Cảnh cho AI)**
- **Node "AI Agent - Prepare Context"**:
  - **Credentials**: Chọn `openRouterApi`.
  - **Prompt Template**:
    ```plaintext
    You are an AI assistant that prepares context for a given text chunk.
    Your task is to analyze the chunk and provide a relevant context that will help in understanding the chunk better.
    Context: {context}
    Chunk: {text}
    Provide a concise and relevant context.
    ```
  - **Model**: Chọn mô hình phù hợp từ OpenRouter (ví dụ: `mistral-tiny`).
- **Node "Concatenate the context and section text"**:
  - Gộp `context` và `text` thành một chuỗi duy nhất để truyền vào node tiếp theo.

##### **📌 Phần 3: Convert Text To Vectors (Tạo và Lưu Embedding)**
- **Node "Embeddings Google Gemini"**:
  - **Credentials**: Chọn `googlePalmApi`.
  - **Model**: Chọn `embeddings-001` (hoặc mô hình Gemini phù hợp).
- **Node "Pinecone Vector Store"**:
  - **Credentials**: Chọn `pineconeApi`.
  - **Index Name**: Điền tên index Pinecone muốn lưu trữ.
  - **Namespace**: Điền namespace (nếu có).
  - **Vector Field**: Điền tên trường lưu trữ embedding (ví dụ: `embedding`).
  - **Metadata Field**: Điền tên trường lưu trữ metadata (ví dụ: `metadata`).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Chạy **Test Run** với một tài liệu mẫu để kiểm tra workflow.
- **Bước 2**: Sau khi kiểm tra thành công, **bật Active** workflow.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành hoặc có lỗi.
2. **Lưu Log**:
   - Sử dụng node **Set** hoặc **Code** để lưu log vào Google Sheets hoặc một file CSV để theo dõi quá trình.
3. **Tự động Chạy Định Kỳ**:
   - Sử dụng node **Schedule** để chạy workflow hàng ngày hoặc hàng tuần để cập nhật dữ liệu mới.
4. **Tối Ưu Hóa Chunking**:
   - Thay đổi `chunkSize` và `chunkOverlap` trong node **Code** để phù hợp với loại tài liệu của các sếp.

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quá trình xử lý tài liệu, chia nhỏ và lưu trữ embedding vào Pinecone để sử dụng trong các ứng dụng AI như RAG, chatbot hay search thông minh. **Không cần viết code**, chỉ cần import và cấu hình một vài tham số là xong!

**Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất AI của doanh nghiệp!** 🚀