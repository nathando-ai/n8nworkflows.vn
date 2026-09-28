---
title: "🚀 Tự Động Hoá Tạo Căn Trữ Vector AI từ Tài Liệu Google Drive bằng Gemini & Supabase (Không Code)"
description: "Workflow này tự động chuyển đổi toàn bộ tài liệu trong Google Drive thành cơ sở dữ liệu vector AI trên Supabase, giúp các sếp xây dựng hệ thống RAG (Retrieval-Augmented Generation) để tra cứu thông tin siêu nhanh và chính xác. Giảm thời gian xử lý từ hàng giờ xuống phút!"
slug: "tay-dong-hoa-tao-can-tru-vector-ai-tu-google-drive"
tags: [n8n, automation, ai-rag, google-drive, supabase, gemini-ai]
keywords: [n8n workflow google drive, tự động hóa tài liệu AI, tạo cơ sở dữ liệu vector, RAG với Gemini, Supabase vector database]
---

# 🚀 **Tự Động Hoá Tạo Căn Trữ Vector AI từ Tài Liệu Google Drive bằng Gemini & Supabase**

### **Giải Phẫu Nỗi Đau Của Các Sếp**
Hiện nay, khi các sếp phải xử lý **nghìn trang tài liệu pháp lý, báo cáo kinh doanh, hoặc tài liệu nghiên cứu**, việc tra cứu thông tin thủ công không chỉ tốn thời gian mà còn dễ gây sai sót. Hệ thống **RAG (Retrieval-Augmented Generation)** là giải pháp tối ưu, nhưng cần một **cơ sở dữ liệu vector** để lưu trữ và tra cứu thông tin một cách **siêu nhanh và chính xác**.

Workflow này **tự động hóa toàn bộ quy trình** từ việc **tải xuống tài liệu từ Google Drive** đến **tạo vector embeddings bằng AI Gemini**, cuối cùng **lưu vào Supabase** để các sếp có thể **tra cứu thông tin bằng từ khóa tự nhiên** mà không cần viết code!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và **ổn định**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần tải xuống và xử lý tài liệu thủ công.
✅ **Tra cứu siêu nhanh**: Sử dụng **RAG** để trả lời câu hỏi bằng AI với độ chính xác cao.
✅ **Cập nhật tự động**: Khi tài liệu mới được thêm vào Google Drive, workflow sẽ **tự động cập nhật cơ sở dữ liệu**.
✅ **Không cần code**: Sử dụng **n8n + AI Gemini** để tự động hóa toàn bộ quy trình.
✅ **Mở rộng dễ dàng**: Có thể kết nối với **Slack/Telegram** để thông báo kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã cấp quyền OAuth2 cho n8n).
2. **Supabase + Postgres** (đã cài đặt **pgvector extension** và tạo bảng `documents`).
3. **Google Gemini API Key** (để tạo embeddings).
4. **URL của thư mục Google Drive** (các sếp sẽ truyền vào khi kích hoạt workflow).

