---
title: "🚀 Tự động hóa xử lý hóa đơn từ Gmail lên Google Drive và Google Sheets với AI"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt hóa đơn từ Gmail, lưu trữ PDF lên Google Drive và dùng OpenAI để trích xuất dữ liệu vào Google Sheets."
slug: "tu-dong-hoa-xu-ly-hoa-don-tu-gmail-len-drive-va-google-sheets"
tags: [n8n, automation, no-code, gmail, google-drive, google-sheets, ai, openai]
keywords: [n8n workflow, tự động hóa hóa đơn, trích xuất hóa đơn AI, gpt-4o google sheets, t-rích xuất pdf hóa đơn n8n]
---

# 🚀 Tự động hóa xử lý hóa đơn từ Gmail lên Google Drive và Google Sheets với AI

Các sếp có đang mệt mỏi mỗi cuối tháng khi phải ngồi "mò kim đáy biển" trong hộp thư Gmail, tải từng file PDF hóa đơn về máy, đổi tên, sắp xếp vào thư mục rồi lại cặm cụi nhập tay từng con số vào Google Sheets để làm báo cáo tài chính? Công việc thủ công nhàm chán này không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **Gmail**, **Google Drive**, **OpenAI (GPT-4o)** và **Google Sheets**. Hệ thống sẽ tự động hóa từ A-Z: nhận email, lọc hóa đơn, lưu trữ file an toàn và dùng AI thông minh đọc hiểu, trích xuất dữ liệu chính xác vào bảng tính.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Ngay khi có email hóa đơn đến, hệ thống tự kích hoạt mà không cần can thiệp thủ công.
- **Lưu trữ khoa học:** File PDF được tự động tải về, đổi tên và phân loại gọn gàng trên Google Drive.
- **Trích xuất thông minh bằng AI:** Sử dụng GPT-4o kết hợp Structured Output Parser để bóc tách các trường dữ liệu (số hóa đơn, ngày tháng, tổng tiền, tên nhà cung cấp...) chuẩn xác vào Google Sheets mà không cần chỉnh sửa thêm.
- **Đánh dấu đã đọc:** Tự động đánh dấu email đã xử lý để tránh trùng lặp.
:::

### 🔍 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (để cấu hình Gmail, Google Drive và Google Sheets OAuth2).
- **OpenAI API Key** (có hạn mức sử dụng cho mô hình GPT-4o).
- **Một file Google Sheets** mẫu dùng làm bảng kê khai tài chính/hóa đơn (Reconciliation Sheet).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn cấp) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 14 nodes hoạt động nhịp nhàng với nhau. Các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Node `Gmail Trigger1` & `Gmail`:** 
  - Chọn credentials `gmailOAuth2` của tài khoản Gmail nhận hóa đơn.
  - Cấu hình điều kiện lọc email ở node `Only invoice mails with attachments` để chỉ bắt các email có file đính kèm là hóa đơn (PDF).
- **Nodes Google Drive (`Upload PDF to Drive1`, `Rename file1`, `Move to the correct folder1`, `Google Drive`):**
  - Kết nối chung credentials `googleDriveOAuth2Api`.
  - Chỉ định ID thư mục đích trên Google Drive nơi các sếp muốn lưu trữ file PDF hóa đơn tải về.
- **Node `OpenAI Model` & `Apply Data Extraction Rules`:**
  - Kết nối `openAiApi` credentials.
  - Model được cấu hình sẵn là `gpt-4o` để đảm bảo khả năng đọc hiểu cấu trúc tài liệu phức tạp.
- **Node `Structured Output Parser`:**
  - Định nghĩa cấu trúc JSON đầu ra (Schema) nếu các sếp muốn tùy chỉnh thêm các thuộc tính cần trích xuất (Ví dụ: Tiền thuế, mã số thuế, tên khách hàng...).
- **Node `Append to Reconciliation Sheet`:**
  - Chọn credentials `googleSheetsOAuth2Api`.
  - Trỏ đúng đến file Google Sheets và Sheet Name (Bảng kê khai) để dữ liệu AI trích xuất tự động được ghi vào dòng mới.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** với một email hóa đơn mẫu để kiểm tra xem dữ liệu có chảy mượt mà từ Gmail qua Google Drive rồi vào Google Sheets hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động túc trực 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay lập tức mỗi khi có một hóa đơn mới được xử lý và ghi nhận thành công.
- **Xử lý ngoại lệ (Error Handling):** Thêm Error Trigger để bắt các trường hợp AI không đọc được file PDF hỏng/mờ, sau đó gửi email cảnh báo về cho bộ phận kế toán.
- **Phân loại thư mục thông minh:** Dùng AI phân loại tên nhà cung cấp từ nội dung hóa đơn để tự động đẩy file PDF vào các thư mục con tương ứng trên Google Drive.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn không chỉ giúp tiết kiệm hàng chục giờ làm việc mỗi tháng mà còn loại bỏ hoàn toàn sai sót do nhập liệu thủ công. Hãy triển khai ngay workflow này để tối ưu hóa năng suất cho đội ngũ tài chính - kế toán của doanh nghiệp các sếp nhé!