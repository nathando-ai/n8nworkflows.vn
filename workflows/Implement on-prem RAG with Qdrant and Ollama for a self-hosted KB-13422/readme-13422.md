---
title: "🚀 Xây dựng hệ thống RAG On-Premise bảo mật với Qdrant và Ollama trong n8n"
description: "Hướng dẫn triển khai hệ thống hỏi đáp tài liệu nội bộ (RAG) hoàn toàn tự túc, bảo mật dữ liệu tuyệt đối bằng n8n, Qdrant và mô hình AI cục bộ Ollama."
slug: "xay-dung-he-thong-rag-on-premise-qdrant-ollama-n8n"
tags: [n8n, automation, ai-rag, qdrant, ollama, self-hosted, llm]
keywords: [n8n workflow, rag on-premise, qdrant vector store, ollama ai, tu dong hoa tai lieu, ai agent]
---

# 🚀 Xây dựng hệ thống RAG On-Premise bảo mật với Qdrant và Ollama trong n8n

Các doanh nghiệp và đội ngũ thường gặp khó khăn khi muốn ứng dụng AI vào kho tri thức nội bộ nhưng lại ngại đưa tài liệu mật lên các dịch vụ đám mây công cộng (như OpenAI, Anthropic). Việc phụ thuộc vào cloud bên thứ ba vừa tốn kém lại tiềm ẩn rủi ro lộ lọt thông tin.

Workflow này chính là giải pháp **tự động hóa 100% On-Premise (chạy cục bộ)**, giúp các sếp xây dựng một hệ thống Trích xuất tài liệu kết hợp Tạo sinh (RAG) hoàn toàn khép kín, bảo mật tuyệt đối, không tốn phí API bên ngoài nhờ kết hợp sức mạnh của **n8n, Qdrant Vector Store và Ollama**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết hợp mượt mà với các dịch vụ On-Premise, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối:** Dữ liệu tài liệu và câu hỏi không bao giờ rời khỏi hệ thống mạng nội bộ hoặc VPS riêng của các sếp.
- **Tự động hóa kho tri thức:** Tải lên tài liệu mới qua giao diện Web Form gọn gàng, hệ thống tự động băm nhỏ (chunking) và lưu vào cơ sở dữ liệu vector.
- **Hỏi đáp thông minh (RAG):** AI Agent tự động tìm kiếm các đoạn tài liệu liên quan nhất trong Qdrant để trả lời chính xác, hạn chế tối đa tình trạng "ảo giác" (hallucination).
- **Tiết kiệm chi phí:** Không tốn một đồng tiền phí token API nào nhờ chạy các mô hình nguồn mở qua Ollama.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hạ tầng n8n:** Đã cài đặt n8n (Self-hosted khuyến nghị).
- **Ollama:** Cài đặt sẵn trên máy chủ cục bộ hoặc VPS kèm các model (`mistral:7b`, `nomic-embed-text:latest`).
- **Qdrant Vector Database:** Chạy qua Docker hoặc native trên server.
- **Credentials trong n8n:** 
  - `ollamaApi`: Kết nối tới Ollama instance.
  - `qdrantApi`: Kết nối tới Qdrant instance.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sao chép đoạn JSON và dán trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 2 nhánh chính rõ rệt: **Cập nhật kho tri thức (Update Knowledge Base)** và **Truy vấn kho tri thức (Query Knowledge Base)**.

* **Cài đặt hạ tầng nền tảng trước khi cấu hình n8n:**
  - Cài đặt Ollama trên server:
    ```bash
    mkdir ollama && cd ollama
    curl -fsSL https://ollama.com/install.sh | sh
    ```
  - Tải các model cần thiết:
    ```bash
    ollama pull mistral:7b
    ollama pull nomic-embed-text:latest
    ```
  - Khởi chạy Qdrant qua Docker:
    ```bash
    docker run -d -p 6333:6333 -p 6334:6334 -v $(pwd)/qdrant_storage:/qdrant/storage qdrant/qdrant
    ```
  - Truy cập Qdrant Dashboard tại `http://localhost:6333/dashboard` và tạo một Collection tên là `knowledge-base` với kích thước vector (vector length) tương ứng với model embedding (ví dụ: `768` cho `nomic-embed-text`).

* **Cấu hình các Nodes trong n8n:**
  - **Upload document (`formTrigger`):** Tạo giao diện web form để người dùng kéo thả tài liệu vào hệ thống.
  - **Default Data Loader (`documentDefaultDataLoader`):** Xử lý việc đọc và tách nhỏ cấu trúc tài liệu tải lên.
  - **Embeddings Ollama & Add to Qdrant Vector Store:** Trỏ cấu hình `ollamaApi` về địa chỉ Ollama của các sếp (ví dụ: `http://localhost:11434`), chọn model `nomic-embed-text:latest`. Kết nối `qdrantApi` tới Qdrant collection `knowledge-base`.
  - **When chat message received (`chatTrigger`) & AI Agent:** Cung cấp khung chat giao tiếp thân thiện cho người dùng cuối.
  - **Ollama Chat Model (`lmChatOllama`):** Chọn model sinh văn bản chính, ví dụ `mistral:7b`.
  - **Read from Qdrant Vector Store:** Đóng vai trò retriever, tự động quét kho vector tìm kiếm ngữ cảnh phù hợp nhất khi người dùng đặt câu hỏi trên chat.
  - **Simple Memory (`memoryBufferWindow`):** Lưu trữ ngữ cảnh hội thoại ngắn hạn giúp AI nhớ được các câu hỏi trước đó trong phiên chat.

#### 3. Kích hoạt ⚡️
- Bấm **Execute workflow** và thử tải lên một tài liệu mẫu qua Web Form của node `Upload document`.
- Mở giao diện chat từ node `When chat message received` để kiểm tra khả năng trả lời dựa trên tài liệu vừa nạp.
- Khi mọi thứ hoạt động trơn tru, bật trạng thái **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm node Google Drive, IMAP (Email) hoặc Telegram để tự động thu thập tài liệu đưa vào kho Qdrant thay vì chỉ dùng Web Form thủ công.
- **Tích hợp kênh chat:** Thay vì dùng khung chat mặc định của n8n, các sếp có thể đổi trigger sang Telegram Trigger hoặc Slack Trigger để tạo trợ lý ảo nội bộ ngay trên ứng dụng chat của công ty.
- **Log và Giám sát:** Thêm một node lưu lịch sử câu hỏi và câu trả lời vào PostgreSQL hoặc Google Sheets để phân tích nhu cầu tìm kiếm thông tin của nhân sự.

### 📌 Kết luận
Việc tự xây dựng một hệ thống RAG nội bộ chưa bao giờ dễ dàng và tiết kiệm đến thế với sự kết hợp của n8n, Qdrant và Ollama. Hãy triển khai ngay hôm nay để tối ưu hóa việc quản lý tri thức cho doanh nghiệp mà vẫn đảm bảo an toàn dữ liệu tuyệt đối!