---
title: "🚀 Đánh Giá Độ Chính Xác RAG với OpenAI: Đo Lường Tính Groundedness Tài Liệu"
description: "Hướng dẫn chi tiết sử dụng n8n AI Evaluation để kiểm tra xem câu trả lời của AI Agent có dựa trên tài liệu thực tế hay không, tránh hiện tượng ảo giác (hallucination)."
slug: "danh-gia-do-chinh-xac-rag-openai-document-groundedness"
tags: [n8n, automation, no-code, ai-agents, openai, rag]
keywords: [n8n workflow, đánh giá rag, document groundedness, openai chat model, vector store, tự động hóa ai]
---

# 🚀 Đánh Giá Độ Chính Xác RAG với OpenAI: Đo Lường Tính Groundedness Tài Liệu

Các sếp xây dựng hệ thống RAG (Retrieval-Augmented Generation) cho chatbot hoặc trợ lý ảo nhưng luôn đau đầu vì không biết liệu AI có đang tự "bịa" ra câu trả lời (ảo giác - hallucination) hay thực sự dựa vào tài liệu được cung cấp? Việc kiểm thử thủ công từng câu hỏi là bất khả thi và tốn kém thời gian.

Workflow n8n chuyên nghiệp này (được thiết kế bởi chuyên gia Jimleuk) sẽ giúp các sếp tự động hóa quá trình đánh giá độ chính xác của RAG dựa trên chỉ số **Document Groundedness** sử dụng OpenAI và tính năng Evaluation mạnh mẽ của n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát ảo giác AI:** Tự động đo lường xem câu trả lời của AI Agent có bám sát tài liệu gốc trong Vector Store hay không.
- **Tự động hóa toàn diện:** Sử dụng bộ công cụ Evaluation của n8n kết hợp Google Sheets để chạy tập dữ liệu kiểm thử (test dataset) hàng loạt.
- **Chấm điểm chuẩn xác:** Áp dụng phương pháp đánh giá đạt chuẩn (Pointwise Groundedness) mô phỏng theo tiêu chuẩn của Google Cloud Vertex AI.
- **Cải thiện prompt hiệu quả:** Dựa vào điểm số chi tiết để biết khi nào cần tối ưu lại prompt hoặc thay đổi mô hình LLM.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Version:** Từ phiên bản `1.94+` trở lên (hỗ trợ đầy đủ Evaluation nodes).
- **OpenAI API Key:** Cần thiết cho các node Chat Model và Embeddings.
- **Google Sheets Credentials:** Để kết nối và đọc/ghi dữ liệu đánh giá từ Google Sheets mẫu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang template chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu của các sếp, hãy lưu ý cấu hình kỹ các node sau:
- **OpenAI Chat Model / Embeddings OpenAI:** Thiết lập credentials `openAiApi` chứa API Key của các sếp. Đảm bảo chọn đúng model (ví dụ: `gpt-4o-mini` hoặc `gpt-4.1-mini`).
- **Get Datasheet / When fetching a dataset row:** Kết nối tài khoản Google Sheets của các sếp và trỏ tới file Google Sheet mẫu chứa dữ liệu test (hoặc tự tạo file Sheet theo cấu trúc tương tự).
- **Simple Vector Store & Default Data Loader:** Trong ví dụ này, workflow sử dụng tài liệu mẫu *Bitcoin Whitepaper*. Các sếp có thể thay thế bằng bộ tài liệu tri thức (knowledge base) riêng của doanh nghiệp mình.
- **Set Outputs & Set Metrics:** Đảm bảo cấu hình đúng Evaluation node để ghi kết quả chấm điểm trả về Google Sheets.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công bằng nút `When clicking ‘Execute workflow’` hoặc sử dụng giao diện chat (`When chat message received`) để test nhanh.
- Sau khi kiểm tra dữ liệu trả về chính xác, các sếp có thể chạy chuỗi Evaluation tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Slack/Telegram:** Thiết lập thêm node gửi tin nhắn cảnh báo mỗi khi điểm số Groundedness của một câu trả lời rơi xuống dưới mức cho phép (< 70%).
- **Lưu log chi tiết vào Database:** Thay vì chỉ ghi ra Google Sheets, các sếp có thể lưu trữ lịch sử đánh giá vào PostgreSQL hoặc Supabase để theo dõi sự cải thiện chất lượng RAG theo thời gian.
- **A/B Testing Model:** Thử nghiệm thay thế OpenAI bằng các mô hình mã nguồn mở như Claude 3.5 Sonnet hoặc Llama 3 qua Ollama để so sánh độ trung thực của tài liệu.

### 📌 Kết luận
Việc đánh giá chất lượng RAG không còn là bài toán khó khi đã có automation hỗ trợ. Hãy áp dụng ngay workflow này để đảm bảo trợ lý AI của doanh nghiệp luôn đưa ra thông tin chính xác, trung thực dựa trên tài liệu nội bộ!