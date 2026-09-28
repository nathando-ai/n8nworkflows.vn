---
title: "🚀 Tự động hóa Vectorize Dữ liệu Y tế với n8n, Gemini & pgVector"
description: "Hướng dẫn tự động hóa vectorize dữ liệu thủ tục y tế từ Oracle sang PostgreSQL với pgVector, Gemini Embeddings và LangChain trong n8n"
slug: "tu-dong-hoa-vectorize-du-lieu-y-te-voi-n8n-gemini-pgvector"
tags: [n8n, automation, no-code, ai, semantic-search, pgvector, langchain]
keywords: [n8n workflow, tự động hóa y tế, vectorize dữ liệu, semantic search, pgvector, langchain]
---

# 🚀 Tự động hóa Vectorize Dữ liệu Y tế với n8n, Gemini & pgVector

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình vectorize dữ liệu y tế từ Oracle sang PostgreSQL
- Tạo ra vector embeddings chất lượng cao sử dụng Google Gemini
- Tích hợp LangChain để xử lý và chia nhỏ dữ liệu văn bản
- Tìm kiếm ngữ nghĩa chính xác cho các thủ tục y tế
- Hệ thống hoạt động liên tục 24/7 với dữ liệu luôn được cập nhật
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- PostgreSQL với extension pgvector đã cài đặt
- Oracle Database chứa bảng dữ liệu y tế (bảng TUSS với các cột CD_ITEM và DS_ITEM)
- Tài khoản n8n đã cài đặt các node: LangChain, Oracle Database Parameterization
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/6543)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from JSON" và dán nội dung đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "ORACLE DATABASE CONNECTION"**:
   - Thiết lập credentials Oracle với thông tin kết nối đến database của bạn
   - Chỉnh sửa query để lấy dữ liệu từ bảng TUSS (bảng chứa dữ liệu thủ tục y tế)

2. **Node "Postgres PGVector Store2"**:
   - Thiết lập credentials PostgreSQL với thông tin kết nối đến database của bạn
   - Đảm bảo database đã cài đặt extension pgvector
   - Tạo collection (bảng) để lưu trữ vector embeddings

3. **Node "Embeddings Google Gemini"**:
   - Thiết lập credentials Google Palm API với API key của bạn
   - Có thể điều chỉnh các tham số như model, temperature, topP nếu cần

4. **Node "Token Splitter"**:
   - Điều chỉnh các tham số như chunk size, overlap nếu cần
   - Chunk size mặc định là 500 tokens, có thể tăng giảm tùy theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" trên node "VECTORIZE TUSS TABLE" để chạy workflow lần đầu
2. Sau khi chạy thành công, có thể kích hoạt workflow bằng cách nhấn nút "Activate" để chạy tự động
3. Để kiểm tra kết quả, có thể thêm node "Postgres" sau node "Postgres PGVector Store2" để query dữ liệu vector đã lưu

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với ứng dụng tìm kiếm**:
   - Kết nối workflow với ứng dụng tìm kiếm của bạn để cung cấp kết quả tìm kiếm ngữ nghĩa
   - Sử dụng node "HTTP Request" để gửi kết quả tìm kiếm đến API của ứng dụng

2. **Cập nhật dữ liệu định kỳ**:
   - Thiết lập lịch chạy workflow hàng ngày để cập nhật dữ liệu mới từ Oracle
   - Sử dụng node "Schedule Trigger" để kích hoạt workflow theo lịch

3. **Mở rộng dữ liệu đầu vào**:
   - Thêm các nguồn dữ liệu khác như file CSV, JSON hoặc API để tăng cường dữ liệu huấn luyện
   - Sử dụng node "File" hoặc "HTTP Request" để lấy dữ liệu từ các nguồn khác

4. **Tối ưu hóa hiệu suất**:
   - Điều chỉnh các tham số của node "Token Splitter" để tối ưu hóa kích thước chunk
   - Sử dụng node "Delay" giữa các bước xử lý để tránh quá tải hệ thống

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để tự động hóa quá trình vectorize dữ liệu y tế từ Oracle sang PostgreSQL với pgVector và Google Gemini. Với khả năng tìm kiếm ngữ nghĩa tiên tiến, workflow này giúp các tổ chức y tế cải thiện hiệu quả tìm kiếm và truy xuất thông tin. Hãy thử nghiệm và tùy chỉnh workflow theo nhu cầu cụ thể của bạn để đạt được kết quả tối ưu nhất.