---
:::note[CHUẨN BỊ SUPABASE]
Nếu chưa có Supabase, các sếp có thể tạo miễn phí tại: [https://supabase.com](https://supabase.com)
**Bước cài đặt pgvector:**
```sql
CREATE EXTENSION vector;
CREATE TABLE documents (
    id SERIAL PRIMARY KEY,
    content TEXT,
    embedding vector(768),
    metadata JSONB
);
CREATE FUNCTION match_documents(
    search_text TEXT,
    search_vector vector(768),
    filter_metadata JSONB
) RETURNS SETOF documents AS $$
    SELECT * FROM documents
    WHERE embedding <=> search_vector < 0.7
    AND (filter_metadata IS NULL OR metadata @> filter_metadata)
$$ LANGUAGE SQL;
```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **tải xuống file JSON** từ [n8n.io/workflows/10651](https://n8n.io/workflows/10651) và import vào **n8n Editor** theo cách sau:
1. Mở **n8n Editor** (trên VPS hoặc phiên bản cloud).
2. Nhấn **Import** → Chọn file JSON đã tải xuống.
3. **Hoặc** copy/paste JSON từ file vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần **cấu hình kỹ lưỡng** các phần sau:

##### **🔹 Node 1: "When Executed by Another Workflow" (Trigger)**
- **Chức năng**: Kích hoạt workflow khi nhận được **URL của thư mục Google Drive**.
- **Cấu hình**:
  - **Credentials**: Không cần (là node trigger).
  - **Input**: `{"Drive_Folder_link": "your_drive_url"}` (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp`).
  - **Lưu ý**: Nếu không muốn dùng trigger từ workflow khác, có thể **bỏ qua node này** và sử dụng **Webhook** thay thế.

##### **🔹 Node 2: "Search files and folders" (Google Drive)**
- **Chức năng**: Lấy danh sách tất cả file trong thư mục Google Drive.
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
  - **Key Parameters**:
    - `folderId`: **Trích xuất từ URL** (node sau sẽ xử lý).
    - `mimeType`: Chọn `application/vnd.google-apps.folder` (nếu muốn chỉ lấy thư mục con) hoặc bỏ trống để lấy tất cả file.
  - **Lưu ý**: Nếu URL không chứa `folders/`, node **Extract Folder ID** sẽ tự động xử lý.

##### **🔹 Node 3: "Code in JavaScript" (Extract Folder ID)**
- **Chức năng**: **Trích xuất ID của thư mục** từ URL Google Drive.
- **Mã JavaScript**:
  ```javascript
  const url = $input.all().Drive_Folder_link;
  const regex = /folders\/([a-zA-Z0-9_-]+)/;
  const match = url.match(regex);
  if (match) {
    $output.current().folderId = match[1];
  } else {
    throw new Error("URL Google Drive không hợp lệ!");
  }
  ```
  - **Lưu ý**: Nếu URL đã chứa `folders/`, node này sẽ **trả về ID** để node sau sử dụng.

##### **🔹 Node 4: "Loop Over Items" (Split in Batches)**
- **Chức năng**: **Lặp qua từng file** trong thư mục.
- **Cấu hình**:
  - **Batch Size**: Đặt **10-20 file/lần** để tránh quá tải.
  - **Lưu ý**: Nếu file quá lớn, có thể **tách thành nhiều batch**.

##### **🔹 Node 5: "Download File" (Google Drive)**
- **Chức năng**: **Tải xuống từng file** từ Google Drive.
- **Cấu hình**:
  - **Credentials**: `googleDriveOAuth2Api`.
  - **Key Parameters**:
    - `fileId`: Lấy từ input của node trước.
    - `mimeType`: Chọn `application/pdf` (nếu là PDF) hoặc `text/plain` (nếu là text).
  - **Lưu ý**: Nếu file là **Word/Excel**, có thể cần **node Code** để chuyển đổi sang text.

##### **🔹 Node 6: "Default Data Loader" (Document Loader)**
- **Chức năng**: **Trích xuất nội dung text** từ file tải xuống.
- **Cấu hình**:
  - **File Type**: Chọn **PDF, DOCX, TXT** tùy theo file.
  - **Lưu ý**: Nếu file là **Excel**, có thể cần **node Code** để chuyển đổi sang text.

##### **🔹 Node 7: "Embeddings Google Gemini4" (AI Embeddings)**
- **Chức năng**: **Chuyển đổi text thành vector embeddings** (768 chiều) bằng AI Gemini.
- **Cấu hình**:
  - **Credentials**: `googlePalmApi` (đã cấu hình API Key).
  - **Key Parameters**:
    - `model`: `text-embedding-004`.
    - `input`: `$node["Default Data Loader"].json.content`.
  - **Lưu ý**: **Mỗi request có giới hạn 1000 token**, nếu text quá dài, cần **tách nhỏ**.

##### **🔹 Node 8: "Insert into Supabase Vectorstore" (Supabase)**
- **Chức năng**: **Lưu embeddings vào Supabase** để tra cứu.
- **Cấu hình**:
  - **Credentials**: `supabaseApi`.
  - **Key Parameters**:
    - `table`: `documents` (bảng đã tạo trước).
    - `embedding`: `$node["Embeddings Google Gemini4"].json.embedding`.
    - `content`: `$node["Default Data Loader"].json.content`.
  - **Lưu ý**: **Bảng `documents` phải có cột `embedding vector(768)`**.

##### **🔹 Node 9: "Execute a SQL query" (Optional - Kiểm tra)**
- **Chức năng**: **Kiểm tra số lượng embeddings** đã lưu vào Supabase.
- **Cấu hình**:
  ```sql
  SELECT COUNT(*) FROM documents;
  ```
  - **Lưu ý**: **Không bắt buộc**, chỉ dùng để **kiểm tra kết quả**.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **URL mẫu**:
   ```json
   {
     "Drive_Folder_link": "https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp"
   }
   ```
2. **Chạy workflow** và **kiểm tra Supabase**:
   - Mở **Supabase Dashboard** → **Table `documents`** → Kiểm tra số lượng record.
3. **Bật Active** nếu kết quả đúng.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau node **Insert into Supabase** để **thông báo kết quả**.
   - Ví dụ: `Tự động hoàn thành: ${$node["Insert into Supabase"].json.count} embeddings đã lưu!`.

2. **Lưu log vào Google Sheets**:
   - Thêm **node Google Sheets** để **ghi lại lịch sử chạy workflow**.

3. **Tự động cập nhật định kỳ**:
   - Sử dụng **n8n Cron Trigger** để **chạy workflow hàng ngày** và cập nhật mới.

4. **Tạo API cho RAG**:
   - Sử dụng **Supabase Edge Functions** để **tạo API tra cứu** bằng RAG.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **xử lý thủ công tài liệu**, đồng thời **xây dựng cơ sở dữ liệu vector AI** để **tra cứu thông tin siêu nhanh** bằng RAG. **Không cần code**, chỉ cần **n8n + AI Gemini + Supabase** là có thể **tự động hóa toàn bộ quy trình**!

**🚀 Hãy áp dụng ngay và nâng cao hiệu suất công việc của mình!**
**👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/10651) và bắt đầu tự động hóa!**