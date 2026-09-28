---
title: "🤖 **Tự Động Hóa Chatbot Trí Tuệ Nhân Tạo (RAG) với GitHub API: Hỏi Đáp Tự Động bằng OpenAI & Pinecone trên n8n**"
description: "Workflow này tự động hóa việc tạo chatbot RAG (Retrieval-Augmented Generation) để trả lời các câu hỏi về API GitHub bằng cách kết hợp OpenAI (GPT-4o-mini) và Pinecone Vector Database. Giúp các sếp tiết kiệm thời gian hỗ trợ kỹ thuật, cải thiện trải nghiệm người dùng và tự động hóa tri thức API."
slug: "tieu-dong-hoa-chatbot-rag-github-api-openai-pinecone-n8n"
tags: [n8n, automation, AI, RAG, OpenAI, Pinecone, no-code, chatbot, API, engineering]
keywords: [n8n workflow RAG, tự động hóa chatbot GitHub API, OpenAI Pinecone n8n, RAG với n8n, chatbot trí tuệ nhân tạo không code, tự động hóa hỗ trợ kỹ thuật]
---

# 🚀 **Chatbot Trí Tuệ Nhân Tạo (RAG) với GitHub API: Hỏi Đáp Tự Động bằng OpenAI & Pinecone**

## **🔍 Nỗi Đau Của Các Sếp**
Hỗ trợ kỹ thuật API GitHub là một công việc tốn thời gian và dễ gây nhầm lẫn. Các sếp thường phải:
- **Trả lời lại cùng một câu hỏi hàng trăm lần** về cách sử dụng API.
- **Tốn thời gian tìm kiếm tài liệu** trong OpenAPI Specifications để giải đáp.
- **Không thể cung cấp câu trả lời chính xác** vì tri thức phân tán trên nhiều tài liệu.
- **Không có hệ thống tự động hóa** để giảm bớt gánh nặng cho team IT.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách xây dựng một **chatbot RAG (Retrieval-Augmented Generation)** tự động hóa việc trả lời câu hỏi về API GitHub bằng trí tuệ nhân tạo.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** – Chatbot trả lời tự động trong giây lát thay vì phải tìm kiếm tài liệu.
✅ **Chính xác 100%** – Dựa trên dữ liệu chính thức từ GitHub API.
✅ **Cải thiện trải nghiệm người dùng** – Trả lời nhanh chóng, 24/7, không cần chờ đợi.
✅ **Tự động hóa tri thức** – Không cần phải ghi nhớ hoặc tra cứu lại thông tin.
✅ **Dễ dàng mở rộng** – Thêm các API khác vào vector database để chatbot hỗ trợ nhiều hơn.
:::

---

## **🎯 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini và Embeddings).
2. **Tài khoản Pinecone** (để lưu trữ vector database).
3. **API Keys**:
   - `openaiApi` (từ OpenAI).
   - `pineconeApi` (từ Pinecone).
4. **Index Pinecone** có tên `"n8n-demo"` (hoặc điều chỉnh trong workflow).
5. **n8n Self-hosted** (để chạy 24/7, không phụ thuộc vào phiên bản miễn phí).
6. **Node LangChain** (đã cài đặt trong n8n để hỗ trợ RAG).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa workflow này 24/7.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/2705) (hoặc sử dụng link gốc).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON hoặc dán JSON vào ô `Import Workflow`.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **2 phần chính**:
#### **A. Indexing Content (Lưu Trữ Tri Thức vào Pinecone)**
1. **Node `HTTP Request`**
   - **Tham số cần chỉnh**:
     - **Method**: `GET`
     - **URL**: `https://raw.githubusercontent.com/github/rest-api-description/main/openapi.json` (tải OpenAPI Specifications của GitHub).
     - **Headers**: `Accept: application/json`
   - **Lưu ý**: Nếu URL thay đổi, các sếp phải cập nhật lại.

2. **Node `Default Data Loader`**
   - **Không cần chỉnh**, nó tự động xử lý dữ liệu từ `HTTP Request`.

