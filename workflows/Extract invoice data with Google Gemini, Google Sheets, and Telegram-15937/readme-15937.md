---
title: "🚀 Tự động hóa trích xuất hóa đơn (Invoice OCR) với Google Gemini, Google Sheets và Telegram"
description: "Hướng dẫn xây dựng workflow n8n xử lý hóa đơn PDF/ảnh tự động bằng AI Gemini, lưu kết quả vào Google Sheets và thông báo qua Telegram."
slug: "tu-dong-hoa-trich-xuat-hoa-don-gemini-sheets-telegram"
tags: [n8n, automation, google-gemini, google-sheets, telegram, invoice-ocr]
keywords: [n8n workflow, trích xuất hóa đơn tự động, google gemini ocr, google sheets invoice, telegram automation]
---

# 🚀 Tự động hóa trích xuất hóa đơn thông minh với Google Gemini, Google Sheets & Telegram

Các sếp có đang mệt mỏi với việc nhập liệu hóa đơn thủ công mỗi tháng? Việc đọc từng tờ hóa đơn PDF, copy số tiền, tên nhà cung cấp, mã số thuế rồi gõ vào Google Sheets không chỉ tốn hàng giờ đồng hồ mà còn dễ xảy ra sai sót. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow **n8n** cực kỳ mạnh mẽ do tác giả Hồ Đình Huy phát triển. Workflow này sẽ tự động hóa 100% quy trình: nhận hóa đơn từ Form hoặc Telegram $\rightarrow$ dùng AI **Google Gemini** để đọc và trích xuất dữ liệu chuẩn xác $\rightarrow$ kiểm tra tính hợp lệ $\rightarrow$ lưu vào **Google Sheets** $\rightarrow$ gửi thông báo kết quả qua **Telegram**. Không cần viết code phức tạp, các sếp chỉ cần "lắp ráp" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hóa đơn tức thì thay vì nhập liệu thủ công từng cái.
- **Trích xuất thông minh bằng AI:** Google Gemini đọc hiểu linh hoạt các định dạng hóa đơn PDF, PNG, JPG, WEBP...
- **Quản lý tập trung:** Tự động đồng bộ dữ liệu chuẩn chỉnh vào Google Sheets để làm báo cáo kế toán.
- **Tương tác đa kênh & Thời gian thực:** Nhận hóa đơn qua Web Form hoặc trực tiếp qua Telegram Bot, có ngay thông báo xác nhận thành công hay từ chối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Tài khoản Google AI Studio / Gemini API.
- **Google Account:** Truy cập Google Sheets để lưu trữ dữ liệu.
- **Telegram Bot:** Tạo một Bot thông qua `@BotFather` để nhận/gửi tin nhắn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc tải file về, sau đó chọn **Import from File / Clipboard** trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các credential và tham số tại các node sau:

- **Google Gemini Nodes (`Upload a media file`, `Analyze document`, `Analyze an image`):** 
  - Thêm credential Google Palm/Gemini API Key của các sếp vào các node này.
- **Google Sheets Node (`Append Invoice to Google Sheets`):** 
  - Chọn credential Google Sheets OAuth2 API.
  - Trỏ đến Spreadsheet và Worksheet của các sếp (Khuyến nghị đặt tên sheet là `Invoices`).
  - Đảm bảo các cột trong Google Sheets khớp với cấu trúc sau:
    `processed_at`, `source_filename`, `vendor_name`, `vendor_tax_id`, `invoice_number`, `invoice_date`, `due_date`, `currency`, `subtotal`, `tax_amount`, `total_amount`, `payment_terms`, `line_items_json`, `confidence`, `validation_status`, `validation_errors`, `raw_response_id`
- **Telegram Nodes (`Telegram Trigger`, `Send Telegram Notification1`, `Send Telegram Rejection1`):** 
  - Thêm credential Telegram Bot API (Token lấy từ BotFather).
  - Cấu hình Chat ID nhận thông báo.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test run** bằng cách upload thử một file PDF/ảnh hóa đơn qua Form hoặc Telegram.
- Kiểm tra xem Google Sheets đã nhận được dòng dữ liệu mới chưa và Telegram có báo tin nhắn về không.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ lưu Google Sheets, các sếp có thể kết hợp thêm node gửi email tự động cho phòng kế toán hoặc lưu trữ file gốc vào Google Drive / Dropbox.
- **Tích hợp Chatbot nâng cao:** Kết hợp thêm các node AI Agent để các sếp có thể chat trực tiếp với Telegram Bot hỏi về tổng chi phí hóa đơn trong tháng.
- **Xử lý lỗi thông minh:** Tận dụng node `Build Invalid File Result` để tùy chỉnh thông báo từ chối chi tiết hơn khi khách hàng hoặc nhân viên gửi nhầm định dạng file.

### 📌 Kết luận
Workflow tự động hóa xử lý hóa đơn với Gemini, Google Sheets và Telegram này là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình tài chính - kế toán cho các doanh nghiệp vừa và nhỏ, creator hoặc các team vận hành. Hãy triển khai ngay hôm nay để giải phóng sức lao động khỏi những con số thủ công!