---
title: "🚀 Tự động hóa tải file JSON từ FTP và đồng bộ Vector Database vào Qdrant với n8n"
description: "Hướng dẫn chi tiết cách xây dựng pipeline tự động lấy file JSON từ FTP server, xử lý chia nhỏ văn bản, tạo embedding bằng OpenAI và lưu trữ vào Qdrant Vector Database."
slug: "tu-dong-hoa-tai-file-json-tu-ftp-vao-qdrant-vector-database"
tags: [n8n, automation, qdrant, openai, vector-database, ai, ftp]
keywords: [n8n workflow, qdrant vector store, openai embeddings, ftp automation, rag pipeline, tự động hóa ai]
---

# 🚀 Tự động hóa tải file JSON từ FTP và đồng bộ Vector Database vào Qdrant

Các sếp có đang gặp khó khăn trong việc cập nhật dữ liệu tài liệu (JSON) từ hệ thống lưu trữ cũ (FTP server) lên các hệ thống Trí tuệ nhân tạo (RAG/Vector Database) một cách thủ công không? Việc tải file, đọc nội dung, chia nhỏ văn bản (chunking), tạo embedding và lưu trữ tốn vô số thời gian và dễ xảy ra sai sót.

Bài toán này sẽ được giải quyết triệt để với workflow n8n **"Loading JSON via FTP to Qdrant Vector Database Embedding Pipeline"**. Workflow này tự động hóa 100% quy trình quét file JSON trên FTP, chuyển đổi, tạo embedding qua OpenAI và nạp thẳng vào Qdrant Vector Store mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các file dữ liệu lớn mà không bị timeout, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thủ công tải file từ FTP hay gọi API tạo vector từng cái một.
- **Xử lý thông minh:** Tự động chia nhỏ văn bản (Text Splitting) và chuyển đổi định dạng JSON sang dạng Document tương thích với AI.
- **Đồng bộ mượt mà:** Đưa dữ liệu trực tiếp vào Qdrant Vector Database sẵn sàng cho các ứng dụng RAG, Chatbot AI.
- **Hoạt động bền bỉ:** Cơ chế lặp qua từng file (Loop/Batch) giúp kiểm soát tài nguyên hệ thống, tránh quá tải RAM/CPU.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
2. **FTP Server:** Thông tin truy cập FTP (Host, User, Password) chứa các file JSON cần nhúng (embedding).
3. **OpenAI API Key:** Để sử dụng dịch vụ tạo embeddings (`text-embedding-ada-002` hoặc tương đương).
4. **Qdrant Vector Database:** URL và API Key của cụm Qdrant Cloud hoặc Qdrant chạy Self-hosted.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow này hoặc tải file JSON về máy.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 8 nodes chính, các sếp cần cấu hình chuẩn xác các thông số sau:

- **List all the files (Node FTP - List):**
  - Cần cấu hình **Credentials** kết nối FTP của sếp.
  - Mục **Path**: Trỏ tới thư mục chứa file JSON trên server (Ví dụ: `Oracle/AI/embedding/svenska`).
- **Downloading item (Node FTP - Download):**
  - Cấu hình chung credentials FTP.
  - Đường dẫn file được tự động nhận diện dựa trên kết quả vòng lặp: `Oracle/AI/embedding/svenska/{{ $json.name }}`.
- **Default Data Loader & Character Text Splitter:**
  - Node này nhận dữ liệu dạng binary từ file JSON tải về, tự động chuyển đổi thành cấu trúc văn bản và chia nhỏ các đoạn text (`chunks`) để tối ưu hóa việc học của AI.
- **Embeddings OpenAI:**
  - Chọn **Credentials** OpenAI API.
  - Đảm bảo model vector tương thích với cấu hình trong Qdrant (mặc định 1536 chiều cho `text-embedding-ada-002`).
- **Qdrant Vector Store:**
  - Điền **Credentials** Qdrant API.
  - Khai báo tên **Collection** chính xác trên cụm Qdrant của sếp.
  - *Lưu ý cấu hình Collection trên Qdrant trước khi chạy:*
    ```json
    PUT /collections/{collection_name}
    {
        "vectors": {
          "size": 1536,
          "distance": "Cosine"
        }
    }
    ```

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm với một vài file đầu tiên.
- Kiểm tra kết quả trả về trong Qdrant Dashboard xem các vector đã được nạp thành công chưa.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** để workflow tự động hoạt động theo lịch trình (nếu cài đặt Trigger định kỳ) hoặc kích hoạt thủ công.

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi Trigger:** Thay thế node `When clicking ‘Test workflow’` bằng node **Schedule Trigger** (ví dụ chạy lúc 2 giờ đêm hàng ngày) để tự động cập nhật dữ liệu mới từ FTP.
- **Thêm thông báo:** Gắn thêm node **Slack** hoặc **Telegram** ở cuối luồng để nhận thông báo thành công hoặc cảnh báo khi file FTP lỗi cấu trúc JSON.
- **Lưu Log:** Thêm node **Google Sheets** hoặc **Postgres** để ghi lại lịch sử các file JSON đã được embedding thành công nhằm tránh xử lý trùng lặp.

### 📌 Kết luận
Việc tích hợp dữ liệu từ hệ thống lưu trữ truyền thống (FTP) vào các nền tảng AI hiện đại (Qdrant RAG) nay đã trở nên vô cùng đơn giản với n8n. Hãy áp dụng ngay workflow này để tiết kiệm hàng giờ thao tác thủ công và nâng cấp hệ thống trợ lý AI của doanh nghiệp các sếp lên một tầm cao mới!