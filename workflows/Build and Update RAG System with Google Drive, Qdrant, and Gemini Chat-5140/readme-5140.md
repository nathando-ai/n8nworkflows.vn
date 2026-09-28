---
title: "🤖 Tự Động Xây Dựng & Cập Nhật Hệ Thống RAG (Gemini + Qdrant + Google Drive) - Không Cần Code"
description: "Workflow tự động hóa xây dựng hệ thống RAG (Retrieval-Augmented Generation) với Google Drive làm nguồn tài liệu, Qdrant lưu trữ vector, và Gemini Chat trả lời câu hỏi thông minh. Giúp doanh nghiệp cập nhật dữ liệu liên tục, tiết kiệm 80% thời gian so với cách làm thủ công."
slug: "tieu-dong-xay-dung-rag-gemini-qdrant-google-drive"
tags: [n8n, automation, ai, rag, google-drive, qdrant, gemini, no-code, vector-database]
keywords: [n8n workflow rag, tự động hóa hệ thống gemini, qdrant google drive, chatbot ai không code, cập nhật dữ liệu tự động, vector database]
---

# 🚀 **Tự Động Xây Dựng & Cập Nhật Hệ Thống RAG (Gemini + Qdrant + Google Drive) - Không Cần Code**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã từng phải **tìm kiếm thông tin trong hàng trăm tài liệu**, **cập nhật dữ liệu thủ công** vào hệ thống AI, hoặc **mất nhiều giờ để xây dựng một chatbot trả lời câu hỏi chính xác**? Với **Workflow này**, các sếp có thể:
✅ **Tự động hóa việc xây dựng hệ thống RAG** (Retrieval-Augmented Generation) chỉ với một cú nhấp chuột.
✅ **Cập nhật dữ liệu liên tục** từ Google Drive vào Qdrant (vector database) mà không cần viết một dòng code.
✅ **Sử dụng Gemini Chat** để trả lời câu hỏi từ dữ liệu của doanh nghiệp với độ chính xác cao.
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công, đồng thời giảm thiểu lỗi do con người gây ra.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi cập nhật dữ liệu.
- **Cập nhật liên tục**: Hệ thống tự động đồng bộ dữ liệu mới từ Google Drive vào Qdrant.
- **Trả lời câu hỏi thông minh**: Gemini Chat trả lời dựa trên dữ liệu doanh nghiệp, không phụ thuộc vào kiến thức chung.
- **Giảm chi phí**: Không cần thuê chuyên gia AI để xây dựng hệ thống.
- **Mở rộng dễ dàng**: Thêm tài liệu mới vào Google Drive, hệ thống tự động cập nhật.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu trữ tài liệu nguồn).
2. **Tài khoản Qdrant Cloud** (hoặc tự host Qdrant) với:
   - **URL Qdrant** (ví dụ: `https://your-qdrant-url.cloud.qdrant.io`).
   - **Tên Collection** (ví dụ: `rag_collection`).
   - **API Key Qdrant** (để kết nối).
3. **API Key OpenAI** (để tạo embedding).
4. **API Key Google Gemini** (để chạy chatbot).
5. **File mẫu** (PDF, DOCX, TXT) trong Google Drive để test.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/5140](https://n8n.io/workflows/5140) (chọn **Export JSON**).
2. Trên n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create a new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/5140](https://n8n.io/workflows/5140).
2. Trên n8n Editor, nhấn **Import** → **Paste JSON**.
3. Chọn **Create a new workflow** và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Step 1: Cấu Hình Qdrant**
Workflow yêu cầu **cấu hình Qdrant** ở hai node chính:
- **Node "Create collection"** (`httpRequest`):
  - Thay đổi **URL** thành:
    ```
    https://your-qdrant-url.cloud.qdrant.io/collections/{COLLECTION}
    ```
    (Thay `{COLLECTION}` bằng tên collection của bạn, ví dụ: `rag_collection`).
  - **Headers**:
    - `Authorization`: `Bearer {QDRANT_API_KEY}`.
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "points": [],
      "vectors": {
        "size": 768,
        "distance": "Cosine"
      }
    }
    ```

- **Node "Qdrant Vector Store"** (`vectorStoreQdrant`):
  - **Qdrant URL**: `https://your-qdrant-url.cloud.qdrant.io`.
  - **Collection Name**: `{COLLECTION}` (ví dụ: `rag_collection`).
  - **API Key**: Điền `qdrantApi` (đã cấu hình trước).

