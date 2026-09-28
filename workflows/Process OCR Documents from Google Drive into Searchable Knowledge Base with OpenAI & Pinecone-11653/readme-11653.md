---
title: "🚀 Tự Động Hóa Chuyển Đổi Tài Liệu OCR từ Google Drive thành Cơ Sở Dữ Liệu Tìm Kiếm Tốc Độ với OpenAI & Pinecone"
description: "Giải pháp tự động hóa 100% không code giúp các sếp chuyển đổi tất cả tài liệu OCR từ Google Drive thành cơ sở tri thức tìm kiếm nhanh bằng trí tuệ nhân tạo, tiết kiệm thời gian và nâng cao hiệu suất công việc hàng ngày."
slug: "tieu-dong-hoa-chuyen-doi-tailieu-ocr-google-drive-veo-coso-du-lieu-tim-kiem"
tags: [n8n, automation, no-code, ai-rag, google-drive, openai, pinecone, document-extraction]
keywords: [n8n workflow OCR, tự động hóa tài liệu Google Drive, RAG với OpenAI, Pinecone vector database, tìm kiếm trí tuệ nhân tạo, xử lý văn bản tự động]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Tài Liệu OCR từ Google Drive thành Cơ Sở Dữ Liệu Tìm Kiếm Tốc Độ với OpenAI & Pinecone**

