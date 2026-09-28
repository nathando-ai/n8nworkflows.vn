---
title: "🚀 Tự Động Học & Tạo RAG Stack từ Webpage với Firecrawl + OpenAI (Không Cần Code)"
description: "Workflow tự động hóa scrape nội dung webpage, chuyển đổi thành embeddings, lưu trữ trong Pinecone, và xây dựng hệ thống RAG (Retrieval-Augmented Generation) để trả lời câu hỏi bằng AI. Giúp các sếp tiết kiệm thời gian nghiên cứu và cải thiện hiệu suất tìm kiếm thông tin."
slug: "tieu-dong-hoa-scrape-rag-stack-firecrawl-openai"
tags: [n8n, automation, no-code, AI RAG, Firecrawl, Pinecone, OpenAI, document-extraction]
keywords: [n8n workflow scrape webpage, tự động hóa RAG stack, Firecrawl API, OpenAI embeddings, Pinecone vector database, AI chatbot từ dữ liệu web]
---

# 🚀 **Tự Động Học & Tạo RAG Stack từ Webpage với Firecrawl + OpenAI**

### **Giải pháp cho vấn đề gì?**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm và tổng hợp** thông tin từ nhiều trang web.
- **Lọc và xử lý** nội dung rác, trùng lặp, hoặc không liên quan.
- **Tạo cơ sở tri thức** cho AI để trả lời câu hỏi một cách chính xác và tự động.

