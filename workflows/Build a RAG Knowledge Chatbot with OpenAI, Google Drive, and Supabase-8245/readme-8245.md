---
title: "🚀 Xây dựng Chatbot RAG Knowledge với OpenAI, Google Drive & Supabase"
description: "Tự động hoá quy trình nhập tài liệu, tạo vector store và triển khai chatbot trả lời dựa trên nội dung tài liệu, không cần viết code."
slug: "xay-dung-chatbot-rag-openai-google-drive-supabase"
tags: [n8n, automation, no-code, AI, RAG, chatbot]
keywords: [n8n workflow, tự động hóa, RAG, chatbot AI, OpenAI, Supabase, Google Drive]
---

# 🚀 Xây dựng Chatbot RAG Knowledge với OpenAI, Google Drive & Supabase

Bạn có bao nhiêu giờ mỗi tuần phải **đọc lại các tài liệu, tìm kiếm thông tin trong PDF, rồi sao chép‑dán vào email hoặc chat**?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến kiến thức quan trọng bị mất mát.  

**Workflow này** sẽ biến mọi tài liệu trong Google Drive thành một **cơ sở tri thức vector** lưu trên Supabase, sau đó kết hợp với **OpenAI Chat** để tạo một **chatbot RAG (Retrieval‑Augmented Generation)**. Kết quả: người dùng chỉ cần hỏi “Chatbot ơi, nội dung chương 3 nói gì?” và nhận được câu trả lời chính xác, ngay lập tức – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hoá việc trích xuất, chia nhỏ và tạo embeddings cho mọi tài liệu mới.  
- **Độ chính xác cao**: Vector store cho phép truy vấn ngữ nghĩa, trả lời dựa trên nội dung thực tế.  
- **Hoạt động liên tục**: Khi tài liệu được cập nhật, workflow tự động cập nhật vector store mà không cần can thiệp.  
- **Dễ mở rộng**: Có thể thêm Slack/Telegram, báo cáo định kỳ, hoặc tích hợp CRM chỉ bằng vài node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive** (đã bật Drive API, tạo OAuth2 credentials).  
- **API Key OpenAI** (có quyền sử dụng `text-embedding-ada-002` và `gpt‑4o` hoặc `gpt‑3.5‑turbo`).  
- **Tài khoản Supabase** (URL dự án + Service Role Key).  
- **PostgreSQL** (có thể dùng DB của Supabase để lưu chat memory).  
- **n8n** (cài đặt trên VPS hoặc Docker, phiên bản >= 1.0).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow từ trang gốc: <https://n8n.io/workflows/8245>.  
2. Mở n8n → **Workflows** → **Import** → **Upload JSON** hoặc **Copy/Paste** nội dung JSON vào ô.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần thay đổi |
|------|---------|-----------------------|
| **File Updated** (googleDriveTrigger) | Lắng nghe thay đổi file trong thư mục Google Drive | Điền **Folder ID** của thư mục chứa PDF cần index. |
| **File Created** (googleDriveTrigger) | Lắng nghe file mới được tạo (để hỗ trợ upload đồng thời) | Cũng cần **Folder ID** (có thể dùng cùng thư mục). |
| **Set File ID** (set) | Lưu `fileId` từ trigger để dùng cho các node tiếp theo | Không cần thay đổi, chỉ đảm bảo trường `fileId` đúng. |
| **Download the file** (googleDrive) | Tải file PDF về để xử lý | Chọn **Credentials** Google Drive đã tạo. |
| **Extract from File** (extractFromFile) | Trích xuất nội dung văn bản từ PDF | Đặt `Operation` = **text**; nếu PDF có hình ảnh, bật OCR (nếu cần). |
| **Recursive Character Text Splitter** (textSplitterRecursiveCharacterTextSplitter) | Chia văn bản thành các chunk nhỏ (khoảng 1000 ký tự) | Tham số `Chunk Size` và `Chunk Overlap` tùy ý (mặc định OK). |
| **Embeddings OpenAI** (embeddingsOpenAi) | Tạo embeddings cho mỗi chunk | Chọn **OpenAI API Key**; model `text-embedding-ada-002`. |
| **Supabase Vector Store** (vectorStoreSupabase) | Lưu embeddings vào Supabase vector table | Điền **Supabase URL**, **Service Role Key**, và **Table name** (`documents`). |
| **Delete a row** (supabase) | Xóa vector cũ khi file được cập nhật | Đảm bảo `operation = delete` và truyền `file_id` để xóa đúng bản ghi. |
| **Postgres Chat Memory** (memoryPostgresChat) | Lưu lịch sử chat cho mỗi người dùng | Kết nối tới PostgreSQL (có thể dùng DB Supabase). |
| **When chat message received** (chatTrigger) | Nhận tin nhắn từ giao diện chat (WebSocket/Telegram…) | Chọn **Credential** phù hợp (ví dụ: WebSocket hoặc Telegram Bot). |
| **OpenAI Chat Model** (lmChatOpenAi) | Tạo câu trả lời dựa trên prompt RAG | Chọn **OpenAI API Key**, model `gpt‑4o` (hoặc `gpt‑3.5‑turbo`). |
| **RAG Vector store** (vectorStoreSupabase) | Tìm kiếm chunk phù hợp trong Supabase | Cùng cấu hình như node Vector Store ở trên, nhưng `operation = query`. |
| **RAG AI Agent** (agent) | Kết hợp retrieval + LLM để trả lời | Đặt **Prompt**: “Trả lời câu hỏi dựa trên các đoạn tài liệu được cung cấp, nếu không biết trả lời, hãy nói không có thông tin.” |
| **Embeddings OpenAI1** (embeddingsOpenAi) | (Optional) Tạo embeddings cho câu hỏi người dùng nếu muốn** | Thông thường không cần thay đổi, chỉ dùng để tính similarity. |
| **Default Data Loader** (documentDefaultDataLoader) | Định dạng dữ liệu đầu vào cho LangChain | Không cần thay đổi, giữ mặc định. |
| **Loop Over Items** (splitInBatches) | Xử lý batch embeddings để tránh limit API | Đặt `Batch Size` = 100 (hoặc tùy tài nguyên). |

