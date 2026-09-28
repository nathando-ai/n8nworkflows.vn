---
title: "🚀 Tự động hóa xử lý hóa đơn với Google Vision OCR, Gemini LLM & Google Sheets trên n8n"
description: "Xây dựng hệ thống tự động trích xuất thông tin hóa đơn từ hình ảnh, phân tích bằng AI Gemini qua OpenRouter, lưu vào Google Sheets và thông báo qua Telegram."
slug: "tu-dong-hoa-xu-ly-hoa-don-google-vision-gemini-n8n"
tags: [n8n, automation, no-code, ai, google-sheets, telegram]
keywords: [n8n workflow, xử lý hóa đơn tự động, google vision ocr, gemini llm, google sheets automation]
keywords: [n8n workflow, xử lý hóa đơn tự động, google vision ocr, gemini llm, google sheets automation]
---

# 🚀 Tự động hóa xử lý hóa đơn với Google Vision OCR, Gemini LLM & Google Sheets trên n8n

Việc nhập liệu hóa đơn thủ công (ngày tháng, mã chứng từ, nhà cung cấp, tổng tiền...) luôn là nỗi ám ảnh tốn rất nhiều thời gian của bộ phận kế toán và hành chính. Sai sót là điều khó tránh khỏi khi khối lượng chứng từ lớn. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách tự động hóa 100 quy trình: từ việc nhận form upload hóa đơn, đọc chữ bằng **Google Vision OCR**, phân tích dữ liệu thông minh qua **Gemini LLM**, đồng bộ hóa vào **Google Sheets** và bắn thông báo tức thì qua **Telegram**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Triệt tiêu hoàn toàn công đoạn gõ tay dữ liệu hóa đơn vào Excel/Google Sheets.
- **Độ chính xác cao**: Kết hợp sức mạnh OCR của Google Vision và khả năng hiểu ngữ cảnh siêu việt của Gemini LLM.
- **Chống trùng lặp**: Tự động nhận diện và cập nhật dựa trên File ID làm khóa chính (matching key).
- **Giám sát thời gian thực**: Nhận báo cáo chi tiết ngay lập tức qua Telegram mỗi khi có hóa đơn mới được xử lý thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Google Vision API Key**: Dùng cho node HTTP Request để chạy OCR.
- **OpenRouter API Key**: Để kết nối với mô hình `google/gemini-2.0-flash-exp:free`.
- **Google Drive OAuth2**: Để upload file hóa đơn từ form và lấy link xem trước.
- **Google Sheets OAuth2**: Để ghi/cập nhật dữ liệu vào bảng tính.
- **Telegram Bot Token & Chat ID**: Để gửi tin nhắn thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes được thiết kế tỉ mỉ bởi tác giả Budi SJ. Các sếp cần cấu hình chính xác các điểm sau:
- **On form submission**: Form nhận file hóa đơn đầu vào. Các sếp có thể tuỳ chỉnh giao diện form theo ý muốn.
- **Upload file & Download file (Google Drive)**: Chọn đúng tài khoản Google Drive OAuth2 và chỉ định thư mục (Folder ID) lưu trữ hóa đơn.
- **Set Vision API & HTTP Request**: Điền Google Vision API Key vào biến cấu hình để node `HTTP Request` gửi hình ảnh dạng Base64 sang Google Vision xử lý OCR.
- **Basic LLM Chain & OpenRouter Chat Model**: Chọn credential OpenRouter, cấu hình model là `google/gemini-2.0-flash-exp:free`. Node `Structured Output Parser` sẽ ép LLM trả về đúng định dạng JSON các trường: Ngày, Mã chứng từ, Nội dung giao dịch, Nhà cung cấp và Giá trị.
- **Code & Code1**: Các node xử lý dữ liệu, làm sạch và chuẩn hóa các giá trị số (loại bỏ ký hiệu tiền tệ) trước khi đẩy vào Google Sheets.
- **Append or update row in sheet (Google Sheets)**: Kết nối tài khoản Google Sheets, trỏ tới file mẫu ([Template Google Sheets](https://docs.google.com/spreadsheets/d/1HMzQtFK9T-GDxGFSD7ErW_QLlq-PvCvoFASiHGG2fGM/edit?gid=0#gid=0)) và chọn chế độ `appendOrUpdate` dựa trên File ID.
- **Send a text message (Telegram)**: Cấu hình Bot Token và Chat ID để nhận tin nhắn tóm tắt giao dịch.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách upload một hình ảnh hóa đơn lên Form.
- Kiểm tra kết quả trên Google Drive, Google Sheets và Telegram.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để workflow tự động làm việc 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Ngoài Telegram, các sếp có thể gắn thêm node Slack hoặc Microsoft Teams để gửi thông báo cho đội ngũ kế toán.
- **Phân loại tự động**: Thêm các node điều kiện (If) sau bước LLM để phân loại hóa đơn theo hạn mức chi phí hoặc phòng ban.
- **Lưu trữ Log lỗi**: Thiết lập nhánh Error Trigger để bắt lỗi nếu hình ảnh hóa đơn quá mờ hoặc API quá tải, sau đó gửi cảnh báo về nhóm kỹ thuật.

### 📌 Kết luận
Workflow xử lý hóa đơn tự động này là một mảnh ghép hoàn hảo giúp các doanh nghiệp, hộ kinh doanh tối ưu hóa quy trình kế toán, tiết kiệm hàng chục giờ làm việc mỗi tháng. Hãy áp dụng ngay vào hệ thống của các sếp nhé!