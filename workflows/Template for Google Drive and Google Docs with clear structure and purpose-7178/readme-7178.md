---
title: "🚀 Tự động hóa chèn ảnh từ Google Drive vào Google Docs với n8n - Giải pháp hoàn hảo cho quản lý tài liệu"
description: "Hướng dẫn chi tiết cách tự động tải ảnh từ Google Drive, xử lý và chèn vào Google Docs bằng n8n. Tiết kiệm thời gian và nâng cao hiệu quả làm việc."
slug: "tu-dong-hoa-chen-anh-google-drive-vao-google-docs"
tags: [n8n, automation, no-code, google-drive, google-docs]
keywords: [n8n workflow, tự động hóa tài liệu, xử lý ảnh, google drive, google docs]
---

# 🚀 Tự động hóa chèn ảnh từ Google Drive vào Google Docs với n8n - Giải pháp hoàn hảo cho quản lý tài liệu

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tải và chèn nhiều ảnh từ Google Drive vào Google Docs một cách thủ công. Quá trình này tốn thời gian, dễ gây lỗi và không hiệu quả khi phải làm với lượng lớn ảnh. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi tự động hóa quá trình tải và chèn ảnh.
- Đảm bảo tính chính xác và nhất quán trong việc xử lý ảnh.
- Tự động hóa quy trình làm việc, giảm thiểu lỗi con người.
- Hiệu quả cao hơn khi xử lý lượng lớn ảnh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive chứa ảnh cần xử lý.
- Tài khoản Google Docs để chèn ảnh.
- Quyền truy cập vào Google Drive và Google Docs API.
- ID thư mục Google Drive chứa ảnh.
- ID tài liệu Google Docs mục tiêu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào n8n Editor. Để import, các sếp làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" hoặc "Import from JSON".
3. Dán URL hoặc nội dung JSON của workflow vào ô tương ứng.
4. Nhấn "Import" để hoàn tất.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **When clicking ‘Execute workflow’ (manualTrigger)**: Node này kích hoạt workflow khi người dùng nhấn nút "Execute workflow". Các sếp không cần cấu hình gì thêm.

- **Loop Over Items (splitInBatches)**: Node này chia dữ liệu thành các batch để xử lý. Các sếp có thể điều chỉnh kích thước batch nếu cần thiết.

- **Download File (googleDrive)**: Node này tải ảnh từ Google Drive. Các sếp cần cấu hình:
  - Chọn credentials "googleDriveOAuth2Api".
  - Đảm bảo tài khoản Google Drive có quyền truy cập vào thư mục chứa ảnh.

- **Filtering URI (code)**: Node này xử lý URI của ảnh. Các sếp không cần cấu hình gì thêm.

- **Search File in Google Drive (googleDrive)**: Node này tìm kiếm ảnh trong Google Drive. Các sếp cần cấu hình:
  - Chọn credentials "googleDriveOAuth2Api".
  - Thay thế `{{YOUR_FOLDER_ID}}` bằng ID thư mục Google Drive chứa ảnh.

- **Resize Image (code)**: Node này thay đổi kích thước ảnh. Các sếp không cần cấu hình gì thêm.

- **Insert Image to Google Doc (httpRequest)**: Node này chèn ảnh vào Google Docs. Các sếp cần cấu hình:
  - Chọn credentials "googleDocsOAuth2Api".
  - Thay thế `{{YOUR_DOCUMENT_ID}}` bằng ID tài liệu Google Docs mục tiêu.

- **Batch Wait Timer-1, Batch Wait Timer-2, Batch Wait Timer-3 (wait)**: Các node này tạo độ trễ giữa các batch để tránh bị timeout. Các sếp có thể điều chỉnh thời gian chờ nếu cần thiết.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp workflow này với Slack hoặc Telegram để nhận thông báo khi quá trình hoàn thành.
- Lưu log các hoạt động để theo dõi và kiểm tra lại sau này.
- Gửi báo cáo định kỳ về tiến độ xử lý ảnh.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình tải và chèn ảnh từ Google Drive vào Google Docs một cách hiệu quả và chính xác. Các sếp chỉ cần cấu hình một lần và sau đó có thể chạy workflow bất kỳ lúc nào. Hãy áp dụng ngay để nâng cao hiệu quả làm việc!