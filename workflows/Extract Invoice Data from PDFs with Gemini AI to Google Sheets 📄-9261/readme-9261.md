---
title: "🚀 Tự động trích xuất thông tin hóa đơn PDF bằng Gemini AI vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình đọc file hóa đơn PDF từ Google Drive, trích xuất dữ liệu thông minh bằng Google Gemini AI và lưu trữ gọn gàng vào Google Sheets."
slug: "trich-xuat-hoa-don-pdf-gemini-ai-google-sheets"
tags: [n8n, automation, no-code, google-sheets, google-drive, gemini-ai]
keywords: [n8n workflow, trích xuất hóa đơn PDF, Gemini AI, Google Sheets automation, tự động hóa kế toán, AI Agent n8n]
---

# 🚀 Tự động trích xuất thông tin hóa đơn PDF bằng Gemini AI vào Google Sheets

Các sếp có đang mệt mỏi với việc kiểm tra hàng trăm hóa đơn, chứng từ PDF mỗi tháng, sau đó lọ mọ nhập từng con số, tên nhà cung cấp, mã số thuế vào Google Sheets hay phần mềm kế toán? Công việc thủ công này không chỉ ngốn hàng giờ đồng hồ quý giá mà còn cực kỳ dễ xảy ra sai sót.

Đừng lo nữa các sếp ơi! Bài viết này sẽ hướng dẫn các sếp thiết lập một siêu workflow n8n sử dụng sức mạnh đa phương thức (Multimodal AI) của **Google Gemini AI** kết hợp cùng **Google Drive** và **Google Sheets**. Hệ thống sẽ tự động "đọc hiểu" hóa đơn PDF, bóc tách chính xác các trường dữ liệu cần thiết và ghi nhận tự động 100% không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công (data entry), loại bỏ hoàn toàn các lỗi sai sót do gõ nhầm số liệu.
- **Xử lý thông minh với AI:** Gemini AI có khả năng đọc hiểu các định dạng hóa đơn khác nhau từ nhiều nhà cung cấp mà không cần template cố định.
- **Đồng bộ thời gian thực:** Hóa đơn vừa bỏ lên Google Drive là tự động được quét, xử lý và cập nhật ngay vào Google Sheets.
- **Tự động hóa toàn diện:** Tích hợp sẵn cơ chế kiểm tra file trùng lặp (`Compare Datasets1`), ghi log (`Log the processing of the doc1`) và gửi thông báo qua Gmail (`Send a message1`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Drive & Google Sheets Accounts:** Để lưu trữ file PDF hóa đơn và bảng tính lưu dữ liệu đầu ra.
- **Google Gemini API Key (Google AI Studio):** Để cấp quyền cho các node AI Agent và Chat Model đọc hiểu tài liệu.
- **Gmail Account (Tuỳ chọn):** Dùng để gửi email thông báo khi có hóa đơn mới được xử lý xong.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình bằng cách chọn `Add workflow` -> `Import from Clipboard`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Google Drive Trigger1 & Download file1:** Kết nối tài khoản Google Drive của các sếp và trỏ đến thư mục chuyên chứa hóa đơn PDF đầu vào.
- **Compare Datasets1 & Read processed docs1:** Node này giúp so sánh xem file PDF nào đã được xử lý trước đó hay chưa, tránh việc xử lý lặp lại gây tốn tài nguyên và trùng dữ liệu. Các sếp cần liên kết chính xác với file Google Sheets chứa log xử lý.
- **AI Agent - get targeted elements from text1, Google Gemini Chat Model2 & 3:** 
  - Chọn credential Google Gemini API cho các chat model.
  - Tinh chỉnh Prompt trong AI Agent để hướng dẫn AI trích xuất đúng các trường thông tin mong muốn (Ví dụ: Tên công ty, Mã số thuế, Tổng tiền, Ngày hóa đơn, v.v.).
- **Structured Output Parser1:** Định nghĩa schema JSON chuẩn đầu ra để đảm bảo dữ liệu Gemini trả về luôn đúng định dạng cấu trúc mà Google Sheets yêu cầu.
- **Update invoice Fields1 & Log the processing of the doc1:** Kết nối tài khoản Google Sheets và chọn đúng file bảng tính (Spreadsheet) cùng tên Sheet (Worksheet) để lưu trữ kết quả bóc tách.
- **Send a message1 (Gmail):** Cấu hình tài khoản Gmail để gửi thông báo xác nhận mỗi khi một hóa đơn mới được phân tích thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một vài file PDF mẫu trên Google Drive để kiểm tra xem dữ liệu có đổ về Google Sheets chuẩn xác hay không.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7 mỗi khi có hóa đơn mới xuất hiện trong thư mục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot thông báo:** Thêm node **Telegram** hoặc **Slack** ngay sau bước xử lý hóa đơn để bắn thông báo tức thời cho kế toán trưởng mỗi khi có hóa đơn giá trị lớn.
- **Phân loại tự động:** Dùng thêm một bước AI phụ để tự động phân loại hóa đơn thuộc danh mục chi phí nào (Marketing, Vận hành, Công nghệ,...) trước khi đẩy vào Google Sheets.
- **Báo cáo định kỳ:** Kết hợp thêm node **Cron (Schedule Trigger)** để chạy báo cáo tổng hợp chi phí hàng tuần/tháng rồi gửi thẳng vào email ban giám đốc.

### 📌 Kết luận
Việc tự động hóa trích xuất hóa đơn PDF bằng Gemini AI và n8n chính là bước đi đầu tiên cực kỳ hiệu quả để đưa doanh nghiệp bước vào kỷ kỷ nguyên tự động hóa thông minh. Hãy triển khai ngay hôm nay để giải phóng sức lao động cho đội ngũ kế toán và tối ưu hóa vận hành các sếp nhé!