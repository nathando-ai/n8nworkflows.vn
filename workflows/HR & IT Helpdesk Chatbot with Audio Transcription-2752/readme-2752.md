---
title: "🚀 Xây dựng HR & IT Helpdesk Chatbot thông minh với tính năng chuyển đổi giọng nói trên Telegram"
description: "Hướng dẫn xây dựng trợ lý ảo AI hỗ trợ nhân sự và IT tự động trên Telegram bằng n8n, hỗ trợ đọc file chính sách công ty và xử lý cả tin nhắn thoại."
slug: "hr-it-helpdesk-chatbot-telegram-audio-transcription"
tags: [n8n, ai-agent, telegram, openai, postgres, chatbot, hr-automation]
keywords: [n8n workflow, chatbot nhân sự, telegram bot ai, openai whisper n8n, rag vector store postgres]
---

# 🚀 Xây dựng HR & IT Helpdesk Chatbot thông minh với tính năng chuyển đổi giọng nói trên Telegram

Các sếp có bao giờ cảm thấy quá tải khi nhân viên liên tục hỏi đi hỏi lại những câu hỏi muôn thuở về quy chế công ty, ngày phép, hay các sự cố IT cơ bản? Việc phải trả lời thủ công những nội dung này ngốn rất nhiều thời gian quý báu của bộ phận HR và IT.

Giải pháp đây rồi! Workflow n8n này sẽ giúp các sếp dựng lên một **Trợ lý ảo AI Helpdesk** hoạt động trực tiếp trên **Telegram**. Điểm "ăn tiền" của bot này là không chỉ đọc hiểu tin nhắn văn bản, mà còn **tự động nghe và chuyển đổi tin nhắn thoại (voice message) thành văn bản** nhờ AI, sau đó tra cứu thông tin từ tài liệu nội bộ (RAG) để trả lời chính xác 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7**: Giải đáp mọi thắc mắc về HR và IT cho nhân viên ngay lập tức bất kể ngày đêm.
- **Hỗ trợ tin nhắn thoại thông minh**: Nhân viên chỉ cần gửi voice chat, bot tự nghe, hiểu và trả lời như người thật.
- **Độ chính xác cao nhờ RAG**: Bot chỉ trả lời dựa trên tài liệu chính thống của công ty (Sổ tay nhân viên, chính sách IT), tránh tình trạng AI "tự chế" câu trả lời (hallucination).
- **Ghi nhớ ngữ cảnh**: Tích hợp bộ nhớ hội thoại giúp bot hiểu được các câu hỏi tiếp nối trong cùng một cuộc trò chuyện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Bản self-hosted hoặc n8n Cloud.
- **Telegram Bot Token**: Tạo qua BotFather trên Telegram.
- **OpenAI API Key**: Dùng cho tính năng Embeddings, Transcription (Whisper) và Chat Model (GPT).
- **PostgreSQL Database**: Hỗ trợ extension `pgvector` để lưu trữ và truy vấn vector kho tri thức nội bộ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Node "HTTP Request" & "Extract from File"**: Trỏ đường dẫn URL đến file tài liệu nội bộ (ví dụ: file PDF Sổ tay nhân viên lưu trên Cloud/S3). Node này sẽ tải file về và bóc tách nội dung văn bản.
- **Node "Create HR Policies" & "Postgres PGVector Store"**: Kết nối vào cơ sở dữ liệu PostgreSQL của các sếp (đã bật `pgvector`) để lưu trữ các đoạn văn bản (chunks) đã được số hóa dạng vector.
- **Node "Telegram Trigger" & Các node Telegram khác**: Điền `Credential` của Telegram Bot Token để bot có thể lắng nghe tin nhắn và gửi phản hồi.
- **Node "OpenAI" (Operation: Transcribe)**: Chọn credential OpenAI, node này sẽ chịu trách nhiệm chuyển đổi file audio từ Telegram thành text.
- **Node "AI Agent" & "OpenAI Chat Model"**: Cấu hình mô hình ngôn ngữ lớn (ví dụ: `gpt-4o` hoặc `gpt-4o-mini`) để làm "bộ não" tổng hợp câu trả lời dựa trên tool tra cứu vector store (`Answer questions with a vector store`) và bộ nhớ (`Postgres Chat Memory`).

#### 3. Kích hoạt ⚡️
- Chạy thử một vài dữ liệu mẫu bằng cách nhấn nút **Test workflow** ở các node nạp tài liệu (khởi tạo vector store ban đầu).
- Gửi tin nhắn text hoặc voice trực tiếp tới Telegram Bot của các sếp để kiểm tra.
- Bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thêm thông báo**: Thêm node Slack hoặc Google Chat để chuyển tiếp những câu hỏi khó mà bot không trả lời được cho đội ngũ HR/IT xử lý.
- **Ghi log câu hỏi**: Lưu trữ lịch sử câu hỏi của nhân viên vào Google Sheets hoặc Airtable để phân tích những vấn đề nhân viên quan tâm nhiều nhất.
- **Đa ngôn ngữ**: Tinh chỉnh system prompt trong AI Agent để bot có thể giao tiếp mượt mà bằng cả tiếng Việt, tiếng Anh hoặc ngôn ngữ khác tùy theo nhân sự công ty.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp tối ưu hóa vận hành nội bộ, tiết kiệm hàng chục giờ đồng hồ giải đáp thắc mắc thủ công cho đội ngũ HR và IT mỗi tuần. Hãy triển khai ngay cho doanh nghiệp của các sếp nhé!