---
title: "🤖 **Hệ Thống RAG PDF Tự Động Hóa với OpenAI, Pinecone & Cohere – Tự Trả Lời Câu Hỏi Từ Tài Liệu PDF (Không Cần Code!)"**
description: "Tự động hóa hệ thống RAG (Retrieval-Augmented Generation) để phân tích, lưu trữ và trả lời câu hỏi từ các tài liệu PDF bằng AI, giảm thời gian tìm kiếm thông tin từ 30 phút xuống chỉ vài giây. Phù hợp cho doanh nghiệp, giáo viên, nghiên cứu viên."
slug: "huong-dan-rag-pdf-openai-pinecone-cohere"
tags: [n8n, automation, ai-rag, openai, pinecone, cohere, no-code, vector-database, pdf-automation]
keywords: [n8n workflow rag pdf, tự động hóa trả lời câu hỏi từ pdf, pinecone vector database, cohere reranker, openai embeddings, hệ thống ai tự động hóa]
---

# 🚀 **Tự Động Hóa Hệ Thống RAG PDF: Trả Lời Câu Hỏi Từ Tài Liệu Bằng AI (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất **30 phút đến 1 giờ** để tìm kiếm thông tin trong các tài liệu PDF dài (ví dụ: báo cáo, hợp đồng, tài liệu nghiên cứu) bằng cách:
- **Tìm kiếm thủ công** trên Google hoặc trong file Excel.
- **Đọc từng trang** để tìm câu trả lời chính xác.
- **Mất thời gian** vì thông tin phân tán trên nhiều tài liệu.

