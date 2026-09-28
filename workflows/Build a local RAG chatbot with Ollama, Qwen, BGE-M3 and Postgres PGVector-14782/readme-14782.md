---
title: "🤖 Xây Dự Chatbot RAG Cục Bộ với Ollama, Qwen & PostgreSQL PGVector - Tự Động Hóa Trí Tuệ Nhân Tạo 100% Offline"
description: "Workflow này giúp các sếp xây dựng một chatbot RAG hoàn toàn chạy trên máy chủ nội bộ, không cần API cloud, với Ollama + Qwen3:14B (tạo câu trả lời) và Qwen2.5:7B (xác định ý định). Tiết kiệm chi phí, bảo mật dữ liệu và hoạt động ổn định 24/7."
slug: "xay-du-chatbot-rag-cuc-bo-ollama-qwen-postgres"
tags: [n8n, automation, AI RAG, Ollama, PostgreSQL, no-code, trí tuệ nhân tạo]
keywords: [n8n workflow RAG, chatbot cục bộ, Ollama Qwen, PostgreSQL PGVector, tự động hóa trí tuệ nhân tạo, không cần cloud]
---

# 🚀 **Xây Dự Chatbot RAG Cục Bộ với Ollama, Qwen & PostgreSQL - Giải Pháp Trí Tuệ Nhân Tạo Offline Cho Doanh Nghiệp**

## **Tại Sao Các Sếp Cần Một Chatbot RAG Cục Bộ?**
Hiện nay, nhiều doanh nghiệp vẫn phụ thuộc vào các dịch vụ AI cloud như OpenAI, Mistral hay Google Vertex AI để xây dựng chatbot. Tuy nhiên, những giải pháp này mang lại **nhược điểm lớn**:
- **Chi phí cao**: Tăng theo lượng truy vấn và thời gian sử dụng.
- **Rủi ro bảo mật**: Dữ liệu nhạy cảm có thể bị lộ hoặc bị giám sát.
- **Tính ổn định kém**: Nếu cloud bị down, hệ thống sẽ ngừng hoạt động.
- **Trễ phản hồi**: Do phụ thuộc vào mạng internet và API rate limit.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Chạy hoàn toàn trên máy chủ nội bộ** (Self-hosted) với Ollama và PostgreSQL.
✅ **Không cần API cloud**, tiết kiệm chi phí và bảo mật tuyệt đối.
✅ **Sử dụng mô hình Qwen3:14B** (tối ưu hóa cho trả lời chính xác) và **Qwen2.5:7B** (xác định ý định).
✅ **Hỗ trợ RAG (Retrieval-Augmented Generation)** để trả lời dựa trên dữ liệu nội bộ (chẳng hạn như tài liệu doanh nghiệp, hợp đồng, FAQ).
✅ **Hoạt động liên tục 24/7** mà không phụ thuộc vào internet.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí**: Không cần trả phí API cho mỗi truy vấn.
- **Bảo mật tuyệt đối**: Dữ liệu không rời khỏi máy chủ nội bộ.
- **Trả lời chính xác**: Sử dụng RAG để lấy thông tin từ cơ sở dữ liệu nội bộ.
- **Tính ổn định cao**: Không bị ảnh hưởng bởi vấn đề mạng hoặc API rate limit.
- **Cá nhân hóa**: Hỗ trợ nhớ lịch sử trò chuyện qua `session_id`.
- **Dễ mở rộng**: Thêm dữ liệu mới vào PostgreSQL mà không cần tái huấn luyện mô hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Máy chủ VPS** (Self-hosted) để cài đặt n8n, Ollama và PostgreSQL.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Cài đặt Ollama** và tải các mô hình cần thiết:
   ```bash
   ollama pull qwen2.5:7b
   ollama pull qwen3:14b
   ollama pull bge-m3:latest
   ```
   - **Host URL của Ollama**: `http://localhost:11434` (hoặc IP VPS nếu chạy trên máy chủ xa).

3. **Cài đặt PostgreSQL với pgvector**:
   - Cài đặt PostgreSQL và kích hoạt extension `pgvector`:
     ```sql
     CREATE EXTENSION vector;
     ```
   - Tạo bảng `vector_store` (chứa embeddings của tài liệu) và `chat_histories` (lưu lịch sử trò chuyện).

4. **Tài liệu để ingest**:
   - Các sếp cần chuẩn bị **tài liệu nội bộ** (PDF, DOCX, TXT) để chuyển thành embeddings và lưu vào PostgreSQL.
   - **Mô hình embeddings**: Sử dụng `bge-m3:latest` từ Ollama.

5. **Credentials cần thiết**:
   - **Ollama**: Thêm vào tất cả các node Ollama (`lmChatOllama`, `embeddingsOllama`).
   - **PostgreSQL**: Thêm vào node `vectorStorePGVector` và `memoryPostgresChat`.

