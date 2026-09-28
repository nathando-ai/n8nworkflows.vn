---
title: "🤖 Xây dựng Chatbot RAG chạy hoàn toàn nội bộ (Local AI) với n8n, Ollama và Qdrant"
description: "Hướng dẫn chi tiết cách tự động hóa nạp dữ liệu và xây dựng trợ lý AI thông minh (RAG) sử dụng mô hình LLM chạy cục bộ, bảo mật tuyệt đối dữ liệu doanh nghiệp."
slug: "xay-dung-local-chatbot-rag-n8n-ollama-qdrant"
tags: [n8n, automation, ai-agent, ollama, qdrant, rag, local-ai]
keywords: [n8n workflow, local chatbot rag, ollama n8n, qdrant vector store, ai agent n8n, tự động hóa ai]
---

# 🤖 Xây dựng Chatbot RAG chạy hoàn toàn nội bộ (Local AI) với n8n, Ollama và Qdrant

Các sếp có bao giờ đau đầu vì muốn ứng dụng AI vào doanh nghiệp để tra cứu tài liệu nội bộ, nhưng lại sợ lộ dữ liệu nhạy cảm khi phải gửi lên các server đám mây của OpenAI, Anthropic hay Google? Việc xây dựng một hệ thống AI tự chủ hoàn toàn (Local AI) từng rất phức tạp và đòi hỏi đội ngũ lập trình viên chuyên sâu.

Nhưng với workflow n8n này, các sếp có thể tự tay thiết lập một hệ thống **Chatbot RAG (Retrieval-Augmented Generation)** chạy hoàn toàn trên hạ tầng của mình, kết hợp giữa **Ollama** (chạy LLM nội bộ) và **Qdrant** (Vector Database) mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow và các mô hình AI chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối:** Dữ liệu tài liệu và câu hỏi của khách hàng/nhân viên không bị rò rỉ ra ngoài internet vì mọi thứ chạy Local.
- **Trợ lý thông minh bám sát tài liệu:** Chatbot có khả năng đọc hiểu tài liệu nội bộ (PDF, Text...) thông qua tính năng nạp dữ liệu tự động (`On form submission`) và trả lời chính xác dựa trên nguồn dữ liệu đó.
- **Tiết kiệm chi phí API:** Không tốn tiền mua Token của các bên thứ ba nhờ sử dụng sức mạnh tính toán của phần cứng sẵn có kết hợp Ollama.
- **Trải nghiệm mượt mà:** Tích hợp giao diện chat trực quan (`When chat message received`) kết hợp bộ nhớ ngữ cảnh (`Simple Memory`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted để kết nối mượt mà với Ollama và Qdrant local).
- **Ollama:** Đã cài đặt Ollama trên máy chủ/VPS, đã tải model LLM chat và model Embedding (`mxbai-embed-large:latest`).
- **Qdrant Vector Database:** Đã khởi chạy Qdrant (có thể chạy qua Docker) kèm theo Qdrant API Key.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow hoặc tạo mới một workflow trống trong n8n, sau đó paste toàn bộ cấu trúc 11 nodes vào giao diện Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 2 luồng chính: **Data Ingestion** (Nạp dữ liệu vào database) và **RAG Chatbot** (Giao diện trò chuyện). Các sếp cần cấu hình kỹ các node sau:

- **Embeddings Ollama & Embeddings Ollama1:** 
  - Chọn `ollamaApi` credentials (trỏ về địa chỉ server Ollama của các sếp, ví dụ: `http://localhost:11434`).
  - Đảm bảo tham số model được điền chính xác: `mxbai-embed-large:latest` (hoặc model embedding tương ứng đã pull về Ollama).
- **Qdrant Vector Store & Qdrant Vector Store1:**
  - Cấu hình `qdrantApi` credentials với URL của Qdrant server và API Key tương ứng.
  - Đặt tên Collection phù hợp (ví dụ: `documents`) để đồng bộ giữa phần nạp dữ liệu và phần truy vấn của AI Agent.
- **Ollama Chat Model:**
  - Kết nối với `ollamaApi` credentials.
  - Chọn model LLM chat các sếp muốn sử dụng (ví dụ: `llama3`, `mistral` hoặc `qwen2.5`).
- **On form submission & Default Data Loader:**
  - Node này tạo một form để các sếp upload tài liệu (PDF, txt...). Hãy kiểm tra lại đường dẫn lưu trữ tạm hoặc cấu hình data loader để hệ thống tự động băm nhỏ tài liệu (`Recursive Character Text Splitter`) trước khi đẩy vào Qdrant.
- **AI Agent & Simple Memory:**
  - Đảm bảo `AI Agent` được kết nối đúng với `Ollama Chat Model`, `Simple Memory` (giúp lưu lịch sử chat ngắn hạn) và `Qdrant Vector Store` (đóng vai trò làm công cụ tra cứu - Tool/Retriever).

#### 3. Kích hoạt ⚡️
- **Test Ingestion:** Thử submit một tài liệu qua form trigger để chắc chắn dữ liệu đã được embedding và lưu thành công vào Qdrant.
- **Test Chat:** Mở giao diện chat từ trigger `When chat message received` và đặt câu hỏi liên quan đến tài liệu vừa nạp.
- Nếu câu trả lời chính xác dựa trên tài liệu, hãy bật công tắc **Active workflow** lên màu xanh để chạy chính thức!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh giao tiếp:** Các sếp có thể thay thế node `When chat message received` bằng Telegram Trigger hoặc Slack Trigger để nhân viên công ty có thể hỏi đáp với tài liệu nội bộ ngay trên nhóm chat công việc.
- **Tự động hóa nạp dữ liệu:** Thay vì dùng Form Trigger thủ công, các sếp có thể kết nối node `Google Drive` hoặc `Local File Read` để tự động quét và nạp tài liệu mới mỗi khi có file được tải lên thư mục chung.
- **Quản lý Log:** Thêm một node lưu lịch sử câu hỏi vào Google Sheets hoặc Database để phân tích nhu cầu tìm kiếm thông tin của đội ngũ.

### 📌 Kết luận
Việc tự chủ một hệ thống RAG Local AI chưa bao giờ dễ dàng đến thế với n8n. Không còn nỗi lo lộ dữ liệu, không tốn kém chi phí API hàng tháng – các sếp hãy áp dụng ngay workflow này để nâng tầm hiệu suất vận hành doanh nghiệp ngay hôm nay!