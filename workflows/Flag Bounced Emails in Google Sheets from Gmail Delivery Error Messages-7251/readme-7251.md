---
title: "🚀 Tự động đánh dấu email bị lỗi (Bounced Emails) trong Google Sheets từ Gmail với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét hộp thư Gmail tìm email lỗi gửi (bounce/delivery error), sau đó cập nhật cờ trạng thái vào Google Sheets để tối ưu các chiến dịch email marketing tiếp theo."
slug: "tu-dong-danh-dau-email-bi-loi-trong-google-sheets-tu-gmail"
tags: [n8n, automation, no-code, gmail, google-sheets, email-marketing]
keywords: [n8n workflow, tự động hóa email bounce, check bounced email google sheets, gmail delivery error n8n, quản lý email lỗi marketing]
---

# 🚀 Tự động đánh dấu email bị lỗi (Bounced Emails) trong Google Sheets từ Gmail

Các sếp có bao giờ đau đầu khi chạy chiến dịch email marketing nhưng hàng loạt email gửi đi bị trả về (bounced) do sai địa chỉ, hộp thư đầy hoặc lỗi hệ thống? Việc lọc thủ công từng email lỗi để loại bỏ khỏi danh sách gửi lần sau cực kỳ mất thời gian và dễ sai sót.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: quét hòm thư Gmail tìm các thông báo lỗi (Undelivered/Failure), trích xuất chính xác địa chỉ email bị lỗi, đối chiếu với Google Sheets và tự động đánh dấu (`err = "Y"`) để các chiến dịch sau tự động né các địa chỉ "chết" này ra.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần thủ công kiểm tra hòm thư và dò tìm danh sách gửi.
- **Bảo vệ uy tín tên miền (Sender Reputation):** Tự động loại bỏ các email lỗi ở các chiến dịch sau, giảm tỷ lệ đưa vào Spam của Gmail/Outlook.
- **Đồng bộ thời gian thực:** Cập nhật ngay lập tức trạng thái lỗi (`err = "Y"`) vào Google Sheets quản lý chiến dịch.
- **Hoạt động bền bỉ:** Chạy định kỳ hoặc theo kịch bản test thủ công nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt (khuyến nghị phiên bản 1.105.2 trở lên).
- **Tài khoản Google:** Cần quyền truy cập Gmail và Google Sheets (chuẩn bị Credentials OAuth2).
- **Google Sheet Template:** Sử dụng [Mẫu Google Sheet có sẵn](https://docs.google.com/spreadsheets/d/1mFKp3wmbV9qp2tpGGsN72zdiC32y8H1nhjdgP885y-U/edit?usp=sharing) (tương thích với workflow gửi email chiến dịch).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> **Import from File / Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:
- **Node `settings` (Set):** Điền chính xác **Google Sheet ID** của các sếp vào đây (chuỗi ký tự nằm giữa `/d/` và `/edit` trên URL của Google Sheet).
- **Node `readspamfolder` (Gmail):** 
  - Kết nối tài khoản Gmail thông qua `gmailOAuth2`.
  - Cấu hình để quét các email thông báo lỗi trả về (thường nằm ở thư mục Spam hoặc Inbox tùy cấu hình hệ thống mail).
- **Node `undelivered_failure` (If):** Kiểm tra điều kiện tiêu đề hoặc nội dung email chứa từ khóa *"Undelivered"* hoặc *"Failure"*.
- **Node `geterremail` (Code) & `listerremail` (Set):** Xử lý logic trích xuất địa chỉ email bị lỗi từ phần thân message và lọc bỏ các bản ghi trùng lặp (duplication).
- **Node `lookupemail` & `update_err` (Google Sheets):** 
  - Kết nối tài khoản `googleSheetsOAuth2Api`.
  - Node `lookupemail` sẽ tìm số dòng (`row_number`) khớp với cột `email` bằng biểu thức: `{{ $('geterremail').item.json.extractedEmails }}`.
  - Node `update_err` sẽ cập nhật giá trị cột err thành `"Y"` dựa trên `{{ $('lookupemail').item.json.row_number }}`.

#### 3. Kích hoạt ⚡️
- Click vào node **When clicking ‘Test workflow’** (`manualTrigger`) để chạy thử nghiệm xem dữ liệu email lỗi có được trích xuất và update vào Sheet thành công hay không.
- Sau khi test OK, gạt công tắc **Active** ở góc trên cùng bên phải để bật chế độ tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Nối thêm node Telegram hoặc Slack ở cuối luồng để nhận tin nhắn cảnh báo mỗi khi có một email bị bounce mới được ghi nhận vào hệ thống.
- **Chạy tự động định kỳ:** Thay thế node `manualTrigger` bằng node `Schedule Trigger` (ví dụ: chạy mỗi 2 tiếng hoặc mỗi ngày 1 lần) để hệ thống tự quét hòm thư mà không cần can thiệp thủ công.
- **Mở rộng báo cáo:** Tạo thêm một trang tính (Tab) thống kê tỷ lệ Bounce Rate theo ngày để dễ dàng theo dõi sức khỏe chiến dịch marketing.

### 📌 Kết luận
Việc kiểm soát email bị lỗi bounce là chìa khóa sống còn để giữ sạch danh sách khách hàng (Clean Email List) và nâng cao tỷ lệ mở email. Hãy áp dụng ngay workflow n8n này để tối ưu hóa toàn bộ quy trình vận hành marketing của doanh nghiệp các sếp nhé!