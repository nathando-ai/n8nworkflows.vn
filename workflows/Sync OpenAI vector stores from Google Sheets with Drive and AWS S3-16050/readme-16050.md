---
title: "🚀 Tự động đồng bộ dữ liệu từ Google Sheets lên OpenAI Vector Store với Drive và AWS S3"
description: "Hướng dẫn chi tiết cách tự động đồng bộ dữ liệu từ Google Sheets lên OpenAI Vector Store thông qua Google Drive và AWS S3, tiết kiệm thời gian và tăng hiệu suất xử lý dữ liệu."
slug: "tu-dong-dong-bo-du-lieu-google-sheets-openai-vector-store"
tags: [n8n, automation, no-code, ai, vector-store]
keywords: [n8n workflow, tự động hóa, openai vector store, google sheets, aws s3]
---

# 🚀 Tự động đồng bộ dữ liệu từ Google Sheets lên OpenAI Vector Store với Drive và AWS S3

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình trạng phải thủ công đồng bộ dữ liệu từ Google Sheets lên OpenAI Vector Store, đặc biệt là khi dữ liệu được lưu trữ trên nhiều nguồn khác nhau như Google Drive, AWS S3, hoặc các URL tùy chỉnh. Quá trình này không chỉ tốn thời gian mà còn dễ gây lỗi và không nhất quán. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách dễ dàng và hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình đồng bộ dữ liệu, giảm thiểu thời gian thủ công.
- Chính xác: Đảm bảo dữ liệu được đồng bộ chính xác và nhất quán.
- Cá nhân hóa: Có thể tùy chỉnh các điều kiện và quy trình đồng bộ theo nhu cầu cụ thể.
- Hoạt động liên tục: Workflow chạy tự động mỗi 2 phút, đảm bảo dữ liệu luôn được cập nhật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với quyền truy cập vào bảng dữ liệu.
- Tài khoản OpenAI với quyền truy cập vào Vector Store.
- Tài khoản AWS S3 (nếu sử dụng).
- Tài khoản Google Drive (nếu sử dụng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Every 2 Minutes**: Node này sẽ kích hoạt workflow mỗi 2 phút.
- **Get Row(s) From Sheet**: Node này sẽ lấy dữ liệu từ Google Sheets. Các sếp cần thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của bảng dữ liệu.
- **If Outdated**: Node này kiểm tra xem dữ liệu có trạng thái `outdated` không. Nếu có, nó sẽ xóa dữ liệu cũ khỏi Vector Store.
- **Delete File From Vector Store**: Node này sẽ xóa dữ liệu cũ khỏi Vector Store. Các sếp cần thay thế `YOUR_VECTOR_STORE_ID` bằng ID của Vector Store.
- **Mark Row as Deleted**: Node này sẽ đánh dấu dữ liệu đã bị xóa trong Google Sheets. Các sếp cần thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của bảng dữ liệu.
- **Filter New Files**: Node này sẽ lọc các dữ liệu mới chưa được xử lý.
- **Route by File Source**: Node này sẽ định tuyến dữ liệu đến các node xử lý tương ứng dựa trên nguồn dữ liệu (Google Drive, AWS S3, hoặc URL tùy chỉnh).
- **Download from Google Drive**: Node này sẽ tải dữ liệu từ Google Drive. Các sếp cần thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của bảng dữ liệu.
- **Upload File to OpenAI**: Node này sẽ tải dữ liệu lên OpenAI. Các sếp cần thay thế `YOUR_VECTOR_STORE_ID` bằng ID của Vector Store.
- **Download from S3**: Node này sẽ tải dữ liệu từ AWS S3. Các sếp cần thay thế `YOUR_S3_BUCKET_NAME` bằng tên bucket của AWS S3.
- **Download via HTTP**: Node này sẽ tải dữ liệu từ URL tùy chỉnh. Các sếp cần thay thế `YOUR_ARTICLES_DOMAIN` bằng tên miền của dữ liệu.
- **Loop Over Items**: Node này sẽ lặp qua các dữ liệu một cách tuần tự.
- **Add File to Vector Store**: Node này sẽ thêm dữ liệu vào Vector Store. Các sếp cần thay thế `YOUR_VECTOR_STORE_ID` bằng ID của Vector Store.
- **Wait 30 Seconds**: Node này sẽ chờ 30 giây trước khi tiếp tục xử lý.
- **Poll Vector Store File Status**: Node này sẽ kiểm tra trạng thái của dữ liệu trong Vector Store. Các sếp cần thay thế `YOUR_VECTOR_STORE_ID` bằng ID của Vector Store.
- **Route by Embedding Status**: Node này sẽ định tuyến dữ liệu đến các node xử lý tương ứng dựa trên trạng thái của dữ liệu (completed, in_progress, hoặc error).
- **Mark Row as Active**: Node này sẽ đánh dấu dữ liệu đã được xử lý thành công trong Google Sheets. Các sếp cần thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của bảng dữ liệu.
- **Mark Row as Error**: Node này sẽ đánh dấu dữ liệu đã bị lỗi trong Google Sheets. Các sếp cần thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID của bảng dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi.
- Lưu log các hoạt động của workflow để theo dõi và kiểm tra.
- Gửi báo cáo định kỳ về trạng thái của dữ liệu trong Vector Store.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình đồng bộ dữ liệu từ Google Sheets lên OpenAI Vector Store một cách dễ dàng và hiệu quả. Với các bước cấu hình đơn giản và các lưu ý chi tiết, các sếp có thể áp dụng ngay workflow này vào thực tế.