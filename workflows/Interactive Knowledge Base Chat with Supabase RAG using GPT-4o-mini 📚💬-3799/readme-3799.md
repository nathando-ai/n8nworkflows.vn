---
title: "🚀 Xây dựng hệ thống Hỏi-Đáp Tri thức Tự động (RAG) với Supabase và GPT-4o-mini trên n8n"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n tự động đồng bộ tài liệu từ Google Drive, xử lý vector hóa với Supabase và tích hợp AI Agent để trả lời câu hỏi thông minh."
slug: "xay-dung-he-thong-hoi-dap-tri-thuc-rag-supbase-gpt-4o-mini-n8n"
tags: [n8n, automation, ai, rag, supabase, openai, gpt-4o-mini]
keywords: [n8n workflow, rag supabase, openai gpt-4o-mini, ai agent n8n, tu dong hoa tai lieu, google drive vector store]
---

# 🚀 Xây dựng hệ thống Hỏi-Đáp Tri thức Tự động (RAG) với Supabase và GPT-4o-mini trên n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục tìm kiếm thông tin trong hàng đống tài liệu, file PDF, Google Docs hay Excel của công ty để trả lời khách hàng hoặc nhân viên mới chưa? Việc tra cứu thủ công vừa tốn thời gian, dễ sót ý lại cực kỳ nhàm chán.

Giải pháp ở đây là gì? Hãy tự động hóa toàn bộ quy trình này với một **AI Knowledge Base Chatbot** ứng dụng công nghệ **RAG (Retrieval-Augmented Generation)**. Workflow n8n mạnh mẽ này sẽ tự động lắng nghe tài liệu mới trên Google Drive, bóc tách nội dung, lưu trữ vector vào Supabase và cung cấp một trợ lý AI thông minh (sử dụng GPT-4o-mini) sẵn sàng giải đáp mọi thắc mắc dựa trên chính tài liệu nội bộ của các sếp! 100% tự động, không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các file dữ liệu lớn và chạy AI Agent ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng bộ thời gian thực**: Tự động nhận diện file mới hoặc file được cập nhật trên Google Drive (`File Created`, `Update to File`).
- **Xử lý đa định dạng**: Hỗ trợ trích xuất văn bản từ PDF, CSV, XLSX, RTF, DOC, TXT một cách mượt mà.
- **Vector Search thông minh**: Lưu trữ và tìm kiếm ngữ nghĩa siêu tốc bằng **Supabase Vector Store** kết hợp với **OpenAI Embeddings**.
- **Trợ lý AI chuyên sâu**: AI Agent (`RAG AI Agent`) kết hợp bộ nhớ hội thoại (`Postgres Chat Memory`) và các công cụ tra cứu cơ sở dữ liệu (`PostgresTool`) giúp đưa ra câu trả lời chính xác, đúng trọng tâm tài liệu doanh nghiệp.
- **Cảnh báo lỗi tự động**: Gửi thông báo qua Gmail khi có lỗi xảy ra hoặc phát hiện file trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance** (phiên bản tích hợp sẵn các nodes LangChain/AI).
- **Tài khoản Google Drive** (để làm nguồn chứa tài liệu tri thức).
- **Tài khoản Supabase** (đã bật tiện ích mở rộng `pgvector` để lưu trữ vector embedding).
- **OpenAI API Key** (cho GPT-4o-mini và OpenAI Embeddings).
- **PostgreSQL Database** (hoặc dùng chung cơ sở dữ liệu của Supabase) để lưu metadata và chat memory.
- **Tài khoản Gmail** (để nhận thông báo lỗi/trùng lặp file nếu cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n -> chọn **Workflows** -> **Import from JSON** và dán vào là xong!

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì hệ thống này kết hợp nhiều dịch vụ ngoài, các sếp cần cấu hình kỹ các node sau:
- **Google Drive Trigger (`File Created`, `Update to File`)**: Kết nối tài khoản Google Drive của các sếp và chọn thư mục (Folder) chứa tài liệu tri thức doanh nghiệp.
- **Node Trích xuất (`Extract from File PDF`, `Extract from CSV`, `Extract from XLSX`, v.v.)**: Đảm bảo các node này nhận đúng định dạng file từ bước tải về (`Download File`).
- **Supabase Vector Store & Embeddings (`Supabase Vector Store`, `Embeddings OpenAI`)**: Điền thông tin kết nối Supabase (URL và Service Role Key), cấu hình tên bảng (table) lưu vector, và chọn model `text-embedding-3-small` hoặc tương đương cho phần Embeddings.
- **RAG AI Agent & OpenAI Chat Model**: Chọn model `gpt-4o-mini` để tối ưu chi phí và tốc độ phản hồi. Cấu hình System Prompt cho Agent hiểu rõ vai trò là trợ lý tri thức nội bộ.
- **Postgres Chat Memory**: Trỏ tới cơ sở dữ liệu PostgreSQL để lưu lịch sử chat của người dùng, giúp AI có trí nhớ ngữ cảnh trong suốt cuộc trò chuyện.
- **Node thông báo (`Slack Duplicate Notification`, `Error Notification`)**: Cấu hình email nhận thông báo khi có lỗi hệ thống hoặc file trùng lặp.

#### 3. Kích hoạt ⚡️
- Thử tải một file PDF mẫu lên thư mục Google Drive đã cấu hình và bấm **Execute Workflow** ở trigger Google Drive để test luồng chạy.
- Sau khi kiểm tra dữ liệu đã vào Supabase và chat thử nghiệm qua `When chat message received` hoạt động trơn tru, các sếp hãy bấm nút **Active** để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chat Interface**: Thay vì chỉ test trong n8n chat trigger, các sếp có thể kết nối node `When chat message received` với Webhook để nhúng khung chat AI trực tiếp vào Website nội bộ, Notion hoặc nhóm Telegram/Slack của công ty.
- **Quản lý giới hạn Token**: Sử dụng `Character Text Splitter` với kích thước chunk hợp lý (ví dụ: 500-1000 ký tự) để đảm bảo không vượt quá giới hạn ngữ cảnh của GPT-4o-mini nhưng vẫn giữ đủ ý nghĩa tài liệu.
- **Báo cáo định kỳ**: Thêm một Schedule Trigger để tổng hợp số lượng câu hỏi mà chatbot đã giải đáp trong tuần và gửi báo cáo về email quản lý.

### 📌 Kết luận
Với workflow n8n kết hợp Supabase RAG và GPT-4o-mini này, các sếp đã sở hữu ngay một "bộ não số" tự động cập nhật tài liệu và giải đáp thắc mắc cho toàn doanh nghiệp chỉ trong vài nốt nhạc. Triển khai ngay hôm nay để tối ưu hóa năng suất làm việc nào!