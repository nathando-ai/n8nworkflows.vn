---
title: "🚀 Tự động cập nhật hệ thống RAG với Supabase Vector DB khi Google Drive thay đổi"
description: "Hướng dẫn xây dựng hệ thống RAG tự động đồng bộ tài liệu từ Google Drive lên Supabase Vector Database bằng n8n, hỗ trợ đa định dạng PDF, Excel, Text."
slug: "tu-dong-cap-nhat-rag-google-drive-supabase-n8n"
tags: [n8n, automation, ai-rag, google-drive, supabase, openai]
keywords: [n8n workflow, rag automation, google drive to supabase, vector database, ai document extraction]
---

# 🚀 Tự động cập nhật hệ thống RAG với Supabase Vector DB khi Google Drive thay đổi

Việc duy trì cơ sở dữ liệu tri thức (Vector DB) luôn đồng bộ với các tài liệu mới trên Google Drive là một "cực hình" nếu phải làm thủ công. Mỗi khi có file sửa đổi hay tài liệu mới, đội ngũ lại mất công convert, cắt nhỏ đoạn văn (chunking), tạo embedding rồi đẩy lên database. 

Hôm nay, các sếp sẽ được hướng dẫn triển khai một workflow n8n cực kỳ mạnh mẽ (được phát triển bởi edisantosa và Nate Herk) giúp tự động hóa 100% quy trình này: Lắng nghe thay đổi trên Google Drive ➔ Nhận diện định dạng file ➔ Trích xuất văn bản thông minh ➔ Chia nhỏ và tạo Embeddings ➔ Lưu trữ lên Supabase Vector Database.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng bộ thời gian thực:** Hệ thống RAG (AI chatbot) của doanh nghiệp luôn được cập nhật kiến thức mới nhất từ Google Drive ngay khi file được chỉnh sửa.
- **Hỗ trợ đa định dạng:** Tự động xử lý mượt mà các file PDF, Excel (XLSX), Google Docs và Text thông qua các node trích xuất chuyên dụng.
- **Tối ưu hóa Vector Search:** Tự động xóa các bản ghi cũ (`Delete Old Doc Rows`) trước khi nhúng vector mới, tránh tình trạng trùng lặp dữ liệu trong Supabase.
- **Vận hành tự động 24/7:** Không cần sự can thiệp thủ công, loại bỏ hoàn toàn sai sót con người trong quá trình cập nhật tài liệu AI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Drive Account:** Tài khoản Google có quyền truy cập Drive và cấu hình OAuth2 Credentials.
- **Supabase Account:** Đã tạo project Supabase, cài đặt extension `pgvector` và bảng chứa vector (vector store table).
- **OpenAI API Key:** Tài khoản OpenAI để sử dụng mô hình Embeddings và các tính năng xử lý văn bản.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và paste trực tiếp vào n8n Editor, hoặc sử dụng file JSON được cung cấp từ nguồn gốc để import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình chính xác các node sau:

- **File Updated (Google Drive Trigger):** Kết nối tài khoản Google Drive qua `googleDriveOAuth2Api` và chọn thư mục cần theo dõi sự kiện chỉnh sửa file.
- **Download File / Convert to Google Doc2:** Đảm bảo credentials Google Drive được cấp quyền đầy đủ để đọc và tải file.
- **Extract PDF Text1, Extract from Excel1, Extract from Text File1:** Các node này thực hiện nhiệm vụ bóc tách nội dung thô tùy theo định dạng file được nhận diện qua nhánh `Switch`.
- **Delete Old Doc Rows & Insert into Supabase Vectorstore:** Cấu hình `supabaseApi` credentials, điền chính xác Table Name và Connection URL từ dự án Supabase của các sếp.
- **Embeddings OpenAI2:** Nhập OpenAI API Key để hệ thống tiến hành vector hóa dữ liệu trước khi lưu vào Supabase.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một file mẫu trên Google Drive để kiểm tra toàn bộ luồng dữ liệu từ trigger đến Supabase Vector DB.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack:** Gắn thêm node gửi tin nhắn vào cuối workflow để báo cáo mỗi khi có tài liệu mới được cập nhật thành công vào hệ thống RAG.
- **Quản lý lỗi (Error Handling):** Sử dụng Error Trigger để bắt các trường hợp file lỗi định dạng hoặc hết quota OpenAI, giúp hệ thống không bị dừng đột ngột.
- **Lọc định dạng file:** Tùy chỉnh node `If` hoặc `Switch` để chỉ cho phép xử lý một số định dạng file cụ thể (như PDF và Docx) nhằm tiết kiệm tài nguyên token.

### 📌 Kết luận
Workflow này là mảnh ghép hoàn hảo cho bất kỳ tổ chức hay cá nhân nào đang xây dựng hệ thống trợ lý ảo AI RAG dựa trên tài liệu nội bộ. Thiết lập một lần, tự động hóa mãi mãi giúp tiết kiệm hàng tá giờ làm việc thủ công mỗi tuần. Hãy triển khai ngay hôm nay các sếp nhé!