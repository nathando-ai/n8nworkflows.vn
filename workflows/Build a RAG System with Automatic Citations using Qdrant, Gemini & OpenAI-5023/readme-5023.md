---
title: "🤖 Xây Dựng Hệ Thống RAG Tự Động Với Trích Dẫn Nguồn Chất Lượng - Qdrant + Gemini + OpenAI"
description: "Workflow tự động hóa hoàn chỉnh cho doanh nghiệp cần hệ thống AI trả lời câu hỏi với trích dẫn nguồn chính xác từ tài liệu Google Drive, sử dụng Qdrant lưu trữ vector và Gemini/OpenAI xử lý. Giúp tiết kiệm 80% thời gian tra cứu thông tin và đảm bảo độ tin cậy cao cho nội dung AI."
slug: "xay-dung-he-thong-rag-tu-dong-voi-qdrant-gemini-openai"
tags: [n8n, automation, ai, rag, qdrant, google-gemini, openai, google-drive, no-code]
keywords: [n8n workflow rag, tự động hóa hệ thống ai, trích dẫn nguồn tự động, qdrant n8n, gemini api n8n, openai embeddings]
---

# 🚀 **Xây Dựng Hệ Thống RAG Tự Động Với Trích Dẫn Nguồn Chất Lượng - Qdrant + Gemini + OpenAI**

