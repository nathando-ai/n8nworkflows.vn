---
title: "🤖 Chatbot AI Hỗ Trợ Tài Liệu với Google Drive + Gemini + Qdrant"
description: "Hướng dẫn tự động hóa hoàn toàn việc tạo chatbot AI có thể truy xuất và tương tác với tài liệu từ Google Drive bằng công nghệ RAG (Retrieval-Augmented Generation)"
slug: "chatbot-ai-ho-tro-tai-lieu-google-drive-gemini-qdrant"
tags: [n8n, automation, no-code, AI, RAG, Google Drive, Qdrant, Gemini]
keywords: [n8n workflow, tự động hóa, chatbot AI, RAG, Google Drive, Qdrant, Gemini]
---

# 🤖 Chatbot AI Hỗ Trợ Tài Liệu với Google Drive + Gemini + Qdrant

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý và tương tác với lượng tài liệu lớn. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình xử lý và tương tác với tài liệu
- Tạo chatbot AI có thể truy xuất thông tin từ Google Drive
- Tích hợp công nghệ RAG để cung cấp câu trả lời chính xác và liên quan
- Lưu trữ và quản lý tài liệu một cách hiệu quả
- Giao diện chat thân thiện và dễ sử dụng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào thư mục chứa tài liệu
- Tài khoản Google Docs để lưu trữ lịch sử chat
- API Key cho Google Gemini
- Tài khoản Qdrant để lưu trữ vector
- Tài khoản Telegram (tùy chọn) để nhận thông báo
- Tài khoản OpenAI (tùy chọn) để sử dụng mô hình OpenAI
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang workflow gốc: [https://n8n.io/workflows/2982](https://n8n.io/workflows/2982)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Drive Folder ID**:
   - Tìm node "Google Folder ID" trong workflow
   - Thay đổi giá trị của biến "googleDriveFolderId" thành ID của thư mục Google Drive chứa tài liệu của bạn

2. **Qdrant Collection Name**:
   - Tìm node "Qdrant Collection Name" trong workflow
   - Thay đổi giá trị của biến "qdrantCollectionName" thành tên collection bạn muốn sử dụng trong Qdrant

3. **Google Drive API Credentials**:
   - Tạo một Google OAuth 2.0 credential trong n8n
   - Đảm bảo credential có quyền truy cập vào Google Drive và Google Docs
   - Áp dụng credential này cho các node Google Drive và Google Docs trong workflow

4. **Google Gemini API Credentials**:
   - Tạo một Google Palm API credential trong n8n
   - Nhập API Key của bạn vào credential
   - Áp dụng credential này cho các node Google Gemini trong workflow

5. **Qdrant API Credentials**:
   - Tạo một Qdrant API credential trong n8n
   - Nhập thông tin kết nối Qdrant của bạn (URL và API Key)
   - Áp dụng credential này cho các node Qdrant trong workflow

6. **Telegram API Credentials (tùy chọn)**:
   - Tạo một Telegram API credential trong n8n
   - Nhập thông tin bot của bạn (Bot Token và Chat ID)
   - Áp dụng credential này cho các node Telegram trong workflow

7. **OpenAI API Credentials (tùy chọn)**:
   - Tạo một OpenAI API credential trong n8n
   - Nhập API Key của bạn
   - Áp dụng credential này cho các node OpenAI trong workflow

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test workflow" để kiểm tra quá trình xử lý tài liệu
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow
3. Bây giờ bạn có thể bắt đầu tương tác với chatbot của mình

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack**: Thay thế các node Telegram bằng các node Slack để nhận thông báo trên Slack
2. **Lưu log hoạt động**: Thêm các node để lưu log hoạt động của chatbot vào Google Sheets hoặc cơ sở dữ liệu
3. **Tự động hóa cập nhật**: Thiết lập workflow chạy định kỳ để tự động cập nhật tài liệu mới từ Google Drive
4. **Tích hợp với các nền tảng khác**: Kết nối với các nền tảng khác như Notion, Airtable để mở rộng khả năng lưu trữ và quản lý tài liệu

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tạo chatbot AI có thể truy xuất và tương tác với tài liệu từ Google Drive. Với công nghệ RAG và tích hợp với Google Gemini, chatbot sẽ cung cấp câu trả lời chính xác và liên quan dựa trên nội dung của tài liệu. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tối ưu hóa quy trình làm việc của doanh nghiệp!