**Giải pháp?** Một **hệ thống RAG (Retrieval-Augmented Generation)** tự động hóa quá trình này bằng cách:
✅ **Chuyển đổi PDF thành vector** và lưu trữ trên **Pinecone** (vector database).
✅ **Trả lời câu hỏi chính xác** bằng **OpenAI GPT-4** kết hợp với **Cohere Reranker** (tối ưu hóa kết quả).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Trả lời câu hỏi từ PDF chỉ trong **vài giây** thay vì 30 phút.
- **Chính xác cao**: AI tìm kiếm và tổng hợp thông tin từ nhiều tài liệu đồng thời.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, hoạt động liên tục.
- **Cá nhân hóa**: Dễ dàng mở rộng cho nhiều loại tài liệu (PDF, Word, Excel).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản API** (cần đăng ký trước):
   - [OpenAI API](https://platform.openai.com/) (để tạo **Embeddings** và **Chat Model**).
   - [Pinecone](https://www.pinecone.io/) (để lưu trữ vector).
   - [Cohere API](https://cohere.com/) (để **rerank** kết quả tìm kiếm).
2. **Tài liệu PDF** (các sếp muốn tự động hóa).
3. **n8n Self-Hosted** (để chạy workflow 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/5734](https://n8n.io/workflows/5734) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ link trên vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **11 node** quan trọng, các sếp cần cấu hình như sau:

#### **🔹 Node 1: "On form submission" (n8n-nodes-base.formTrigger)**
- **Chức năng**: Khởi động workflow khi có **form submission** (có thể là form web, Slack, Telegram...).
- **Lưu ý**:
  - Các sếp cần **định nghĩa form** (ví dụ: một form Google Form hoặc Slack button) để gửi **tài liệu PDF** và **câu hỏi** vào workflow.

#### **🔹 Node 2 & 10: "Pinecone Vector Store" (vectorStorePinecone)**
- **Chức năng**: Lưu trữ **vector embeddings** của tài liệu PDF vào Pinecone.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `pineconeApi` (đã đăng ký trước).
  - **Index Name**: Tên index Pinecone (ví dụ: `pdf-rag-system`).
  - **Environment**: Chọn môi trường Pinecone (ví dụ: `us-west1-gcp`).
  - **Namespace**: Có thể để trống hoặc đặt tên riêng.

#### **🔹 Node 3: "Embeddings OpenAI" (embeddingsOpenAi)**
- **Chức năng**: Chuyển đổi **text từ PDF thành vector embeddings** để Pinecone lưu trữ.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Chọn `text-embedding-ada-002` (mặc định).
  - **Input**: Lấy từ **Default Data Loader** (node sau).

#### **🔹 Node 4: "Default Data Loader" (documentDefaultDataLoader)**
- **Chức năng**: Đọc **tài liệu PDF** và chuyển thành text.
- **Cấu hình cần thiết**:
  - **File Path**: Đặt đường dẫn đến **tài liệu PDF** (có thể là URL hoặc file local).
  - **Lưu ý**: Nếu sử dụng **form submission**, các sếp cần **định nghĩa input** để nhận file PDF từ form.

#### **🔹 Node 5: "Recursive Character Text Splitter" (textSplitterRecursiveCharacterTextSplitter)**
- **Chức năng**: Chia **text thành các chunk nhỏ** để dễ dàng xử lý.
- **Cấu hình cần thiết**:
  - **Chunk Size**: Đặt **500-1000 characters** (tùy thuộc vào tài liệu).
  - **Chunk Overlap**: Đặt **50-100 characters** để tránh mất thông tin.

#### **🔹 Node 6: "AI Agent" (agent)**
- **Chức năng**: **Tìm kiếm và trả lời câu hỏi** dựa trên vector store.
- **Cấu hình cần thiết**:
  - **Model**: Chọn `gpt-4.1` (đã cấu hình trong `OpenAI Chat Model`).
  - **Vector Store**: Chọn `Pinecone Vector Store` (node 2).
  - **Memory**: Chọn `Simple Memory` (node 9) để lưu lịch sử chat.

#### **🔹 Node 7: "When chat message received" (chatTrigger)**
- **Chức năng**: Khởi động **AI Agent** khi nhận được **câu hỏi** (có thể từ Slack, Telegram, hoặc form).
- **Lưu ý**:
  - Các sếp cần **định nghĩa input** để nhận **câu hỏi** từ người dùng.

#### **🔹 Node 8: "OpenAI Chat Model" (lmChatOpenAi)**
- **Chức năng**: Sử dụng **GPT-4** để **tổng hợp và trả lời** câu hỏi.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Đã cấu hình là `gpt-4.1`.
  - **Input**: Lấy từ **AI Agent** (node 6).

#### **🔹 Node 9: "Simple Memory" (memoryBufferWindow)**
- **Chức năng**: Lưu **lịch sử chat** để AI nhớ các câu hỏi trước đó.
- **Cấu hình cần thiết**:
  - **Window Size**: Đặt **5-10 messages** để AI nhớ các câu hỏi gần đây.

#### **🔹 Node 11: "Reranker Cohere" (rerankerCohere)**
- **Chức năng**: **Tối ưu hóa kết quả tìm kiếm** trước khi trả lời.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `cohereApi`.
  - **Model**: Chọn `rerank-english-v2.0`.
  - **Input**: Lấy từ **AI Agent** (node 6).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi **tài liệu PDF** và **câu hỏi mẫu** vào form.
   - Kiểm tra **output** của workflow (AI trả lời chính xác không?).
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để hoạt động 24/7.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **Slack App** hoặc **Telegram Bot** để người dùng gửi câu hỏi dễ dàng.
2. **Lưu Log**:
   - Thêm **node `n8n-nodes-base.httpRequest`** để lưu **lịch sử câu hỏi** vào Google Sheets.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để gửi **báo cáo tổng hợp** về tài liệu PDF mỗi tuần.
4. **Mở Rộng Cho Nhiều Tài Liệu**:
   - Sử dụng **node `n8n-nodes-base.iterate`** để xử lý **nhiều PDF cùng lúc**.

---
## 📌 **Kết Luận**
Workflow này giúp **tự động hóa hoàn toàn** quá trình tìm kiếm và trả lời câu hỏi từ **tài liệu PDF**, tiết kiệm **thời gian và công sức** cho các sếp. **Không cần code**, chỉ cần **cấu hình API và import workflow** là có thể sử dụng ngay!

**🚀 Hãy áp dụng ngay và tự động hóa công việc của mình!**

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/5734)
- [Hướng dẫn Pinecone](https://www.pinecone.io/)
- [Hướng dẫn OpenAI API](https://platform.openai.com/docs/api-reference)
- [Hướng dẫn Cohere Reranker](https://cohere.com/docs/api-v2/rerank)