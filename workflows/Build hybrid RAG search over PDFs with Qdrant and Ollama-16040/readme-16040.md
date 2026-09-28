---
title: "🔍 **Tự Động Hóa Tìm Kiếm Hybrid RAG Trên PDF Với Qdrant & Ollama (Không Cần Code!)""
description: "Workflow tự động hóa xây dựng hệ thống tìm kiếm thông minh kết hợp vector dense (semantic) và sparse (keyword) trên tài liệu PDF, sử dụng Qdrant và mô hình Ollama. Giúp các sếp tìm kiếm thông tin nhanh chóng, chính xác và cá nhân hóa từ hàng trăm trang tài liệu pháp lý, hợp đồng hoặc báo cáo."
slug: "tieu-dong-hoa-tim-kiem-hybrid-rag-voi-qdrant-ollama"
tags: [n8n, automation, AI RAG, Qdrant, Ollama, document extraction, no-code, vector search]
keywords: [n8n workflow tìm kiếm PDF, tự động hóa RAG, Qdrant Ollama, hybrid search, tìm kiếm thông minh không code, vector database]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Hybrid RAG Trên PDF Với Qdrant & Ollama**

### **Giải Pháp Cho Nỗi Đau "Tìm Thông Tin Trong PDF Làm Sao?"**
Các sếp đã từng gặp phải tình huống này chưa?
- **Tìm kiếm trong hàng trăm trang PDF** (hợp đồng, báo cáo pháp lý, tài liệu nội bộ) nhưng kết quả chỉ trả về danh sách trang chứ không hiểu nội dung thực sự.
- **Không tìm thấy thông tin chính xác** vì tìm kiếm keyword đơn giản không hiểu ngữ nghĩa.
- **Phải đọc thủ công** từng trang để xác nhận thông tin, tốn thời gian và dễ mắc sai sót.

Workflow này **xây dựng một hệ thống tìm kiếm thông minh kết hợp hai kỹ thuật mạnh mẽ**:
1. **Hybrid Search**: Tìm kiếm **semantic** (hiểu ngữ nghĩa) bằng vector dense + **keyword exact** bằng vector sparse.
2. **RAG (Retrieval-Augmented Generation)**: Trích xuất thông tin từ PDF, chuyển thành vector, và trả về kết quả chính xác khi người dùng nhập câu hỏi.

