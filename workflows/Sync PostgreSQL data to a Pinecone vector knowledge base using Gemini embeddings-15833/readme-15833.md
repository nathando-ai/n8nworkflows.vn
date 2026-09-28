---
title: "🚀 Tự động đồng bộ dữ liệu PostgreSQL sang cơ sở kiến thức vector Pinecone với embeddings Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa việc chuyển đổi dữ liệu từ PostgreSQL sang Pinecone để xây dựng hệ thống tìm kiếm ngữ nghĩa và RAG (Retrieval-Augmented Generation) hoàn toàn không cần code."
slug: "tu-dong-dong-bo-du-lieu-postgresql-sang-pinecone-voi-gemini"
tags: [n8n, automation, no-code, PostgreSQL, Pinecone, AI, RAG, vector database]
keywords: [n8n workflow, tự động hóa dữ liệu, PostgreSQL, Pinecone, Gemini embeddings, RAG, tìm kiếm ngữ nghĩa]
---

# 🚀 Tự động đồng bộ dữ liệu PostgreSQL sang cơ sở kiến thức vector Pinecone với embeddings Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải quản lý và tìm kiếm dữ liệu từ nhiều nguồn khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để chuyển đổi dữ liệu từ PostgreSQL sang Pinecone.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình chuyển đổi dữ liệu từ PostgreSQL sang Pinecone
- Tiết kiệm thời gian và công sức cho việc quản lý dữ liệu
- Xây dựng hệ thống tìm kiếm ngữ nghĩa và RAG (Retrieval-Augmented Generation) mạnh mẽ
- Dữ liệu được đồng bộ tự động và liên tục
- Giữ nguyên ngữ cảnh và cấu trúc dữ liệu ban đầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản PostgreSQL với quyền truy cập đầy đủ
- API key của Gemini và Pinecone
- Kiến thức cơ bản về cấu trúc dữ liệu trong PostgreSQL
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn "From JSON" và dán nội dung JSON của workflow
4. Hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Workflow Configuration** (Node "set"):
   - Thiết lập các tham số cấu hình chính:
     - `allowedSchemas`: Danh sách các schema cho phép (ví dụ: `["public"]`)
     - `tableFilters`: Biểu thức regex để lọc bảng (ví dụ: `.*` để chọn tất cả bảng)
     - `pineconeIndexHost`: URL của Pinecone index (ví dụ: `https://your-index-host.svc.us-west1-gcp.pinecone.io`)
     - `maxRowsPerTable`: Số lượng hàng tối đa mỗi bảng (ví dụ: `1000`)
     - `maxDocumentsPerRun`: Số lượng tài liệu tối đa mỗi lần chạy (ví dụ: `100`)
     - `geminiSmokeTestMode`: Chế độ kiểm tra (true/false)
     - `namespacePrefix`: Tiền tố cho namespace Pinecone (ví dụ: `pg_`)

2. **Discover PostgreSQL Metadata** (Node "postgres"):
   - Cấu hình credentials PostgreSQL
   - Đảm bảo credentials có quyền truy cập đầy đủ vào các schema và bảng cần đồng bộ

3. **Generate Gemini Embeddings** (Node "httpRequest"):
   - Cấu hình credentials cho API Gemini
   - Đảm bảo API key có quyền truy cập vào dịch vụ embeddings

4. **Upsert Vectors to Pinecone** (Node "httpRequest"):
   - Cấu hình credentials cho API Pinecone
   - Đảm bảo API key có quyền ghi vào index đã chỉ định

#### 3. Kích hoạt ⚡️
1. Thiết lập các tham số kiểm tra ban đầu:
   - `geminiSmokeTestMode = true`
   - `maxRowsPerTable = 1`
   - `maxDocumentsPerRun = 1`
2. Chạy workflow thủ công để kiểm tra hoạt động
3. Sau khi kiểm tra thành công, tắt chế độ kiểm tra và tăng các tham số giới hạn
4. Bật chế độ tự động hóa bằng cách kích hoạt node "Cron Trigger" nếu cần

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Slack" hoặc "Telegram" để nhận thông báo khi workflow hoàn thành
- Lưu log chi tiết của quá trình đồng bộ vào Google Sheets hoặc cơ sở dữ liệu
- Thiết lập báo cáo định kỳ về số lượng tài liệu đã đồng bộ và thời gian chạy
- Tích hợp với hệ thống giám sát để theo dõi hiệu suất workflow
- Sử dụng biến môi trường để quản lý các thông tin nhạy cảm như API keys

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa việc chuyển đổi dữ liệu từ PostgreSQL sang Pinecone, giúp xây dựng hệ thống tìm kiếm ngữ nghĩa và RAG mạnh mẽ. Bằng cách tuân theo các bước cấu hình và kiểm tra được đề xuất, các sếp có thể triển khai hệ thống này một cách hiệu quả và đáng tin cậy.