#### **🔹 Step 2: Cấu Hình Google Drive**
- **Node "Get files"** (`googleDrive`):
  - **Folder ID**: Điền ID của thư mục trong Google Drive chứa tài liệu (lấy từ liên kết thư mục: `https://drive.google.com/drive/folders/{FOLDER_ID}`).
  - **File Type**: Chọn `file` (để lấy tất cả file, không bao gồm thư mục con).

- **Node "Download files"** (`googleDrive`):
  - **File ID**: Điền **ID cụ thể của file** muốn cập nhật (lấy từ node "Get files" hoặc từ liên kết file: `https://drive.google.com/file/d/{FILE_ID}`).

#### **🔹 Step 3: Cấu Hình OpenAI & Gemini**
- **Node "Embeddings OpenAI"** (`embeddingsOpenAi`):
  - **API Key**: Điền `openAiApi` (đã cấu hình trước).
  - **Model**: Chọn `text-embedding-ada-002`.

- **Node "Google Gemini Chat Model"** (`lmChatGoogleGemini`):
  - **API Key**: Điền `googlePalmApi` (đã cấu hình trước).
  - **Model**: Chọn `gemini-pro`.

#### **🔹 Step 4: Test Workflow**
1. Nhấn **Test workflow** để chạy thử.
2. Kiểm tra:
   - Dữ liệu từ Google Drive có được tải xuống và chuyển thành embedding không?
   - Qdrant có tạo collection và lưu vector không?
   - Gemini có trả lời câu hỏi dựa trên dữ liệu không?

---
### **3. Kích Hoạt Workflow ⚡️**
1. Sau khi cấu hình xong, nhấn **Active** để bật workflow.
2. **Cập nhật dữ liệu tự động**:
   - Khi thêm/xóa/sửa file trong Google Drive, workflow sẽ tự động đồng bộ.
3. **Sử dụng chatbot**:
   - Node **"When chat message received"** (`chatTrigger`) sẽ kích hoạt khi có câu hỏi.
   - Gemini sẽ trả lời dựa trên dữ liệu trong Qdrant.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Cập Nhật Tự Động Hàng Ngày**
- Sử dụng **n8n Cron Trigger** để chạy workflow định kỳ (ví dụ: mỗi ngày 3h sáng).
- Cấu hình ở **Manual Trigger** → **Schedule**:
  ```
  0 3 * * *
  ```
  (Chạy lúc 3h sáng hàng ngày).

### **2. Gửi Báo Cáo Lỗi qua Slack/Email**
- Thêm **node "Set"** sau node "Clear collection" để lưu log lỗi.
- Kết nối với **Slack** hoặc **Email** để thông báo khi có lỗi:
  ```json
  {
    "error": "{{$node.error.json}}",
    "timestamp": "{{$node.error.timestamp}}"
  }
  ```

### **3. Lưu Trữ Log Dữ liệu**
- Sử dụng **Google Sheets** hoặc **Notion API** để ghi lại lịch sử cập nhật:
  - Node **"Set"** → **Google Sheets** (điền dữ liệu vào sheet mới).
  - Cột: `File Name`, `Update Time`, `Status`.

### **4. Mở Rộng với Dữ liệu từ Nhiều Nguồn**
- Thêm **node "Google Drive"** để lấy file từ nhiều thư mục khác nhau.
- Sử dụng **node "Set"** để hợp nhất dữ liệu từ nhiều nguồn trước khi tạo embedding.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng cường hiệu suất** của hệ thống AI bằng cách tự động cập nhật dữ liệu từ Google Drive vào Qdrant. **Gemini Chat** sẽ trở thành một **công cụ trả lời câu hỏi thông minh**, dựa trên kiến thức nội bộ của doanh nghiệp.

**👉 Hãy áp dụng ngay và bắt đầu tự động hóa hệ thống RAG của mình!**
Nếu có vấn đề, hãy liên hệ với **Davide** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/davideboizza) hoặc email **info@n3w.it**.

---
:::info[**Gợi Ý Hạ Tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Chúc các sếp thành công với hệ thống RAG tự động hóa!** 🚀