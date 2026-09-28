---
title: "🚀 Tự Động Tạo Dataset Vector AI Sẵn Sàng Cho LLMs Với Bright Data, Gemini & Pinecone (N8n)"
description: "Workflow tự động hóa hoàn toàn không code để thu thập, xử lý và lưu trữ dữ liệu web thành dataset vector sẵn sàng cho mô hình Gemini và Pinecone, giúp các sếp tiết kiệm 80% thời gian phân tích và chuẩn bị dữ liệu AI."
slug: "tay-dong-tao-dataset-vector-ai-cho-llms"
tags: [n8n, automation, ai, vector-database, pinecone, gemini, no-code, data-processing]
keywords: [n8n workflow ai, tự động hóa dataset vector, gemini api n8n, pinecone vector database, thu thập dữ liệu web tự động, dataset cho llm]
---

# 🚀 Tự Động Tạo Dataset Vector AI Sẵn Sàng Cho LLMs Với Bright Data, Gemini & Pinecone

## 🔍 Nỗi Đau Của Các Sếp Khi Làm Thủ Công
Hiện nay, việc chuẩn bị dataset vector cho mô hình AI như Gemini hay các LLM khác là một quá trình **phức tạp, tốn thời gian và dễ sai sót**:
- **Thu thập dữ liệu web** từ nhiều nguồn khác nhau (blog, bài báo, trang web thương mại) phải làm thủ công hoặc qua các công cụ có hạn chế.
- **Xử lý và phân tích** nội dung để tạo embedding vector phải qua nhiều bước thủ công, dễ dẫn đến mất mát thông tin hoặc sai lệch.
- **Lưu trữ và quản lý** dataset vector trong Pinecone hoặc vector database khác cũng cần kiến thức chuyên sâu về API và cấu trúc dữ liệu.

Workflow này **giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình**, từ thu thập dữ liệu web đến tạo embedding vector và lưu trữ trong Pinecone.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc thu thập và xử lý dữ liệu web.
- **Chuẩn bị dataset vector sẵn sàng** cho mô hình Gemini, Bard, hoặc các LLM khác chỉ với một cú nhấp chuột.
- **Lưu trữ và quản lý** dữ liệu trong Pinecone một cách tự động và chính xác.
- **Tích hợp webhook** để nhận thông báo kết quả hoặc gửi dữ liệu đến các hệ thống khác (Slack, Email, CRM...).
- **Cá nhân hóa** quá trình xử lý bằng AI Agent và Information Extractor, đảm bảo chất lượng cao.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - **Google Gemini API** (để tạo embedding và chat model).
   - **Pinecone API** (để lưu trữ dataset vector).
   - **Web-Unlocker API** (để thu thập dữ liệu web).
   - **Credentials cho HTTP Request** (nếu cần gửi dữ liệu đến các hệ thống bên ngoài).

2. **Dữ liệu đầu vào**:
   - URL hoặc danh sách URL của các trang web cần thu thập dữ liệu.
   - Thông tin cấu hình Pinecone (Environment, Index Name).

3. **Cài đặt Node**:
   - Các node LangChain trong n8n (đã được hỗ trợ trong phiên bản mới nhất của n8n).
   - Node **Webhook** để nhận dữ liệu từ bên ngoài (nếu cần).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3542) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **Import Workflow** (từ menu bên trái).
- Chọn file JSON đã tải hoặc dán toàn bộ JSON vào ô **Paste JSON**.
- Nhấn **Import** để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **16 node** quan trọng, các sếp cần chú ý cấu hình như sau:

##### **A. Cấu hình Web Crawling (Thu thập dữ liệu)**
- **Node: "Set Fields - URL and Webhook URL"**
  - Điền **URL hoặc danh sách URL** cần thu thập vào trường `url`.
  - Ví dụ: `https://example.com/blog` hoặc `["https://example1.com", "https://example2.com"]`.

- **Node: "Make a web request"**
  - Sử dụng **Web-Unlocker API** để thu thập dữ liệu từ URL.
  - Cấu hình **credentials** là `httpHeaderAuth` (nếu cần).
  - Tham số quan trọng:
    - **Method**: `GET`
    - **URL**: `{ $json["url"] }` (để lấy URL từ node trước).
    - **Headers**: Thêm `Authorization` nếu cần (nếu Web-Unlocker yêu cầu).

##### **B. Xử lý và Tạo Embedding Vector**
- **Node: "Default Data Loader"**
  - Đây là node tự động tải dữ liệu từ kết quả thu thập được.
  - Không cần cấu hình thêm (n8n sẽ tự động xử lý).

