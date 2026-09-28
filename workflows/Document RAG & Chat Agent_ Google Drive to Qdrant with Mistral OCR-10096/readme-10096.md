---
title: "🚀 Xây dựng hệ thống RAG & Chat AI tự động đọc tài liệu Google Drive với Mistral OCR và Qdrant trong n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình đồng bộ tài liệu từ Google Drive, trích xuất OCR bằng Mistral, phân loại metadata bằng AI và lưu trữ vào Qdrant Vector Store để chatbot nội bộ tra cứu."
slug: "rag-chat-ai-google-drive-mistral-ocr-qdrant"
tags: [n8n, automation, ai-rag, qdrant, mistral-ocr, openai, google-drive]
keywords: [n8n workflow, RAG, chatbot nội bộ, Mistral OCR, Qdrant vector database, Google Drive automation, AI chat agent]
---

# 🚀 Xây dựng hệ thống RAG & Chat AI tự động hóa tài liệu với Google Drive, Mistral OCR & Qdrant

Các sếp có bao giờ cảm thấy đau đầu khi nhân sự mới (hoặc chính mình) mất hàng giờ để lục lọi tài liệu, hợp đồng, báo cáo rải rác trên Google Drive? Việc tìm kiếm thông tin thủ công vừa tốn thời gian, vừa dễ bỏ sót các dữ liệu quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống **Retrieval-Augmented Generation (RAG) & Chat AI thông minh 100% tự động**. Hệ thống sẽ tự động quét thư mục Google Drive, trích xuất văn bản từ mọi định dạng (PDF, ảnh, docx...) bằng công nghệ **Mistral OCR**, tự động gắn nhãn metadata thông minh, chuyển đổi thành vector và lưu trữ vào **Qdrant Vector Database**. Cuối cùng, nhân sự chỉ cần chat trực tiếp với trợ lý AI để tra cứu mọi thông tin nội bộ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các file nặng qua OCR mà không lo treo máy, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ việc đọc file trên Google Drive, OCR, gắn metadata đến lưu trữ Vector Database mà không cần đụng tay.
- **Trợ lý AI thông minh:** Chatbot nội bộ hiểu sâu về tài liệu của công ty, trả lời chính xác trích dẫn từ nguồn gốc.
- **Metadata phong phú:** Tự động phân loại tài liệu theo loại (`document_type`), dự án (`project`) và nhân sự phụ trách (`assigned_to`).
- **Kết hợp linh hoạt:** Vừa tra cứu tài liệu nội bộ (Qdrant), vừa có thể tìm kiếm dữ liệu ngoài Internet (Tavily Web Search) khi cần mở rộng thông tin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản hỗ trợ LangChain/AI nodes).
- **Google Drive Account & Credentials** (OAuth2 API để đọc file).
- **Mistral Cloud API Key** (Dùng cho Mistral OCR và Chat Model).
- **OpenAI API Key** (Dùng cho Embeddings và Chat Model `gpt-4.1-mini`).
- **Qdrant Cloud/Local API** (Vector Database để lưu trữ knowledge base).
- **Tavily API Key** (Tùy chọn: Dùng cho tính năng Web Search mở rộng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 luồng chính: **Data Ingestion Pipeline** (nạp và xử lý tài liệu) và **Chat Agent Pipeline** (tương tác với người dùng). Các sếp cần cấu hình kỹ các node sau:

- **Google Drive (List Files & Download File):** Kết nối tài khoản Google Drive của sếp và cấu hình đúng ID thư mục chứa tài liệu nguồn (ví dụ: thư mục `knowledgebaseforaibot`).
- **Mistral OCR (HTTP Request Nodes - Upload, Signed URL, OCR):** Điền `Mistral Cloud API Key` để hệ thống thực hiện gọi API trích xuất chữ từ file PDF/ảnh.
- **Information Extractor & Metadata Nodes:** Cấu hình mô hình AI để tự động trích xuất các trường metadata (`document_type`, `project`, `assigned_to`).
- **OpenAI Embeddings & Qdrant Vector Store:** 
  - Kết nối `OpenAI API` cho các node Embeddings (`text-embedding-3-small`).
  - Kết nối `Qdrant API` và trỏ tới collection chuẩn bị sẵn (ví dụ: `docaiauto`).
- **AI Chat Agent & OpenAI Chat Model:** Chọn model `gpt-4.1-mini` để đảm bảo tốc độ phản hồi nhanh và chi phí tối ưu.

#### 3. Kích hoạt ⚡️
- Chạy thử luồng nạp dữ liệu bằng cách nhấn nút **Test workflow** trên Manual Trigger để kiểm tra quá trình đọc file từ Google Drive sang Qdrant.
- Mở giao diện chat tích hợp sẵn (Chat Trigger) để test câu hỏi với trợ lý AI.
- Sau khi mọi thứ mượt mà, gạt công tắc **Active** để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch (Cron):** Thay thế Manual Trigger bằng một **Schedule Trigger** để hệ thống tự động quét Google Drive mỗi đêm lúc 2:00 sáng.
- **Gửi thông báo qua Slack/Telegram:** Thêm node thông báo vào cuối luồng xử lý tài liệu để đội ngũ biết khi nào một tài liệu mới được đưa vào hệ thống RAG thành công.
- **Tối ưu Chunking:** Tùy chỉnh kích thước đoạn văn bản (chunk size) trong Code Node để phù hợp với độ dài tài liệu đặc thù của doanh nghiệp (ví dụ: hợp đồng dài cần chunk lớn hơn, FAQ cần chunk nhỏ gọn).

### 📌 Kết luận
Hệ thống **Document RAG & Chat Agent** này là mảnh ghép hoàn hảo giúp doanh nghiệp số hóa tri thức, biến kho tài liệu rời rạc trên Google Drive thành một bộ não AI thông minh, sẵn sàng phục vụ đội ngũ bất cứ lúc nào. Chúc các sếp cài đặt thành công và nâng tầm tự động hóa doanh nghiệp!