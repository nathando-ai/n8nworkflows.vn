---
title: "🚀 Xây dựng hệ thống Hybrid Search và Đánh giá Legal AI với Qdrant & n8n"
description: "Hướng dẫn chi tiết cách tự động hóa kiểm tra chất lượng tìm kiếm lai (Hybrid Search) kết hợp BM25 và Vector Search trên tập dữ liệu pháp lý bằng Qdrant và n8n."
slug: "hybrid-search-qdrant-legal-ai-n8n"
tags: [n8n, automation, qdrant, vector-database, legal-ai, hybrid-search, huggingface]
keywords: [n8n workflow, qdrant vector search, hybrid search n8n, legal ai rag, đánh giá retriever, bm25 qdrant]
---

# 🚀 Xây dựng hệ thống Hybrid Search và Đánh giá Legal AI với Qdrant & n8n

Trong các ứng dụng Trí tuệ Nhân tạo Pháp lý (Legal AI) và RAG (Retrieval-Augmented Generation), việc tìm kiếm chính xác các điều luật hoặc văn bản liên quan là yếu tố "sống còn". Tuy nhiên, việc thực hiện thủ công các bài kiểm tra đánh giá chất lượng tìm kiếm (retrieval evaluation) thường mất rất nhiều thời gian và công sức. 

Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Lấy dữ liệu câu hỏi từ Hugging Face, thực hiện **Hybrid Search** (kết hợp tìm kiếm từ khóa BM25 và tìm kiếm ngữ nghĩa Vector Search qua mxbai-embed-large-v1) trên **Qdrant**, sau đó tự động tính toán chỉ số đánh giá `hits@1` để đo lường độ chính xác mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá RAG:** Tự động hóa hoàn toàn quy trình test độ chính xác của bộ lọc (retriever) dựa trên tập dữ liệu chuẩn.
- **Hybrid Search tối ưu:** Kết hợp sức mạnh của từ khóa chính xác (BM25) và ngữ nghĩa sâu (Vector embedding) sử dụng Qdrant Cloud Inference.
- **Đo lường rõ ràng:** Tự động tính toán tỷ lệ `hits@1` (phần trăm câu trả lời đúng nằm ở kết quả top-1).
- **Nền tảng cho Agentic RAG:** Có thể tái sử dụng node Qdrant làm công cụ (tool) cho các hệ thống chatbot pháp lý thông minh sau khi đã tối ưu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
- **Qdrant Cloud Account:** Đã hoàn thành phần Indexing (Phần 1) với collection chứa tập dữ liệu `LegalQAEval (isaacus)` trên Qdrant.
- **Qdrant Credentials:** API Key và URL kết nối với Qdrant Vector Database.
- **Kết nối Internet:** Để gọi API Dataset Viewer từ Hugging Face.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp (Ctrl+V / Cmd+V) vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 14 nodes, trong đó các điểm mấu chốt cần lưu ý cấu hình:
- **Index Dataset from HuggingFace (manualTrigger):** Nút khởi chạy thủ công quy trình test.
- **Get Dataset Splits & Get Test Queries (httpRequest):** Gọi API từ Hugging Face Dataset Viewer lấy tập dữ liệu `LegalQAEval (isaacus)`. Các sếp có thể cấu hình thêm phân trang (pagination) nếu muốn test với toàn bộ tập dữ liệu thay vì một subset nhỏ.
- **Query Points (Qdrant Node):** 
  - Chọn đúng **Credentials** kết nối tới Qdrant Cloud của các sếp.
  - Cấu hình collection name trùng với tên collection đã tạo ở Phần 1 (Indexing).
  - Node này sẽ thực hiện Hybrid Search (kết hợp BM25 sparse vector và dense vector `mxbai-embed-large-v1`) và áp dụng Reciprocal Rank Fusion (RRF) để lấy ra top kết quả tốt nhất.
- **Loop Over Items / Filter Nodes:** Xử lý lặp qua từng câu hỏi, lọc các câu hỏi có chứa đáp án hợp lệ để đảm bảo tính công bằng cho bài kiểm tra.
- **Aggregate Evals & Percentage of isHits in Evals (set/aggregate):** Tổng hợp dữ liệu kết quả để tính ra phần trăm `hits@1`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với tập dữ liệu mẫu và kiểm tra kết quả đầu ra ở các node thống kê cuối luồng.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, có thể chuyển trạng thái workflow sang **Active** nếu muốn tự động hóa định kỳ.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram vào cuối luồng để tự động gửi báo cáo tỷ lệ `hits@1` mỗi khi chạy đánh giá.
- **Mở rộng RAG Agent:** Tái sử dụng node `Query Points` từ workflow này làm công cụ tra cứu (Tool) cho AI Agent chuyên tư vấn luật.
- **Cải thiện độ chính xác:** Nếu kết quả `hits@1` chưa đạt kỳ vọng, hãy thử nghiệm thêm các kỹ thuật như Reranking (Cohere/Jina), điều chỉnh trọng số score boosting, hoặc tinh chỉnh tham số vector index trên Qdrant.

### 📌 Kết luận
Workflow này là bước đệm hoàn hảo giúp các sếp tự động hóa việc đo lường và tối ưu hóa chất lượng tìm kiếm cho các ứng dụng Legal AI. Hãy áp dụng ngay để nâng cấp hệ thống RAG của doanh nghiệp lên một tầm cao mới!