### **Giải pháp cho các sếp:**
Tại sao phải mất hàng giờ để quét, chuyển đổi và tổ chức lại hàng trăm tài liệu OCR từ Google Drive? Hay phải lo lắng khi tìm kiếm thông tin trong tài liệu không hiệu quả? **Workflow này tự động hóa toàn bộ quy trình**, từ tải xuống tài liệu đến tạo cơ sở dữ liệu tìm kiếm trí tuệ nhân tạo (RAG) với OpenAI và Pinecone, giúp các sếp **tìm kiếm thông tin trong giây lát** và **tiết kiệm thời gian lên đến 80%** cho công việc hàng ngày.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần can thiệp thủ công khi có tài liệu mới từ Google Drive.
- **Tìm kiếm trí tuệ nhân tạo (RAG):** Dùng OpenAI và Pinecone để tạo cơ sở dữ liệu vector, giúp tìm kiếm thông tin **nhanh chóng và chính xác** như người dùng.
- **Tối ưu hóa không gian:** Tự động di chuyển tài liệu đã xử lý sang thư mục "Archive" để giữ gìn sạch sẽ Google Drive.
- **Chuẩn bị sẵn sàng cho AI:** Tất cả dữ liệu được chuyển đổi thành **text chunks** sạch sẽ, dễ dàng tích hợp vào hệ thống RAG của doanh nghiệp.
- **Hoạt động liên tục:** Workflow chạy 24/7, không cần phải khởi động lại hoặc can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** và **API Key OAuth2** (để truy cập và tải xuống tài liệu).
2. **Tài khoản OpenAI** với **API Key** (để tạo embeddings).
3. **Tài khoản Pinecone** với **API Key** và **Environment/Index Name** (để lưu trữ vector).
4. **Thư mục Google Drive** để lưu trữ tài liệu OCR (JSON) cần xử lý.
5. **Thư mục Archive** (tự tạo) để lưu trữ tài liệu đã xử lý.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [đây](https://n8n.io/workflows/11653) hoặc sao chép JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create Workflow"** để lưu vào workspace của mình.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **9 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Watch Drive Folder (new files)**
- **Cấu hình:**
  - Chọn **Google Drive OAuth2** credentials đã thiết lập.
  - Điền **Folder ID** của thư mục chứa tài liệu OCR (JSON).
  - **Lưu ý:** Thư mục này phải có **tất cả file JSON** từ OCR (ví dụ: `OCR_Outputs`).

##### **🔹 Node 2: Download file**
- **Cấu hình:**
  - Chọn **Google Drive OAuth2** credentials.
  - **Operation:** `download`.
  - **Lưu ý:** Node này sẽ tải xuống file JSON mới từ Google Drive.

##### **🔹 Node 3: Filename → Lesson Metadata (Code Node)**
- **Cấu hình:**
  - Mở **Code Editor** và chỉnh sửa logic để **trích xuất metadata** từ tên file (ví dụ: `Lesson_123_2024.json` → `Lesson ID: 123`, `Date: 2024`).
  - **Lưu ý:** Các sếp có thể tham khảo mã mẫu từ [n8n Code Node](https://docs.n8n.io/code-node/) để viết logic phù hợp.

##### **🔹 Node 4: Default Data Loader**
- **Cấu hình:**
  - Node này **đọc file JSON** đã tải xuống và chuẩn bị dữ liệu cho bước tiếp theo.
  - **Không cần chỉnh sửa** nếu sử dụng mặc định.

##### **🔹 Node 5: Vision JSON → Clean Text Chunks (Code Node)**
- **Cấu hình:**
  - Mở **Code Editor** và viết logic để:
    1. **Trích xuất text** từ JSON OCR (ví dụ: từ trường `fullTextAnnotation`).
    2. **Lọc bỏ noise** (ký tự đặc biệt, dòng trống).
    3. **Chia text thành chunks** (ví dụ: theo độ dài hoặc ngữ cảnh).
  - **Lưu ý:** Các sếp có thể sử dụng **RecursiveCharacterTextSplitter** (Node 6) để tự động chia text thành chunks.

##### **🔹 Node 6: Recursive Character Text Splitter**
- **Cấu hình:**
  - **Chunk Size:** 500-1000 ký tự (thường dùng).
  - **Chunk Overlap:** 50-100 ký tự (để tránh mất ngữ cảnh).
  - **Lưu ý:** Node này sẽ **tách text thành các đoạn nhỏ** để dễ dàng xử lý.

##### **🔹 Node 7: Generate Embeddings (OpenAI)**
- **Cấu hình:**
  - Chọn **OpenAI API** credentials.
  - **Model:** `text-embedding-ada-002` (mặc định).
  - **Lưu ý:** Đảm bảo **API Key OpenAI** được điền chính xác.

##### **🔹 Node 8: Insert into Pinecone Vector Store**
- **Cấu hình:**
  - Chọn **Pinecone API** credentials.
  - **Environment:** Tên môi trường Pinecone (ví dụ: `us-west1-gcp`).
  - **Index Name:** Tên index vector (ví dụ: `knowledge_base`).
  - **Lưu ý:** Đảm bảo **API Key Pinecone** và **index đã được tạo trước**.

##### **🔹 Node 9: Move File to Archive**
- **Cấu hình:**
  - Chọn **Google Drive OAuth2** credentials.
  - **Operation:** `move`.
  - **Destination Folder ID:** Thư mục Archive (tự tạo trước).
  - **Lưu ý:** Node này sẽ **di chuyển file đã xử lý** sang thư mục Archive để tránh xử lý lại.

---

#### **3. Kích hoạt ⚡️**
- **Bước 1:** **Test Run** với một file mẫu (ví dụ: `Lesson_001_2024.json`).
- **Bước 2:** Kiểm tra **log** trong n8n để đảm bảo không có lỗi.
- **Bước 3:** Bật **Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có file mới được xử lý thành công.

2. **Lưu log vào Google Sheets:**
   - Sử dụng node **Google Sheets** để ghi lại lịch sử xử lý (file nào đã được chuyển đổi, thời gian, status).

3. **Tạo báo cáo định kỳ:**
   - Dùng node **Set** + **Schedule Trigger** để gửi báo cáo tổng hợp về số lượng tài liệu đã xử lý hàng tháng.

4. **Tối ưu hóa OpenAI:**
   - Nếu có nhiều file, có thể **batch embeddings** bằng cách sử dụng **Batch Request** của OpenAI API.

5. **Xử lý lỗi tự động:**
   - Thêm node **If** để kiểm tra lỗi (ví dụ: file không phải JSON) và gửi thông báo lỗi qua email.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa quy trình xử lý tài liệu OCR, chuyển đổi thành cơ sở dữ liệu tìm kiếm trí tuệ nhân tạo. **Không cần code**, chỉ cần cấu hình và chạy 24/7. **Hãy áp dụng ngay** và trải nghiệm sự **tiện lợi và hiệu quả** mà nó mang lại!

👉 **Bắt đầu ngay:** [Tải workflow từ n8n.io](https://n8n.io/workflows/11653) và cài đặt trên VPS của mình!