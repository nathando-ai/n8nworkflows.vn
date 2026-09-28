---
title: "💰 Tiết Kiệm Chi Phí AI Trong RAG Workflows: Công Cụ Trả Lời Câu Hỏi Với Nhiều Mô Hình Khác Nhau (GPT-4.1 + GPT-4.1-Mini)"
description: "Workflow tự động hóa tiết kiệm chi phí AI lên đến 90% bằng cách sử dụng mô hình rẻ (GPT-4.1-Mini) thay thế mô hình đắt (GPT-4.1) khi trả lời câu hỏi dựa trên dữ liệu vector. Giúp doanh nghiệp tối ưu hóa chi phí AI trong các ứng dụng RAG (Retrieval-Augmented Generation) mà không giảm chất lượng."
slug: "tiet-kiem-chi-phi-ai-rag-workflow"
tags: [n8n, automation, ai, rag, openai, tiết-kiệm-chi-phí]
keywords: [n8n workflow rag, tự động hóa ai tiết kiệm chi phí, gpt-4.1 mini vs gpt-4.1, vector database n8n, chatbot tiết kiệm chi phí]
---

# 🚀 **Tiết Kiệm Chi Phí AI Trong RAG Workflows: Sử Dụng Mô Hình GPT-4.1-Mini Thay Vì GPT-4.1**

