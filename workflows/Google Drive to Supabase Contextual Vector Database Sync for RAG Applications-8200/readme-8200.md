---
title: "🚀 Đồng bộ Google Drive với Supabase Vector Database cho ứng dụng RAG thông minh"
description: "Tự động hóa đồng bộ tài liệu từ Google Drive lên Supabase Vector Database với tính năng Hybrid Search và AI Contextualization cho ứng dụng RAG."
slug: "google-drive-supabase-rag-vector-database-sync"
tags: [n8n, automation, ai-rag, supabase, google-drive, openai]
keywords: [n8n workflow, rag automation, google drive supabase, hybrid search supabase, vector database sync]
---

# 🚀 Đồng bộ Google Drive với Supabase Vector Database cho ứng dụng RAG thông minh

Các sếp đang xây dựng các ứng dụng Trợ lý ảo AI (RAG - Retrieval-Augmented Generation) nhưng gặp khó khăn trong việc cập nhật tài liệu? Việc copy thủ công, chia nhỏ file PDF, tạo embedding và đồng bộ vào Vector Database mỗi khi tài liệu thay đổi trên Google Drive cực kỳ tốn thời gian và dễ xảy ra lỗi.

Workflow n8n chuyên nghiệp này (được thiết kế bởi chuyên gia Michael Taleb) sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động theo dõi thư mục Google Drive, trích xuất văn bản, làm giàu ngữ cảnh bằng AI, tạo vector embedding và đồng bộ thời gian thực vào Supabase (hỗ trợ Hybrid Search đỉnh cao).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** File mới thêm vào hoặc chỉnh sửa trên Google Drive sẽ tự động cập nhật vào Vector Database mà không cần đụng tay.
- **Tìm kiếm siêu chính xác (Hybrid Search):** Kết hợp tìm kiếm ngữ nghĩa (Semantic Vector Search) và tìm kiếm từ khóa (Keyword Search) trên Supabase giúp AI trả lời cực kỳ chuẩn xác.
- **Làm giàu ngữ cảnh (Contextual RAG):** Mỗi đoạn chunk tài liệu được AI tóm tắt và gắn metadata chi tiết trước khi embedding, giải quyết triệt để vấn đề mất ngữ cảnh của RAG truyền thống.
- **Quản lý thông minh:** Tự động phát hiện file bị xóa trong Thùng rác (Trash) để dọn dẹp dữ liệu tương ứng trong database.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Google Drive & OAuth2 Credentials**.
- **Tài khoản Supabase** (để lưu trữ Vector Database và Record Manager).
- **OpenAI API Key** (dùng cho LLM và Embedding model `text-embedding-3` / `gpt-4`).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 8200) và import trực tiếp vào giao diện n8n của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình các bước quan trọng sau:

1. **Cấu hình Supabase & SQL Schema:**
   - Vào Supabase Project -> SQL Editor, copy đoạn code tạo bảng `documentsHS` và `record_managerHS` (đã được đính kèm sẵn trong ghi chú của workflow) rồi chạy lệnh `Run`.
   - Tạo Edge Function trong Supabase gọi hàm `match_documentshs_hybrid` để hỗ trợ Hybrid Search qua API.
2. **Credentials cần kết nối:**
   - **Google Drive Trigger & Google Drive Nodes:** Kết nối tài khoản Google qua OAuth2 và chọn đúng thư mục (Folder ID) cần theo dõi tài liệu RAG.
   - **Supabase API:** Điền Project URL và Service Role/API Key vào các node Supabase (`Search Record Manager`, `Create Row in Record Manager`, `Supabase Vector Store1`...).
   - **OpenAI API:** Cấu hình cho các node `OpenAI Chat Model`, `OpenAI Chat Model1`, `Embeddings OpenAI1`.
   - **HTTP Header Auth (Edge Function):** Điền Bearer Token từ Edge Function của Supabase vào node `Edge Function` và `Embedding`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test Run) bằng cách tải một file PDF mẫu lên thư mục Google Drive đã cấu hình.
- Kiểm tra dữ liệu đã được chia chunk, tạo embedding và đẩy thành công lên Supabase.
- Bật công tắc **Active** để workflow chạy tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng xử lý để nhận thông báo mỗi khi có tài liệu mới được cập nhật hoặc đồng bộ thành công vào Vector DB.
- **Mở rộng định dạng file:** Mặc định workflow xử lý cực tốt file PDF (`Extract from File`), các sếp có thể mở rộng thêm để đọc Google Docs, file Word (.docx) hoặc file Markdown.
- **Tối ưu Token:** Sử dụng mô hình `gpt-4.1-nano` hoặc `gpt-4o-mini` cho các tác vụ tóm tắt phụ (như node `Add Context`) để tiết kiệm chi phí gọi API OpenAI.

---

### 📌 Kết luận
Với workflow **Google Drive to Supabase Contextual Vector Database Sync**, các sếp đã sở hữu ngay một hệ thống quản lý Knowledge Base tự động, thông minh và cực kỳ mạnh mẽ. Không còn lo lỗi thời tài liệu hay bot AI trả lời "ngớ ngẩn" do thiếu ngữ cảnh. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất cho doanh nghiệp!