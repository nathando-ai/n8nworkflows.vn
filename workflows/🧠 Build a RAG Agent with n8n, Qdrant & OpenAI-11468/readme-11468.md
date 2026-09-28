---
title: "🚀 Xây dựng RAG Agent với n8n, Qdrant & OpenAI"
description: "Tự động hoá quy trình ingest tài liệu từ Google Drive, tạo vector embeddings và trả lời câu hỏi qua chatbot AI – không cần viết một dòng code."
slug: "xay-dung-rag-agent-n8n-qdrant-openai"
tags: [n8n, automation, no-code, AI, RAG, Qdrant, OpenAI, Google Drive]
keywords: [n8n workflow, tự động hóa, RAG agent, Qdrant, OpenAI, chatbot]
---

# 🚀 Xây dựng RAG Agent với n8n, Qdrant & OpenAI

Bạn từng cảm thấy mệt mỏi khi phải tìm kiếm thông tin trong hàng chục tài liệu PDF, Word hoặc Google Docs? Quy trình thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, khiến đội ngũ không thể tập trung vào công việc sáng tạo. Workflow **RAG Agent** này giải quyết triệt để vấn đề đó: mỗi khi bạn tải file mới lên Google Drive, hệ thống sẽ tự động chuyển đổi nội dung thành Markdown, chia nhỏ, tạo embeddings bằng OpenAI và lưu trữ trong Qdrant – một vector database siêu nhanh. Sau khi cơ sở kiến thức được xây dựng, bạn chỉ cần trò chuyện với agent qua giao diện chat để nhận được câu trả lời chính xác, dựa trên tài liệu đã có.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ công**: Tài liệu mới được ingest và sẵn sàng để truy vấn trong vòng vài giây.
- **Chính xác cao**: Câu trả lời được sinh ra từ các đoạn văn bản thực tế trong kho kiến thức, giảm ảo觉.
- **Cá nhân hoá dễ dàng**: Chỉ cần thay đổi folder Google Drive hoặc model LLM để phù hợp với từng dự án.
- **Hoạt động liên tục**: Workflow kích hoạt tự động khi có file mới, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Drive OAuth2 API** – để node *Detect New Files* và *Download as Markdown* truy cập tài liệu.
- **Qdrant API** – để hai node *Insert into Vector Store* và *Search Documents* lưu trữ và truy xuất vector.
- **OpenAI API Key** – để node *Generate Embeddings* (embeddingsOpenAi) và *Generate Response* (lmChatOpenAi) hoạt động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Trong n8n Editor, nhấn **Import** → **From URL** hoặc **Upload file JSON** của workflow.
2. Hoặc copy toàn bộ JSON từ trang mẫu và dán vào ô **Paste JSON** → **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình cụ thể cho từng node sau:

| Node (tên chính xác) | Loại node | Cần cấu hình |
|----------------------|-----------|--------------|
| **Detect New Files** | `googleDriveTrigger` | - Chọn **Credentials** → Google Drive OAuth2 đã chuẩn bị.<br>- Đặt **Folder ID** của thư mục Google Drive nơi bạn sẽ upload file (ví dụ: `1BevhU5qdgNDFbK4D9oAYGeK0Dt5sEaxQ`). |
| **Download as Markdown** | `httpRequest` | - Sử dụng cùng **Credentials** Google Drive.<br>- Đảm bảo **URL** được điền đúng dạng `https://www.googleapis.com/drive/v3/files/{{$json["id"]}}?alt=media&mimeType=text/markdown` (n8n thường tự động điền từ node trước). |
| **Add Metadata** | `merge` | - Thường không cần thay đổi; node này gộp metadata từ trigger và nội dung file. Bạn có thể thêm trường tùy chỉnh nếu muốn (ví dụ: `department`, `project`). |
| **Insert into Vector Store** | `vectorStoreQdrant` (lần đầu) | - **Credentials** → Qdrant API.<br>- **Collection Name**: đặt tên collection (ví dụ: `my_rag_collection`).<br>- **Payload Fields**: chọn các trường metadata bạn muốn lưu kèm vector (ví dụ: `fileName`, `uploadedAt`). |
| **Load File Content & Metadata** | `documentDefaultDataLoader` | - Giữ mặc định; node này đọc output từ *Download as Markdown* và chuẩn bị cho bước chia chunk. |
| **Split into Chunks** | `textSplitterRecursiveCharacterTextSplitter` | - Đặt **Chunk Size** (số ký tự mỗi chunk, ví dụ: 1000).<br>- **Chunk Overlap** (số ký tự chồng lấp, ví dụ: 200) để giữ ngữ cảnh. |
| **Generate Embeddings** | `embeddingsOpenAi` | - **Credentials** → OpenAI API.<br>- **Model**: chọn `text-embedding-3-small` hoặc `text-embedding-3-large` tùy chi phí và chất lượng mong muốn. |
| **Chat with a RAG Agent** | `chatTrigger` | - Không cần credential; chỉ cần kích hoạt để mở giao diện chat trong n8n (URL thường là `/chat`). |
| **Answer Questions** | `agent` | - Đảm bảo **Tools** đã được kết nối: node *Search Documents* (vectorStoreQdrant) và *Memory* (memoryBufferWindow).<br>- Đặt **Agent Type** thành `OpenAI Functions` (mặc định). |
| **Generate Response** | `lmChatOpenAi` | - **Credentials** → OpenAI API.<br>- **Model**: `gpt-4o` (đã được pre‑set trong workflow).<br>- **Temperature**: điều chỉnh mức độ sáng tạo (0.2‑0.7 phù hợp cho RAG). |
| **Search Documents** | `vectorStoreQdrant` (lần hai) | - Sử dụng cùng **Credentials** Qdrant.<br>- **Collection Name** phải trùng với collection đã tạo ở node *Insert into Vector Store*.<br>- **Top K**: số lượng chunk trả về (ví dụ: 4). |
| **Store Conversation** | `memoryBufferWindow` | - Đặt **Window Size** (số tin nhắn gần nhất được lưu, ví dụ: 5) để agent nhớ bối cảnh trò chuyện ngắn hạn. |

> **Lưu ý quan trọng**: Sau khi thay đổi bất kỳ trường nào (Credentials, IDs, model, chunk size…), nhấn **Save** trên mỗi node rồi **Deploy** workflow để cập nhật.

#### 3. Kích hoạt ⚡️
1. Nhấn **Test Workflow** và chọn **Upload a file** vào folder Google Drive đã cấu hình để kiểm tra pipeline ingest.
2. Xác nhận rằng file đã được chuyển thành Markdown, chia chunk, tạo embeddings và xuất hiện trong Qdrant (có thể kiểm tra qua Qdrant Dashboard).
3. Mở giao diện chat (thường tại `http://<your-n8n-domain>/chat`) và đặt câu hỏi liên quan đến nội dung file vừa upload.
4. Nếu mọi thứ hoạt động bình thường, bật toggle **Active** ở góc trên bên phải workflow để chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node *Slack* hoặc *Telegram* sau node *Insert into Vector Store* để gửi thông báo khi có tài liệu mới được ingest.
- **Lưu log chi tiết**: Kết hợp node *PostgreSQL* hoặc *MongoDB* để lưu trữ metadata (tên file, thời gian ingest, số chunk) để audit và báo cáo.
- **Báo cáo tuần tự**: Sử dụng node *Cron* để kích hoạt một workflow khác mỗi tuần, truy xuất thống kê từ Qdrant (số vector, trung bình độ dài chunk) và gửi email qua *SendGrid* hoặc *Gmail*.
- **Fallback tìm kiếm web**: Kết hợp node *HTTP Request* với API của Google Search hoặc SerpAPI khi agent không tìm thấy đủ thông tin trong vector store.
- **Tùy chỉnh prompt**: Thêm node *Set* trước *Generate Response* để chèn hướng dẫn cụ thể (ví dụ: “Trả lời bằng tiếng Việt, trích dẫn nguồn nếu có”).
- **Đánh giá chất lượng**: Sau mỗi trả lời, thêm nút “👍 / 👎” qua node *HTTP Request* gửi feedback tới Google Sheet để cải tiến model sau này.

### 📌 Kết luận
Workflow **RAG Agent với n8n, Qdrant & OpenAI** biến việc quản lý kiến thức nội bộ từ một công việc thủ công tốn thời gian thành một hệ thống tự động, thông minh và luôn sẵn sàng trả lời. Các sếp chỉ cần tải file lên Google Drive, để n8n làm phần còn lại, và trò chuyện với AI để nhận được câu trả lời chính xác ngay lập tức. Hãy áp dụng ngay hôm nay để giải phóng sức sáng tạo cho đội ngũ và nâng cao hiệu suất làm việc!