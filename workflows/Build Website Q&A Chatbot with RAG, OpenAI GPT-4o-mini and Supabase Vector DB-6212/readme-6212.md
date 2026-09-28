---
title: "🤖 Tự Động Hóa Chatbot Trả Lời Câu Hỏi (Q&A) Cho Website Bằng RAG + OpenAI GPT-4o-mini & Supabase Vector DB"
description: "Workflow tự động hóa xây dựng chatbot trả lời câu hỏi thông minh cho website bằng công nghệ RAG (Retrieval-Augmented Generation), tích hợp OpenAI GPT-4o-mini và cơ sở dữ liệu vector Supabase. Giúp các sếp tiết kiệm thời gian hỗ trợ khách hàng, cải thiện trải nghiệm người dùng và tự động hóa quá trình tìm kiếm thông tin trên website."
slug: "tự-dộng-hoa-chatbot-qa-rag-openai-supabase"
tags: [n8n, automation, ai-rag, chatbot, openai, supabase, no-code]
keywords: [n8n workflow chatbot, tự động hóa chatbot website, RAG với OpenAI, Supabase vector database, GPT-4o-mini tự động hóa]
---

# 🚀 **Xây Dựng Chatbot Trả Lời Câu Hỏi (Q&A) Cho Website Bằng RAG + OpenAI GPT-4o-mini & Supabase**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, khi website của các sếp phát triển và nội dung ngày càng phong phú, việc trả lời các câu hỏi thường gặp của khách hàng thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Các sếp phải:
- **Tìm kiếm thủ công** thông tin trên website để trả lời khách hàng.
- **Đáp ứng chậm** khi có nhiều câu hỏi đồng thời.
- **Không đảm bảo tính chính xác** vì phụ thuộc vào kiến thức cá nhân của nhân viên.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa** quá trình trích xuất và lưu trữ thông tin từ website.
✅ **Sử dụng công nghệ RAG (Retrieval-Augmented Generation)** để trả lời chính xác và liên quan đến nội dung website.
✅ **Tích hợp OpenAI GPT-4o-mini** để sinh tổng hợp câu trả lời thông minh.
✅ **Lưu trữ dữ liệu vector trên Supabase**, giúp truy xuất nhanh chóng và hiệu quả.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hỗ trợ khách hàng** (chatbot tự động trả lời 24/7).
- **Tăng trải nghiệm người dùng** với câu trả lời chính xác và liên quan đến nội dung website.
- **Cải thiện SEO** bằng cách tự động hóa việc trích xuất và sử dụng nội dung website.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Dễ dàng mở rộng** cho nhiều website khác nhau.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **OpenAI API Key** (để sử dụng GPT-4o-mini).
   - **Cohere API Key** (để tạo embeddings).
   - **Supabase API Key** (để lưu trữ và truy xuất dữ liệu vector).
   - **PostgreSQL Credentials** (để lưu trữ bộ nhớ chat).

2. **Website cần trích xuất dữ liệu**:
   - URL của website mà các sếp muốn xây dựng chatbot Q&A.

3. **Cài đặt các Node mở rộng**:
   - Các node LangChain trong n8n (n8n-nodes-langchain) để hỗ trợ RAG và vector store.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Create"** → **"Import Workflow"**.
3. Chọn file JSON hoặc dán JSON vào ô nhập liệu.
4. Nhấp **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **14 node** với các bước chính sau:

##### **A. Trích Xuất Dữ Liệu Từ Website**
1. **Node "Enter Website Url" (formTrigger)**
   - **Cấu hình**:
     - Điền **URL của website** cần trích xuất vào trường `websiteUrl`.
     - Ví dụ: `https://example.com`.

2. **Node "Website Data Scrapping" (httpRequest)**
   - **Cấu hình**:
     - **Method**: `GET`.
     - **URL**: `{ $json["websiteUrl"] }`.
     - **Headers**: Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).

3. **Node "Convert to File" (convertToFile)**
   - **Cấu hình**:
     - **Operation**: `toJson`.
     - **File Name**: `website_data.json`.
     - **Content**: `{ $json }`.

