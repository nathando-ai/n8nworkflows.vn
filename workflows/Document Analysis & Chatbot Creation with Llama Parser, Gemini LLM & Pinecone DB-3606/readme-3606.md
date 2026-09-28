---
title: "🚀 Xây dựng hệ thống Phân tích Tài liệu & Chatbot AI tự động với Llama Parser, Gemini & Pinecone trên n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình phân tích tài liệu, trích xuất thông tin, lưu trữ vector Pinecone và tạo chatbot AI thông minh trả lời dựa trên tài liệu sử dụng n8n."
slug: "phan-tich-tai-lieu-chatbot-ai-llama-parser-gemini-pinecone"
tags: [n8n, automation, ai-chatbot, gemini, pinecone, liam-parser]
keywords: [n8n workflow, phân tích tài liệu ai, chatbot ai n8n, pinecone vector store, google gemini n8n]
---

# 🚀 Xây dựng hệ thống Phân tích Tài liệu & Chatbot AI tự động với Llama Parser, Gemini & Pinecone

Các sếp có bao giờ cảm thấy ngợp thở khi phải đọc hàng loạt tài liệu PDF dài dặc, trích xuất thông tin thủ công, rồi lại phải mò mẫm tạo chatbot để trả lời câu hỏi dựa trên các tài liệu đó chưa? Công việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ mạnh mẽ gồm 33 nodes, tự động hóa toàn bộ quy trình: nhận tài liệu từ form, phân tích nội dung bằng Llama Parser, trích xuất thông tin và dịch thuật bằng Google Gemini, lưu trữ vector vào Pinecone DB, đồng thời tự động gửi link chatbot qua Gmail để khách hàng/nhân sự có thể hỏi đáp trực tiếp với tài liệu!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow AI xử lý các tài liệu nặng và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ lúc người dùng upload file qua Form cho đến khi hệ thống phân tích, lưu trữ và kích hoạt Chatbot.
- **Trích xuất & Xử lý thông minh:** Sử dụng Llama Parser để bóc tách tài liệu phức tạp, kết hợp Google Gemini LLM để phân tích ngữ nghĩa sâu sắc.
- **Knowledge Base chuẩn xác:** Lưu trữ kiến thức tài liệu vào Pinecone Vector Database kết hợp Mistral Embeddings, giúp chatbot trả lời cực kỳ chính xác.
- **Trải nghiệm liền mạch:** Tự động gửi link Chatbot trực tiếp qua Gmail cho người dùng ngay khi tài liệu được xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp nhớ chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Khuyến nghị bản self-hosted mới nhất).
- **Google Gemini API Key** (cho các node Google Gemini Chat Model).
- **Llama Cloud API Key** (cho phần parsing tài liệu qua HTTP Request).
- **Pinecone Account & Index** (cho Vector Store).
- **Mistral AI API Key** (cho Embeddings).
- **Gmail Account Credentials** (để gửi email thông báo link chatbot).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ kho n8n.
- Trong giao diện n8n Editor, nhấn vào nút **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá đồ sộ với 33 nodes chia thành các cụm chức năng rõ rệt. Các sếp cần chú ý cấu hình kỹ các node sau:

- **On form submission4 (`formTrigger`):** Nơi người dùng tải tài liệu lên. Các sếp có thể tùy chỉnh lại giao diện Form theo nhu cầu thực tế của doanh nghiệp.
- **Parsing the document, Check the parsing status, Provide the markdown (`httpRequest`):** Cần điền chính xác Llama Cloud API Key và Endpoint để hệ thống tiến hành gửi và bóc tách file PDF/Document thành dạng Markdown.
- **Google Gemini Chat Model (Các node `lmChatGoogleGemini`):** Kết nối tài khoản Google AI Studio của các sếp vào đây. Đảm bảo chọn đúng model (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`) để tối ưu tốc độ và độ chính xác cho AI Agent, Information Extractor và Translator Agent.
- **Pinecone Vector Store & Embeddings Mistral Cloud:** Điền thông số Index Name, API Key của Pinecone và cấu hình Embeddings Mistral Cloud để hệ thống chuyển đổi văn bản thành vector và lưu trữ chính xác.
- **Gmail (`gmail`):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để workflow tự động gửi email chứa link chatbot khi tài liệu đã được nạp vào cơ sở dữ liệu tri thức.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một file tài liệu mẫu thông qua Form Trigger để kiểm tra từng chặng (Parsing -> Gemini Analysis -> Vector Embedding -> Gửi Email).
- Sau khi test thành công không báo lỗi, hãy bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành chính thức 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống hoàn thiện và phù hợp hơn với nhu cầu doanh nghiệp, các sếp có thể mở rộng thêm:
1. **Tích hợp Slack/Telegram:** Thêm node thông báo về kênh nội bộ mỗi khi có khách hàng hoàn tất việc upload và tạo chatbot mới.
2. **Lưu lịch sử chat:** Kết nối thêm Google Sheets hoặc Supabase để lưu lại các câu hỏi mà người dùng đã hỏi chatbot, giúp đội ngũ kinh doanh nắm bắt nhu cầu.
3. **Mở rộng định dạng file:** Tinh chỉnh các node `Code` và `Convert to File` để hỗ trợ thêm nhiều định dạng tài liệu khác như DOCX, TXT, hoặc XLSX.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa n8n, Llama Parser, Gemini LLM và Pinecone, các sếp đã sở hữu ngay một hệ thống phân tích tài liệu và trợ lý AI thông minh khép kín chỉ trong vài nốt nhạc. Bắt tay vào cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc thôi nào!