3. **Node `Recursive Character Text Splitter`**
   - **Tham số mặc định** (chia văn bản thành chunks nhỏ) là đủ.
   - **Lưu ý**: Nếu dữ liệu quá lớn, có thể điều chỉnh `chunk_size` hoặc `chunk_overlap`.

4. **Node `Pinecone Vector Store` (Indexing)**
   - **Credentials**: Chọn `pineconeApi` (đã cấu hình trước).
   - **Index Name**: `"n8n-demo"` (hoặc thay đổi nếu đã tạo index khác).
   - **Vector Dimension**: `1536` (phù hợp với embeddings OpenAI).
   - **Metric**: `cosine` (độ tương đồng cosine).
   - **Lưu ý**: Nếu index không tồn tại, Pinecone sẽ tự tạo.

---

#### **B. Querying & Response Generation (Trả Lời Câu Hỏi)**
1. **Node `When chat message received` (Manual Trigger)**
   - **Không cần chỉnh**, dùng để kích hoạt chatbot khi người dùng gửi tin nhắn.

2. **Node `Generate User Query Embedding`**
   - **Credentials**: `openaiApi`.
   - **Model**: `text-embedding-ada-002` (mặc định).
   - **Lưu ý**: Nếu muốn sử dụng model khác, phải cập nhật trong `OpenAI API`.

3. **Node `Pinecone Vector Store (Querying)`**
   - **Credentials**: `pineconeApi`.
   - **Index Name**: `"n8n-demo"`.
   - **Top K**: `3` (số lượng kết quả tương đồng nhất được trả về).
   - **Lưu ý**: Giá trị này ảnh hưởng đến độ chính xác của chatbot.

4. **Node `OpenAI Chat Model` (GPT-4o-mini)**
   - **Credentials**: `openaiApi`.
   - **Model**: `gpt-4o-mini` (mặc định).
   - **Prompt Template**:
     ```plaintext
     You are a helpful assistant that answers questions about the GitHub API.
     Use the provided context to answer the question.
     If you don't know the answer, say "I don't know".
     ```
   - **Lưu ý**: Có thể tùy chỉnh prompt để phù hợp với yêu cầu cụ thể.

5. **Node `Window Buffer Memory`**
   - **Không cần chỉnh**, nó lưu lịch sử chat để chatbot nhớ các câu hỏi trước đó.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với Dữ liệu Mẫu**
   - Gửi một câu hỏi về API GitHub (ví dụ: *"Làm thế nào để tạo một issue mới bằng API?"*).
   - Kiểm tra chatbot trả lời có chính xác không.

2. **Bật Active Workflow**
   - Sau khi test thành công, **bật `Active`** để workflow chạy tự động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH TIẾP CẬN HỢP LÝ**]
1. **Kết Nối với Slack/Telegram**
   - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để chatbot trả lời trên kênh team.

2. **Lưu Log Hỏi Đáp**
   - Thêm **node `n8n-nodes-base.manual`** để ghi lại lịch sử chat vào Google Sheets hoặc Notion.

3. **Báo Cáo Định Kỳ**
   - Sử dụng **node `n8n-nodes-base.schedule`** để gửi báo cáo thống kê về số lượng câu hỏi được trả lời hàng ngày.

4. **Mở Rộng Cho Các API Khác**
   - Thêm **OpenAPI Specifications** của các API khác (ví dụ: Stripe, Twilio) vào vector database để chatbot hỗ trợ nhiều hơn.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc trả lời lại cùng một câu hỏi về API GitHub hàng ngày. Bằng cách kết hợp **OpenAI (GPT-4o-mini) và Pinecone**, chatbot không chỉ **trả lời chính xác** mà còn **học hỏi từ lịch sử tương tác**.

👉 **Hãy tự động hóa ngay hôm nay!**
- **Import workflow** và **cấu hình API keys**.
- **Test với câu hỏi mẫu** và **bật Active**.
- **Mở rộng** để hỗ trợ nhiều API khác.

**Nếu cần hỗ trợ thêm**, các sếp có thể liên hệ với tác giả **Mihai Farcas** qua [đây](https://mihaifarcas.com/) để tư vấn tối ưu hóa workflow!

---
**🚀 Chúc các sếp thành công với tự động hóa trí tuệ nhân tạo!** 🤖✨