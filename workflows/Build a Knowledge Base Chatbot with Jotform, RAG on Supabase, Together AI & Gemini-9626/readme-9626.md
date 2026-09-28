---
title: "🤖 Xây Dựng Chatbot RAG Thông Minh Với Jotform, Supabase & Gemini"
description: "Tự động hóa quy trình nạp dữ liệu PDF từ Jotform vào Supabase Vector DB và tạo chatbot RAG chính xác bằng Gemini, không cần code."
slug: "chatbot-rag-jotform-supabase-gemini"
tags: [n8n, rag, supabase, gemini, ai-agent, no-code]
keywords: [n8n workflow, chatbot rag, supabase vector, gemini api, tự động hóa ai]
---

# 🤖 Xây Dựng Chatbot RAG Thông Minh Với Jotform, Supabase & Gemini

Trong kỷ nguyên AI, việc xây dựng một trợ lý ảo (Chatbot) không chỉ là gọi API LLM đơn thuần. Nỗi đau lớn nhất của các doanh nghiệp là **Hallucination (ảo giác)** – AI bịa đặt thông tin vì không có ngữ cảnh (context) cụ thể của doanh nghiệp.

Workflow này giải quyết triệt để vấn đề đó bằng kỹ thuật **RAG (Retrieval-Augmented Generation)**. Thay vì để AI "tự nghĩ", workflow sẽ:
1. **Nạp dữ liệu:** Tự động lấy file PDF từ Jotform, cắt nhỏ (chunking), tạo vector (embedding) và lưu vào Supabase.
2. **Tra cứu & Trả lời:** Khi người dùng hỏi, hệ thống tìm kiếm các đoạn văn bản liên quan nhất từ kho dữ liệu, sau đó đưa cho Gemini để trả lời chính xác dựa trên tài liệu thực tế.

Đây là giải pháp "All-in-one" hoàn chỉnh, từ khâu nhập liệu đến khâu trả lời, tất cả đều được tự động hóa 100% trên n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý vector và gọi API AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Độ chính xác cao:** AI chỉ trả lời dựa trên tài liệu thực tế, giảm thiểu tối đa việc bịa đặt.
- **Tự động hóa nhập liệu:** Chỉ cần upload PDF lên Jotform, hệ thống tự động "học" kiến thức mới mà không cần can thiệp thủ công.
- **Cá nhân hóa sâu:** Chatbot hiểu rõ ngữ cảnh của từng tài liệu (hợp đồng, sách, tài liệu nội bộ).
- **Chi phí tối ưu:** Kết hợp Supabase (Vector DB) và Gemini (LLM) giúp giảm chi phí so với việc thuê các dịch vụ RAG quản lý sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị các tài khoản và API Keys sau:
1. **Jotform:** Tài khoản để tạo form upload file.
2. **Supabase:**
   - Tạo project mới.
   - Bật **Vector Extension** (pgvector).
   - Tạo bảng (table) để lưu trữ embeddings (ví dụ: `documents`).
   - Lấy `Supabase API Key` và `Project URL`.
3. **Together AI:**
   - Dùng để tạo Embeddings (Vector hóa văn bản).
   - Lấy `API Key`.
4. **Google Gemini:**
   - Dùng làm LLM chính để trả lời.
   - Lấy `API Key` từ Google AI Studio.
5. **n8n:**
   - Cài đặt các node LangChain (Agent, Chat Trigger) nếu chưa có.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Mở n8n, chọn **Import from URL** hoặc **Import from File**.
- Dán link workflow gốc: `https://n8n.io/workflows/9626` hoặc tải file JSON về và import.
- Workflow gồm 2 luồng chính: Luồng nạp dữ liệu (Jotform Trigger) và Luồng chat (Chat Trigger).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ từng node:

**A. Luồng Nạp Dữ Liệu (The "Librarian" Part)**

1. **JotForm Trigger**:
   - Chọn credentials Jotform của bạn.
   - Chọn **Form ID** của form upload file.
   - *Lưu ý:* Form Jotform cần có trường "File Upload" để người dùng tải lên PDF.

2. **Grab the uploaded knowledgebase file link**:
   - Node này dùng `httpRequest` để lấy link file từ response của Jotform.
   - Kiểm tra mapping data để đảm bảo lấy đúng URL của file PDF.

3. **Extract Text from PDF File**:
   - Node `extractFromFile` (operation: pdf).
   - Đảm bảo input là URL hoặc Binary data của file PDF.

4. **Splitting into Chunks**:
   - Node `code`.
   - Mặc định workflow đã có code cắt text. Các sếp có thể chỉnh sửa tham số `chunkSize` (số ký tự mỗi mảnh) và `chunkOverlap` (số ký tự chồng chéo) để tối ưu chất lượng tìm kiếm.

5. **Embedding Uploaded document**:
   - Node `httpRequest` gọi API **Together AI**.
   - **Credentials:** Chọn `httpBearerAuth` và điền API Key của Together AI.
   - **Body:** Kiểm tra model embedding (ví dụ: `togethercomputer/m2-bert-80M` hoặc model khác hỗ trợ đa ngôn ngữ nếu tài liệu tiếng Việt).

