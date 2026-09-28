---
title: "🚀 Tự động hóa biến Gmail thành Vector Embeddings với PGVector và Ollama trong n8n"
description: "Hướng dẫn cấu hình workflow n8n đồng bộ email Gmail vào cơ sở dữ liệu PostgreSQL kèm PGVector và Ollama, giúp tìm kiếm ngữ nghĩa thông minh và lưu trữ thông tin có cấu trúc."
slug: "gmail-to-vector-embeddings-pgvector-ollama-n8n"
tags: [n8n, automation, ai, langchain, postgres, ollama, vector-embeddings]
keywords: [n8n workflow, gmail to vector, pgvector ollama, nomic-embed-text, ai search email, n8n việt nam]
---

# 🚀 Đồng bộ và biến đổi Gmail thành Vector Embeddings với PGVector & Ollama

Các sếp có bao giờ cảm thấy đuối sức khi phải lục tìm hàng ngàn email cũ, hoặc muốn ứng dụng AI vào dữ liệu hòm thư cá nhân/doanh nghiệp nhưng lại lo ngại về vấn đề bảo mật dữ liệu riêng tư? Việc quản lý, trích xuất và tìm kiếm thông tin thủ công từ Gmail thường tốn rất nhiều thời gian và không thể thực hiện các truy vấn ngữ nghĩa thông minh (semantic search).

Giải pháp là đây! Workflow n8n siêu việt được thiết kế bởi **Alfonso Corretti** sẽ tự động hóa toàn bộ quy trình: lấy email từ Gmail, lưu trữ thông tin có cấu trúc vào PostgreSQL, đồng thời biến chúng thành các **Vector Embeddings** cục bộ bằng **Ollama** và **PGVector**. Tất cả diễn ra tự động 100%, bảo mật tuyệt đối vì chạy trên hạ tầng tự host mà không cần gửi dữ liệu qua các API trả phí bên thứ ba!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các dịch vụ Local AI như Ollama, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Vừa hỗ trợ import hàng loạt (bulk import) toàn bộ lịch sử email cũ, vừa tự động cập nhật email mới mỗi phút.
- **Tìm kiếm thông minh (Semantic Search):** Biến email thành Vector Embeddings nhờ mô hình `nomic-embed-text` qua Ollama và lưu trữ vào PGVector để truy vấn tìm kiếm ngữ nghĩa cực đỉnh.
- **Lưu trữ dữ liệu kép:** Vừa lưu trữ thông tin có cấu trúc (metadata, tiêu đề, nội dung...) vào bảng PostgreSQL (`emails_metadata`), vừa lưu vector embeddings (`emails_embeddings`) có liên kết chặt chẽ qua `email_id` và `thread_id`.
- **Bảo mật tuyệt đối:** Hoàn toàn chạy local với Ollama và database riêng, không lo rò rỉ dữ liệu nhạy cảm ra ngoài.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted trên VPS).
- **PostgreSQL Database:** Đã bật extension `vector` (PGVector) để lưu trữ vector embeddings.
- **Ollama Server:** Đã cài đặt Ollama và kéo sẵn mô hình embed (`nomic-embed-text:latest`).
- **Gmail Account / Credentials:** Tài khoản Gmail đã cấu hình OAuth2 Credentials trong n8n để đọc email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n (hoặc tải file JSON từ link gốc [n8n Workflow #3762](https://n8n.io/workflows/3762)), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 16 nodes kết hợp linh hoạt giữa Trigger thủ công/tự động, LangChain components và xử lý database:
- **Gmail Trigger & Get a batch of messages:** Kết nối với tài khoản Gmail của bạn thông qua Gmail OAuth2 Credentials để lấy dữ liệu hòm thư.
- **Set before and after dates & Explode interval into weeks:** Cấu hình mốc thời gian bắt đầu quét email. *Lưu ý quan trọng:* Hãy chỉnh sửa node Code và Set để khớp với ngày tạo tài khoản Gmail hoặc mốc thời gian sếp muốn bắt đầu lấy dữ liệu cũ.
- **Store structured (Postgres) & Create the table:** Đảm bảo kết nối tới database PostgreSQL của sếp, node `Create the table` sẽ chuẩn bị sẵn cấu trúc bảng `emails_metadata`.
- **Embeddings Ollama:** Cấu hình địa chỉ URL của Ollama server và chọn model `nomic-embed-text:latest`.
- **Store vectorized (vectorStorePGVector):** Kết nối tới bảng vector embeddings (`emails_embeddings`) trong PostgreSQL để lưu các vector được tạo từ `Default Data Loader` và `Recursive Character Text Splitter`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm chế độ bulk import toàn bộ email lịch sử.
- Sau khi kiểm tra dữ liệu đã đổ về Database chính xác, hãy bật công tắc **Active workflow** để hệ thống tự động bắt email mới mỗi phút.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chat AI với Email:** Kết nối các vector embeddings vừa tạo với một LangChain Agent để hỏi đáp trực tiếp với hòm thư của bạn (Ví dụ: *"Tìm cho tôi tất cả các email bàn về dự án X tháng trước"*).
- **Gửi thông báo qua Telegram/Slack:** Thêm node gửi cảnh báo khi có email quan trọng được phân loại và lưu trữ thành công.
- **Lên lịch định kỳ dọn dẹp log:** Sử dụng Cron node để tối ưu hóa database định kỳ.

### 📌 Kết luận
Workflow **Gmail to Vector Embeddings with PGVector and Ollama** là một công cụ cực kỳ mạnh mẽ giúp các sếp cá nhân hóa dữ liệu email, đưa vào hệ sinh thái AI nội bộ một cách an toàn và tự động. Hãy triển khai ngay lên VPS của mình để làm chủ toàn bộ kho tri thức từ hòm thư!