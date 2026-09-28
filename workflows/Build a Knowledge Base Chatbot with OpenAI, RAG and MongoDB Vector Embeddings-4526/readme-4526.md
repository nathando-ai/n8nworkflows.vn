---
title: "🚀 Xây dựng Chatbot Kiến Thức với OpenAI, RAG và MongoDB Vector Embeddings"
description: "Tự động nhập tài liệu Google Docs, lưu trữ vector embeddings trong MongoDB và trả lời câu hỏi nhanh chóng bằng RAG."
slug: "xay-dung-chatbot-ki-thuc-openai-rag-mongodb"
tags: [n8n, automation, no-code, ai, mongodb, rag]
keywords: [n8n workflow, tự động hóa, chatbot, RAG, vector embeddings, MongoDB, OpenAI]
---

# 🚀 Xây dựng Chatbot Kiến Thức với OpenAI, RAG và MongoDB Vector Embeddings

Bạn đang phải trả lời hàng trăm câu hỏi từ khách hàng, đồng nghiệp hoặc người dùng cuối dựa trên tài liệu nội bộ? Việc tra cứu thủ công trong Google Docs, PDF hay wiki khiến bạn mất thời gian, dễ sai sót và không thể đáp ứng nhu cầu 24/7.  
Workflow này sẽ **tự động** lấy nội dung từ Google Docs, **tách** thành các đoạn nhỏ, **tạo embeddings** bằng OpenAI, **lưu trữ** vào MongoDB Vector Store, và khi có câu hỏi mới, **tìm kiếm** nhanh nhất và **tạo câu trả lời** bằng RAG (Retrieval‑Augmented Generation). Không cần viết code, chỉ cần cấu hình một vài credentials và chạy workflow!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 <https://tino.vn/vps-n8n?affid=388> (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 <https://my.bnix.one/aff.php?aff=172> (VPS Xeon 4GB chỉ 50k/tháng)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động nhập và lập chỉ mục tài liệu trong vài phút.  
- **Đáp ứng nhanh**: Trả lời câu hỏi trong < 1s nhờ vector search.  
- **Chính xác cao**: Dựa vào dữ liệu thực tế, tránh sai lệch thông tin.  
- **Hoạt động liên tục**: 24/7, không phụ thuộc vào con người.  
- **Dễ mở rộng**: Thêm tài liệu mới, cập nhật nhanh chóng.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ | Mô tả | Credential cần thiết |
|---------|-------|-----------------------|
| **Google Docs** | Truy cập tài liệu cần lập chỉ mục | `googleDocsOAuth2Api` |
| **OpenAI** | Tạo embeddings & trả lời chat | `openAiApi` |
| **MongoDB Atlas** | Lưu trữ vector embeddings | `mongoDb` |
| **n8n** | Chạy workflow | (Self‑hosted hoặc n8n.cloud) |

> **Lưu ý**: Đảm bảo tài khoản OpenAI có quyền truy cập mô hình `gpt-4o-mini` và API key đủ hạn mức. MongoDB Atlas cần cấu hình **Vector Index** với `knnVector` (độ dài 1536, similarity cosine).  

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON workflow từ <https://n8n.io/workflows/4526> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên Node | Cấu hình cần chỉnh | Ghi chú |
|------|----------|---------------------|---------|
| 1 | **Google Docs Importer** | `operation: get` + `documentId` (ID tài liệu Google Docs) | Chỉ lấy nội dung cần lập chỉ mục. |
| 2 | **Document Section Loader** | `source` (định dạng dữ liệu) | Tải nội dung đã lấy từ Google Docs. |
| 3 | **Document Chunker** | `chunkSize`, `chunkOverlap` | Đặt kích thước đoạn phù hợp (vd: 1000 ký tự). |
| 4 | **OpenAI Embeddings Generator** | `model: text-embedding-3-large` | Tạo embeddings cho từng đoạn. |
| 5 | **MongoDB Vector Store Inserter** | `collectionName`, `vectorField` | Đặt tên collection và trường vector. |
| 6 | **MongoDB Vector Search** | `collectionName`, `vectorField`, `k` (số kết quả) | Tìm kiếm khi chat. |
| 7 | **Knowledge Base Agent** | `retrievalMode: vector`, `vectorStore: MongoDB`, `llm: OpenAI Chat Model` | Kết nối các thành phần. |
| 8 | **OpenAI Chat Model** | `model: gpt-4o-mini` | Đặt mô hình và API key. |
| 9 | **Simple Memory** | `windowSize` | Lưu trữ ngắn hạn các câu hỏi/đáp án. |
| 10 | **When clicking "Execute Workflow"** | Không cần chỉnh | Trigger nhập dữ liệu. |
| 11 | **When chat message received** | Không cần chỉnh | Trigger trả lời. |
| 12 | **Knowledge Base Agent** | `promptTemplate` | Tùy chỉnh prompt nếu cần. |

> **Tip**: Kiểm tra **MongoDB Atlas** → **Indexes** → **Vector Index** đã được tạo đúng cấu trúc (dimensions 1536, similarity cosine).  
> **Note**: Nếu sử dụng **n8n.cloud**, hãy bật **Vector Search** trong cài đặt workflow.

### 3. Kích hoạt ⚡️

1. **Test run**: Chạy workflow thủ công (`Execute Workflow`) để nhập dữ liệu Google Docs và lưu trữ vào MongoDB. Kiểm tra bảng `collection` có dữ liệu embeddings.  
2. **Activate