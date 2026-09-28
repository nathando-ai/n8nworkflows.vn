---
title: "🤖 Tạo Trợ Lý Học Tập Chuyên Nghiệp Với RAG, Gemini, Telegram & MongoDB – Tự Động Hóa Học Tập 100% Đúng Factual"
description: "Workflow này giúp các giáo viên, trung tâm đào tạo và doanh nghiệp xây dựng một trợ lý AI dựa trên kiến thức riêng, trả lời chính xác và không 'ảo giác' (hallucinate) thông qua RAG + Gemini. Đáp ứng ngay mọi câu hỏi từ học viên qua Telegram với dữ liệu từ tài liệu PDF, sách giáo khoa hoặc tài liệu nội bộ."
slug: "tao-tro-ly-hoc-tap-rag-gemini-telegram-mongodb"
tags: [n8n, automation, ai-agent, rag, google-gemini, mongodb-atlas, telegram-bot, no-code]
keywords: [n8n workflow rag, tự động hóa học tập, gemini ai, trợ lý học tập tự động, mongodb vector search, telegram bot học tập]
---

# 🚀 **Trợ Lý Học Tập Chuyên Nghiệp Bằng RAG + Gemini: Học Với AI Đúng Factual, Không "Đoán"**

## **📌 Nỗi Đau Của Các Sếp & Giải Pháp Của Workflow**
Các giáo viên, trung tâm đào tạo (UPSC, GMAT, kỹ thuật) hoặc doanh nghiệp đang gặp khó khăn khi:
- **Học viên hỏi nhiều câu hỏi lặp lại**, tiêu tốn thời gian trả lời thủ công.
- **AI "ảo giác" (hallucinate)** khi trả lời dựa trên kiến thức chung chứ không phải tài liệu riêng.
- **Không có hệ thống tri thức trung tâm**, dẫn đến thông tin không đồng nhất giữa giáo viên và học viên.

**Workflow này giải quyết tất cả bằng cách:**
✅ **Tạo một trợ lý AI riêng** chỉ trả lời dựa trên **tài liệu của bạn** (PDF, sách giáo khoa, tài liệu nội bộ).
✅ **Không "ảo giác"**: AI chỉ sử dụng kiến thức từ **MongoDB Vector Store**, không truy cập internet.
✅ **Học viên gửi câu hỏi qua Telegram**, AI trả lời ngay lập tức với **dữ liệu chính xác**.
✅ **Tự động hóa ingest knowledge**: Khi có tài liệu mới (upload qua Google Form hoặc Google Drive), nó tự động được chuyển thành vector và lưu vào MongoDB.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho RAG + Gemini)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI trả lời học viên thay vì giáo viên, giảm thiểu công việc lặp lại.
- **Chính xác 100%**: AI chỉ sử dụng **kiến thức từ tài liệu của bạn**, không "ảo giác".
- **Cá nhân hóa học tập**: Học viên có thể tương tác với AI 24/7, nhận phản hồi tức thời.
- **Bảo mật cao**: Tất cả dữ liệu được lưu trên **MongoDB Atlas** (không chia sẻ với bên thứ ba).
- **Dễ dàng mở rộng**: Thêm tài liệu mới mà không cần code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (self-hosted hoặc n8n.cloud).
2. **Google Gemini API Key**:
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey).
   - Cần **$30/month** (miễn phí 300 USD credit đầu tiên).
