---
title: "🚀 Xây dựng hệ thống Agentic RAG nội bộ với Ollama, PGVector và n8n hoàn toàn miễn phí"
description: "Hướng dẫn chi tiết cách triển khai hệ thống Agentic RAG chạy local 100% sử dụng Ollama, PostgreSQL/PGVector và n8n để hỏi đáp tài liệu thông minh."
slug: "local-document-qa-ollama-agentic-rag-pgvector"
tags: [n8n, automation, ai, rag, ollama, postgres, pgvector]
keywords: [n8n workflow, agentic rag, ollama local ai, pgvector n8n, hỏi đáp tài liệu ai, tự động hóa n8n]
---

# 🚀 Xây dựng hệ thống Agentic RAG nội bộ với Ollama, PGVector và n8n hoàn toàn miễn phí

Các doanh nghiệp và đội ngũ thường gặp khó khăn khi quản lý hàng đống tài liệu (PDF, Excel, CSV, Text). Việc tìm kiếm thông tin thủ công vừa mất thời gian, vừa dễ bỏ sót. Các giải pháp RAG thông thường (Retrieval-Augmented Generation) lại quá cứng nhắc, không xử lý tốt dữ liệu bảng biểu hoặc thiếu khả năng suy luận chéo giữa các tài liệu.

Workflow này giải quyết triệt để bài toán trên bằng cách xây dựng một **Hệ thống Agentic RAG chạy hoàn toàn nội bộ (Local)** thông qua n8n, kết hợp sức mạnh của Ollama (LLM mã nguồn mở), PostgreSQL (PGVector) và AI Agent thông minh. Toàn bộ dữ liệu của các sếp được giữ an toàn tuyệt đối trên server riêng mà không cần gửi lên các bên thứ ba!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các mô hình AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa xử lý tài liệu**: Tự động nhận diện file mới đưa vào hệ thống (PDF, Excel, CSV, Text), chia nhỏ văn bản và lưu trữ vector embeddings.
- **Agentic RAG thông minh**: AI Agent có khả năng tự động lựa chọn công cụ phù hợp (tìm kiếm vector, chạy truy vấn SQL cho dữ liệu bảng, hoặc đọc toàn bộ tài liệu) dựa trên câu hỏi của người dùng.
- **Bảo mật tuyệt đối**: Chạy 100% local với Ollama, dữ liệu không rời khỏi hệ thống của doanh nghiệp.
- **Phân tích số liệu chính xác**: Xử lý mượt mà các file bảng biểu (Excel/CSV) nhờ lưu trữ dạng JSONB trên PostgreSQL thay vì chỉ cắt đoạn văn bản đơn thuần.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (phiên bản hỗ trợ LangChain/AI nodes).
- **Ollama**: Đã cài đặt Ollama chạy local hoặc trên Docker với các model:
  - LLM: `qwen2.5:14b-8k` (hoặc model tùy chọn qua OpenAI-compatible API).
  - Embedding: `nomic-embed-text:latest`.
- **PostgreSQL Database**: Đã bật extension `pgvector` để lưu trữ vector embeddings và dữ liệu bảng.
- **Thư mục chia sẻ (Shared Folder)**: Thư mục trên ổ cứng được mount vào container n8n (mặc định đường dẫn `/data/shared`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Khởi tạo Database**: Chạy các node như `Create Document Metadata Table`, `Create Document Rows Table (for Tabular Data)` một lần trước để thiết lập các bảng cần thiết trong PostgreSQL/Supabase.
- **Cấu hình Ollama & OpenAI Chat Model**: 
  - Do có một số điểm lưu ý về node Ollama trong n8n, tác giả khuyến nghị sử dụng node `Ollama (Change Base URL)` (thuộc loại `lmChatOpenAi`) với Base URL trỏ về Ollama của các sếp (ví dụ: `http://ollama:11434/v1`). API Key có thể điền bất kỳ chuỗi nào vì Ollama local không yêu cầu xác thực.
- **Embeddings Ollama**: Cấu hình các node `Embeddings Ollama` và `Embeddings Ollama1` sử dụng model `nomic-embed-text:latest`.
- **Local File Trigger**: Cấu hình đường dẫn thư mục `path` trỏ chính xác đến `/data/shared` nơi các sếp sẽ bỏ tài liệu vào.
- **Postgres PGVector Store**: Điền thông tin kết nối Database PostgreSQL (đã cài extension `pgvector`) cho các node Vector Store.

#### 3. Kích hoạt ⚡️
- Thử nghiệm bỏ một file PDF hoặc Excel mẫu vào thư mục `/data/shared` để workflow tự động kích hoạt xử lý.
- Sử dụng giao diện Chat (`When chat message received` / Webhook) để đặt câu hỏi thử nghiệm và kiểm tra phản hồi từ Agent.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối giao diện Chat**: Tích hợp thêm webhook trả về qua Telegram Bot hoặc Slack để nhân viên có thể tra cứu tài liệu nội bộ trực tiếp từ ứng dụng chat hàng ngày.
- **Tùy chỉnh System Prompt**: Tinh chỉnh prompt trong node `RAG AI Agent` để AI phản hồi theo đúng văn phong và chuyên ngành của công ty các sếp.
- **Quản lý lịch sử chat**: Tận dụng node `Postgres Chat Memory` để duy trì ngữ cảnh trò chuyện mượt mà qua nhiều lượt hỏi đáp.

### 📌 Kết luận
Hệ thống Agentic RAG local với Ollama và PGVector là giải pháp hoàn hảo để xây dựng "Bộ não AI nội bộ" cho doanh nghiệp mà không tốn chi phí API đắt đỏ hay lo ngại rò rỉ dữ liệu. Hãy triển khai ngay hôm nay để tối ưu hóa việc quản lý và khai thác tri thức của doanh nghiệp các sếp!