6. **Workflow n8n**:
   - Cài đặt n8n trên VPS và mở port `5678` (default) để webhook hoạt động.
   - Cài đặt **n8n nodes LangChain** để hỗ trợ RAG và chat memory.
     ```bash
     n8n install @n8n/n8n-nodes-langchain
     ```

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14782](https://n8n.io/workflows/14782) hoặc copy toàn bộ JSON từ link trên.
- **Mở n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** sau khi import xong.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **25 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Credentials**
1. **Ollama**:
   - Tất cả các node `lmChatOllama` và `embeddingsOllama` cần **credentials Ollama**.
   - Thêm **credentials mới** trong n8n:
     - **Name**: `ollama`
     - **Host**: `http://localhost:11434` (hoặc IP VPS nếu chạy trên máy chủ xa).
     - **Port**: `11434` (default).
     - **Use Basic Authentication**: **Không** (nếu không sử dụng mật khẩu).

2. **PostgreSQL**:
   - Node `vectorStorePGVector` và `memoryPostgresChat` cần **credentials PostgreSQL**.
   - Thêm **credentials mới**:
     - **Name**: `postgres`
     - **Host**: `localhost` (hoặc IP VPS).
     - **Port**: `5432` (default).
     - **Database**: Tên cơ sở dữ liệu chứa `vector_store` và `chat_histories`.
     - **Username** và **Password**: Đăng nhập PostgreSQL.

##### **B. Cấu Hình Node Quá Trình**
1. **Webhook**:
   - Node `Webhook` (path: `rag-chatbot`) sẽ nhận yêu cầu từ client.
   - **HTTP Method**: `POST`.
   - **Expected Body**: JSON với các trường:
     ```json
     {
       "chatInput": "Câu hỏi của người dùng",
       "session_id": "id_nhóm_trò_chuyện"
     }
     ```

2. **Classify & Decompose (Qwen2.5:7B)**:
   - Node `Ollama Chat Model (Classifier — Qwen2.5:7b)` sẽ phân loại yêu cầu và tạo **sub-queries** (câu hỏi con).
   - **Prompt mặc định** đã được cấu hình trong node `chainLlm` (`Understand Request`).

3. **RAG Retrieval Pipeline**:
   - Node `Ollama Embeddings (BGE-M3)` tạo embeddings cho mỗi `sub-query`.
   - Node `PGVector Store — Retrieve Chunks` lấy **chunks** từ PostgreSQL dựa trên độ tương đồng.
   - Node `Keep score over 0.4` **lọc bỏ** các chunks có độ tương đồng < 0.4.
   - Node `Aggregate Matching Chunks` **tổng hợp** kết quả cho mỗi `sub-query`.

4. **Answer Generator (Qwen3:14B)**:
   - Node `Ollama Chat Model (Answer Generator — Qwen3:14b)` tạo câu trả lời dựa trên **chunks** được lấy.
   - **Think Tag Stripper**: Loại bỏ phần `<think>...</think>` trong câu trả lời (nếu không cần, có thể xóa node này).

5. **Small Talk Path**:
   - Nếu yêu cầu không phải là câu hỏi (ví dụ: "Xin chào"), nó sẽ được chuyển đến `Small Talk AI Agent` (Qwen3:14B) với **bảo mật lịch sử trò chuyện** qua `Postgres Chat Memory`.

##### **C. Kích Hoạt Workflow**
1. **Test Run**:
   - Gửi yêu cầu mẫu qua webhook:
     ```bash
     curl -X POST http://<IP_VPS>:5678/webhook/rag-chatbot \
       -H "Content-Type: application/json" \
       -d '{"chatInput": "Tôi muốn biết về chính sách bảo mật của công ty", "session_id": "session1"}'
     ```
   - Kiểm tra kết quả trong **n8n Dashboard**.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐI ƯU HỌC]
1. **Tăng tốc độ retrieval**:
   - Sử dụng **indexing** cho PostgreSQL PGVector để giảm thời gian lấy chunks.
   - Thêm **caching** cho embeddings bằng Redis.

2. **Lưu log trò chuyện**:
   - Thêm node `Set` sau `Respond to Webhook` để lưu toàn bộ lịch sử vào PostgreSQL hoặc Elasticsearch.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron** để gửi báo cáo thống kê (ví dụ: số lượng câu hỏi, chủ đề phổ biến) qua Email/Slack.

4. **Kết hợp với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` để người dùng tương tác qua kênh chat.

5. **Tối ưu mô hình**:
   - Thay thế `Qwen3:14B` bằng `Qwen2.5:7B` (nếu không cần độ chính xác cao) để tiết kiệm tài nguyên.
   - Sử dụng **LoRA** hoặc **QLoRA** để fine-tune mô hình trên dữ liệu nội bộ.

6. **Bảo mật thêm**:
   - Sử dụng **JWT** để xác thực yêu cầu webhook.
   - Mật mã hóa `session_id` trước khi lưu vào PostgreSQL.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn xây dựng một chatbot trí tuệ nhân tạo **cục bộ, bảo mật và hiệu quả chi phí**. Bằng cách sử dụng **Ollama + Qwen + PostgreSQL PGVector**, các sếp có thể:
✔ **Tiết kiệm hàng nghìn USD** mỗi tháng so với các dịch vụ cloud.
✔ **Bảo mật tuyệt đối** dữ liệu nhạy cảm.
✔ **Hoạt động ổn định** 24/7 mà không phụ thuộc vào internet.
✔ **Tự động hóa hỗ trợ khách hàng** với trả lời chính xác dựa trên dữ liệu nội bộ.

**Hãy áp dụng ngay workflow này và nâng cao hiệu suất công việc của doanh nghiệp!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/14782)
👉 [Cài đặt VPS cho n8n](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

---
**Chia sẻ và đóng góp ý kiến để workflow này ngày càng hoàn thiện!** 🚀