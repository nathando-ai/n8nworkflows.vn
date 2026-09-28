---
title: "🤖 Tạo Bot Hướng Dẫn Tài Liệu AI RAG với Gemini & Supabase trên n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc xây dựng một chatbot chuyên gia về tài liệu n8n bằng RAG, Gemini 2.5 Flash và Supabase Vector Store – không cần viết code."
slug: "tao-bot-huong-dan-tai-lieu-ai-rag-gemini-supabase-n8n"
tags: [n8n, automation, no-code, AI, RAG, Gemini, Supabase, chatbot]
keywords: [n8n workflow, tự động hóa tài liệu, RAG chatbot, Gemini embedding, Supabase vector store, n8n documentation expert]
---

# 🤖 Tạo Bot Hướng Dẫn Tài Liệu AI RAG với Gemini & Supabase trên n8n

Bạn từng cảm thấy mệt mỏi khi phải tìm kiếm thủ công trong hàng trăm trang tài liệu n8n để trả lời câu hỏi của đồng nghiệp hoặc khách hàng? Workflow này giúp bạn xây dựng một **AI Expert Bot** hoàn toàn tự động: bot đọc toàn bộ tài liệu n8n, chia thành các đoạn nhỏ, lưu trữ dưới dạng vector trong Supabase và trả lời câu hỏi chỉ dựa trên tài liệu thực tế – không “láo” câu trả lời.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ làm việc:** Bot trả lời ngay lập tức, không cần tra tài liệu thủ công.
- **Độ chính xác cao:** Câu trả lời chỉ được sinh ra từ tài liệu n8n đã được lưu trữ, giảm nguy cơ hallucination.
- **Cá nhân hóa & mở rộng:** Dễ dàng thay đổi nguồn dữ liệu (tài liệu sản phẩm, SOP nội bộ…) và tích hợp với Slack, Telegram, email…
- **Hoạt động liên tục:** Sau một lần lập chỉ mục (indexing), bot sẵn sàng trả lời 24/7; có thể lên lịch cập nhật kiến thức tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Supabase** (miễn phí đủ để bắt đầu) – cần bật extension `pgvector` và tạo bảng `documents` theo script SQL được cung cấp.
- **API Key Gemini** (Google AI) – dùng cho model `Gemini 2.5 Flash` và embeddings.
- **n8n phiên bản ≥ 1.0** (có thể chạy trên Docker, VPS hoặc n8n.cloud).
- **Kết nối internet** để workflow có thể truy cập trang documentation của n8n (https://docs.n8n.io/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang n8n.io/workflows/5993 (nút **Download**).
2. Trong n8n Editor, nhấn **Import** → **Upload file** hoặc dán JSON vào ô **Paste JSON** → **Import**.
3. Workflow sẽ xuất hiện với tên **🤖 Create a Documentation Expert Bot with RAG, Gemini, and Supabase**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, cần cấu hình các node sau để workflow hoạt động:

| Node (tên trên canvas) | Loại node | Cấu hình bắt buộc |
|------------------------|-----------|-------------------|
| **Your Supabase Vector Store** | `vectorStoreSupabase` | Chọn credential **Supabase** (tạo mới nếu chưa có). Đảm bảo node đang ở mode **Insert** (mặc định). |
| **Official n8n Documentation** | `vectorStoreSupabase` | Chọn cùng credential Supabase. Node này dùng để lưu trữ bản sao của tài liệu n8n gốc (tùy chọn, có thể bỏ nếu không cần). |
| **Keep Supabase Instance Alive** | `supabase` | Chọn credential Supabase. Thiết lập **Operation** = `Get All` trên một bảng bất kỳ (ví dụ: `documents`) chỉ để chạy một query nhẹ mỗi 6 ngày. |
| **Gemini 2.5 Flash** | `lmChatGoogleGemini` | Chọn credential **Google AI** (Gemini API key). Model mặc định là `gemini-2.5-flash`. |
| **Gemini Chunk Embedding** | `embeddingsGoogleGemini` | Chọn credential Google AI. Đảm bảo dimension = `768` (phù hợp với script Supabase). |
| **Gemini Query Embedding** | `embeddingsGoogleGemini` | Chọn credential Google AI (cùng node type). |
| **Add Documentation Page to Vector Store** (sub‑workflow) | `executeWorkflow` | Không cần cấu hình thêm; node này gọi workflow con để xử lý từng trang documentation. |
| **Start Indexing** | `manualTrigger` | Node này dùng để chạy một lần quy trình lập chỉ mục (indexing). Không cần credential. |
| **RAG Chatbot** | `chatTrigger` | Sau khi kích hoạt workflow, mở node này để lấy **Public URL** hoặc nhấn **Open Chat** để thử trực tiếp. |

**Tạo Credential:**
- **Supabase:** Vào *Credentials* → *New Credential* → *Supabase API*. Điền **Host** (URL dự án, ví dụ: `https://xxx.supabase.co`) và **API Key** (service_role key). Lưu tên là `supabaseApi`.
- **Google AI:** Vào *Credentials* → *New Credential* → *Google Palm API* (node dùng gemini). Dán **Gemini API key** và lưu tên là `googlePalmApi`.

Sau khi tạo, quay lại từng node ở trên và chọn credential tương ứng trong dropdown **Credential**.

#### 3. Kích hoạt ⚡️
1. **Chạy một lần lập chỉ mục (Indexing):**  
   - Mở node **Start Indexing** (góc trên‑trái).  
   - Nhấn **Execute workflow**. Quy trình sẽ tải tất cả trang docs.n8n.io, chia thành chunks, tạo embedding bằng Gemini và lưu vào Supabase. Thời gian ước tính **15‑20 phút** (tùy thuộc vào mạng và tài nguyên).  
   - Lưu ý: nhờ sử dụng sub‑workflow, n8n sẽ giải phóng RAM sau mỗi trang, tránh crash dù có hơn 1.000 trang.
2. **Kích hoạt workflow chính:**  
   - Bật toggle **Active** ở góc trên‑phải của editor.  
   - Mở node **RAG Chatbot** → sao chép **Public URL** hoặc nhấn **Open Chat** để bắt đầu trò chuyện.
3. (Tùy chọn) **Lưu database thức:** Node **Keep Supabase Instance Alive** đã được kết nối với trigger **Every 6 Days** (scheduleTrigger). Nếu bạn dùng dự án Supabase trả tiền hoặc self‑hosted, có thể xóa nút này.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm nguồn dữ liệu khác:** Sao chép phần **Get All n8n Documentation Links** → **Extract Links from HTML** → **Loop Over Documentation Pages** và thay URL bằng trang tài liệu nội bộ, wiki công ty hoặc blog sản phẩm.
- **Thông báo Slack/Telegram:** Sau node **RAG Chatbot**, thêm node **Slack** hoặc **Telegram** để forward câu hỏi và câu trả lời vào kênh hỗ trợ.
- **Lưu log truy vấn:** Kết nối node **PostgreSQL** hoặc **Supabase** để lưu mỗi câu hỏi, embedding và câu trả lời để phân tích sau này.
- **Điều chỉnh chunk size:** Ở node **Recursive Character Text Splitter**, thay đổi `Chunk Size` và `Chunk Overlap` để cân bằng giữa độ chi tiết và số lượng vector.
- **Cập nhật mô hình embedding:** Nếu muốn dùng OpenAI `text-embedding-3-small`, đổi dimension trong script SQL thành `1536` và thay các node `embeddingsGoogleGemini` bằng `openaiEmbeddings` (cần credential OpenAI).

### 📌 Kết luận
Workflow này biến việc tra cứu tài liệu n8n từ một công việc thủ công tốn thời gian thành một trải nghiệm trò chuyện thông minh, chính xác và luôn sẵn sàng. Sau chỉ một lần chạy lập chỉ mục, bạn có một chuyên gia AI có thể trả lời bất kỳ câu hỏi nào về n8n – và bạn còn có thể mở rộng nó để trở thành trung tâm kiến thức cho bất kỳ tài liệu nào khác.

**Hãy bắt đầu ngay:** import workflow, cấu hình credentials, chạy **Start Indexing**, sau đó trò chuyện với bot qua **Public URL**. Chúc các sếp tự động hóa thành công và có nhiều thời gian tập trung vào những việc thực sự quan trọng! 🚀