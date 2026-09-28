---
title: "🚀 Chat với Tài liệu Google Drive bằng GPT, Pinecone và RAG"
description: "Tự động trả lời câu hỏi dựa trên nội dung tài liệu Google Drive, sử dụng GPT-4o, Pinecone và kỹ thuật Retrieval‑Augmented Generation (RAG) – hoàn toàn không cần code."
slug: "chat-voi-tai-lieu-google-drive-gpt-pinecone-rag"
tags: [n8n, automation, no-code, AI RAG, Multimodal AI]
keywords: [n8n workflow, tự động hóa, GPT, Pinecone, RAG, AI Agent, Google Drive]
---

# 🚀 Chat với Tài liệu Google Drive bằng GPT, Pinecone và RAG

Bạn đang phải trả lời hàng trăm câu hỏi về nội dung tài liệu trong Google Drive?  
Bạn muốn khách hàng hoặc đồng nghiệp có thể “đặt câu hỏi” và nhận câu trả lời ngay lập tức, chính xác, dựa trên dữ liệu thực tế trong tài liệu?  

Workflow này sẽ giúp bạn:

- **Tự động** tải xuống tài liệu mới hoặc cập nhật từ Google Drive.
- **Chia nhỏ** tài liệu thành các đoạn văn bản ngắn, **tạo embeddings** bằng OpenAI.
- **Lưu trữ** embeddings vào Pinecone để truy vấn nhanh.
- Khi có **câu hỏi** qua chat (Slack, Telegram, Webhook...), **AI Agent** sẽ tìm kiếm trong vector store, kết hợp với lịch sử hội thoại (memory buffer) và trả lời chính xác.

> **Đây là một giải pháp 100% no‑code**: chỉ cần kéo‑thả node, điền credential và vài tham số, workflow đã sẵn sàng chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code, chỉ cần cấu hình 1 workflow.  
- **Chính xác cao**: GPT-4o kết hợp với embeddings chính xác trích xuất thông tin.  
- **Cá nhân hóa**: Mỗi người dùng có lịch sử hội thoại riêng (memory buffer).  
- **Hoạt động liên tục**: Khi tài liệu được cập nhật, dữ liệu mới tự động được thêm vào vector store.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Credential | Mô tả |
|---------|------------|-------|
| **OpenAI** | `openAiApi` | API key cho GPT‑4o và embeddings `text-embedding-3-small`. |
| **Google Drive** | `googleDriveOAuth2Api` | OAuth2 token, cần quyền đọc/viết tài liệu. |
| **Pinecone** | `pineconeApi` | API key, namespace và index đã được tạo. |
| **Chat Platform** | - | Đối với `chatTrigger` (Slack, Telegram, Webhook, …) cần cấu hình token/URL. |
| **VPS** | - | Để chạy n8n 24/7. |
:::

### Cấu hình Pinecone

- **Index name**: `n8n-rag-index` (hoặc tên tùy ý).  
- **Dimension**: 1536 (kích thước embedding `text-embedding-3-small`).  
- **Metric**: `cosine`.  
- **Namespace**: `default` (hoặc tên riêng).  

### Cấu hình Google Drive

- **Folder ID**: ID thư mục chứa tài liệu cần index.  
- **File ID**: ID file khi cần tải xuống.  

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON từ link gốc: <https://n8n.io/workflows/7979>  
2. Trong n8n Editor, chọn **Import** → **Upload JSON** → chọn file.  
3. Hoặc copy toàn bộ JSON và dán vào **Import JSON**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên trong workflow | Credential cần chọn | Tham số cần chỉnh |
|------|--------------------|----------------------|-------------------|
| **Google Drive Trigger** | `Google Drive File Created`, `Google Drive File Updated` | `googleDriveOAuth2Api` | `Folder ID` (đặt ID thư mục cần theo dõi) |
| **Google Drive (download)** | `Download File From Google Drive`, `Download File From Google Drive1` | `googleDriveOAuth2Api` | `File ID` (được truyền từ trigger) |
| **OpenAI Chat Model** | `OpenAI Chat Model`, `OpenAI Chat Model1` | `openAiApi` | `Model` = `gpt-4o-2024-08-06` |
| **Embeddings OpenAI** | `Generate Embeddings for Search with OpenAI`, `Embeddings OpenAI1` | `openAiApi` | `Model` = `text-embedding-3-small` |
| **Vector Store (Pinecone)** | `Pinecone Vector Store`, `Pinecone Vector Store (Retrieval)` | `pineconeApi` | `Index name`, `Namespace`, `Dimension` = 1536 |
| **Tool Vector Store** | `Vector Store Tool` | - | `Vector Store` = `Pinecone Vector Store` |
| **Memory Buffer Window** | `Window Buffer Memory` | - | `Window size` (định số lượng tin nhắn lưu) |
| **Agent** | `AI Sales Agent` | - | `Tools` = `Vector Store Tool`, `Memory` = `Window Buffer Memory` |
| **Chat Trigger** | `When chat message received` | - | `Platform` (Slack/Telegram/Webhook) |
| **Document Loader** | `Default Data Loader` | - | `Data` = nội dung file đã tải xuống |
| **Text Splitter** | `Recursive Character Text Splitter` | - | `Chunk size` (định độ dài đoạn) |
| **Sticky Note** | `Sticky Note` | - | - (để ghi chú, không ảnh hưởng tới workflow) |

> **Lưu ý**:  
> - Đảm bảo **API keys** đã được cấp quyền đầy đủ.  
> - Nếu sử dụng **Slack**, cần tạo bot, cấp quyền `chat:write`, `chat:read`.  
> - Nếu sử dụng **Telegram**, cần tạo bot và cấu hình webhook.  

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow với dữ liệu mẫu (đăng một file vào thư mục Google Drive, gửi tin nhắn qua chat).  
2. Kiểm tra log: xem embeddings được tạo, lưu vào Pinecone, và AI Agent trả lời.  
3. Khi mọi thứ ổn, bật **Active** cho workflow.  
4. Đảm bảo n8n luôn chạy (đặt cron hoặc systemd service).

## ✍️ Mẹo & gợi ý nâng cao

- **Gửi báo cáo định kỳ**: Thêm node `Cron` + `HTTP Request` để gửi summary qua Slack.  
- **Lưu log**: Dùng node `Write Binary File` để ghi log vào Google Drive hoặc S3.  
- **Tích hợp thêm Slack/Telegram**: Thêm `Slack` hoặc `Telegram` node vào `chatTrigger` để mở rộng kênh.  
- **Cập nhật index tự động**: Khi file được cập nhật, workflow sẽ tự động re‑embed và cập nhật Pinecone.  
- **Sử dụng LLM khác**: Thay `lmChatOpenAi` bằng `lmChatAnthropic` nếu muốn thử nghiệm.  

## 📌 Kết luận

Workflow “Chat với Tài liệu Google Drive bằng GPT, Pinecone và RAG” là công cụ mạnh mẽ giúp doanh nghiệp chuyển đổi dữ liệu tài liệu thành nguồn tri thức sống động, trả lời nhanh chóng và chính xác.  
Hãy **cài đặt ngay** trên VPS, cấu hình credential, và trải nghiệm sức mạnh của AI trong quy trình làm việc của bạn!