> **Lưu ý:** Mọi node **Credentials** phải được tạo trước trong n8n → **Credentials** → **New Credential** → chọn loại (Google Drive, OpenAI, Supabase, PostgreSQL). Sau khi tạo, quay lại node và chọn credential tương ứng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Upload một file PDF mẫu vào thư mục Google Drive đã cấu hình.  
2. Kiểm tra **Supabase → Table `documents`** để chắc chắn các chunk và embeddings đã được tạo.  
3. Mở giao diện chat (có thể là WebSocket UI hoặc Telegram Bot) → gửi câu hỏi “Tóm tắt nội dung file X”.  
4. Nếu trả lời đúng, **bật** nút **Active** trên workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `When chat message received` để nhận và trả lời tin nhắn trực tiếp trên kênh làm việc.  
- **Lưu log chi tiết**: Dùng node `Function` hoặc `Write Binary File` để ghi lại request/response vào một bucket S3 hoặc Google Cloud Storage, hỗ trợ debug.  
- **Báo cáo định kỳ**: Thêm node `Cron` → `Supabase → Select` → `Send Email` để gửi danh sách tài liệu mới được index mỗi tuần.  
- **Tối ưu chi phí**: Chỉ bật `Embeddings OpenAI` khi file mới hoặc đã thay đổi; sử dụng `splitInBatches` để giảm số lần gọi API.  

### 📌 Kết luận
Với **n8n**, bạn có thể xây dựng một chatbot RAG mạnh mẽ chỉ trong vài phút, biến mọi tài liệu Google Drive thành nguồn tri thức có thể truy vấn ngay lập tức. Hãy **import workflow**, **cấu hình credentials**, **kiểm tra** một file mẫu và **bật** ngay – các sếp sẽ thấy lợi ích rõ rệt: giảm thời gian tìm kiếm, tăng độ chính xác và nâng cao năng suất làm việc.  

**Áp dụng ngay hôm nay, để AI làm việc thay bạn!**