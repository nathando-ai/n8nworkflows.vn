---
title: "🚀 Xây dựng Hệ thống Tìm kiếm PDF với Mistral OCR & Weaviate"
description: "Tự động trích xuất nội dung PDF bằng OCR Mistral, tạo embedding Cohere và lưu trữ trong Weaviate để tìm kiếm nhanh, chính xác 100% không cần viết code."
slug: "he-thong-tim-kiem-pdf-mistral-ocr-weaviate"
tags: [n8n, automation, no-code, AI, OCR, vector-database]
keywords: [n8n workflow, tự động hóa, OCR, Weaviate, Mistral AI, Cohere embeddings]
---

# 🚀 Xây dựng Hệ thống Tìm kiếm PDF với Mistral OCR & Weaviate

Doanh nghiệp y tế, phòng khám hay bất kỳ tổ chức nào cần truy cập nhanh vào tài liệu y khoa, báo cáo lâm sàng hay hướng dẫn điều trị thường phải đối mặt với **công việc nhập liệu thủ công**: mở PDF, sao chép nội dung, dán vào công cụ tìm kiếm…  
Quá trình này tốn thời gian, dễ sai sót và không thể mở rộng khi lượng tài liệu tăng lên.

**Workflow n8n** này giải quyết toàn bộ vấn đề bằng cách:
1. **Nhận PDF** từ người dùng qua form web.  
2. **OCR** bằng Mistral AI để chuyển hình ảnh thành văn bản thuần.  
3. **Tách đoạn** (text splitter) và **tạo embedding** bằng Cohere.  
4. **Lưu trữ vector** trong **Weaviate DB** – một vector database mạnh mẽ, hỗ trợ tìm kiếm ngữ nghĩa.  
5. **Cung cấp API** (MCP Knowledge Server) để các mô hình AI khác có thể truy vấn kiến thức ngay lập tức.

Kết quả: **tìm kiếm PDF nhanh gấp 10‑20 lần**, độ chính xác cao, luôn sẵn sàng 24/7 mà không cần viết một dòng code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động trích xuất và lập chỉ mục trong vài giây.  
- **Độ chính xác cao**: OCR Mistral + embedding Cohere giảm lỗi ngữ nghĩa.  
- **Tìm kiếm ngữ nghĩa**: Không cần nhớ từ khóa chính xác, chỉ nhập câu hỏi.  
- **Hoạt động liên tục**: Workflow chạy trên server, luôn sẵn sàng trả lời yêu cầu.  
- **Mở rộng dễ dàng**: Thêm nguồn dữ liệu (Word, TXT) chỉ bằng một node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Mistral AI** → API Key (để OCR).  
- **Tài khoản Cohere** → API Key (để embeddings & rerank).  
- **Weaviate DB**: URL, Port và API Key (có thể dùng Weaviate Cloud hoặc tự host).  
- **n8n**: Đã cài đặt và truy cập được UI.  
- **MCP Server**: Được bật trong workflow (để các AI khác gọi).  
- **Form Trigger**: URL công khai để người dùng upload PDF.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `pdf-search-mistral-weaviate.json` (được cung cấp trong mục **Resources**).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** → **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **10 node** quan trọng và cách cấu hình chúng:

| Node | Loại | Hướng dẫn cấu hình chi tiết |
|------|------|-----------------------------|
| **Upload PDF** | `formTrigger` | - **Form URL**: Đặt URL công khai (ví dụ: `https://your-n8n.com/webhook/pdf-upload`). <br>- **Field**: `file` (type: File). <br>- **Method**: POST. |
| **Extract Text from PDF** | `mistralAi` | - **Credentials**: Chọn **Mistral API** → nhập **API Key**.<br>- **Operation**: `OCR`.<br>- **Input**: Đường dẫn file PDF từ node `Upload PDF` ({{ $json["file"]["path"] }}). |
| **Text Splitter** | `textSplitterRecursiveCharacterTextSplitter` | - **Chunk Size**: 1000 (hoặc tùy tài liệu). <br>- **Chunk Overlap**: 200.<br>- **Input**: Kết quả `Extract Text from PDF`. |
| **Cohere Embeddings** | `embeddingsCohere` | - **Credentials**: **Cohere API** → nhập **API Key**.<br>- **Model**: `embed-english-v3.0` (hoặc model phù hợp). |
| **Cohere Reranker** | `rerankerCohere` | - **Credentials**: **Cohere API**.<br>- **Model**: **Same** với node Embeddings (đảm bảo **không đổi**). |
| **Prepare Document Data** | `set` | - **Values**: <br>  - `content`: `{{$json["text"]}}` (từ Text Splitter). <br>  - `metadata`: `{ "source": "PDF", "filename": "{{$json["file"]["originalName"]}}" }`. |
| **Store in Vector Database** | `vectorStoreWeaviate` (lưu trữ) | - **Credentials**: **Weaviate** → URL, API Key.<br>- **Class Name**: `DocumentChunk` (tạo trước trong Weaviate). <br>- **Embedding**: Chọn **Cohere Embeddings**.<br>- **Metadata**: Map `metadata` field. |
| **Search Knowledge Base** | `vectorStoreWeaviate` (truy vấn) | - **Credentials**: Same Weaviate.<br>- **Class Name**: `DocumentChunk`.<br>- **Embedding**: Same Cohere model.<br>- **Top K**: 5‑10. |
| **Document Loader** | `documentDefaultDataLoader` | - **Input**: Kết quả từ `Search Knowledge Base`. <br>- **Output**: Dữ liệu dạng `Document[]` để trả về cho MCP. |
| **MCP Knowledge Server** | `mcpTrigger` | - **Path**: `c74c97f5-0197-45e3-b4dd-f3efbd4bab22` (không thay đổi). <br>- **Method**: POST. <br>- **Response**: Trả về danh sách tài liệu đã tìm được. |

> **Lưu ý quan trọng:** *Embedding* và *Rerank* **phải** dùng **cùng một model** của Cohere. Nếu đổi model ở một node, hãy đồng bộ ngay ở node còn lại, tránh lỗi “model mismatch”.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → tải một PDF mẫu (khoảng 2‑3 trang). Kiểm tra log ở các node để chắc chắn OCR, split, embedding và lưu vào Weaviate thành công.  
2. Khi mọi thứ ổn → **Toggle** nút **Active** (ở góc trên bên phải).  
3. Kiểm tra API MCP: Gửi POST tới `https://your-n8n.com/webhook/c74c97f5-0197-45e3-b4dd-f3efbd4bab22` với payload `{ "query": "triệu chứng viêm loét dạ dày" }`. Kết quả sẽ là danh sách đoạn PDF liên quan.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `Search Knowledge Base` để tự động gửi kết quả cho bác sĩ qua chat.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` để ghi lại file PDF gốc và văn bản OCR vào bucket S3, phục vụ audit.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `Weaviate` query để tổng hợp số lượng tài liệu mới, tần suất truy vấn, gửi email weekly.  
- **Mở rộng nguồn dữ liệu**: Thêm node `Google Drive Trigger` hoặc `Dropbox` để tự động ingest tài liệu mới mà không cần upload thủ công.  

### 📌 Kết luận
Với workflow này, các sếp có thể **biến kho tài liệu PDF thành một trí tuệ tìm kiếm ngữ nghĩa** chỉ trong vài phút, giảm tải công việc nhập liệu và tăng tốc độ ra quyết định lâm sàng. Hãy **import ngay**, cấu hình các API key và bật workflow – khám phá sức mạnh của AI trong quản lý kiến thức y tế! 🚀