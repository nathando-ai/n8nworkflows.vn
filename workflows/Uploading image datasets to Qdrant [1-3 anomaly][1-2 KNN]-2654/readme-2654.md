---
title: "🚀 Tự động hóa tải dữ liệu hình ảnh lên Qdrant cho phát hiện bất thường và KNN"
description: "Hướng dẫn tự động hóa tải dữ liệu hình ảnh lên Qdrant để xây dựng hệ thống phát hiện bất thường và phân loại KNN bằng n8n. Tiết kiệm thời gian và nâng cao hiệu suất xử lý dữ liệu hình ảnh."
slug: "tu-dong-hoa-tai-du-lieu-hinh-anh-len-qdrant"
tags: [n8n, automation, no-code, qdrant, vector-database]
keywords: [n8n workflow, tự động hóa, qdrant, vector database, phát hiện bất thường, knn]
---

# 🚀 Tự động hóa tải dữ liệu hình ảnh lên Qdrant cho phát hiện bất thường và KNN

[Các sếp đang gặp khó khăn khi phải tải thủ công hàng nghìn hình ảnh lên Qdrant để xây dựng hệ thống phát hiện bất thường và phân loại KNN. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình tải dữ liệu lên Qdrant, giảm thời gian xử lý từ vài giờ xuống còn vài phút.
- **Chính xác cao**: Đảm bảo dữ liệu được tải lên đúng định dạng và cấu trúc yêu cầu của Qdrant.
- **Tích hợp liền mạch**: Kết nối tự động với Google Cloud Storage, Voyage AI và Qdrant Cloud.
- **Hiệu suất cao**: Xử lý dữ liệu theo batch, tối ưu hóa tài nguyên và tốc độ tải lên.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud Storage với dữ liệu hình ảnh đã tải lên.
- API Key của Qdrant Cloud.
- API Key của Voyage AI.
- Dữ liệu hình ảnh đã được tổ chức theo cấu trúc thư mục (ví dụ: cucumber, tomato).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/2654).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Google Cloud Storage"**:
   - Chọn credentials "googleCloudStorageOAuth2Api".
   - Điền thông tin bucket chứa dữ liệu hình ảnh.

2. **Node "Embed crop image"**:
   - Chọn credentials "httpHeaderAuth".
   - Điền API Key của Voyage AI vào header.

3. **Node "Create Qdrant Collection" và "Check Qdrant Collection Existence"**:
   - Chọn credentials "qdrantApi".
   - Điền URL của Qdrant Cloud vào biến "Cloud URL".
   - Điền tên collection vào biến "Collection name".

4. **Node "Qdrant cluster variables"**:
   - Điền các thông số cần thiết:
     - "Cloud URL": URL của Qdrant Cloud.
     - "Collection name": Tên collection trong Qdrant.
     - "Size of Voyage embeddings": Kích thước embeddings của Voyage (mặc định là 1024).
     - "Batch size": Kích thước batch cho việc tải lên (ví dụ: 100).

5. **Node "Batches in the API's format"**:
   - Đảm bảo cấu trúc dữ liệu phù hợp với định dạng yêu cầu của Qdrant và Voyage API.

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, click vào nút "Active workflow" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi quá trình tải dữ liệu hoàn thành.
- **Lưu log**: Thêm node lưu log quá trình tải dữ liệu để theo dõi và debug.
- **Gửi báo cáo định kỳ**: Thêm node gửi báo cáo tổng hợp sau mỗi lần tải dữ liệu.
- **Tối ưu hóa tài nguyên**: Điều chỉnh kích thước batch và số lượng request đồng thời để tối ưu hóa hiệu suất.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tải dữ liệu hình ảnh lên Qdrant, xây dựng hệ thống phát hiện bất thường và phân loại KNN một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất xử lý dữ liệu hình ảnh!