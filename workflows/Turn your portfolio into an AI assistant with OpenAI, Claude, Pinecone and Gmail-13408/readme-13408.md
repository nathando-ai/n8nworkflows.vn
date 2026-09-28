---
title: "🚀 Chuyển Portfolio của bạn thành Trợ lý AI với OpenAI, Claude, Pinecone và Gmail"
description: "Tự động hóa portfolio của bạn thành trợ lý AI 24/7 với n8n. Tự động cập nhật nội dung, trả lời câu hỏi tuyển dụng và gửi CV qua email."
slug: "chuyen-portfolio-thanh-tru-ly-ai-voi-openai-claude-pinecone-gmail"
tags: [n8n, automation, no-code, AI, RAG]
keywords: [n8n workflow, tự động hóa, AI portfolio, RAG, n8n automation]
---

# 🚀 Chuyển Portfolio của bạn thành Trợ lý AI với OpenAI, Claude, Pinecone và Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý portfolio và trả lời câu hỏi tuyển dụng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động cập nhật nội dung**: Portfolio của bạn luôn được cập nhật khi có thay đổi trong Google Drive.
- **Trả lời câu hỏi tuyển dụng 24/7**: Trợ lý AI của bạn có thể trả lời các câu hỏi về portfolio của bạn bất cứ lúc nào.
- **Gửi CV tự động**: Tự động gửi CV của bạn qua email khi có yêu cầu từ nhà tuyển dụng.
- **Tích hợp AI tiên tiến**: Sử dụng các công nghệ AI tiên tiến như OpenAI, Claude, Pinecone và Cohere để cung cấp các câu trả lời chính xác và hữu ích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với các tài liệu portfolio của bạn.
- Tài khoản OpenAI với API key.
- Tài khoản Pinecone với API key và một index đã tạo.
- Tài khoản Anthropic với API key.
- Tài khoản Cohere với API key.
- Tài khoản Gmail với API key.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/13408](https://n8n.io/workflows/13408).
3. Hoặc tải file JSON về và import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **File Created Trigger** và **File Updated Trigger**: Cấu hình credentials Google Drive và chọn folder ID chứa các tài liệu portfolio của bạn.
- **Download File**: Cấu hình credentials Google Drive.
- **Enrich Metadata**: Cấu hình các trường metadata bạn muốn thêm vào tài liệu.
- **Pinecone Insert**: Cấu hình credentials Pinecone và chọn index đã tạo.
- **OpenAI Embeddings**: Cấu hình credentials OpenAI.
- **Document Loader**: Cấu hình các loại tài liệu bạn muốn tải lên.
- **Text Splitter**: Cấu hình kích thước chunk và overlap.
- **Chat Webhook**: Cấu hình path và HTTP method cho webhook.
- **Portfolio AI Agent**: Cấu hình system prompt với thông tin cá nhân của bạn.
- **Claude Sonnet 4.5**: Cấu hình credentials Anthropic.
- **Chat Memory**: Cấu hình kích thước bộ nhớ chat.
- **Structured Output Parser**: Cấu hình schema cho output parser.
- **Portfolio Vector Tool**: Cấu hình credentials Pinecone.
- **Claude Retrieval Model**: Cấu hình credentials Anthropic.
- **Pinecone Retrieval**: Cấu hình credentials Pinecone.
- **Cohere Reranker**: Cấu hình credentials Cohere.
- **OpenAI Embeddings Retrieval**: Cấu hình credentials OpenAI.
- **Check CV Request**: Cấu hình điều kiện kiểm tra yêu cầu CV.
- **Download CV PDF**: Cấu hình credentials Google Drive và file ID của CV.
- **Send CV Email**: Cấu hình credentials Gmail và địa chỉ email nhận CV.
- **Respond CV Sent**: Cấu hình thông báo khi CV được gửi.
- **Respond with Answer**: Cấu hình thông báo khi câu hỏi được trả lời.
- **Error Trigger**: Cấu hình thông báo lỗi.
- **Format Error Data**: Cấu hình định dạng thông báo lỗi.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo khi có yêu cầu CV.
- Lưu log các câu hỏi và câu trả lời để phân tích và cải thiện.
- Gửi báo cáo định kỳ về các câu hỏi thường gặp để tối ưu hóa portfolio của bạn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa portfolio của mình thành một trợ lý AI 24/7, giúp trả lời các câu hỏi tuyển dụng một cách chính xác và hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất tuyển dụng của bạn!