## **🔍 Nỗi Đau Của Doanh Nghiệp Khi Sử Dụng AI Trong RAG**
Hiện nay, nhiều doanh nghiệp đang áp dụng **RAG (Retrieval-Augmented Generation)** để xây dựng chatbot, hệ thống hỗ trợ khách hàng hoặc phân tích dữ liệu từ tài liệu nội bộ. Tuy nhiên, chi phí sử dụng các mô hình AI như **GPT-4.1** của OpenAI là một vấn đề lớn:
- **Mô hình GPT-4.1** có chi phí cao (khoảng **$0.03/1000 token**), làm tăng đáng kể chi phí vận hành.
- **Mô hình GPT-4.1-Mini** (chi phí **~$0.0015/1000 token**) mang lại hiệu suất tương đương trong nhiều trường hợp, nhưng ít được tối ưu hóa trong các workflow RAG hiện tại.
- **Không có giải pháp tự động hóa** để tự động chuyển đổi giữa hai mô hình dựa trên yêu cầu cụ thể của người dùng.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động lưu trữ dữ liệu** vào vector database (Vector Store) để hỗ trợ RAG.
✅ **Sử dụng mô hình rẻ (GPT-4.1-Mini)** để trả lời câu hỏi cơ bản.
✅ **Chuyển sang mô hình đắt (GPT-4.1)** **chỉ khi cần** (ví dụ: câu hỏi phức tạp).
✅ **Tiết kiệm chi phí lên đến 90%** so với việc sử dụng GPT-4.1 toàn bộ workflow.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí AI lên đến 90%** bằng cách tự động chọn mô hình phù hợp.
- **Chất lượng trả lời không giảm** do sử dụng vector store để hỗ trợ RAG.
- **Hoạt động liên tục 24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa trải nghiệm** cho người dùng (mô hình đắt chỉ được kích hoạt khi cần thiết).
- **Dễ dàng mở rộng** cho nhiều loại tài liệu (PDF, Word, CSV, JSON).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** với **API Key** (để kết nối với GPT-4.1 và GPT-4.1-Mini).
✔ **Tài liệu cần phân tích** (PDF, Word, CSV, JSON, hoặc văn bản plain text).
✔ **N8n Self-hosted** (không dùng phiên bản cloud để tối ưu hóa chi phí).
✔ **Node LangChain** được cài đặt (n8n sẽ tự động cài đặt nếu chưa có).

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/5011) (hoặc sao chép JSON từ trang này).
2. **Mở n8n Editor** và nhấn **Import Workflow** (icon "↑" ở góc trên bên trái).
3. **Dán JSON** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và nhấn **Create New Workflow**.
2. **Nhấn "Import Workflow"** và chọn **Paste JSON**.
3. **Dán toàn bộ JSON** từ [đây](https://n8n.io/workflows/5011) và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

Workflow này được chia thành **2 phần chính**:
- **📚 Load Data Flow** (Lưu trữ dữ liệu vào vector store).
- **🐕 Retriever Flow** (Trả lời câu hỏi bằng AI).

#### **🔹 Bước 1: Cấu Hình API Key OpenAI**
1. **Tạo credentials OpenAI** trong n8n:
   - Nhấn **Credentials** (icon "🔑") ở góc trên bên phải.
   - Chọn **Add Credentials** → **OpenAI**.
   - Điền **API Key** từ tài khoản OpenAI của bạn.
   - **Lưu** với tên `openAiApi`.

2. **Kiểm tra trong workflow**:
   - Các node **`Embeddings OpenAI`**, **`Expensive model`** và **`Cheap Model`** đều sử dụng `openAiApi`.
   - **Không cần chỉnh sửa** nếu đã điền đúng API Key.

#### **🔹 Bước 2: Upload Tài Liệu (Load Data Flow)**
1. **Node `Upload your file here` (formTrigger)**:
   - Đây là **điểm kích hoạt** để tải file lên.
   - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định (tải file qua form).
   - **Lưu ý**: Nếu muốn tự động hóa, có thể thay thế bằng **HTTP Request** hoặc **File System** node.

2. **Node `Default Data Loader`**:
   - **Chỉnh `File Path`** nếu tải file từ đường dẫn cụ thể.
   - **Chọn loại file** (PDF, Word, CSV, JSON) trong `File Type`.

3. **Node `Embeddings OpenAI`**:
   - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định (GPT-3.5-turbo-0613).
   - **Lưu ý**: Nếu muốn sử dụng mô hình khác, chỉnh `model` trong `keyParameters`.

4. **Node `Insert Data to Store` (vectorStoreInMemory)**:
   - **Không cần chỉnh sửa** (sử dụng vector store trong bộ nhớ).
   - **Nếu muốn lưu vĩnh viễn**, thay thế bằng **`vectorStoreChroma`** hoặc **`vectorStoreQdrant`**.

#### **🔹 Bước 3: Cấu Hình Chatbot (Retriever Flow)**
1. **Node `When chat message received` (chatTrigger)**:
   - Đây là **điểm kích hoạt** khi người dùng gửi tin nhắn.
   - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định (gửi qua form).

2. **Node `Query Data Tool`**:
   - **Không cần chỉnh sửa** (sử dụng vector store đã lưu trước đó).

3. **Node `AI Agent`**:
   - **Chỉnh `Prompt`** nếu muốn thay đổi logic trả lời.
   - **Mặc định**, nó sẽ sử dụng **`Cheap Model`** (GPT-4.1-Mini) trước, sau đó chuyển sang **`Expensive model`** (GPT-4.1) nếu cần.

4. **Node `Answer questions with a vector store` (toolVectorStore)**:
   - **Không cần chỉnh sửa** (sử dụng vector store để hỗ trợ RAG).

5. **Node `Expensive model` (GPT-4.1)**:
   - **Chỉ sử dụng khi cần** (câu hỏi phức tạp).
   - **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.

6. **Node `Cheap Model` (GPT-4.1-Mini)**:
   - **Sử dụng mặc định** cho câu hỏi đơn giản.
   - **Chi phí thấp hơn** so với GPT-4.1.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Tải **1 file PDF/Word** lên node `Upload your file here`.
   - Chạy **Load Data Flow** (nhấn **Execute Workflow**).
   - Mở **Retriever Flow** và gửi câu hỏi:
     - **Câu hỏi đơn giản** → Sẽ trả lời bằng **GPT-4.1-Mini**.
     - **Câu hỏi phức tạp** → Sẽ tự động chuyển sang **GPT-4.1**.

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật Active** cho cả hai flow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa Chi Phí Thêm**
- **Sử dụng mô hình rẻ hơn** như **GPT-3.5-turbo** cho các câu hỏi cơ bản.
- **Lưu vector store vào Chroma/Qdrant** thay vì bộ nhớ (nếu workflow dài hạn).

### **2. Kết Nối Với Slack/Telegram**
- Thay thế **`chatTrigger`** bằng **`Slack Webhook`** hoặc **`Telegram Bot`** để người dùng gửi tin nhắn qua chat.

### **3. Gửi Báo Cáo Chi Phí Hàng Tháng**
- Sử dụng **`n8n-nodes-base.email`** để gửi báo cáo chi phí OpenAI định kỳ.

### **4. Lưu Log Trả Lời**
- Thêm **`n8n-nodes-base.set`** sau node **`AI Agent`** để lưu câu hỏi và trả lời vào **Google Sheets** hoặc **Airtable**.

### **5. Mở Rộng Cho Nhiều Ngôn Ngữ**
- Sử dụng **`n8n-nodes-base.if`** để chuyển đổi ngôn ngữ trước khi gửi đến AI.

---

## **📌 Kết Luận**
Workflow này **giải quyết vấn đề chi phí cao trong RAG** bằng cách tự động chọn mô hình AI phù hợp. **Các sếp có thể:**
✔ **Tiết kiệm chi phí lên đến 90%** so với việc sử dụng GPT-4.1 toàn bộ.
✔ **Cải thiện trải nghiệm người dùng** bằng cách sử dụng mô hình đắt chỉ khi cần thiết.
✔ **Tự động hóa hoàn toàn** từ tải file đến trả lời câu hỏi.

**Hãy thử ngay và tối ưu hóa chi phí AI của doanh nghiệp!** 🚀

---
**🔗 [Xem workflow gốc](https://n8n.io/workflows/5011)**
**📚 [Tìm hiểu thêm về RAG trong n8n](https://docs.n8n.io/advanced-ai/rag-in-n8n/)**