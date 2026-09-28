---
title: "🚀 Tự Động Viết Blog Chuyên Sâu: Kết Hợp Slack, Perplexity, Pinecone & Google Docs"
description: "Biến ý tưởng blog thành bài viết nghiên cứu chuyên sâu, đúng giọng văn thương hiệu chỉ với một lệnh @mention trong Slack. Workflow n8n kết hợp AI Agent, RAG và Google Docs."
slug: "tu-dong-viet-blog-slack-perplexity-pinecone"
tags: [n8n, automation, no-code, ai-agent, content-marketing, rag]
keywords: [n8n workflow, tự động hóa nội dung, viết blog bằng AI, Perplexity API, Pinecone RAG, Google Docs automation]
---

# 🚀 Tự Động Viết Blog Chuyên Sâu: Kết Hợp Slack, Perplexity, Pinecone & Google Docs

Viết nội dung chất lượng cao luôn là bài toán nan giải cho các đội ngũ Marketing. Bạn muốn bài viết có chiều sâu nghiên cứu, cập nhật xu hướng mới nhất, nhưng đồng thời phải giữ đúng "giọng văn" (brand voice) đặc trưng của công ty? Làm thủ công tốn rất nhiều thời gian để tra cứu dữ liệu, tổng hợp ý tưởng và chỉnh sửa văn phong.

Workflow n8n này giải quyết triệt để vấn đề đó. Chỉ cần một thành viên trong team Marketing @mention bot trong Slack với một chủ đề, hệ thống sẽ tự động:
1. Tra cứu thông tin mới nhất từ **Perplexity**.
2. Tham chiếu bộ quy tắc thương hiệu (Brand Guidelines) đã lưu trong **Pinecone** (Vector Database).
3. Sử dụng **AI Agent** (Claude Sonnet) để tổng hợp thành một bài blog hoàn chỉnh, có cấu trúc và đúng phong cách.
4. Tự động tạo và lưu bài viết vào **Google Docs** để team duyệt và đăng tải.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Rút ngắn quy trình từ ý tưởng đến bài viết hoàn chỉnh từ vài giờ xuống còn vài phút.
- **Đúng giọng văn thương hiệu 100%:** Nhờ cơ chế RAG (Retrieval-Augmented Generation) với Pinecone, AI luôn tham chiếu bộ quy tắc văn phong của công ty.
- **Nội dung có cơ sở khoa học:** Perplexity đảm bảo thông tin trong bài viết là mới nhất và có nguồn gốc rõ ràng.
- **Hợp tác liền mạch:** Trigger trực tiếp trong Slack, nơi team Marketing đang làm việc, không cần chuyển đổi giữa các ứng dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Slack App:** Tạo ứng dụng trong Slack với các quyền (scopes) `app_mentions:read` và `chat:write`.
2. **Pinecone Account:** Tài khoản Pinecone đã có sẵn một Index chứa các vector của Brand Guidelines (quy tắc thương hiệu, giọng văn, từ khóa cấm...).
3. **Perplexity API Key:** Để truy cập công cụ tìm kiếm AI.
4. **Anthropic API Key:** Để sử dụng model Claude Sonnet (hoặc OpenAI nếu thay thế).
5. **Google Docs Account:** Tài khoản Google có quyền tạo và chỉnh sửa tài liệu.
6. **OpenAI API Key:** (Tùy chọn) Nếu sử dụng node Embeddings OpenAI để chuyển đổi văn bản thành vector.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu bạn đã tải file JSON về).
3. Dán link gốc: `https://n8n.io/workflows/8021` hoặc dán trực tiếp nội dung JSON vào editor.
4. Lưu workflow với tên dễ nhớ, ví dụ: `AI Blog Writer - Slack`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình từng node quan trọng sau:

**1. Node `Slack Trigger`**
- Chọn **Credentials** của Slack App đã tạo.
- Đảm bảo channel mà bot được mời vào là channel mà team Marketing sử dụng.
- *Lưu ý:* Bot chỉ phản hồi khi được @mention.

**2. Node `Message a model in Perplexity`**
- Chọn **Credentials** của Perplexity.
- Kiểm tra model đang dùng (mặc định là `sonar-pro`). Đây là model mạnh về tìm kiếm và tổng hợp thông tin.

**3. Node `Pinecone Vector Store` & `Embeddings OpenAI`**
- **Pinecone:** Chọn Credentials Pinecone. Điền đúng **Index Name** nơi các sếp đã lưu trữ Brand Guidelines.
- **Embeddings:** Chọn Credentials OpenAI. Đảm bảo model embedding (ví dụ: `text-embedding-ada-002`) khớp với loại embedding đã dùng khi nạp dữ liệu vào Pinecone.

**4. Node `Anthropic Chat Model`**
- Chọn **Credentials** của Anthropic.
- Model mặc định là `claude-sonnet-4-20250514`. Các sếp có thể giữ nguyên hoặc đổi sang model khác nếu cần.

**5. Node `Blogpost AI Agent`**
- Đây là "bộ não" của workflow. Kiểm tra **System Prompt** (nếu có) để đảm bảo nó hướng dẫn AI cách kết hợp thông tin từ Perplexity và Pinecone.
- Đảm bảo các tool (Perplexity, Pinecone) đã được gắn vào Agent.

**6. Node `Create a document` & `Update a document` (Google Docs)**
- Chọn **Credentials** của Google.
- **Create a document:** Đặt tên file động (ví dụ: `Blog: {{ $json.topic }}`).
- **Update a document:** Đảm bảo node này nhận đúng ID document từ node Create để ghi nội dung vào.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Mở Slack, vào channel đã mời bot.
   - Gõ: `@BotName Viết một bài blog về "Xu hướng AI trong Marketing 2024"`.
   - Chạy workflow trong n8n (bấm Execute Workflow).
   - Kiểm tra xem Google Docs có được tạo và điền nội dung không.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc phải trên cùng của n8n.
   - Từ giờ, mọi lệnh @mention trong Slack sẽ tự động kích hoạt quy trình viết blog.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh Prompt Agent:** Trong node `Blogpost AI Agent`, các sếp có thể thêm yêu cầu cụ thể về độ dài bài viết, cấu trúc (H1, H2, H3), hoặc yêu cầu thêm CTA (Call to Action) ở cuối bài.
- **Gửi thông báo hoàn thành:** Thêm một node `Slack` sau node `Update a document` để bot gửi lại link Google Docs vào Slack, kèm theo thông báo "Bài viết đã sẵn sàng, mời duyệt!".
- **Lưu log vào Google Sheets:** Thêm node `Google Sheets` để ghi lại lịch sử các bài viết đã tạo (ngày, chủ đề, link doc) giúp theo dõi hiệu suất nội dung.
- **Đa ngôn ngữ:** Thay đổi prompt trong Agent để yêu cầu viết bằng tiếng Việt hoặc bất kỳ ngôn ngữ nào khác, phù hợp với thị trường mục tiêu.

### 📌 Kết luận
Workflow này là một ví dụ điển hình của việc kết hợp **Agentic AI** với **RAG** để tạo ra nội dung chất lượng cao, có kiểm soát. Thay vì để AI "tự do" sáng tạo và có thể gây hallucination (ảo giác), chúng ta dùng Perplexity để lấy dữ liệu thật và Pinecone để ràng buộc phong cách.

Các sếp hãy thử áp dụng ngay để biến đội ngũ Marketing của mình thành một cỗ máy sản xuất nội dung mạnh mẽ, tiết kiệm chi phí và tăng tốc độ ra mắt bài viết. Chúc các sếp thành công!