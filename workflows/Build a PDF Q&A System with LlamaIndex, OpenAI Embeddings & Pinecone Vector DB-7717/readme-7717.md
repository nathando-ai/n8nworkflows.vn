---
title: "🤖 **Hệ Thống Trả Lời Câu Hỏi (Q&A) Tự Động từ PDF bằng LlamaIndex, OpenAI & Pinecone - Tự Động Hóa 100% Không Code**"
description: "Tự động hóa việc chuyển đổi PDF thành hệ thống trả lời câu hỏi thông minh bằng AI, lưu trữ vector trong Pinecone và sử dụng OpenAI để trả lời chính xác. Giúp doanh nghiệp tiết kiệm thời gian tìm kiếm thông tin trong hợp đồng, chính sách bảo hiểm, tài liệu pháp lý với độ chính xác cao."
slug: "hop-dong-ai-rag-qna-pdf-llamaindex-pinecone"
tags: [n8n, automation, AI RAG, no-code, vector-database, openai, pinecone, llm]
keywords: [n8n workflow pdf qna, tự động hóa trả lời câu hỏi từ pdf, llamaindex pinecone openai, hệ thống chatbot từ tài liệu pháp lý, tự động hóa bảo hiểm, giải pháp raq cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Hệ Thống Trả Lời Câu Hỏi (Q&A) từ PDF bằng AI RAG - Không Cần Code**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất **giờ đồng hồ** để tìm kiếm thông tin trong các tài liệu PDF phức tạp như:
- **Hợp đồng pháp lý** (điều khoản, thời hạn, trách nhiệm)
- **Chính sách bảo hiểm** (điều kiện, ngoại lệ, thủ tục khiếu nại)
- **Tài liệu kỹ thuật** (sơ đồ, quy trình, thông số kỹ thuật)
- **Báo cáo tài chính** (định nghĩa, định nghĩa tài sản, nợ phải trả)

Với **n8n + LlamaIndex + Pinecone**, các sếp có thể **tự động hóa toàn bộ quy trình** này, tạo ra một **hệ thống trả lời câu hỏi (Q&A) thông minh** chỉ với một lần setup. **Không cần viết code**, không cần kiến thức kỹ thuật sâu!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Trả lời câu hỏi trong giây lát thay vì tìm kiếm thủ công trong hàng trăm trang PDF.
- **Độ chính xác cao**: AI hiểu ngữ cảnh và trả lời dựa trên **vector search** (không chỉ tìm kiếm từ khóa).
- **Hoạt động 24/7**: Hệ thống tự động cập nhật khi có tài liệu mới được upload lên Google Drive.
- **Cá nhân hóa**: Dễ dàng mở rộng cho nhiều loại tài liệu khác nhau (bảo hiểm, hợp đồng, tài liệu kỹ thuật).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ PDF nguồn).
2. **Tài khoản LlamaIndex Cloud** (API key để parse PDF thành Markdown).
3. **Tài khoản Pinecone** (để lưu trữ vector embeddings).
4. **Tài khoản OpenAI** (để tạo embeddings và chatbot).
5. **Mã giảm giá VPS** (n8n chạy ổn định 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/7717](https://n8n.io/workflows/7717) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ link trên vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflows này gồm **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Google Drive Trigger**
- **Cấu hình**:
  - Chọn **Google Drive OAuth2** (đã setup trước).
  - **Folder ID**: Thay đổi thành folder Google Drive chứa PDF nguồn (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **File Type**: Chỉ chọn **PDF** (`application/pdf`).

##### **🔹 Node 2: Download File**
- **Cấu hình**:
  - **File ID**: Auto lấy từ trigger.
  - **Destination**: Chọn **temporary file** (n8n sẽ tự xoá sau khi xử lý xong).

##### **🔹 Node 3: Default Data Loader (LlamaIndex)**
- **Cấu hình**:
  - **API Key**: Điền từ **LlamaIndex Cloud** (đăng ký tại [llama.cloud](https://llama.cloud/)).
  - **Endpoint**: `https://api.llamaindex.cloud/v1/parse`.

##### **🔹 Node 4: Upload to Llama Cloud**
- **Cấu hình**:
  - **URL**: `https://api.llamaindex.cloud/v1/parse`.
  - **Headers**: `Content-Type: application/json`.
  - **Body**:
    ```json
    {
      "file": "base64_encoded_pdf",
      "format": "markdown"
    }
    ```
  - **Credentials**: Chọn `httpBearerAuth` (đã setup API key LlamaIndex).

##### **🔹 Node 5: Normalize Text (Code Node)**
- **Cấu hình**:
  - **Mã JavaScript** (cần chỉnh sửa theo yêu cầu):
    ```javascript
    // Giữ nguyên hoặc chỉnh sửa regex để loại bỏ header/footer
    const cleanedText = $input.all().map(item => {
      const text = item.json.markdown;
      // Loại bỏ header/footer, page numbers
      const cleaned = text.replace(/^\s*\d+\s+-\s+/gm, ''); // Loại bỏ số trang
      return cleaned;
    });
    return { json: { normalizedText: cleanedText } };
    ```
  - **Lưu ý**: Các sếp có thể **tùy chỉnh regex** để phù hợp với định dạng PDF của mình.

##### **🔹 Node 6: Chunk Text (Text Splitter)**
- **Cấu hình**:
  - **Chunk Size**: `1200` (tối ưu cho OpenAI).
  - **Overlap**: `150` (giúp giữ ngữ cảnh giữa chunk).

##### **🔹 Node 7: Generate Embeddings (OpenAI)**
- **Cấu hình**:
  - **Model**: `text-embedding-ada-002` (mặc định).
  - **API Key**: Điền từ **OpenAI** (đăng ký tại [openai.com](https://openai.com/)).

##### **🔹 Node 8: Store in Pinecone**
- **Cấu hình**:
  - **Environment**: Chọn môi trường Pinecone (ví dụ: `us-west1-gcp`).
  - **Index Name**: Tạo một index mới (ví dụ: `pdf-qna-index`).
  - **Namespace**: `default` (hoặc tạo namespace riêng).
  - **API Key**: Điền từ **Pinecone** (đăng ký tại [pinecone.io](https://pinecone.io/)).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với một PDF mẫu:
   - Upload một PDF vào Google Drive folder đã cấu hình.
   - Chạy workflow và kiểm tra **Pinecone Console** để xem embeddings đã lưu trữ.
2. **Bật Active**:
   - Đánh dấu workflow thành **Active** để tự động xử lý khi có file mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Mở Rộng Hệ Thống**]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có câu hỏi mới.
2. **Lưu Log & Báo Cáo**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu lịch sử truy vấn và kết quả.
3. **Tạo Chatbot Trả Lời Câu Hỏi**:
   - Kết hợp với **OpenAI ChatGPT API** để trả lời tự động qua **Discord/Email**.
4. **Tự động Cập Nhật Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để kiểm tra folder Google Drive mỗi ngày.
:::

---

### 📌 **Kết Luận**
Với workflow này, các sếp đã **tự động hóa hoàn toàn** việc chuyển đổi PDF thành hệ thống trả lời câu hỏi thông minh, **không cần viết một dòng code**. **Tiết kiệm thời gian, tăng độ chính xác và mở rộng khả năng tự động hóa** cho nhiều loại tài liệu khác nhau.

**🚀 Hãy thử ngay và tự động hóa công việc của mình!**
Nếu có vấn đề, các sếp có thể **đăng câu hỏi trên [n8n Forum](https://community.n8n.io/)** để được hỗ trợ.

---
**Happy Automating! 🤖✨**