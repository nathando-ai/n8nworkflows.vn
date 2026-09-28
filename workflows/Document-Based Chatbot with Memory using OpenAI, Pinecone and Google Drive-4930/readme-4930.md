---
title: "🚀 Xây dựng Chatbot thông minh tra cứu tài liệu Google Drive với AI Agent, Pinecone và OpenAI trên n8n"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n tự động hóa việc đọc tài liệu từ Google Drive, lưu trữ vector vào Pinecone và tích hợp trí nhớ dài hạn với Airtable."
slug: "chatbot-tai-lieu-google-drive-pinecone-openai-n8n"
tags: [n8n, automation, ai, openai, pinecone, googledrive]
keywords: [n8n workflow, chatbot tài liệu, google drive ai, pinecone vector store, airtable memory, tự động hóa n8n]
---

# 🚀 Xây dựng Chatbot thông minh tra cứu tài liệu Google Drive với AI Agent, Pinecone và OpenAI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải lục tung hàng đống tài liệu, PDF hay báo cáo trên Google Drive chỉ để tìm một con số hoặc một quy trình cũ? Việc tra cứu thủ công vừa tốn thời gian, vừa dễ bỏ sót thông tin quan trọng trong doanh nghiệp.

Đừng lo, bài viết này sẽ hướng dẫn các sếp "lên đồ" một workflow n8n cực kỳ xịn sò mang tên **Document-Based Chatbot with Memory using OpenAI, Pinecone and Google Drive** do tác giả Sally chia sẻ. Giải pháp này giúp tự động hóa 100% quy trình đọc tài liệu, nhúng vector, tích hợp bộ nhớ dài hạn và trả lời câu hỏi thông minh qua AI Agent mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các file tài liệu lớn mà không bị timeout, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa xử lý tài liệu:** Tự động lấy file từ Google Drive, cắt nhỏ văn bản và lưu trữ vector vào Pinecone một cách mượt mà.
- **Chatbot thông minh có trí nhớ:** AI Agent không chỉ trả lời dựa trên tài liệu mà còn ghi nhớ ngữ cảnh trò chuyện (qua bộ nhớ ngắn hạn và dài hạn với Airtable).
- **Tiết kiệm 90% thời gian tra cứu:** Khách hàng hoặc đội ngũ nội bộ có thể đặt câu hỏi tự nhiên và nhận được câu trả lời chính xác ngay lập tức.
- **Hoạt động 24/7:** Bot sẵn sàng túc trực giải đáp thắc mắc bất cứ lúc nào qua giao diện chat trực quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI API Key** (Dành cho LLM `gpt-4o-mini` và Embeddings).
- **Tài khoản OpenRouter API Key** (Dành cho model thay thế/bổ sung).
- **Tài khoản Pinecone** (Tạo một Index để lưu trữ Vector Database).
- **Tài khoản Google Drive** (Nơi lưu trữ các tài liệu PDF, CSV,... cần AI đọc).
- **Tài khoản Airtable** (Dành cho node lưu trữ bộ nhớ dài hạn của Chatbot).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này từ nguồn gốc (hoặc tải file JSON), sau đó vào giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 phân đoạn chính: Xử lý tài liệu (Document Processing) và AI Agent Chatbot. Các sếp cần cấu hình kỹ các node sau:

- **Google Drive & Get Content:** Kết nối tài khoản Google Drive của các sếp. Chọn đúng thư mục chứa tài liệu nguồn (PDF, CSV,...) để workflow quét và tải nội dung xuống.
- **Pinecone Vector Store & Embeddings OpenAI:** Điền thông tin kết nối Pinecone API, chọn đúng Index name đã tạo sẵn trên Pinecone để lưu trữ vector. Node Embeddings sẽ dùng OpenAI API Key để chuyển văn bản thành vector.
- **Recursive Character Text Splitter & Default Data Loader:** Giữ nguyên cấu hình mặc định hoặc tinh chỉnh kích thước chunk (chunk size) nếu tài liệu của các sếp quá dài hoặc quá phức tạp.
- **OpenAI Chat Model1 / OpenRouter Chat Model:** Chọn model AI chính (khuyến nghị dùng `gpt-4o-mini` để tối ưu chi phí và tốc độ) và điền Credentials tương ứng.
- **Save Memory & Get Memories (Airtable):** Cấu hình kết nối Airtable (`airtableTokenApi`) để chatbot có thể ghi và đọc lịch sử, ngữ cảnh trò chuyện, giúp AI thông minh hơn qua từng phiên chat.
- **When chat message received:** Điểm khởi đầu giao diện trò chuyện của người dùng với AI Agent.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm phân đoạn nạp tài liệu bằng nút **When clicking 'Test Workflow' button** để đảm bảo dữ liệu từ Google Drive đã được đẩy lên Pinecone thành công.
- Test thử khung chat với node **When chat message received**.
- Khi mọi thứ mượt mà, gạt công tắc sang **Active** để đưa chatbot vào hoạt động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh Chat:** Các sếp có thể thay thế trigger chat mặc định bằng Telegram Bot, Slack hoặc Webhook tích hợp trực tiếp lên Website doanh nghiệp.
- **Tự động cập nhật tài liệu:** Thêm trigger định kỳ (Cron node) để workflow tự động quét Google Drive mỗi đêm, cập nhật các tài liệu mới vào Pinecone mà không cần thủ công.
- **Bảo mật dữ liệu:** Phân tách rõ ràng các thư mục tài liệu nội bộ và tài liệu công khai trên Google Drive để tránh rò rỉ thông tin nhạy cảm.

### 📌 Kết luận
Với workflow n8n tích hợp AI Agent, Pinecone và Google Drive này, các sếp đã sở hữu ngay một "trợ lý ảo" siêu trí tuệ, am hiểu toàn bộ tài liệu nội bộ của doanh nghiệp. Áp dụng ngay để tối ưu hóa vận hành và nâng tầm trải nghiệm khách hàng thôi nào các sếp!