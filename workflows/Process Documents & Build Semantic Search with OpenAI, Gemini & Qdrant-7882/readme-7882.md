---
title: "🚀 Tự Động Xử Lý Tài Liệu & Xây Dựng Hệ Thống Tìm Kiếm Bằng AI (OpenAI + Gemini + Qdrant) - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh để tải, phân tích, chuyển đổi tài liệu thành vector embeddings, lưu trữ trên Qdrant và tạo hệ thống tìm kiếm thông minh bằng AI. Giúp doanh nghiệp xây dựng knowledge base tự động, tiết kiệm 90% thời gian so với cách làm thủ công."
slug: "tu-dong-xu-ly-ta-lieu-va-tim-kiem-bang-ai"
tags: [n8n, automation, ai-rag, multimodal-ai, google-drive, qdrant, openai, gemini]
keywords: [n8n workflow tự động hóa tài liệu, xây dựng hệ thống tìm kiếm bằng AI, OpenAI embeddings, Qdrant vector database, tự động hóa knowledge base, Google Drive + AI]
---

# 🚀 **Tự Động Xử Lý Tài Liệu & Xây Dựng Hệ Thống Tìm Kiếm Bằng AI (OpenAI + Gemini + Qdrant)**

## **🔍 Nỗi Đau Của Doanh Nghiệp Khi Làm Thủ Công**
Hiện nay, hầu hết các doanh nghiệp phải **tốn thời gian và công sức** để:
- **Tải và phân loại** hàng trăm tài liệu từ Google Drive.
- **Chuyển đổi** các file (PDF, Word, Excel) thành dữ liệu có thể tìm kiếm.
- **Xây dựng hệ thống tìm kiếm thông minh** để trả kết quả chính xác, không chỉ dựa trên từ khóa mà còn **hiểu ngữ nghĩa** (semantic search).
- **Cập nhật liên tục** knowledge base khi có tài liệu mới.

Kết quả? **Tốn nhiều thời gian, dễ sai sót, và không thể mở rộng** khi doanh nghiệp phát triển.

**Workflow này giải quyết tất cả vấn đề đó bằng cách:**
✅ **Tự động tải và xử lý** tất cả tài liệu từ Google Drive.
✅ **Chuyển đổi thành vector embeddings** (OpenAI) để tìm kiếm thông minh.
✅ **Lưu trữ trên Qdrant** (vector database) cho tốc độ truy vấn siêu nhanh.
✅ **Cho phép tìm kiếm bằng AI** (OpenAI + Gemini) trả kết quả chính xác như con người.
✅ **Xóa hoặc di chuyển file** sau khi xử lý (tùy chọn).

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 90% thời gian** so với cách làm thủ công.
- **Tìm kiếm thông minh** (semantic search) thay vì chỉ dựa trên từ khóa.
- **Cập nhật tự động** khi có tài liệu mới.
- **Không cần kỹ sư AI** – chỉ cần cấu hình n8n.
- **Dễ mở rộng** cho hàng nghìn tài liệu.
- **Giao diện chatbot** để tìm kiếm bằng văn bản tự nhiên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã cấp quyền **Read, Write, Delete**).
2. **API Key OpenAI** (để sử dụng model `text-embedding-3-large`).
3. **Qdrant Cloud** (hoặc self-hosted) với:
   - **Endpoint API** và **API Key**.
   - **Collection name** (tên bộ sưu tập vector).