## **Nỗi Đau Của Các Sếp Và Giải Pháp AI Tự Động Hóa**
Hiện nay, khi doanh nghiệp cần trả lời các câu hỏi phức tạp từ khách hàng hoặc nội bộ (ví dụ: FAQ, tư vấn kỹ thuật, phân tích báo cáo), các sếp thường phải:
- **Tra cứu thủ công** trên hàng trăm tài liệu Google Drive, mất từ 30 phút đến 2 giờ/lần.
- **Lo ngại độ chính xác** của AI nếu không có trích dẫn nguồn rõ ràng.
- **Không có hệ thống AI cá nhân hóa** để trả lời theo ngữ cảnh cụ thể của từng ngành nghề.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** quá trình tra cứu và trả lời câu hỏi AI.
✅ **Trích dẫn nguồn chính xác** từ tài liệu Google Drive (tên file, đoạn trích dẫn).
✅ **Sử dụng Qdrant** lưu trữ vector để tra cứu siêu nhanh (thời gian phản hồi < 1s).
✅ **Kết hợp Gemini (Google) và OpenAI** để đảm bảo chất lượng câu trả lời cao.
✅ **Hoạt động 24/7** trên VPS tự host (không phụ thuộc vào API công cộng).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** tra cứu thông tin so với cách làm thủ công.
- **Độ tin cậy cao** với trích dẫn nguồn rõ ràng (tên file, đoạn trích dẫn).
- **Câu trả lời AI cá nhân hóa** theo ngữ cảnh ngành nghề của doanh nghiệp.
- **Hoạt động liên tục** 24/7, không cần can thiệp của con người.
- **Dễ dàng mở rộng** cho nhiều loại tài liệu (PDF, DOCX, Excel).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [OpenAI API Key](https://platform.openai.com/account/api-keys) (để tạo embeddings).
   - [Google Gemini API](https://makersuite.google.com/) (để xử lý câu hỏi).
   - [Qdrant Cloud](https://qdrant.tech/cloud/) hoặc [Self-hosted Qdrant](https://qdrant.tech/documentation/guides/self-hosting/) (lưu trữ vector).
   - [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) (trích xuất tài liệu).

2. **Tài liệu nguồn**:
   - Các file cần tra cứu (PDF, DOCX, TXT) được upload lên Google Drive.
   - **Yêu cầu**: File phải có định dạng text (n8n sẽ tự động trích xuất nội dung).

3. **Cấu hình Qdrant**:
   - **URL Qdrant**: `https://your-qdrant-cloud-url` (hoặc địa chỉ self-hosted).
   - **Tên Collection**: Bạn tự đặt (ví dụ: `company_faq`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/5023) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON dưới đây và paste vào **Import Workflow** trong n8n:
  ```json
  // (Dữ liệu JSON đầy đủ sẽ được cung cấp sau khi xác nhận)
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **2 phần chính**:
- **Phần 1: Chuẩn bị dữ liệu** (vectorize tài liệu Google Drive).
- **Phần 2: Trả lời câu hỏi AI** (sử dụng Gemini + Qdrant).

##### **A. Cấu Hình Qdrant (Bước 1 & 2)**
1. **Node "Create collection"**:
   - Thay đổi `QDRANTURL` thành URL Qdrant của bạn.
   - Thay đổi `COLLECTION` thành tên collection (ví dụ: `company_faq`).
   - **Headers**:
     - `api-key`: API Key của Qdrant (nếu dùng Cloud).
     - `Authorization`: `Bearer YOUR_QDRANT_API_KEY`.

2. **Node "Get folder" và "Get file"**:
   - **Google Drive OAuth2**:
     - Tạo credential mới trong n8n với **Google Drive API**.
     - Chọn **Scope**: `https://www.googleapis.com/auth/drive.readonly`.
   - **Folder ID**: Thay bằng ID của folder chứa tài liệu (lấy từ liên kết Google Drive).
   - **File ID**: Thay bằng ID của từng file (lấy từ tab "Share" trong Google Drive).

3. **Node "Default Data Loader"**:
   - **Metadata**: Điền theo mẫu:
     ```json
     {
       "source": "blob",
       "blobType": "text/plain",
       "loc": {
         "lines": {
           "from": 1,
           "to": 15
         }
       },
       "file_id": "FILE_ID_GOOGLE_DRIVE",
       "file_name": "TEN_FILE"
     }
     ```
     - `file_id`: ID của file trong Google Drive.
     - `file_name`: Tên file (sẽ xuất hiện trong trích dẫn).

##### **B. Cấu Hình AI (Gemini & OpenAI)**
1. **Node "Embeddings OpenAI"**:
   - Chọn credential `openAiApi` đã tạo trước.
   - **Model**: Chọn `text-embedding-ada-002` (mặc định).

2. **Node "Google Gemini Chat Model"**:
   - Chọn credential `googlePalmApi` đã tạo.
   - **Model**: Chọn `gemini-pro` (hoặc `gemini-1.0-pro`).

3. **Node "Question and Answer Chain"**:
   - **Prompt**: Sử dụng prompt mặc định (có thể tùy chỉnh để phù hợp với ngành nghề):
     ```
     You are a helpful assistant that answers questions based on the provided context.
     Always cite the exact source from the document.
     ```

##### **C. Cấu Hình Trích Dẫn Nguồn**
- **Node "Retrive sources"**:
  - **Prompt**: `={{ $json.chatInput }}` (lấy câu hỏi từ input của người dùng).
  - **Qdrant Collection**: Chọn collection đã tạo (`company_faq`).

- **Node "Response" (Code)**:
  - **Mã JavaScript** (đã được tối ưu):
    ```javascript
    // Mã sẽ tự động trích dẫn nguồn từ metadata của Qdrant
    const sources = $input.all().map(item => item.json.metadata.file_name).join(", ");
    return {
      response: $input.all()[0].json.answer,
      sources: sources
    };
    ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Test Workflow"** và nhập câu hỏi mẫu (ví dụ: *"Làm thế nào để cấu hình API trong n8n?"*).
   - Kiểm tra output có trích dẫn nguồn không.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng node **Slack Webhook** hoặc **Telegram Bot** để nhận câu hỏi từ nhóm chat.
   - Cấu hình **Webhook** trong node `chatTrigger` để nhận dữ liệu từ Slack/Telegram.

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Sheets** để ghi lại lịch sử câu hỏi và trích dẫn.
   - **Cách làm**:
     - Tạo sheet mới trong Google Drive.
     - Sử dụng node `googleSheets` với credential OAuth2.
     - Cấu hình để ghi dữ liệu từ `$json.response` và `$json.sources`.

3. **Tự Động Xóa Collection Cũ**:
   - Thêm node **HTTP Request** để xóa collection cũ trước khi tạo mới (tránh trùng lặp).
   - **URL**: `https://your-qdrant-url/collections/{collection_name}`
   - **Method**: `DELETE`
   - **Headers**: `api-key: YOUR_QDRANT_API_KEY`

4. **Tùy Chỉnh Prompt cho Ngành Nghề**:
   - Mở rộng node `chainRetrievalQa` để thêm **prompt đặc thù** cho ngành:
     - **Ví dụ cho ngành Y tế**:
       ```plaintext
       You are a medical expert. Only answer questions about symptoms and treatments.
       Always cite the exact page number and source document.
       ```
     - **Ví dụ cho ngành Luật**:
       ```plaintext
       You are a legal advisor. Only provide answers based on Vietnamese law.
       Cite the article number and source document.
       ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa hệ thống AI trả lời câu hỏi với **trích dẫn nguồn chính xác**, tiết kiệm thời gian và nâng cao độ tin cậy. Bằng cách kết hợp **Qdrant (lưu trữ vector)**, **Gemini (xử lý AI)** và **Google Drive (tài liệu nguồn)**, doanh nghiệp có thể:
✔ **Tra cứu siêu nhanh** (thời gian phản hồi < 1s).
✔ **Tránh sai sót** với trích dẫn nguồn rõ ràng.
✔ **Hoạt động 24/7** trên VPS tự host.

**Hành động ngay hôm nay**:
1. **Cài đặt VPS** và cài n8n theo hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với câu hỏi thực tế** và tối ưu prompt cho ngành nghề của bạn.

**Nếu cần hỗ trợ**, liên hệ với tác giả Davide qua:
📧 Email: [info@n3w.it](mailto:info@n3w.it)
🔗 LinkedIn: [linkedin.com/in/davideboizza](https://linkedin.com/in/davideboizza)

---
**Chúc các sếp thành công với hệ thống AI tự động hóa chất lượng cao!** 🚀