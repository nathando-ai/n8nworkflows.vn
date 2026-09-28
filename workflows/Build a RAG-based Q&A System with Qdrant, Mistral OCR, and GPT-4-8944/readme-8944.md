---
title: "🤖 Xây Dựng Hệ Thống Trả Lời Câu Hỏi (Q&A) Dựa Trên RAG với Qdrant, Mistral OCR & GPT-4 - Tự Động Hóa AI Không Code"
description: "Hướng dẫn chi tiết xây dựng hệ thống AI trả lời câu hỏi chính xác dựa trên tài liệu PDF, sử dụng công nghệ RAG (Retrieval-Augmented Generation), Qdrant cho lưu trữ vector, Mistral OCR để extra text từ PDF và GPT-4.1 cho khả năng trả lời cao. Phù hợp cho doanh nghiệp cần tự động hóa hỗ trợ khách hàng hoặc phân tích nội dung."
slug: "xay-dung-he-thong-rag-qdrant-mistral-gpt4"
tags: [n8n, automation, no-code, ai-multimodal, qdrant, gpt-4, mistral-ocr, content-creation, vector-database]
keywords: [n8n workflow rag, tự động hóa ai trả lời câu hỏi, qdrant vector store, mistral ocr pdf, gpt-4 tự động hóa, hệ thống q&a dựa trên tài liệu, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Hệ Thống Trả Lời Câu Hỏi (Q&A) Dựa Trên RAG - Giải Pháp AI Không Code Cho Doanh Nghiệp**

## **🔍 Nỗi Đau Của Doanh Nghiệp Và Giải Pháp Của Workflow**
Hiện nay, khi doanh nghiệp có lượng tài liệu PDF lớn (hợp đồng, báo cáo, tài liệu pháp lý, sách kỹ thuật...), việc trả lời câu hỏi của khách hàng hoặc nhân viên dựa trên nội dung này thường gặp phải những vấn đề:
- **Tốn thời gian**: Phải tìm kiếm thủ công trong hàng trăm trang tài liệu.
- **Không chính xác**: Nhân viên có thể bỏ sót hoặc hiểu sai thông tin.
- **Không cập nhật**: Tài liệu thay đổi nhưng hệ thống không tự động đồng bộ.
- **Không cá nhân hóa**: Trả lời chung chung, không phù hợp với từng trường hợp cụ thể.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Tự động extra text từ PDF** (thậm chí là PDF có hình ảnh) bằng Mistral OCR.
✅ **Lưu trữ và tìm kiếm thông tin** bằng Qdrant (vector database) với độ chính xác cao.
✅ **Trả lời câu hỏi tự động** bằng GPT-4.1, kết hợp với RAG (Retrieval-Augmented Generation) để đảm bảo câu trả lời **chính xác và có nguồn gốc**.
✅ **Đánh giá tự động** kết quả trả lời bằng AI Judge để cải thiện chất lượng.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% thời gian tìm kiếm và trả lời câu hỏi thủ công.
- **Chính xác cao**: AI trả lời dựa trên nội dung tài liệu **không hư cấu**, giảm rủi ro sai sót.
- **Hoạt động 24/7**: Hệ thống tự động cập nhật và trả lời bất kỳ lúc nào.
- **Cá nhân hóa**: Hỗ trợ khách hàng hoặc nhân viên với câu trả lời **phù hợp với từng trường hợp**.
- **Đánh giá tự động**: AI Judge kiểm tra chất lượng trả lời và cải thiện liên tục.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [OpenAI API](https://platform.openai.com/) (để sử dụng GPT-4.1 và embeddings).
   - [Cohere API](https://cohere.com/) (để sử dụng reranker).
   - [Mistral Cloud API](https://mistral.ai/) (để OCR PDF).
   - [Qdrant Cloud](https://qdrant.tech/) (self-hosted hoặc cloud) (để lưu trữ vector).

2. **Tài liệu và dữ liệu**:
   - **Google Drive**: Một folder chứa PDF cần xử lý (link mẫu: [Folder PDF](https://drive.google.com/drive/folders/1FqVwbNrAPn2dHhIwSEtlu5kl3z2jEC0U)).
   - **Google Sheets**: Một bảng để lưu kết quả đánh giá (link mẫu: [Google Sheet](https://docs.google.com/spreadsheets/d/1cgZzr0-D5Kpd6HrKowyoN_fI2dY0dkP9Ljljxix0AlI/edit)).

3. **Hệ thống n8n**:
   - Cài đặt n8n trên **VPS riêng** (self-hosted) để đảm bảo ổn định 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải workflow gốc** từ [đây](https://file.notion.so/f/f/d147bfac-0bab-4c58-884f-f45c5f5a13e8/7f8419b8-7ac3-4c55-8c5c-e0874aa7a46f/AgenticArena_Challenge1_StarterWorkflow.json).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file JSON vừa tải và nhấn **Import**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **34 node** và được chia thành **hai phần chính**:
- **Phần 1: Xử lý PDF và tạo vector store** (Qdrant).
- **Phần 2: Trả lời câu hỏi và đánh giá tự động**.

#### **A. Cấu Hình API & Credentials**
Các node quan trọng cần cấu hình:
| **Node**               | **Credentials Cần Thiết**               | **Lưu Ý**                                                                 |
|------------------------|----------------------------------------|---------------------------------------------------------------------------|
| `Mistral Upload`       | `mistralCloudApi`                      | Điền `API Key` từ Mistral Cloud.                                         |
| `Mistral Signed URL`   | `mistralCloudApi`                      | Cùng API Key như trên.                                                    |
| `Mistral DOC OCR`      | `mistralCloudApi`                      | Chọn model OCR phù hợp (ví dụ: `mistral-7b-instruct-v0.1`).                |
| `Embeddings OpenAI`    | `openAiApi`                            | Điền `API Key` từ OpenAI.                                                 |
| `Qdrant Vector Store`  | `qdrantApi`                            | Cấu hình URL và API Key của Qdrant (self-hosted hoặc cloud).              |
| `Reranker Cohere`      | `cohereApi`                            | Điền `API Key` từ Cohere.                                                |
| `OpenAI Chat Model`    | `openAiApi`                            | Chọn model `gpt-4.1` (hoặc `gpt-4o` nếu có).                              |
| `Google Drive`         | `googleDriveOAuth2Api`                 | Cấu hình OAuth 2.0 cho Google Drive.                                      |

#### **B. Cấu Hình Google Sheets**
- Node `Eval Set` và `Save Eval` sử dụng `googleSheetsOAuth2Api`.
- **Lưu ý**:
  - Copy bảng mẫu từ [đây](https://docs.google.com/spreadsheets/d/1cgZzr0-D5Kpd6HrKowyoN_fI2dY0dkP9Ljljxix0AlI/edit) và **đổi tên sheet** thành `Eval_YourName` (ví dụ: `Eval_Davide`).
  - Trong node `Eval Set`, thay đổi `Sheet Name` thành tên sheet mới của bạn.

#### **C. Cấu Hình Qdrant**
- Node `Create collection` và `Refresh collection` cần:
  - **URL**: `http://<your-qdrant-server>:6333` (nếu self-hosted).
  - **API Key**: Nếu Qdrant yêu cầu.
- Node `Qdrant Vector Store` cần cấu hình:
  - `Collection Name`: Tên collection bạn tạo (ví dụ: `pdf_knowledge_base`).
  - `Vector Size`: 1536 (phù hợp với embeddings OpenAI).

#### **D. Cấu Hình AI Judge**
- Node `LLM as a Judge` sử dụng GPT-4.1 để đánh giá độ chính xác của câu trả lời.
- **Prompt đã được tối ưu** trong node `Run Evaluation`, các sếp **không cần chỉnh sửa** trừ khi muốn thay đổi tiêu chí đánh giá.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Execute Workflow** để chạy thử với một PDF mẫu.
   - Kiểm tra các node quan trọng:
     - `Mistral DOC OCR` → Đảm bảo text được extra chính xác.
     - `Embeddings OpenAI` → Kiểm tra embeddings được tạo ra.
     - `Qdrant Vector Store` → Xác nhận dữ liệu đã được lưu vào Qdrant.
     - `OpenAI Chat Model` → Nhập câu hỏi mẫu và kiểm tra câu trả lời.

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Slack/Telegram cho Trả Lời Tự Động**
- Sử dụng node `webhook` để nhận câu hỏi từ Slack/Telegram.
- Sau khi AI trả lời, gửi kết quả về kênh chat thông qua node `slack` hoặc `telegram`.

### **2. Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng node `set` và `executeWorkflow` để tạo workflow phụ lưu trữ log.
- Tích hợp node `googleSheets` để tự động cập nhật báo cáo hàng ngày/tuần.

### **3. Cải Thiện Model Trả Lời**
- Thay đổi model trong node `OpenAI Chat Model` từ `gpt-4.1` sang `gpt-4o` (nếu có API Key).
- Tối ưu prompt trong node `Reranker Cohere` để tăng độ chính xác của kết quả tìm kiếm.

### **4. Xử Lý PDF Có Hình Ảnh**
- Nếu PDF có hình ảnh, Mistral OCR sẽ tự động extra text. Nếu chất lượng thấp, có thể:
  - Chuyển PDF thành image trước khi OCR (sử dụng node `googleDrive` + `httpRequest`).
  - Sử dụng model OCR khác như `Tesseract` (nếu Mistral không phù hợp).

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp cần tự động hóa hệ thống trả lời câu hỏi dựa trên tài liệu PDF. Với sự kết hợp giữa **RAG, Qdrant, Mistral OCR và GPT-4**, hệ thống không chỉ **tiết kiệm thời gian** mà còn **đảm bảo độ chính xác cao** và **hoạt động liên tục**.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài liệu và API keys** theo hướng dẫn trên.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test và bật Active** để bắt đầu tự động hóa!

👉 **Nếu cần hỗ trợ**, liên hệ với tác giả Davide qua [LinkedIn](https://www.linkedin.com/in/davideboizza/) hoặc email: **info@n3w.it**.

---
**Chúc các sếp thành công với hệ thống AI tự động hóa của mình!** 🚀