3. **MongoDB Atlas Cluster**:
   - Tạo **free-tier cluster** tại [MongoDB Atlas](https://www.mongodb.com/atlas/database).
   - **Bật Vector Search** trên collection (hướng dẫn: [MongoDB Vector Search Docs](https://www.mongodb.com/docs/atlas/atlas-search/vector-search/)).
4. **Telegram Bot**:
   - Tạo bot tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Lấy **Chat ID** của nhóm/đối thoại muốn AI tương tác (sử dụng [@userinfobot](https://t.me/userinfobot)).
5. **Google Drive (tùy chọn)**:
   - Nếu muốn ingest từ Google Drive, cần **OAuth 2.0 Credentials** (hướng dẫn: [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python)).
6. **Google Form (tùy chọn)**:
   - Nếu muốn ingest từ form, cần **Webhook URL** của n8n.
:::

---

### 🚀 **Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9595](https://n8n.io/workflows/9595) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab "Import").
- **Cách 3**: Sử dụng **n8n CLI** (nếu self-hosted):
  ```bash
  n8n import workflow.json --name "RAG Learning Assistant"
  ```

#### **2. Các Bước Cấu Hình BẮT BUỘC 📌**
Workflow chia thành **2 phần chính**:
- **Phần 1 (Bên trái)**: **Ingest Knowledge** (chuyển tài liệu thành vector và lưu vào MongoDB).
- **Phần 2 (Bên phải)**: **RAG Chatbot** (trả lời câu hỏi từ Telegram).

##### **🔹 Phần 1: Ingest Knowledge (File Upload → MongoDB)**
| **Node** | **Cấu Hình Cần Thiết** | **Lưu Ý** |
|----------|------------------------|------------|
| **On File Upload** (`formTrigger`) | - Chọn **Google Form** hoặc **Webhook** (nếu upload từ Google Drive). | Nếu dùng Google Drive, cần kết nối **Google Drive Trigger** thay vì Form Trigger. |
| **Download file** (`googleDrive`) | - **Credentials**: Chọn OAuth 2.0 của Google Drive. <br> - **File ID**: Lấy từ URL Google Drive (ví dụ: `https://drive.google.com/file/d/FILE_ID/view`). | Nếu không dùng Google Drive, bỏ qua node này. |
| **Default Data Loader** (`documentDefaultDataLoader`) | - **File Path**: Đặt là `$node["Download file"].json["filePath"]` (nếu dùng Google Drive). | Nếu dùng Form, bỏ qua node này. |
| **Convert Documents to Embeddings** (`embeddingsGoogleGemini`) | - **API Key**: Điền **Google Gemini API Key**. <br> - **Model**: Chọn `models/embedding-gecko-001`. | Đảm bảo tài khoản Gemini có đủ credit. |
| **MongoDB Atlas Vector Store - Insert** (`vectorStoreMongoDBAtlas`) | - **Connection**: Chọn connection MongoDB Atlas. <br> - **Collection**: Tên collection (ví dụ: `learning_documents`). <br> - **Index Name**: Tên index vector (ví dụ: `default_vector_index`). <br> - **Embedding Field**: `embedding`. <br> - **Metadata Fields**: `{"source": "$node["Default Data Loader"].json["source"]"}` (nếu có). | **Bắt buộc**: Tạo **Vector Search Index** trước trên MongoDB. |

##### **🔹 Phần 2: RAG Chatbot (Telegram → Gemini → Telegram)**
| **Node** | **Cấu Hình Cần Thiết** | **Lưu Ý** |
|----------|------------------------|------------|
| **Listen for Aspirant Question** (`telegramTrigger`) | - **Credentials**: Chọn Telegram Bot Token. <br> - **Chat ID**: Điền Chat ID của nhóm/đối thoại. | Test bằng cách gửi tin nhắn cho bot. |
| **RAG Agent** (`agent`) | - **Tools**: Chọn các tool sau: <br>   - `Google Gemini Chat Model` <br>   - `MongoDB Atlas Vector Store - Retrieve` <br>   - `Simple Memory` <br> - **Prompt**: Sử dụng mặc định (có thể tùy chỉnh để phù hợp với lĩnh vực học tập). | **Prompt mẫu**:
   ```json
   "You are a RAG-based learning assistant. Answer questions based ONLY on the retrieved documents from MongoDB. If you don't know the answer, say 'I don't have information about that in my knowledge base.'"
   ``` |
| **Google Gemini Chat Model** (`lmChatGoogleGemini`) | - **API Key**: Điền **Google Gemini API Key**. <br> - **Model**: Chọn `models/gemini-1.0-pro`. | Đảm bảo credit đủ. |
| **MongoDB Atlas Vector Store - Retrieve** (`vectorStoreMongoDBAtlas`) | - **Connection**: Chọn connection MongoDB Atlas. <br> - **Collection**: `learning_documents`. <br> - **Index Name**: `default_vector_index`. <br> - **Query**: `$node["RAG Agent"].json["question"]`. | **Bắt buộc**: Index phải được tạo trước. |
| **Send Answer via Telegram** (`telegram`) | - **Credentials**: Chọn Telegram Bot Token. <br> - **Chat ID**: Điền Chat ID. <br> - **Message**: `$node["RAG Agent"].json["answer"]`. | Test bằng cách gửi câu hỏi và kiểm tra phản hồi. |

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - **Phần Ingest**: Upload một tài liệu mẫu (PDF, DOCX) vào Google Form hoặc Google Drive và kiểm tra xem nó có được chuyển thành vector và lưu vào MongoDB không.
   - **Phần Chatbot**: Gửi một câu hỏi đơn giản qua Telegram (ví dụ: *"Giải thích nguyên lý điện từ?"*) và kiểm tra phản hồi.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động ingest từ nhiều nguồn**:
   - Kết nối **Google Drive + Google Form + OneDrive** bằng cách sử dụng **Switch Node** để chọn nguồn upload.
2. **Lưu log câu hỏi & trả lời**:
   - Thêm node **Google Sheets** hoặc **MongoDB** để ghi lại lịch sử tương tác giữa học viên và AI.
3. **Báo cáo thống kê**:
   - Sử dụng **Google Data Studio** hoặc **Power BI** kết nối với MongoDB để theo dõi:
     - Số lượng câu hỏi được trả lời.
     - Top 5 câu hỏi phổ biến.
     - Thời gian phản hồi trung bình.
4. **Cá nhân hóa AI**:
   - Tùy chỉnh **prompt** của RAG Agent để phù hợp với lĩnh vực (ví dụ: UPSC, GMAT, lập trình).
5. **Bảo mật cao hơn**:
   - Sử dụng **MongoDB Atlas Role-Based Access Control (RBAC)** để chỉ cho phép n8n truy cập vào collection.

---
### 📌 **Kết Luận: Áp Dụng Ngay Để Học Tập Tự Động Hóa!**
Workflow này không chỉ **giải phóng thời gian** cho giáo viên mà còn **cải thiện chất lượng học tập** bằng cách cung cấp **AI trả lời chính xác, dựa trên kiến thức riêng**. Thay vì học viên phải đợi giáo viên trả lời, họ có thể **tương tác với AI 24/7** qua Telegram, nhận phản hồi tức thời và **chính xác**.

**Bước đầu tiên**: Import workflow và cấu hình MongoDB + Telegram. Sau đó, **upload tài liệu đầu tiên** và test với một câu hỏi. Sau vài phút, bạn sẽ có một **trợ lý học tập AI chuyên nghiệp**, hoạt động tự động mà không cần code!

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/9595) và **self-host n8n** trên VPS để tối ưu hiệu suất!