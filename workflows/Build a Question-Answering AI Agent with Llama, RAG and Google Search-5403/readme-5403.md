---
title: "🤖 **Tự Động Hóa Agent Trả Lời Câu Hỏi AI với Llama, RAG & Google Search - Không Cần Code!**"
description: "Xây dựng một agent AI thông minh trả lời câu hỏi dựa trên dữ liệu cá nhân, kết hợp RAG (Retrieval-Augmented Generation) và tìm kiếm Google, hoạt động tự động 24/7. Giúp các sếp tiết kiệm thời gian tra cứu, tăng độ chính xác và cá nhân hóa trải nghiệm cho khách hàng/nhân viên."
slug: "tay-dong-hoa-agent-ai-rag-llama-google-search"
tags: [n8n, automation, ai-rag, llama, ollama, qdrant, no-code]
keywords: [n8n workflow ai, tự động hóa agent trả lời câu hỏi, RAG với n8n, Ollama embeddings, Qdrant vector store, tự động hóa không cần code]
---

# 🚀 **Tạo Agent AI Trả Lời Câu Hỏi Siêu Nhanh với Llama, RAG & Google Search**

Hãy tưởng tượng một AI cá nhân hóa trả lời mọi câu hỏi của bạn **từ dữ liệu nội bộ** (văn bản, PDF, email) **và kết quả tìm kiếm Google** một cách tự động, **không cần viết một dòng code nào**. Đó chính là công cụ **Agent AI RAG** này, giúp các sếp:
- **Tiết kiệm thời gian** tra cứu thông tin từ hàng ngàn tài liệu.
- **Tăng độ chính xác** với kết quả dựa trên dữ liệu thực tế (không phải "hallucination" của AI).
- **Cá nhân hóa trải nghiệm** cho khách hàng/nhân viên với câu trả lời thông minh.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tự động hóa tra cứu thông tin** từ dữ liệu cá nhân (PDF, văn bản, email) **và kết quả Google** trong một workflow duy nhất.
✅ **Tăng độ tin cậy** với AI trả lời dựa trên **RAG (Retrieval-Augmented Generation)**, tránh sai sót như hallucination.
✅ **Cá nhân hóa** cho từng ngành nghề (chăm sóc khách hàng, hỗ trợ kỹ thuật, nghiên cứu thị trường...).
✅ **Hoạt động liên tục** mà không cần can thiệp, tiết kiệm **tối thiểu 10 giờ/lần** tra cứu thủ công.
✅ **Mở rộng khả năng** bằng việc kết nối với **Slack, Telegram, hoặc email** để AI trả lời tự động.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
### **1. Hệ thống AI & Vector Database**
- **Ollama** (để chạy mô hình embeddings `mxbai-embed-large`):
  - Cài đặt Ollama trên máy chủ (Self-hosted) hoặc sử dụng dịch vụ cloud như [Ollama Cloud](https://ollama.com/).
  - **Mô hình yêu cầu**: `mxbai-embed-large:latest` (tải xuống tự động khi chạy lần đầu).
- **Qdrant** (vector database để lưu trữ embeddings):
  - Cài đặt Qdrant trên VPS (Self-hosted) hoặc sử dụng [Qdrant Cloud](https://qdrant.tech/cloud/).
  - **API Key**: Thêm vào n8n dưới **Credentials** với tên `qdrantApi`.

### **2. MCP (Multi-Client Protocol) - Tool cho LangChain**
- **MCP Server** (để trigger workflow):
  - Cài đặt [MCP Server](https://github.com/langchain-ai/mcp) trên máy chủ riêng.
  - **URL & Port**: Cấu hình trong `mcpTrigger` (node `MCP Server Trigger`).
- **MCP Client** (để gọi API từ n8n):
  - Thêm **Credentials** trong n8n với tên `mcpClientApi` (URL của MCP Server + API Key).

### **3. Dữ liệu đầu vào (chạy lần đầu)**
- **Tài liệu cần upload** (PDF, DOCX, TXT, email...) để AI học và trả lời.
- **Google API Key** (nếu muốn kết hợp tìm kiếm Google):
  - Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và thêm vào n8n dưới **Credentials** (nếu workflow mở rộng).

### **4. n8n Self-hosted**
- Workflow này **không chạy được trên n8n Cloud** do yêu cầu MCP Server và Qdrant.
- **👉 Đăng ký VPS Self-hosted** với:
  - **TinoHost** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%):
    [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
  - **BNIX** (VPS Xeon 4GB chỉ 50k/tháng):
    [https://my.bnix.one/aff.php?aff=172](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/5403) (ấn "Export").
2. **Mở n8n Editor** trên VPS của mình.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và đặt tên (ví dụ: `AI-Agent-RAG`).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên và copy toàn bộ nội dung.
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán nội dung.
3. **Chọn "Create new workflow"** và tiếp tục cấu hình.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **RAG Ingestion Pipeline** (chạy **1 lần duy nhất** để upload dữ liệu).
- **MCP Server Trigger** (chạy liên tục để trả lời câu hỏi).

#### **A. Cấu hình RAG Ingestion Pipeline (Upload dữ liệu)**
1. **Node `Default Data Loader`**:
   - **Tham số cần điền**:
     - **File Path**: Đường dẫn đến folder chứa tài liệu (PDF, DOCX, TXT...).
     - **File Types**: Chọn `*.pdf,*.docx,*.txt` (hoặc tùy chỉnh).
   - **Lưu ý**: Folder này phải nằm trên máy chủ VPS của các sếp.

2. **Node `Recursive Character Text Splitter`**:
   - **Tham số mặc định** (không cần chỉnh) để chia văn bản thành chunks nhỏ.

3. **Node `Embeddings Ollama`**:
   - **Model**: Đã cấu hình là `mxbai-embed-large:latest` (không cần đổi).
   - **Credentials**: Đảm bảo đã thêm `ollamaApi` trong n8n.

4. **Node `Qdrant Vector Store`**:
   - **Credentials**: Sử dụng `qdrantApi` (đã cấu hình trước).
   - **Collection Name**: Đặt tên collection (ví dụ: `my_documents`).
   - **Vector Size**: Để mặc định (768, phù hợp với mô hình mxbai).

5. **Node `Qdrant Vector Store1`** (nếu có):
   - **Lưu ý**: Đây là node **không hoạt động** trong workflow gốc (có thể xóa nếu không cần).

#### **B. Cấu hình MCP Server Trigger (Trả lời câu hỏi)**
1. **Node `MCP Server Trigger`**:
   - **Key Parameters**:
     - `path`: Giá trị `8d7910ab-f0db-4042-9da9-f580647a8a8e` (không đổi).
   - **Credentials**: Không cần thêm (nó sẽ gọi MCP Client thông qua `mcpClientApi`).

2. **Node `MCP Client`**:
   - **Credentials**: Đảm bảo đã thêm `mcpClientApi` (URL MCP Server + API Key).
   - **Operation**: Đã cấu hình là `executeTool` (không cần đổi).

3. **Node `MCP Client1`**:
   - **Lưu ý**: Đây là node **không hoạt động** trong workflow gốc (có thể xóa).

4. **Node `On form submission`**:
   - **Lưu ý**: Đây là **trigger mặc định** cho form (nếu muốn thêm UI, các sếp cần kết nối với Slack/Telegram hoặc tạo form riêng).

---
### **3. Kích hoạt ⚡️**
1. **Chạy RAG Ingestion Pipeline (1 lần duy nhất)**:
   - **Bật Active** cho workflow.
   - **Test Run** với dữ liệu mẫu (ví dụ: 1 file PDF).
   - **Kiểm tra Qdrant**: Đăng nhập vào Qdrant Dashboard để xác nhận embeddings đã được lưu.

2. **Chạy MCP Server Trigger (hoạt động liên tục)**:
   - **Bật Active** workflow.
   - **Test với câu hỏi**: Gửi yêu cầu từ MCP Client (ví dụ: `{"question": "Tóm tắt nội dung file ABC.pdf"}`).
   - **Kiểm tra kết quả**: AI sẽ trả lời dựa trên dữ liệu đã upload.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**Mở rộng khả năng**]
### **1. Kết nối với Slack/Telegram**
- Thêm **node `Slack`** hoặc `Telegram Bot` sau `MCP Client` để AI trả lời tự động khi có tin nhắn.
- **Cách làm**:
  ```markdown
  - Sau `MCP Client`, thêm node `Set` để format câu trả lời.
  - Kết nối với `Slack Webhook` hoặc `Telegram Bot` để gửi tin nhắn tự động.
  ```

### **2. Lưu log câu hỏi & trả lời**
- Thêm **node `Google Sheets`** hoặc `Notion` để ghi lại lịch sử tương tác.
- **Cách làm**:
  ```markdown
  - Sau `MCP Client`, thêm node `Set` để format dữ liệu.
  - Kết nối với `Google Sheets` (credentials `googleSheetsApi`) để lưu vào sheet.
  ```

### **3. Kết hợp với Google Search**
- Nếu muốn AI **tìm kiếm Google** khi không tìm thấy trong dữ liệu cá nhân:
  - Thêm **node `Google Search`** (n8n-nodes-google-search).
  - **Cấu hình**:
    - Thêm `Google API Key` vào credentials.
    - Sau `MCP Client`, thêm **node `If`** để kiểm tra:
      - Nếu không tìm thấy trong Qdrant → Gọi `Google Search`.
      - Trả kết quả từ cả 2 nguồn.

### **4. Cập nhật dữ liệu định kỳ**
- Sử dụng **node `Schedule`** để tự động upload dữ liệu mới vào Qdrant.
- **Cách làm**:
  ```markdown
  - Tạo workflow mới với `Schedule` (ví dụ: chạy hàng tuần).
  - Kết nối với `Default Data Loader` và `Qdrant Vector Store` để cập nhật.
  ```

### **5. Tối ưu mô hình embeddings**
- Nếu chất lượng trả lời không cao, thử:
  - **Mô hình khác** trong Ollama (ví dụ: `nomic-embed-text`).
  - **Tăng size chunk** trong `Recursive Character Text Splitter` (ví dụ: `chunk_size: 1000`).
:::

---
## 📌 **Kết luận**
Workflow này là **công cụ mạnh mẽ** để các sếp xây dựng một **Agent AI cá nhân hóa**, trả lời câu hỏi từ dữ liệu nội bộ **và kết quả Google**, **không cần viết code**. Dù là **chăm sóc khách hàng, hỗ trợ kỹ thuật, hay nghiên cứu thị trường**, AI này sẽ **tiết kiệm thời gian, tăng độ chính xác và hoạt động 24/7**.

### **🔥 Bước tiếp theo**
1. **Chạy RAG Ingestion Pipeline** để upload dữ liệu.
2. **Test với câu hỏi mẫu** và điều chỉnh mô hình nếu cần.
3. **Kết nối với Slack/Telegram** để AI trả lời tự động.
4. **Cập nhật dữ liệu định kỳ** để AI luôn có thông tin mới nhất.

**🚀 Hãy áp dụng ngay và tự động hóa công việc tra cứu thông tin của mình!**