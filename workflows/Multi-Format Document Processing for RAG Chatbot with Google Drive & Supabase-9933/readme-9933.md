---
title: "🚀 Tự động hóa xử lý tài liệu đa định dạng cho RAG Chatbot với Google Drive & Supabase"
description: "Hướng dẫn xây dựng workflow n8n tự động phát hiện file mới trên Google Drive, trích xuất dữ liệu từ PDF, Excel, Text, tạo embeddings và lưu vào Supabase Vector Store cho RAG Chatbot."
slug: "xu-ly-tai-lieu-da-dinh-dang-rag-chatbot-google-drive-supabase"
tags: [n8n, automation, ai-rag, google-drive, supabase, openai]
keywords: [n8n workflow, rag chatbot, google drive trigger, supabase vector store, extract pdf excel, ai automation]
---

# 🚀 Tự động hóa xử lý tài liệu đa định dạng cho RAG Chatbot với Google Drive & Supabase

Các sếp đang xây dựng AI RAG Chatbot nhưng phát ngán vì mỗi lần có tài liệu mới (PDF, Excel, Word, Text) lại phải thủ công copy, convert, cắt nhỏ văn bản (chunking) rồi nhét vào Vector Database? Việc này vừa tốn thời gian, dễ sót file lại cực kỳ nhàm chán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cấu hình một siêu workflow n8n tự động hóa 100%: **Lắng nghe file mới trên Google Drive -> Phân loại định dạng -> Trích xuất dữ liệu thông minh -> Chia nhỏ văn bản -> Tạo Embeddings bằng OpenAI -> Lưu trữ trực tiếp vào Supabase Vector Store**. Giúp chatbot của các sếp luôn được cập nhật kiến thức mới nhất mà không cần đụng tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn (Zero-Manual):** Chỉ cần thả file vào thư mục Google Drive định sẵn, phần còn lại n8n lo.
- **Xử lý đa định dạng:** Hỗ trợ mượt mà các định dạng phổ biến như PDF, Excel (XLSX), Text và tự động convert Google Docs.
- **Tối ưu hóa cho RAG:** Tự động cắt nhỏ văn bản (Recursive Character Text Splitter) và đồng bộ hóa vector embeddings vào Supabase chuẩn xác.
- **Hoạt động 24/7:** Chạy ngầm liên tục, đảm bảo cơ sở tri thức của chatbot luôn "tươi mới".
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để chiến workflow này, các sếp cần chuẩn bị sẵn:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Tài khoản Google Cloud / Google Drive** (để cấu hình Trigger và tải/xóa file).
- **OpenAI API Key** (để tạo Embeddings cho tài liệu).
- **Supabase Account** (đã thiết lập Vector Store và extension `pgvector`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ n8n template #9933) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các credentials và tham số quan trọng sau:

- **File Created (Google Drive Trigger):** 
  - Kết nối `googleDriveOAuth2Api`.
  - Chọn thư mục (Folder) trên Google Drive mà các sếp muốn hệ thống theo dõi. Mọi file mới tải lên thư mục này sẽ kích hoạt workflow.
- **Download File1 & Delete File:**
  - Đảm bảo sử dụng chung credential Google Drive. Node này sẽ tải file về để xử lý và tự động dọn dẹp (xóa file tạm trên Drive nếu cần thiết).
- **Switch2:**
  - Node này chịu trách nhiệm phân loại định dạng file dựa trên MIME type hoặc phần mở rộng (PDF, Excel, Text, Google Docs). Các sếp kiểm tra lại điều kiện chuyển hướng (Routing) để đảm bảo file đi đúng node trích xuất.
- **Các node trích xuất dữ liệu (Extract PDF Text, Extract from Excel, Extract from Text File):**
  - Kiểm tra các thiết lập đọc dữ liệu thô từ file tương ứng.
- **Recursive Character Text Splitter & Enhanced Default Data Loader1:**
  - Cấu hình kích thước chunk (Chunk Size) và độ chồng lấp (Chunk Overlap) phù hợp với mô hình LLM mà các sếp đang sử dụng (thường chunk size từ 500 - 1000 token là hợp lý).
- **Embeddings OpenAI1:**
  - Kết nối `openAiApi` credentials và chọn model embedding tiêu chuẩn (ví dụ: `text-embedding-3-small`).
- **Insert into Supabase Vectorstore1:**
  - Kết nối `supabaseApi` credentials, điền thông tin Table Name chứa vector embeddings và cấu hình kết nối database của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử upload một file PDF hoặc Excel mẫu lên thư mục Google Drive đã chọn để test xem dữ liệu có đẩy thành công vào Supabase hay không.
- Nếu mọi thứ xanh mướt, hãy gạt nút **Active** để workflow chính thức vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo:** Gắn thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo: *"Đã cập nhật thành công tài liệu [Tên File] vào RAG Chatbot!"* mỗi khi có file mới được xử lý.
- **Quản lý lỗi (Error Handling):** Thêm Error Trigger để nếu file bị lỗi font hoặc định dạng lạ không đọc được, hệ thống sẽ gửi email cảnh báo thay vì làm gián đoạn toàn bộ luồng.
- **Tạo thư mục Archive:** Thay vì xóa hẳn file sau khi xử lý (node Delete File), các sếp có thể đổi action thành Move file sang thư mục "Processed" trên Google Drive để dễ quản lý.

### 📌 Kết luận
Với workflow tự động hóa này, việc nạp dữ liệu cho AI RAG Chatbot chưa bao giờ trở nên đơn giản đến thế. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tiết kiệm hàng tá thời gian và tối ưu hóa quy trình vận hành AI! Chúc các sếp thao tác thành công!