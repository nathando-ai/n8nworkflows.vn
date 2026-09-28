---
title: "🚀 Tự động hóa Truy xuất & Cập nhật Dữ liệu với Supabase & OpenAI"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình truy xuất, chèn và cập nhật dữ liệu trong Supabase bằng n8n kết hợp với OpenAI Embeddings"
slug: "tu-dong-hoa-truy-xuat-cap-nhat-du-lieu-supabase-openai"
tags: [n8n, automation, no-code, supabase, openai]
keywords: [n8n workflow, tự động hóa, supabase, openai embeddings, vector database]
---

# 🚀 Tự động hóa Truy xuất & Cập nhật Dữ liệu với Supabase & OpenAI

[Các sếp đang gặp khó khăn khi phải quản lý và truy xuất dữ liệu từ cơ sở dữ liệu vector trong Supabase một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ chèn dữ liệu, cập nhật đến truy xuất thông tin một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa toàn bộ quy trình xử lý dữ liệu vector trong Supabase
- Tiết kiệm thời gian và công sức cho các tác vụ thủ công
- Tăng độ chính xác trong việc truy xuất thông tin
- Tích hợp OpenAI Embeddings để tạo ra các vector biểu diễn dữ liệu hiệu quả
- Hỗ trợ cả việc chèn mới và cập nhật dữ liệu hiện có
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Supabase đã kích hoạt extension 'pgvector'
- API Key của OpenAI
- Bảng dữ liệu trong Supabase đã được cấu hình với các cột: embedding (VECTOR), metadata (JSONB), content (TEXT)
- Hàm `match_documents` đã được tạo trong Supabase
- Tài khoản Google Drive (nếu sử dụng node Google Drive)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link: https://n8n.io/workflows/2395
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Google Drive**:
   - Cấu hình credentials cho Google Drive
   - Chỉnh sửa tham số "operation" thành "download"

2. **Node Default Data Loader**:
   - Không cần cấu hình bổ sung

3. **Node Question and Answer Chain**:
   - Kiểm tra các tham số mặc định của chain

4. **Node OpenAI Chat Model**:
   - Cấu hình credentials cho OpenAI
   - Chọn model phù hợp (ví dụ: gpt-3.5-turbo)

5. **Node Vector Store Retriever**:
   - Kiểm tra các tham số mặc định của retriever

6. **Node Recursive Character Text Splitter**:
   - Điều chỉnh tham số "chunkSize" và "chunkOverlap" nếu cần

7. **Node Customize Response**:
   - Cấu hình các trường dữ liệu cần thiết cho response

8. **Node When chat message received**:
   - Cấu hình credentials cho chat service
   - Chỉnh sửa các tham số trigger phù hợp

9. **Node Retrieve by Query**:
   - Cấu hình credentials cho Supabase
   - Chỉnh sửa tham số "queryName" thành "match_documents"
   - Đảm bảo "matchCount" được đặt phù hợp

10. **Node Embeddings OpenAI Retrieval**:
    - Cấu hình credentials cho OpenAI
    - Đảm bảo sử dụng cùng model với node Embeddings OpenAI Insertion

11. **Node Embeddings OpenAI Insertion**:
    - Cấu hình credentials cho OpenAI
    - Đảm bảo model được đặt là "text-embedding-3-small"

12. **Node Placeholder (File/Content to Upsert)**:
    - Cấu hình các trường dữ liệu cần thiết cho quá trình upsert

13. **Node Embeddings OpenAI Upserting**:
    - Cấu hình credentials cho OpenAI
    - Đảm bảo model được đặt là "text-embedding-3-small"

14. **Node Insert Documents**:
    - Cấu hình credentials cho Supabase
    - Kiểm tra các tham số mặc định

15. **Node Retrieve Rows from Table**:
    - Cấu hình credentials cho Supabase
    - Chỉnh sửa tham số "operation" thành "getAll"
    - Đảm bảo bảng và các cột được cấu hình đúng

16. **Node Update Documents**:
    - Cấu hình credentials cho Supabase
    - Kiểm tra các tham số mặc định

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Sau khi xác nhận hoạt động ổn định, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack/Telegram**: Thêm node để thông báo kết quả truy xuất qua các kênh chat
2. **Lưu log hoạt động**: Thêm node để ghi log các hoạt động quan trọng
3. **Gửi báo cáo định kỳ**: Tạo workflow phụ để tổng hợp và gửi báo cáo định kỳ
4. **Xử lý lỗi tự động**: Thêm các node xử lý lỗi và gửi thông báo khi có sự cố

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quản lý dữ liệu vector trong Supabase kết hợp với OpenAI Embeddings. Với các sếp có thể dễ dàng tích hợp vào hệ thống hiện tại và tận dụng tối đa các tính năng của n8n và Supabase để nâng cao hiệu suất làm việc.