---
title: "🚀 Xây dựng Chatbot Gia sư AI thông minh với RAG, Phân loại Ý định và GPT-4o-mini trong n8n"
description: "Hướng dẫn xây dựng hệ thống trợ giảng AI tương tác (Nathan) tự động phân loại ý định người dùng, tra cứu tài liệu qua Pinecone RAG và ghi log vào Google Sheets."
slug: "xay-dung-chatbot-gia-su-ai-voi-rag-va-gpt-4o-mini"
tags: [n8n, automation, no-code, AI Chatbot, RAG, OpenAI, DeepSeek, Pinecone]
keywords: [n8n workflow, chatbot gia sư ai, rag n8n, gpt-4o-mini, deepseek, pinecone vector store, google sheets automation]
---

# 🚀 Xây dựng Chatbot Gia sư AI thông minh với RAG, Phân loại Ý định và GPT-4o-mini

Các thầy cô giáo, trung tâm đào tạo hoặc người làm giáo dục thường gặp khó khăn khi phải hỗ trợ hàng trăm học viên cùng lúc 24/7. Việc trả lời lặp đi lặp lại các câu hỏi, hướng dẫn lộ trình học tập thủ công hoặc tìm kiếm tài liệu giáo trình tiêu tốn rất nhiều thời gian. 

Workflow n8n này sẽ giúp các sếp tạo ra **Nathan** – một chatbot gia sư AI thông minh hoạt động tự động 100%. Chatbot sử dụng công nghệ RAG (Retrieval-Augmented Generation) kết hợp phân loại ý định người dùng, mang lại trải nghiệm học tập cá nhân hóa cho từng học viên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các phiên chat không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn 24/7:** Phản hồi học viên tức thì qua giao diện chat công khai bất kể ngày đêm.
- **Phân loại thông minh:** Sử dụng DeepSeek LLM để phân loại chính xác ý định học viên (*chào hỏi, chọn chủ đề, trả lời, đặt câu hỏi, hoặc trò chuyện ngẫu nhiên*).
- **Học tập chuẩn xác với RAG:** Kết hợp Pinecone Vector Store để truy xuất nội dung sách/giáo trình phù hợp với ngữ cảnh.
- **Lưu trữ minh bạch:** Tự động ghi lại lịch sử câu hỏi và câu trả lời của từng phiên học vào Google Sheets để kiểm tra, đánh giá.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (cho GPT-4o-mini LLM và OpenAI Embeddings).
- **DeepSeek API Key** (cho Intent Classifier).
- **Pinecone Account & Index** (Kho lưu trữ vector cơ sở kiến thức sách/giáo trình).
- **Google Sheets** (Chứa bảng Prompt Library và bảng Log Q&A).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (Link gốc: [Guide students with an AI tutor chatbot using RAG](https://n8n.io/workflows/14291)) hoặc copy JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials sau trong các node:

- **DeepSeek LLM:** Thêm DeepSeek API Credentials để node thực hiện việc phân loại ý định học viên.
- **GPT-4o-mini LLM & OpenAI Embeddings:** Thêm OpenAI API Credentials. Đảm bảo model được chọn ở node GPT-4o-mini là `gpt-4o-mini`.
- **Book Knowledge Base (vectorStorePinecone):** Kết nối tài khoản Pinecone, trỏ tới Index chứa dữ liệu sách/tài liệu học tập của các sếp.
- **Fetch System Prompt & Log Q&A to Sheets (googleSheets):** 
  - Kết nối Google Sheets Credentials.
  - Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID Google Sheet thực tế của các sếp.
  - Đảm bảo Google Sheet có tab `pmt` (chứa thư viện system prompt với cột `Output`) và tab `Preservation` (để lưu log Q&A).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử qua giao diện **Chat Trigger** để kiểm tra phản hồi từ chatbot Nathan.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để đưa vào sử dụng thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat phổ biến:** Kết nối thêm node Telegram, Messenger hoặc Slack ở phần Trigger để học viên có thể học trực tiếp trên các ứng dụng nhắn tin quen thuộc.
- **Mở rộng kho prompt:** Thêm các ý định mới vào Google Sheets tab `pmt` để Nathan có thể xử lý thêm nhiều tình huống sư phạm khác nhau.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy theo lịch (Schedule Trigger) để tổng hợp log từ Google Sheets và gửi báo cáo tóm tắt tình hình học tập qua email cho giáo viên hàng tuần.

### 📌 Kết luận
Workflow chatbot gia sư AI Nathan là một giải pháp tuyệt vời giúp tự động hóa quá trình tương tác và hỗ trợ học viên bằng công nghệ RAG tiên tiến. Hãy áp dụng ngay vào hệ thống giáo dục hoặc dự án của các sếp để tối ưu hóa thời gian và nâng cao trải nghiệm người học!