---
title: "🚀 Tự động đồng bộ Google Drive với Vector Store OpenAI cho Assistants"
description: "Hướng dẫn chi tiết cách tự động đồng bộ các file từ Google Drive lên Vector Store của OpenAI để sử dụng trong Assistants, tiết kiệm thời gian và tối ưu hóa quy trình làm việc."
slug: "tu-dong-dong-bo-google-drive-voi-vector-store-openai"
tags: [n8n, automation, no-code, google-drive, openai, ai]
keywords: [n8n workflow, tự động hóa, google drive, openai, vector store]
---

# 🚀 Tự động đồng bộ Google Drive với Vector Store OpenAI cho Assistants

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ các file từ Google Drive lên Vector Store của OpenAI, giúp Assistants có thể truy cập và xử lý thông tin một cách nhanh chóng và chính xác.
- Tiết kiệm thời gian và công sức cho các sếp trong việc quản lý và cập nhật thông tin.
- Tăng cường khả năng truy xuất thông tin và tối ưu hóa quy trình làm việc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với quyền truy cập vào các file cần đồng bộ.
- Tài khoản OpenAI với quyền truy cập vào Vector Store.
- API Key của Google Drive và OpenAI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Set variables**: Cấu hình các biến môi trường cần thiết cho workflow.
- **Loop over files**: Cấu hình số lượng file cần xử lý trong mỗi lần chạy.
- **Upload new or updated file**: Cấu hình thông tin cần thiết để tải lên file mới hoặc cập nhật file đã có.
- **Search for existing file in vector store [OpenAI]**: Cấu hình thông tin cần thiết để tìm kiếm file trong Vector Store của OpenAI.
- **Add uploaded file to vector store [OpenAI]**: Cấu hình thông tin cần thiết để thêm file đã tải lên vào Vector Store của OpenAI.
- **"Test workflow" clicked**: Cấu hình thông tin cần thiết để kiểm tra workflow.
- **Schedule trigger**: Cấu hình lịch trình chạy workflow.
- **Download new or updated file**: Cấu hình thông tin cần thiết để tải xuống file mới hoặc cập nhật file đã có.
- **Aggregate vector store files**: Cấu hình thông tin cần thiết để tổng hợp các file trong Vector Store.
- **List vector store files [OpenAI]**: Cấu hình thông tin cần thiết để liệt kê các file trong Vector Store của OpenAI.
- **Split vector store files**: Cấu hình thông tin cần thiết để chia nhỏ các file trong Vector Store.
- **Set vector store file**: Cấu hình thông tin cần thiết để đặt file trong Vector Store.
- **List files from folder**: Cấu hình thông tin cần thiết để liệt kê các file từ thư mục.
- **Set Google Drive file**: Cấu hình thông tin cần thiết để đặt file trong Google Drive.
- **Set Google Drive file to create in vector store**: Cấu hình thông tin cần thiết để đặt file trong Google Drive để tạo trong Vector Store.
- **Set Google Drive file to update in vector store**: Cấu hình thông tin cần thiết để đặt file trong Google Drive để cập nhật trong Vector Store.
- **Set Google Drive file to delete from vector store**: Cấu hình thông tin cần thiết để đặt file trong Google Drive để xóa khỏi Vector Store.
- **Set Google Drive file to ignore**: Cấu hình thông tin cần thiết để đặt file trong Google Drive để bỏ qua.
- **Merge Google Drive files**: Cấu hình thông tin cần thiết để hợp nhất các file trong Google Drive.
- **Compare Google Drive files with vector store files**: Cấu hình thông tin cần thiết để so sánh các file trong Google Drive với các file trong Vector Store.
- **Filter out files to ignore**: Cấu hình thông tin cần thiết để lọc bỏ các file cần bỏ qua.
- **Does file need to be created in vector store?**: Cấu hình thông tin cần thiết để kiểm tra xem file có cần được tạo trong Vector Store không.
- **Delete outdated file or previous version**: Cấu hình thông tin cần thiết để xóa file đã cũ hoặc phiên bản trước đó.
- **Does file need to be updated or deleted from vector store?**: Cấu hình thông tin cần thiết để kiểm tra xem file có cần được cập nhật hoặc xóa khỏi Vector Store không.
- **Has file been created or updated?**: Cấu hình thông tin cần thiết để kiểm tra xem file đã được tạo hoặc cập nhật chưa.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có sự kiện quan trọng xảy ra.
- Lưu log các hoạt động để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về trạng thái của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động đồng bộ các file từ Google Drive lên Vector Store của OpenAI, giúp Assistants có thể truy cập và xử lý thông tin một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và tối ưu hóa quy trình làm việc.