4. **Node "Default Data Loader" (documentDefaultDataLoader)**
   - **Cấu hình**:
     - **File**: Chọn file JSON vừa tạo (`website_data.json`).
     - **Loader Type**: `TextLoader` (hoặc tùy chọn phù hợp).

5. **Node "Recursive Character Text Splitter" (textSplitterRecursiveCharacterTextSplitter)**
   - **Cấu hình**:
     - **Chunk Size**: `1000` (tùy chỉnh theo nhu cầu).
     - **Chunk Overlap**: `200`.

##### **B. Lưu Trữ Dữ Liệu Vector Trên Supabase**
6. **Node "Supabase Vector Store" (vectorStoreSupabase)**
   - **Cấu hình**:
     - **Credentials**: Chọn `supabaseApi`.
     - **Table Name**: `documents` (hoặc tên bảng tùy chỉnh).
     - **Embedding Model**: `cohere-embed-multilingual-v3.0` (hoặc tùy chọn khác).
     - **Vector Dimension**: `1024` (phù hợp với Cohere).
     - **Connection String**: Điền vào `supabaseUrl` và `supabaseKey` từ tài khoản Supabase.

7. **Node "Embeddings Cohere" (embeddingsCohere)**
   - **Cấu hình**:
     - **Credentials**: Chọn `cohereApi`.
     - **Model**: `cohere-embed-multilingual-v3.0`.
     - **Input**: `{ $json["text"] }`.

##### **C. Trả Lời Câu Hỏi Bằng RAG**
8. **Node "Question & Answer Retrieve" (agent)**
   - **Cấu hình**:
     - **Vector Store**: Chọn `Supabase Vector Store`.
     - **LLM**: Chọn `OpenAI Chat Modell`.
     - **Prompt**: Sử dụng mặc định hoặc tùy chỉnh để cải thiện chất lượng câu trả lời.

9. **Node "OpenAI Chat Modell" (lmChatOpenAi)**
   - **Cấu hình**:
     - **Credentials**: Chọn `openAiApi`.
     - **Model**: `gpt-4o-mini`.
     - **Temperature**: `0.7` (để đảm bảo câu trả lời logic).
     - **Max Tokens**: `1000`.

10. **Node "Chat Memory" (memoryPostgresChat)**
    - **Cấu hình**:
      - **Credentials**: Chọn `postgres`.
      - **Connection String**: Điền vào `host`, `port`, `database`, `user`, `password`.
      - **Table Name**: `chat_memory`.

##### **D. Trả Lời Câu Hỏi Cho Người Dùng**
11. **Node "When chat message received" (chatTrigger)**
    - **Cấu hình**:
      - **Trigger Type**: `Webhook` (hoặc Slack/Telegram tùy chọn).
      - **Endpoint**: Cần cấu hình URL webhook để nhận câu hỏi từ người dùng.

12. **Node "HTML Extract" (htmlExtract)**
    - **Cấu hình**:
      - **Selector**: Chọn phần tử HTML cần trích xuất (ví dụ: `div.question`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp **"Run"** để kiểm tra workflow với dữ liệu mẫu.
   - Đảm bảo tất cả các node hoạt động bình thường.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, nhấp **"Active"** để workflow chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để chatbot trả lời trên các kênh này.

2. **Lưu Log Câu Trả Lời**:
   - Thêm node `n8n-nodes-base.logger` sau node `OpenAI Chat Modell` để ghi log tất cả các câu hỏi và trả lời.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack` để gửi báo cáo tổng hợp về hoạt động của chatbot.

4. **Cải Thiện Prompt**:
   - Tùy chỉnh prompt trong node `agent` để chatbot trả lời chính xác hơn với nội dung website.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình trả lời câu hỏi trên website** bằng công nghệ RAG và OpenAI GPT-4o-mini. Không chỉ tiết kiệm thời gian mà còn cải thiện trải nghiệm người dùng và tối ưu hóa SEO.

**Hãy áp dụng ngay workflow này và tự động hóa chatbot Q&A cho website của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/6212)** (n8n.io)