6. **Save the embedding in DB**:
   - Node `supabase`.
   - **Credentials:** Chọn `supabaseApi` (điền Project URL và API Key).
   - **Operation:** Insert.
   - **Table:** Chọn bảng đã tạo trong Supabase.
   - **Mapping:** Map trường `text` (nội dung chunk) và `embedding` (vector từ bước trước) vào các cột tương ứng trong bảng Supabase.

**B. Luồng Chat & Trả Lời (The "Researcher" Part)**

1. **When chat message received**:
   - Node `chatTrigger`.
   - Đây là điểm bắt đầu cho người dùng chat.

2. **Embend User Message**:
   - Node `httpRequest` gọi API **Together AI** (giống bước 5 ở trên).
   - Mục đích: Biến câu hỏi của người dùng thành vector để so sánh với kho dữ liệu.

3. **Search Embeddings**:
   - Node `httpRequest` (hoặc có thể dùng node Supabase nếu cấu hình vector search trực tiếp, nhưng workflow này dùng HTTP Request để linh hoạt hơn).
   - **Credentials:** `supabaseApi`.
   - **Query:** Thực hiện truy vấn tìm kiếm vector gần nhất (cosine similarity) trong bảng Supabase.
   - *Lưu ý:* Cần cấu hình SQL query hoặc API call để lấy top K (ví dụ: 5) đoạn văn bản liên quan nhất.

4. **Aggregate**:
   - Gom các kết quả tìm kiếm lại thành một chuỗi văn bản duy nhất để làm context.

5. **AI Agent**:
   - Node `agent` (LangChain).
   - **System Prompt:** Đây là "linh hồn" của chatbot. Hãy viết prompt rõ ràng: *"Bạn là trợ lý chuyên gia. Hãy trả lời câu hỏi dựa CHỈ VÀO thông tin được cung cấp bên dưới. Nếu không có thông tin, hãy nói rằng bạn không biết. Đừng bịa đặt."*
   - **Context:** Map kết quả từ node `Aggregate` vào phần context của Agent.

6. **Google Gemini Chat Model**:
   - Node `lmChatGoogleGemini`.
   - **Credentials:** Chọn `googlePalmApi` và điền API Key Gemini.
   - Chọn model phù hợp (ví dụ: `gemini-pro` hoặc `gemini-1.5-flash`).

#### 3. Kích hoạt ⚡️

1. **Test Luồng Nạp Dữ Liệu:**
   - Upload một file PDF mẫu lên Jotform.
   - Chạy workflow thủ công (Manual Execution) hoặc chờ trigger.
   - Kiểm tra trong Supabase: Liệu các dòng dữ liệu (text + vector) đã được insert vào bảng chưa?

2. **Test Luồng Chat:**
   - Mở giao diện chat của n8n (hoặc tích hợp vào website).
   - Đặt câu hỏi liên quan đến nội dung trong file PDF vừa upload.
   - Kiểm tra xem AI có trích dẫn đúng thông tin không.

3. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc phải trên cùng của n8n.

### ✍️ Mẹo & gợi ý nâng cao

- **Tối ưu Prompt cho Agent:** Thêm vào System Prompt yêu cầu AI phải trích dẫn nguồn (ví dụ: "Trang 5, Đoạn 2") nếu có thể, hoặc yêu cầu trả lời ngắn gọn, đi thẳng vào vấn đề.
- **Lọc theo loại tài liệu:** Trong bảng Supabase, thêm cột `document_type` hoặc `category`. Khi search, có thể thêm điều kiện lọc để AI chỉ tìm trong phạm vi tài liệu cụ thể (ví dụ: chỉ tìm trong "Hợp đồng" mà không lẫn với "Chính sách nhân sự").
- **Tích hợp Telegram/Slack:** Thay vì dùng Chat Trigger mặc định của n8n, các sếp có thể thay bằng `Telegram Trigger` hoặc `Slack Trigger` để biến nó thành một bot chat trực tiếp trên điện thoại hoặc công cụ làm việc nhóm.
- **Xử lý đa ngôn ngữ:** Nếu tài liệu là tiếng Việt, hãy đảm bảo model Embedding của Together AI hỗ trợ tốt tiếng Việt (ví dụ: các model dựa trên BERT đa ngôn ngữ). Nếu không, cân nhắc dùng model Embedding của Hugging Face hoặc OpenAI (nếu chi phí cho phép) để độ chính xác cao hơn.

### 📌 Kết luận

Workflow **Build a Knowledge Base Chatbot** là một nền tảng vững chắc để các sếp xây dựng hệ thống trợ lý ảo doanh nghiệp. Bằng cách kết hợp sức mạnh của **Jotform** (nhập liệu), **Supabase** (lưu trữ vector), **Together AI** (embedding) và **Gemini** (xử lý ngôn ngữ), chúng ta có được một giải pháp RAG hoàn chỉnh, chính xác và dễ bảo trì.

Hãy bắt đầu ngay hôm nay để biến những tài liệu PDF "chết" thành nguồn tri thức sống động, sẵn sàng phục vụ khách hàng và nhân viên 24/7! 🚀