---
title: "🚀 Tự động trích xuất điểm danh từ Google Drive vào Google Sheets bằng AI VLM Run & Gửi Email"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình điểm danh: quét ảnh từ Google Drive, dùng AI trích xuất danh sách, lưu vào Google Sheets và gửi thông báo qua Gmail."
slug: "tu-dong-trich-xuat-diem-danh-google-drive-sheets-vlm-run-ai"
tags: [n8n, automation, no-code, google-drive, google-sheets, ai, vlm-run]
keywords: [n8n workflow, tự động hóa điểm danh, vlm run ai, google drive trigger, google sheets api, trích xuất ảnh thành text]
---

# 🚀 Tự động trích xuất điểm danh từ Google Drive vào Google Sheets bằng AI VLM Run & Gmail

Các lớp học, buổi workshop hay các cuộc họp đứng (standup meeting) thường tốn rất nhiều thời gian để điểm danh thủ công từ bảng trắng (whiteboard), danh sách giấy ký tên hoặc ảnh chụp. Việc nhập liệu thủ công không chỉ nhàm chán mà còn dễ xảy ra sai sót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp giải quyết triệt để bài toán trên: tự động theo dõi ảnh điểm danh mới tải lên Google Drive, sử dụng Trí tuệ nhân tạo (VLM Run AI) để đọc thông tin, tự động cập nhật vào Google Sheets và gửi báo cáo qua Gmail ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần thao tác thủ công từ khâu chụp ảnh đến cập nhật dữ liệu.
- **Độ chính xác cao với AI**: Ứng dụng VLM Run AI đọc văn bản từ hình ảnh (bảng trắng, giấy ký tên) chuẩn xác từng ký tự.
- **Đồng bộ thời gian thực**: Dữ liệu được đưa thẳng vào Google Sheets và gửi thông báo qua Gmail chỉ sau vài giây khi tải ảnh lên.
- **Hoạt động 24/7**: Lắng nghe sự kiện từ Google Drive liên tục không bỏ sót một tệp tin nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã sẵn sàng hoạt động (Self-hosted hoặc n8n Cloud).
- **VLM Run API**: Tài khoản và API Key của VLM Run (hỗ trợ Execute Agent).
- **Google Drive**: Tài khoản cấp quyền OAuth2 để cấu hình Trigger và Download file.
- **Google Sheets & Gmail**: Tài khoản Google cấp quyền OAuth2 để ghi dữ liệu và gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON từ nguồn gốc) vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Monitor List Uploads (`googleDriveTrigger`)**: 
  - Chọn tài khoản Google Drive thông qua `googleDriveOAuth2Api`.
  - Chọn thư mục (folder) đích trên Google Drive chuyên dùng để chứa ảnh điểm danh. Trạng thái trigger sẽ kiểm tra sự kiện `fileCreated` mỗi phút.
- **Download List (`googleDrive`)**: 
  - Nhận file `id` truyền từ Trigger phía trước để tải tệp hình ảnh về dạng dữ liệu nhị phân (`binary`).
- **VLM Run for Extraction (`@vlm-run/n8n-nodes-vlmrun.vlmRun`)**: 
  - Cấu hình `vlmRunApi` credentials.
  - Sử dụng Agent với **Prompt** yêu cầu trả về định dạng JSON chuẩn: 
    `{ "majorDimension": "ROWS", "values": [["YYYY-MM-DD", "user_count", "name1", "name2", ...]] }`.
- **Receives the list (`webhook`)**: 
  - Cấu hình endpoint `check-attendance` (POST). 
  - **Lưu ý quan trọng**: Lấy URL Production của Webhook này và dán vào phần Callback URL trong cài đặt của VLM Run (không dùng URL localhost vì VLM Run không gọi về được).
- **Append New Attendance to Sheet (`httpRequest`)**: 
  - Kết nối với Google Sheets API sử dụng `googleSheetsOAuth2Api` để gọi phương thức `values:append` (`valueInputOption=RAW`, `insertDataOption=INSERT_ROWS`).
- **Send a message (`gmail`)**: 
  - Sử dụng `gmailOAuth2` để gửi email báo cáo với tiêu đề `Attendance List`, định dạng nội dung hiển thị ngày tháng, tổng số người tham gia và danh sách chi tiết.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và tải thử một tấm ảnh điểm danh mẫu lên thư mục Google Drive để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động chạy nền 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Kết hợp thêm node Telegram hoặc Slack để bắn tin nhắn danh sách điểm danh ngay vào group chat của team.
- **Lưu lịch sử lỗi**: Thêm node xử lý lỗi (Error Trigger) để tự động cảnh báo về email cá nhân nếu quá trình trích xuất ảnh của AI gặp sự cố.
- **Tạo bảng thống kê định kỳ**: Kết hợp Google Sheets Trigger để tổng hợp số buổi đi học/họp của từng cá nhân theo tuần hoặc theo tháng.

### 📌 Kết luận
Workflow "Extract Attendance from Google Drive Images to Sheets with VLM Run AI & Gmail Alerts" là một mảnh ghép hoàn hảo giúp số hóa quy trình quản lý nhân sự, học viên tại các doanh nghiệp và tổ chức giáo dục. Hãy áp dụng ngay để tối ưu hóa thời gian và loại bỏ hoàn toàn các thao tác nhập liệu thủ công!