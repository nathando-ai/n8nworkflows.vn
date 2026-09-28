---
title: "🚀 Bitrix24 AI-Powered RAG Chatbot cho kênh Open Line – Tự động trả lời thông minh 100% không code"
description: "Giải pháp tự động hóa chatbot AI tích hợp Bitrix24 Open Line, sử dụng Retrieval-Augmented Generation (RAG) với LangChain, Qdrant, Ollama và Google Gemini để trả lời nhanh, chính xác và liên tục."
slug: "bitrix24-ai-powered-rag-chatbot-open-line-channels"
tags: [n8n, automation, no-code, bitrix24, ai, chatbot, rag, langchain, google-gemini, qdrant]
keywords: [n8n workflow, tự động hóa, chatbot AI, RAG, Bitrix24, LangChain, Google Gemini, Qdrant, Ollama, open line channel]
---

# 🚀 Bitrix24 AI-Powered RAG Chatbot cho kênh Open Line – Tự động trả lời thông minh 100% không code

Bạn đang phải trả lời hàng trăm tin nhắn khách hàng trên Bitrix24 Open Line mỗi ngày?  
Mỗi tin nhắn cần được xử lý nhanh, chính xác và liên tục – nhưng việc viết code, quản lý dữ liệu, tích hợp LLM và lưu trữ vector có thể tốn kém thời gian và nguồn lực.  

Workflow này sẽ **đưa AI vào cuộc trò chuyện** mà không cần viết dòng code.  
- **RAG** (Retrieval‑Augmented Generation) giúp chatbot truy xuất dữ liệu từ kho lưu trữ nội bộ (Qdrant) và kết hợp với mô hình Gemini để trả lời chính xác.  
- **LangChain** giúp bạn dễ dàng cấu hình embeddings, vector store, retriever và chain QA.  
- **Bitrix24 Webhook** nhận sự kiện (tin nhắn, join, install, delete) và trả về phản hồi ngay lập tức.  
- **Subworkflow** tự động đăng ký bot, tải và lưu trữ tài liệu vào vector store.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết code, chỉ cấu hình một vài credential.  
- **Chính xác cao**: RAG kết hợp dữ liệu nội bộ + LLM giúp trả lời đúng ngữ cảnh.  
- **Cá nhân hóa**: Mỗi khách hàng nhận được câu trả lời phù hợp với lịch sử trò chuyện.  
- **Hoạt động liên tục**: Webhook 24/7, không bị gián đoạn.  
- **Dễ mở rộng**: Thêm Slack, Telegram, báo cáo định kỳ chỉ vài dòng cấu hình.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ / Credential | Mô tả | Cách lấy |
|-----------------------|-------|----------|
| **Bitrix24** | API token, Webhook URL | Tạo webhook trong Bitrix24 → Settings → Webhooks |
| **Google Gemini** | API key | Đăng ký tại Google Cloud → API & Services → Credentials |
| **Ollama** | Endpoint (địa chỉ IP:port) | Cài đặt Ollama (Docker hoặc local) |
| **Qdrant** | Host, Port, API key | Cài Qdrant (Docker) hoặc dùng Qdrant Cloud |
| **n8n** | Self‑hosted instance | VPS hoặc Docker |
| **Subworkflow “Register Bot”** | Tệp JSON | Import riêng (đường dẫn dưới “Subworkflow for Register Bot”) |
| **Folder “vector stored”** | Đường dẫn lưu trữ file | Định nghĩa trong node “Move files to Vector stored folder” |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/3094).  
2. Mở n8n → **Workflows** → **Import** → **Upload JSON**.  
3. Hoặc copy toàn bộ JSON vào **n8n Editor** → **File** → **New** → **Import from clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Thông tin cần cấu hình | Ghi chú |
|------|------------------------|---------|
| **Bitrix24 Handler** | `path`: `bitrix24/openchannel-rag-bothandler.php` | Đảm bảo URL trùng với Webhook trong Bitrix24 |
| **Credentials** | `Bitrix24 API Token`,