- **Node: "Recursive Character Text Splitter"**
  - Chia dữ liệu thành các đoạn nhỏ (chunk) để dễ xử lý.
  - Tham số mặc định là hợp lý, nhưng các sếp có thể điều chỉnh:
    - `chunk_size`: Kích thước chunk (ví dụ: 500 từ).
    - `chunk_overlap`: Lượng trùng lặp giữa các chunk (ví dụ: 50 từ).

- **Node: "Embeddings Google Gemini"**
  - Sử dụng **Google Gemini API** để tạo embedding vector.
  - **Bắt buộc**: Điền `googlePalmApi` vào **credentials**.
  - Tham số cần thiết:
    - `model`: Chọn mô hình Gemini phù hợp (ví dụ: `models/text-embedding-001`).
    - `input`: `{ $json["text"] }` (lấy text từ node trước).

- **Node: "Pinecone Vector Store"**
  - Lưu embedding vector vào Pinecone.
  - **Bắt buộc**: Điền `pineconeApi` vào **credentials**.
  - Tham số cần thiết:
    - `environment`: Tên environment Pinecone (ví dụ: `us-west1-gcp`).
    - `index_name`: Tên index Pinecone (ví dụ: `my-vector-index`).
    - `values`: `{ $json["embeddings"] }` (lấy embedding từ node trước).
    - `metadata`: `{ $json["metadata"] }` (thông tin bổ sung về dữ liệu).

##### **C. AI Agent và Information Extractor**
- **Node: "AI Agent"**
  - Sử dụng AI Agent để phân tích và định dạng dữ liệu.
  - **Không cần cấu hình** (n8n sẽ tự động sử dụng cấu hình mặc định của LangChain).

- **Node: "Information Extractor"**
  - Trích xuất thông tin cụ thể từ dữ liệu (ví dụ: tên, ngày, địa chỉ...).
  - Các sếp có thể tùy chỉnh **prompt** để trích xuất thông tin cần thiết.

- **Node: "Structured Output Parser"**
  - Định dạng kết quả trích xuất thành JSON.
  - **Không cần cấu hình** (n8n sẽ tự động xử lý).

##### **D. Webhook và Notification**
- **Node: "Webhook for structured data"**
  - Gửi dữ liệu đã xử lý về dưới dạng JSON.
  - Cấu hình **URL Webhook** của hệ thống bên ngoài (ví dụ: Slack, Email, hoặc CRM).
  - Tham số:
    - `method`: `POST`
    - `url`: `{ $json["webhook_url"] }` (URL từ node "Set Fields").

- **Node: "Webhook for structured AI agent response"**
  - Gửi kết quả từ AI Agent về dưới dạng JSON.
  - Cấu hình tương tự như node trên.

---

#### 3. Kích hoạt ⚡️
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Test Workflow** và điền URL mẫu vào node **"Set Fields - URL and Webhook URL"**.
   - Kiểm tra kết quả ở các node quan trọng như:
     - **"Embeddings Google Gemini"** (đảm bảo embedding được tạo thành công).
     - **"Pinecone Vector Store"** (đảm bảo dữ liệu được lưu vào Pinecone).
     - **"Webhook for structured data"** (đảm bảo dữ liệu được gửi về hệ thống bên ngoài).

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **Inactive** sang **Active**.
   - Nếu cần chạy liên tục, sử dụng **Manual Trigger** hoặc kết nối với **Schedule Node**.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để nhận thông báo khi workflow hoàn thành.
   - Cấu hình trong node **"Webhook for structured AI agent response"** để gửi kết quả đến Slack/Telegram.

2. **Lưu log và báo cáo**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu trữ log của workflow.
   - Cấu hình trong node **"Set Fields"** để thêm thông tin log vào dữ liệu trước khi gửi.

3. **Tùy chỉnh AI Agent**:
   - Các sếp có thể chỉnh sửa **prompt** trong node **"AI Agent"** để trích xuất thông tin cụ thể hơn.
   - Ví dụ: Nếu muốn trích xuất thông tin về sản phẩm, cập nhật prompt như:
     ```
     Extract product name, price, and description from the given text.
     ```

4. **Quản lý dataset trong Pinecone**:
   - Sau khi lưu trữ, các sếp có thể sử dụng **Pinecone Dashboard** để kiểm tra và quản lý dataset.
   - Tích hợp với **LangChain** để query dataset và lấy kết quả từ Gemini.

---

### 📌 Kết luận
Workflow này **giải phóng các sếp khỏi công việc thủ công phức tạp** trong việc chuẩn bị dataset vector cho AI, giúp tiết kiệm thời gian và tăng cường hiệu suất. Bằng cách tự động hóa toàn bộ quy trình từ **thu thập dữ liệu web** đến **tạo embedding vector** và **lưu trữ trong Pinecone**, các sếp có thể tập trung vào việc **phân tích và xây dựng mô hình AI** một cách hiệu quả hơn.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa dataset vector của mình!** 🚀

---