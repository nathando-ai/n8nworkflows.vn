---
title: "🚀 Đánh giá độ phù hợp tài liệu RAG trong n8n với AI Evaluation"
description: "Hướng dẫn xây dựng hệ thống tự động đo lường độ chính xác và độ phù hợp của tài liệu truy xuất (Document Relevance) trong các ứng dụng RAG sử dụng n8n."
slug: "danh-gia-do-phu-hop-tai-lieu-rag-trong-n8n"
tags: [n8n, automation, ai-evaluation, rag, openai, langchain]
keywords: [n8n workflow, rag evaluation, document relevance, ai agent, tự động hóa n8n, langchain vector store]
---

# 🚀 Đánh giá độ phù hợp tài liệu RAG trong n8n với AI Evaluation

Trong các ứng dụng RAG (Retrieval-Augmented Generation), việc đảm bảo tài liệu được truy xuất từ Vector Store thực sự liên quan đến câu hỏi của người dùng là cực kỳ quan trọng. Tuy nhiên, việc kiểm tra thủ công hàng trăm câu hỏi và tài liệu trả về lại tốn rất nhiều thời gian và công sức. 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quá trình đánh giá độ phù hợp của tài liệu (Document Relevance Metric) bằng AI, giúp tối ưu hóa hệ thống RAG một cách chuyên nghiệp mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đo lường RAG:** Tự động kiểm tra xem các tài liệu được AI truy xuất có thực sự trả lời đúng trọng tâm câu hỏi hay không.
- **Tiết kiệm chi phí API:** Chỉ kích hoạt tính năng tính toán metrics khi chạy tiến trình evaluation, tránh lãng phí token OpenAI.
- **Tích hợp Google Sheets mượt mà:** Lấy bộ dataset câu hỏi mẫu và ghi nhận kết quả đánh giá trực tiếp lên Google Sheets.
- **Sẵn sàng mở rộng:** Dễ dàng tích hợp AI Agent kết hợp Vector Store để xây dựng trợ lý thông minh chuẩn xác.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (dùng cho OpenAI Chat Model, Embeddings và tính toán metric).
- **Google Sheets Credentials** (OAuth2 API để đọc dữ liệu dataset câu hỏi).
- **Dataset mẫu**: Chuẩn bị một Google Sheet chứa các câu hỏi kiểm thử theo mẫu của n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow này, dán thẳng vào trình soạn thảo n8n (n8n Editor) hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node quan trọng sau:
- **Google Sheets Nodes (`When fetching a dataset row`, `Get dataset`):** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api` và trỏ tới file Google Sheet chứa bộ dataset câu hỏi kiểm thử RAG.
- **OpenAI Nodes (`Embeddings OpenAI`, `Calculate doc relevance metric`, `OpenAI Chat Model`):** Thêm Credentials `openAiApi` cho tất cả các node liên quan đến OpenAI. Tại node `OpenAI Chat Model`, hãy đảm bảo chọn đúng model (khuyến nghị `gpt-4o-mini` để tối ưu chi phí).
- **AI Agent Node:** Đảm bảo tùy chọn **'Return intermediate steps'** đã được bật trong cấu hình của AI Agent để hệ thống có thể lấy được danh sách các công cụ và tài liệu đã được thực thi/truy xuất.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm lần đầu bằng node `When clicking ‘Execute workflow’` hoặc `When fetching a dataset row` với dữ liệu mẫu từ Google Sheets.
- Sau khi kiểm tra mọi thứ hoạt động chính xác, bật **Active workflow** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo ngay lập tức mỗi khi hoàn tất một phiên chạy Evaluation kèm theo số liệu thống kê độ phù hợp.
- **Lưu lịch sử chi tiết:** Mở rộng workflow để ghi lại lịch sử đánh giá vào cơ sở dữ liệu (như PostgreSQL hoặc Airtable) nhằm theo dõi sự cải thiện của RAG theo thời gian.
- **Tự động hóa định kỳ:** Sử dụng `Schedule Trigger` để chạy quy trình đánh giá chất lượng RAG tự động mỗi tuần/mỗi tháng.

### 📌 Kết luận
Workflow đánh giá độ phù hợp tài liệu RAG là một công cụ cực kỳ mạnh mẽ giúp các sếp kiểm soát và nâng cao chất lượng câu trả lời của AI Agent. Hãy áp dụng ngay vào hệ thống của mình để tối ưu hóa hiệu suất RAG một cách tự động và chuyên nghiệp!