4. **Folder Google Drive** riêng để lưu tài liệu (workflow sẽ **xóa file sau khi xử lý** – **cảnh báo: không phục hồi được!**).
5. **N8n Self-hosted** (không dùng phiên bản miễn phí vì có giới hạn node).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io](https://n8n.io/workflows/7882) (ấn **Download JSON**).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Chọn "Import"** → Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io](https://n8n.io/workflows/7882).
2. **Mở n8n Editor** → **Import** → Chọn **Paste JSON**.
3. **Chọn "Import"** → Workflow sẽ được tạo.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **hai chế độ hoạt động**:
- **Auto Mode (tự động):** Khi có file mới trong Google Drive, workflow sẽ tự động tải, xử lý và xóa.
- **Manual Mode (thủ công):** Sếp có thể **nạp file từ form** hoặc **gọi thủ công** để xử lý.

#### **🔹 Cấu Hình Google Drive**
1. **Tạo một folder mới** (không dùng folder có file cũ, vì workflow sẽ **xóa tất cả**).
2. **Cấu hình OAuth2 Google Drive**:
   - Trong **n8n Credentials** → **Add Credential** → Chọn **Google Drive OAuth2**.
   - **Cấp quyền:** `Read, Write, Delete`.
   - **Folder ID:** Điền ID của folder mới tạo (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
   - **Polling time (thời gian kiểm tra):** Đặt từ **30-60 giây** (tùy thuộc vào tốc độ cập nhật file).

#### **🔹 Cấu Hình OpenAI Embeddings**
1. **Tạo credential OpenAI**:
   - Trong **n8n Credentials** → **Add Credential** → Chọn **OpenAI API**.
   - Điền **API Key** từ tài khoản OpenAI.
   - **Model:** Đặt mặc định là `text-embedding-3-large` (nếu muốn tiết kiệm chi phí, có thể đổi sang `text-embedding-3-small`).

#### **🔹 Cấu Hình Qdrant**
1. **Tạo credential Qdrant**:
   - Trong **n8n Credentials** → **Add Credential** → Chọn **Qdrant API**.
   - Điền:
     - **Endpoint** (URL của Qdrant Cloud hoặc self-hosted).
     - **API Key** (nếu có).
   - **Collection name:** Đặt tên cho bộ sưu tập vector (ví dụ: `company_knowledge_base`).

#### **🔹 Cấu Hình Chunking (Phân đoạn văn bản)**
- Workflow mặc định **chunk size = 1500 tokens** với **overlap = 250 tokens**.
- **Nếu tài liệu quá lớn**, có thể điều chỉnh:
  - **Chunk size nhỏ hơn** (ví dụ: 1000 tokens) để tránh timeout.
  - **Overlap lớn hơn** (ví dụ: 500 tokens) để giữ ngữ cảnh.

#### **🔹 Cấu Hình Chatbot (Tìm Kiếm Bằng AI)**
- Workflow tích hợp **Google Gemini** và **OpenAI** để trả lời câu hỏi từ dữ liệu đã xử lý.
- **Không cần cấu hình thêm**, chỉ cần **bật workflow** và sử dụng **chat trigger** (`When chat message received`).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run (kiểm tra thử)**:
   - Tải một file **PDF/PPT/Word** vào folder Google Drive.
   - Chờ workflow **xử lý và xóa file** (nếu đã cấu hình đúng).
   - Kiểm tra **Qdrant** có xuất hiện embeddings không.

2. **Bật Active**:
   - Đảm bảo **tất cả credential** đã đúng.
   - **Bật workflow** trong n8n Editor.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hiệu Suất**
- **Batch Processing (xử lý theo batch):**
  - Nếu có **hàng trăm file**, chia thành batch nhỏ (ví dụ: 10 file/lần) để tránh timeout.
  - **Cài đặt `batch size = 1`** trong node `Split In Batches` để xử lý một file một lần.

- **Tiết Kiệm Chi Phí OpenAI:**
  - Sử dụng model `text-embedding-3-small` thay vì `text-embedding-3-large`.
  - **Xử lý vào giờ không cao điểm** (OpenAI có giá thấp hơn).

- **Monitor Logs:**
  - Kiểm tra **Execution Logs** trong n8n để phát hiện lỗi (ví dụ: file quá lớn, timeout).

### **2. Tăng Cường An Toàn**
- **Không xóa file quan trọng:**
  - Thay vì **Delete**, sử dụng **Move** để di chuyển file vào folder `processed`.
  - **Cách làm:**
    1. Thay node `Delete File` thành `Move File`.
    2. Đặt **destination folder** là `processed`.

- **Kiểm Tra Trùng Lặp:**
  - Trước khi xử lý, **query Qdrant** để kiểm tra file đã tồn tại chưa.
  - **Cách làm:**
    - Thêm node **HTTP Request** để gọi API Qdrant.
    - Nếu file đã có, **bỏ qua** không xử lý lại.

### **3. Tích Hợp Slack/Telegram**
- **Gửi thông báo khi xử lý xong:**
  - Thêm node **Slack Webhook** hoặc **Telegram Bot** sau khi file được xử lý.
  - **Cách làm:**
    1. Tạo **webhook Slack** hoặc **bot Telegram**.
    2. Thêm node **Slack/Telegram** vào workflow.
    3. Đặt **message template**:
       ```
       File [FILE_NAME] đã được xử lý và lưu vào Qdrant!
       ```

### **4. Tạo Báo Cáo Định Kỳ**
- **Gửi báo cáo hàng tuần:**
  - Sử dụng **n8n + Google Sheets** để lưu lịch sử xử lý.
  - **Cách làm:**
    1. Thêm node **Google Sheets**.
    2. Đặt **sheet name** là `document_processing_log`.
    3. **Schedule** (n8n Pro) để chạy hàng tuần.

---

## 📌 **Kết Luận & Kêu Gọi Hành Động**

Workflow này là **giải pháp hoàn chỉnh** để:
✔ **Tự động hóa xử lý tài liệu** từ Google Drive.
✔ **Xây dựng hệ thống tìm kiếm thông minh** bằng AI.
✔ **Tiết kiệm thời gian và chi phí** so với cách làm thủ công.

**Các sếp hãy:**
1. **Test với file không quan trọng** trước khi áp dụng cho dữ liệu thực.
2. **Cấu hình credential** theo hướng dẫn trên.
3. **Bật workflow** và bắt đầu **tự động hóa knowledge base** của doanh nghiệp!

---
:::note[**Lưu Ý Cuối Cùng**]
- **Files sẽ bị xóa sau khi xử lý** – **không phục hồi được!**
- **Nếu muốn giữ file**, thay **Delete** thành **Move**.
- **N8n Self-hosted** là lựa chọn tốt nhất để workflow **hoạt động 24/7** mà không bị giới hạn.
:::

---
**👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)**
**👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**

---
**🚀 Hãy tự động hóa ngay hôm nay!** 🚀