Kết quả? **Tìm kiếm PDF như tìm kiếm Google, nhưng với độ chính xác 100% từ nội dung thực sự của tài liệu.**

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tìm kiếm thông minh**: Hiểu ngữ nghĩa câu hỏi (ví dụ: "Hợp đồng có quy định về bảo mật dữ liệu không?") thay vì chỉ tra keyword.
- **Tiết kiệm thời gian**: Không cần đọc từng trang PDF, hệ thống tự trích xuất và trả về thông tin liên quan.
- **Cá nhân hóa**: Kết hợp với Ollama (mô hình AI local), có thể trả lời câu hỏi bằng văn bản tự nhiên.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không cần can thiệp thủ công.
- **An toàn dữ liệu**: Tất cả xử lý trên máy chủ riêng (self-hosted), không gửi dữ liệu ra cloud.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Môi trường n8n Self-hosted**:
   - Cài đặt n8n trên **VPS** (khuyến nghị sử dụng [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
   - Cài đặt **Docker** và **Docker Compose** để chạy Qdrant và Ollama.

2. **Dịch vụ & API Keys**:
   - **Qdrant**:
     - Cài đặt Qdrant trên cùng VPS hoặc máy chủ riêng (cách cài: [Qdrant Quickstart](https://qdrant.tech/documentation/quick-start/)).
     - **Credentials trong n8n**:
       - `qdrantRestApi`: URL của Qdrant (ví dụ: `http://localhost:6333`).
       - `qdrantApi`: Thông tin API (nếu cần).
   - **Ollama**:
     - Cài đặt Ollama trên cùng VPS (cách cài: [Ollama Install](https://ollama.com/)).
     - **Credentials trong n8n**:
       - `ollamaApi`: URL của Ollama (ví dụ: `http://localhost:11434`).
     - **Mô hình AI**: Đảm bảo mô hình `nomic-embed-text:latest` đã được pull từ Ollama (`ollama pull nomic-embed-text`).

3. **Tài liệu PDF**:
   - Chọn một file PDF (ví dụ: hợp đồng, tài liệu pháp lý) và đặt ở đường dẫn `/tmp/` trên VPS (hoặc điều chỉnh trong node `Read/Write Files from Disk`).

4. **Cấu hình bổ sung**:
   - **Node `chatTrigger`**: Cần một webhook để nhận câu hỏi từ người dùng (có thể kết nối với Slack, Telegram, hoặc API riêng).
   - **Node `httpRequest`**: Đảm bảo có quyền truy cập đến API của Ollama để generate embeddings cho query.
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/16040](https://n8n.io/workflows/16040) hoặc copy toàn bộ JSON từ trang này.
- **Cách import**:
  - Mở **n8n Editor** trên VPS.
  - Nhấn **Import Workflow** và dán JSON vào.
  - **Hoặc** sử dụng **API Import**:
    ```bash
    curl -X POST "http://<n8n-host>:5678/workflows/import" \
    -H "Content-Type: application/json" \
    -d @workflow.json
    ```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Chuẩn bị dữ liệu (Data Ingestion)** (trên cùng canvas).
- **Phần 2: Tìm kiếm hybrid (Query)** (phần dưới, kết nối với `chatTrigger`).

#### **A. Cấu Hình Phần Chuẩn Bị Dữ liệu**
1. **Node `Read/Write Files from Disk`**:
   - **Parameter `File Path`**: Đặt thành `/tmp/your-document.pdf` (đổi tên file PDF theo thực tế).
   - **Parameter `Operation`**: Chọn `Read`.

2. **Node `Check If Collection Exists`**:
   - **Parameter `Collection Name`**: Đặt thành `"testing"` (hoặc tên collection tùy ý).
   - **Credentials**: Đảm bảo `qdrantRestApi` đã cấu hình đúng URL Qdrant.

3. **Node `Create Collection`**:
   - **Parameter `Collection Name`**: `"testing"` (giống node trên).
   - **Parameter `Config`**:
     ```json
     {
       "vectors": {
         "config": {
           "size": 768,
           "distance": "Cosine"
         }
       },
       "sparse": {
         "index": "sparse-text",
         "bm25": {}
       }
     }
     ```
     - **Lưu ý**: Đảm bảo cấu hình này khớp với mô hình `nomic-embed-text` (768 dimensions).

4. **Node `Embeddings Ollama`**:
   - **Parameter `Model`**: `"nomic-embed-text:latest"`.
   - **Credentials**: Đảm bảo `ollamaApi` trỏ đến `http://localhost:11434`.

5. **Node `Qdrant Vector Store`**:
   - **Parameter `Collection Name`**: `"testing"`.
   - **Credentials**: `qdrantApi` (nếu cần).

6. **Node `Recursive Character Text Splitter`**:
   - **Parameter `Chunk Size`**: 1000 (hoặc điều chỉnh theo dung lượng token của mô hình).
   - **Parameter `Chunk Overlap`**: 200 (để tránh mất mát thông tin giữa chunks).

#### **B. Cấu Hình Phần Tìm Kiếm Hybrid**
1. **Node `When chat message received`**:
   - **Credentials**: Cấu hình webhook để nhận câu hỏi từ người dùng (ví dụ: Slack, Telegram, hoặc API REST).
   - **Example Payload**:
     ```json
     {
       "query": "Hợp đồng có quy định về bảo mật dữ liệu không?"
     }
     ```

2. **Node `Generate the embeddings of the query`**:
   - **Parameter `URL`**: `http://localhost:11434/api/embeddings`.
   - **Parameter `Body`**:
     ```json
     {
       "model": "nomic-embed-text:latest",
       "prompt": "$json.query"
     }
     ```
   - **Credentials**: `ollamaApi`.

3. **Node `Query Points (using the embeddings)`**:
   - **Parameter `Collection Name`**: `"testing"`.
   - **Parameter `Query`**:
     ```json
     {
       "vector": "$json.embeddings",
       "limit": 5,
       "with_payload": true,
       "with_vector": true
     }
     ```

4. **Node `Extract sparse from Qdrant` (Code Node)**:
   - **Mã JavaScript**:
     ```javascript
     // Lấy sparse vectors từ Qdrant
     const sparseData = $input.all()[0].sparse;
     return {
       sparse: sparseData
     };
     ```
   - **Lưu ý**: Node này phụ thuộc vào cấu trúc trả về của Qdrant. Nếu không hoạt động, kiểm tra cấu hình `sparse` trong `Create Collection`.

5. **Node `Update Vectors`**:
   - **Parameter `Collection Name`**: `"testing"`.
   - **Parameter `Points`**:
     ```json
     {
       "ids": ["$json.id"],
       "vectors": "$json.vector",
       "payload": "$json.payload",
       "sparse": "$json.sparse"
     }
     ```
   - **Lưu ý**: Sử dụng `updateVectors` thay vì `upsert` để tránh ghi đè dữ liệu cũ.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** để chạy phần **Data Ingestion** (chuẩn bị dữ liệu).
   - Sau khi collection `"testing"` được tạo thành công, chuyển sang phần **Query**.
   - Gửi một câu hỏi qua webhook (ví dụ: `POST http://<n8n-host>:5678/webhooks/chatTrigger` với body `{ "query": "Tìm thông tin về điều khoản bảo mật" }`).

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH KẾT NỐI VỚI SLACK/TELEGRAM**]
- **Slack**:
  - Sử dụng node `n8n-nodes-slack.webhook` để nhận câu hỏi từ Slack.
  - Cấu hình webhook trong Slack App và truyền payload về `chatTrigger`.
- **Telegram**:
  - Sử dụng bot Telegram và node `n8n-nodes-telegram.webhook` để nhận tin nhắn.
  - Cấu hình bot và truyền payload tương tự.

:::info[**LƯU LOG & BÁO CÁO**]
- **Node `StickyNote`**: Thêm node này để ghi chú các lỗi hoặc trạng thái của workflow.
- **Node `Set` + `HTTP Request`**: Gửi log đến một file CSV hoặc database (ví dụ: PostgreSQL) để theo dõi lịch sử query.

:::info[**CẢI TIẾN HỆ THỐNG**]
- **Thêm mô hình AI khác**: Thay `nomic-embed-text` bằng mô hình khác như `llama3` (nếu Ollama hỗ trợ).
- **Tăng tốc độ**: Sử dụng node `Aggregate` để tối ưu hóa việc xử lý nhiều query đồng thời.
- **Cá nhân hóa kết quả**: Kết hợp với node `LLM` (ví dụ: `@n8n/n8n-nodes-langchain.chatTrigger`) để trả lời câu hỏi bằng văn bản tự nhiên.

---
## 📌 **Kết Luận**
Workflow này **không chỉ đơn giản hóa việc tìm kiếm trong PDF**, mà còn **tăng cường khả năng hiểu ngữ nghĩa** và **tìm kiếm chính xác keyword** thông qua hybrid search. Với **Qdrant** và **Ollama**, các sếp có thể xây dựng một hệ thống AI local, an toàn và hiệu quả, **không cần viết một dòng code**.

**Hành động ngay!**
1. **Cài đặt n8n + Qdrant + Ollama** trên VPS (dùng mã giảm giá **VPSN8N** để tiết kiệm).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với một file PDF** và trải nghiệm tốc độ tìm kiếm siêu nhanh!

**Câu hỏi?** Để lại comment bên dưới hoặc liên hệ admin để hỗ trợ! 🚀