Workflow này **tự động hóa toàn bộ quy trình** từ **scrape webpage → tạo embeddings → lưu trữ trong Pinecone → xây dựng AI RAG** để trả lời câu hỏi bằng ngôn ngữ tự nhiên. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Scrape và xử lý hàng ngàn trang web trong vài phút.
✅ **Tìm kiếm thông minh**: AI trả lời câu hỏi dựa trên dữ liệu webpage với độ chính xác cao.
✅ **Cập nhật tự động**: Khi webpage thay đổi, embeddings cũng được cập nhật.
✅ **Không giới hạn dữ liệu**: Dùng Pinecone để lưu trữ lượng lớn embeddings.
✅ **Tích hợp AI hiện đại**: Sử dụng OpenAI (embeddings), OpenRouter (chatbot), và Cohere (reranking).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
| **Tài nguyên**               | **Mô tả**                                                                 | **Liên kết tham khảo**                          |
|-------------------------------|----------------------------------------------------------------------------|--------------------------------------------------|
| **API Key Firecrawl**         | Để scrape webpage một cách chính xác và nhanh chóng.                     | [Firecrawl API](https://firecrawl.dev/)         |
| **API Key OpenAI**            | Để tạo embeddings (model: `text-embedding-3-small`).                     | [OpenAI API](https://platform.openai.com/)       |
| **API Key OpenRouter**        | Để chạy AI chatbot (model: `anthropic/claude-sonnet-4.6`).               | [OpenRouter API](https://openrouter.ai/)        |
| **API Key Cohere**            | Để reranking kết quả tìm kiếm (tăng độ chính xác).                      | [Cohere API](https://cohere.com/)               |
| **Pinecone Index**            | Để lưu trữ embeddings (cần cấu hình **1536 dimensions**).               | [Pinecone Console](https://pinecone.io/)        |
| **n8n Workflow (Self-hosted)**| Để chạy workflow 24/7 mà không bị giới hạn.                             | [TinoHost VPS](https://tino.vn/)                 |

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13964](https://n8n.io/workflows/13964).
2. **Nhấn vào "Export"** (icon ba chấm) và chọn **"Export as JSON"**.
3. **Trên n8n Editor**, nhấn **"Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo một workflow mới.
2. **Nhấn "Import"** → **"From JSON"** → **Dán JSON** từ [n8n.io/workflows/13964](https://n8n.io/workflows/13964).
3. **Chọn "Import"** để hoàn tất.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Webhook (Receive URL)**
- **Node**: `Receive URL` (Webhook)
- **Cấu hình**:
  - **HTTP Method**: `POST`
  - **Path**: `dedaa64a-3dc9-43ea-82ac-7fac034af0b2` *(không cần thay đổi)*
  - **Request Body**: `{"url": "https://example.com"}`
  - **Test**: Gửi request từ **Postman** hoặc **cURL**:
    ```bash
    curl -X POST https://[your-n8n-domain]/webhook/dedaa64a-3dc9-43ea-82ac-7fac034af0b2 \
    -H "Content-Type: application/json" \
    -d '{"url": "https://example.com"}'
    ```

#### **🔹 Cấu hình Firecrawl (Scrape Page)**
- **Node**: `Scrape page with Firecrawl`
- **Yêu cầu**:
  - **Credentials**: `firecrawlApi` *(đã thêm trong setup)*
  - **Operation**: `scrape` *(không cần thay đổi)*
  - **Lưu ý**:
    - Firecrawl sẽ **convert nội dung thành Markdown** để dễ xử lý.
    - Nếu gặp lỗi, kiểm tra **URL đã được validate** (node `Validate and normalize URL`).

#### **🔹 Cấu hình Pinecone (Lưu trữ Embeddings)**
- **Node**: `Store embeddings in Pinecone` & `Retrieve documents from Pinecone`
- **Yêu cầu**:
  - **Credentials**: `pineconeApi` *(đã thêm trong setup)*
  - **Cấu hình Pinecone**:
    - **Modality**: `Text`
    - **Vector type**: `Dense`
    - **Dimension**: `1536` *(phải khớp với model `text-embedding-3-small` của OpenAI)*
    - **Metric**: `cosine`
  - **Lưu ý**:
    - Nếu index chưa tồn tại, **tạo mới** với tên tương ứng trong workflow.
    - Kiểm tra **API Key Pinecone** có đúng không.

#### **🔹 Cấu hình OpenAI (Tạo Embeddings)**
- **Node**: `Generate OpenAI embeddings` & `Generate OpenAI embeddings1`
- **Yêu cầu**:
  - **Credentials**: `openAiApi` *(đã thêm trong setup)*
  - **Model**: `text-embedding-3-small` *(không cần thay đổi)*
  - **Lưu ý**:
    - Nếu OpenAI bị rate limit, **cài đặt API Key mới** hoặc tăng limit.

#### **🔹 Cấu hình OpenRouter (AI Chatbot)**
- **Node**: `OpenRouter LLM`
- **Yêu cầu**:
  - **Credentials**: `openRouterApi` *(đã thêm trong setup)*
  - **Model**: `anthropic/claude-sonnet-4.6` *(không cần thay đổi)*
  - **Lưu ý**:
    - Nếu muốn thay đổi model, **cập nhật trong node `chatTrigger`** (node `Receive chat message`).

#### **🔹 Cấu hình Cohere (Reranking)**
- **Node**: `Rerank results with Cohere`
- **Yêu cầu**:
  - **Credentials**: `cohereApi` *(đã thêm trong setup)*
  - **Lưu ý**:
    - Cohere sẽ **sắp xếp lại kết quả tìm kiếm** để tăng độ chính xác.

#### **🔹 Cấu hình Chat Agent (Trả lời Câu Hỏi)**
- **Node**: `Answer query from knowledge base` (Agent)
- **Yêu cầu**:
  - **Input**: Dữ liệu từ `Retrieve documents from Pinecone`.
  - **Lưu ý**:
    - Agent sẽ **tích hợp embeddings + chatbot** để trả lời câu hỏi tự nhiên.

---

### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi request POST đến webhook với `{"url": "https://example.com"}`.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy bình thường.
2. **Bật Active**:
   - Nhấn **"Active"** trên workflow để chạy liên tục.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Cập nhật dữ liệu tự động**
- **Sử dụng n8n Cron Trigger** để scrape webpage định kỳ (ví dụ: hàng ngày).
- **Ví dụ**:
  ```json
  {
    "nodeType": "n8n-nodes-base.cron",
    "name": "Daily Scrape",
    "parameters": {
      "cronExpression": "0 0 * * *"  // Lúc 00:00 hàng ngày
    }
  }
  ```

### **🔹 Gửi báo cáo kết quả qua Slack/Email**
- **Thêm node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.email` sau node `Return ingestion result`.
- **Ví dụ**:
  ```json
  {
    "nodeType": "n8n-nodes-base.slack",
    "name": "Notify Slack",
    "parameters": {
      "channel": "#automation",
      "message": "📊 Scrape thành công: {{ $json["url"] }}"
    }
  }
  ```

### **🔹 Lưu log vào Google Sheets**
- **Thêm node `n8n-nodes-base.google-sheets`** sau node `Return ingestion result`.
- **Ví dụ**:
  ```json
  {
    "nodeType": "n8n-nodes-base.google-sheets",
    "name": "Log to Google Sheets",
    "parameters": {
      "sheetName": "Scrape Logs",
      "appendRow": true,
      "rowData": [
        "{{ $json["url"] }}",
        "{{ $json["status"] }}",
        "{{ $json["timestamp"] }}"
      ]
    }
  }
  ```

### **🔹 Tăng hiệu suất với batch processing**
- **Sử dụng node `n8n-nodes-base.set`** để batch scrape nhiều URL cùng lúc.
- **Ví dụ**:
  ```json
  {
    "nodeType": "n8n-nodes-base.set",
    "name": "Batch URLs",
    "parameters": {
      "data": [
        {"url": "https://example1.com"},
        {"url": "https://example2.com"}
      ]
    }
  }
  ```

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **tìm kiếm, tổng hợp, và xử lý dữ liệu thủ công**. Bằng cách **tích hợp Firecrawl, OpenAI, Pinecone, và AI Chatbot**, nó xây dựng một **hệ thống RAG hoàn chỉnh** để trả lời câu hỏi một cách **tự động, chính xác, và nhanh chóng**.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để chạy 24/7).
2. **Import workflow** và cấu hình API keys.
3. **Test với URL đầu tiên** và bắt đầu tự động hóa!

**🚀 Cải thiện hiệu suất công việc của mình với AI mà không cần code!**