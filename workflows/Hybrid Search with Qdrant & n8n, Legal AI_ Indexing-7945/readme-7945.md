---
title: "🚀 Xây Dựng Hệ Thống Tìm Kiếm Lai (Hybrid Search) Pháp Lý với Qdrant và n8n: Phần 1 - Đánh Dữ Liệu (Indexing)"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình lấy tập dữ liệu pháp lý từ Hugging Face, xử lý văn bản, tạo vector (Dense & Sparse) và index vào Qdrant bằng n8n."
slug: "hybrid-search-qdrant-n8n-legal-ai-indexing"
tags: [n8n, qdrant, vector-database, ai, hybrid-search, huggingface]
keywords: [n8n workflow, qdrant hybrid search, legal ai, embedding openai, qdrant cloud inference, bm25]
---

# 🚀 Xây Dựng Hệ Thống Tìm Kiếm Lai (Hybrid Search) Pháp Lý với Qdrant & n8n: Phần 1 - Đánh Dữ Liệu

Các sếp đang gặp khó khăn khi xây dựng hệ thống tìm kiếm tài liệu pháp lý thông minh? Tìm kiếm từ khóa (Keyword search) thì bỏ sót ngữ nghĩa, mà tìm kiếm thuần vector (Semantic search) đôi khi lại bỏ quên các thuật ngữ pháp lý chính xác? 

Workflow **"Hybrid Search with Qdrant & n8n, Legal AI: Indexing"** này chính là giải pháp tự động hóa 100% không cần code giúp các sếp kết hợp sức mạnh của cả **Dense Vectors** (tìm kiếm ngữ nghĩa) và **Sparse Vectors/BM25** (tìm kiếm từ khóa chính xác) thông qua cơ sở dữ liệu vector Qdrant và n8n!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Kéo dữ liệu từ Hugging Face, làm sạch, khử trùng lặp (deduplicate) và đẩy lên Qdrant hoàn toàn tự động.
- **Hỗ trợ Tìm kiếm Lai (Hybrid Search)**: Tạo cả vector dày (Dense) lẫn vector thưa (Sparse cho BM25) để tối ưu độ chính xác cho ngành luật.
- **Linh hoạt phương thức tạo Embedding**: Hỗ trợ 2 cách: Dùng **Qdrant Cloud Inference** (tự động hóa hoàn toàn) hoặc dùng **OpenAI API**.
- **Tiết kiệm thời gian xử lý**: Chia batch thông minh, xử lý dữ liệu lớn không lo tràn bộ nhớ hay lỗi timeout.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (bản self-hosted hoặc cloud).
- **Qdrant Cloud Account**: Một cluster trên [Qdrant Cloud](https://cloud.qdrant.io/) (chọn vùng US nếu dùng tính năng Cloud Inference).
- **OpenAI API Key**: (Tùy chọn) Nếu các sếp muốn dùng mô hình `text-embedding-3-small` thay vì Cloud Inference của Qdrant.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ liên kết gốc hoặc copy toàn bộ JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Click vào dấu 3 chấm góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 30 nodes được chia thành các cụm chức năng chính. Các sếp cần cấu hình kỹ các điểm sau:

- **Cấu hình Qdrant Credentials**: 
  - Tại các node liên quan đến Qdrant như `Create Collection`, `Check Collection Exists`, `Upsert Points`, v.v., các sếp cần cấu hình **Qdrant API Credentials** bao gồm **URL** và **API Key** lấy từ giao diện Qdrant Cloud.
- **Lấy dữ liệu từ Hugging Face (`Index Dataset from HuggingFace`, `Get Dataset Splits`, `Get Dataset Rows`)**:
  - Workflow sử dụng Dataset Viewer API của Hugging Face để tải tập dữ liệu pháp lý `isaacus/LegalQAEval`. Đảm bảo node HTTP Request cấu hình đúng cơ chế phân trang (Pagination) để tải toàn bộ dataset.
- **Lựa chọn Phương án tạo Embedding**:
  - **Option 1 (Mặc định)**: Sử dụng mô hình `mxbai-embed-large-v1` (1024 dimensions) thông qua **Qdrant Cloud Inference** (yêu cầu cluster trả phí ở vùng US).
  - **Option 2**: Sử dụng **OpenAI API** với mô hình `text-embedding-3-small` (1536 dimensions). Nếu chọn cách này, các sếp cần kết nối credential `openAiApi` tại node `Get OpenAI embeddings` và sử dụng nhánh collection thứ hai (`Create Collection1`, `Upsert Points1`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) bằng cách bấm nút **Execute Workflow** tại node `Index Dataset from HuggingFace` để kiểm tra từng cụm xử lý (tính toán chiều dài văn bản trung bình cho BM25, tạo collection, sinh vector và upsert lên Qdrant).
- Sau khi test thành công, gạt công tắc sang **Active** để sẵn sàng đưa vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo Telegram/Slack**: Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi quá trình index hàng ngàn văn bản pháp lý hoàn tất.
- **Tự động hóa định kỳ**: Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` để hệ thống tự động quét và cập nhật dữ liệu mới từ nguồn Hugging Face hàng tuần/hàng tháng.
- **Kiểm tra kết quả**: Sau khi chạy xong, hãy chuyển sang Phần 2 ("Hybrid Search with Qdrant & n8n, Legal AI: Retrieval") để cấu hình hệ thống tìm kiếm và đánh giá độ chính xác.

### 📌 Kết luận
Với workflow n8n này, việc xây dựng một hệ thống cơ sở tri thức pháp lý hỗ trợ Hybrid Search đỉnh cao không còn là điều phức tạp. Hãy áp dụng ngay để tối ưu hóa năng lực tìm kiếm thông tin cho trợ lý ảo hoặc hệ thống AI của doanh nghiệp các sếp!