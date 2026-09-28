---
title: "🚀 Tự động trích xuất biên lai ngân hàng Thái Lan từ LINE bằng OCR và lưu vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động nhận diện ảnh biên lai chuyển khoản ngân hàng Thái Lan từ LINE Chatbot, bóc tách dữ liệu bằng OCR Space và lưu trữ gọn gàng vào Google Sheets."
slug: "tu-dong-trich-xuat-bien-lai-ngan-hang-thai-lan-tu-line-n8n"
tags: [n8n, automation, no-code, line-bot, ocr, google-sheets]
keywords: [n8n workflow, trích xuất biên lai, OCR Space, LINE chatbot, Google Sheets, tự động hóa tài chính]
---

# 🚀 Tự động trích xuất biên lai ngân hàng Thái Lan từ LINE bằng OCR và lưu vào Google Sheets

Các sếp kinh doanh hoặc làm dịch vụ có khách hàng Thái Lan chắc chắn đã từng "đau đầu" với việc kiểm tra hàng trăm bill chuyển khoản mỗi ngày. Việc ngồi nhìn từng cái ảnh bill, đối chiếu số tiền, thời gian rồi nhập tay vào Excel hay Google Sheets vừa mất thời gian, vừa dễ nhầm lẫn chết người. 

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% tự động bằng n8n workflow mà không cần tốn một giọt mồ hôi nhập liệu thủ công nào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Deploy VPS tốc độ cao](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Khách gửi ảnh biên lai (slip) qua LINE Chatbot là hệ thống tự động nhận diện.
- **Bóc tách thông minh:** Sử dụng công nghệ OCR Space để đọc dữ liệu tiếng Thái (số tiền, thời gian, ngân hàng...).
- **Lưu trữ minh bạch:** Tự động lưu ảnh gốc lên Google Drive và ghi toàn bộ thông tin giao dịch vào Google Sheets theo thời gian thực.
- **Loại bỏ sai sót:** Không còn tình trạng nhìn nhầm số tiền hoặc bỏ sót đơn hàng của khách.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance** (Self-hosted hoặc n8n Cloud).
- **LINE Official Account (LINE Messaging API)** để tạo Webhook nhận tin nhắn/ảnh.
- **Tài khoản Google Drive & Google Sheets** để lưu trữ file và dữ liệu.
- **API Key từ OCR.space** (Có bản miễn phí để test thoải mái).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc import file JSON gốc từ nguồn cung cấp) dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **LINE Chatbot (`Webhook`):** 
  - Node này đóng vai trò lắng nghe sự kiện khi khách hàng gửi ảnh biên lai vào khung chat LINE.
  - Cần cấu hình Webhook URL trên LINE Developers Console trỏ về URL của node này.
- **Get image to Binary (`httpRequest`):** 
  - Sử dụng API `https://api-data.line.me/v2/bot/message/xxx/content` để tải file ảnh gốc từ LINE dựa trên ID tin nhắn.
  - Cần cấu hình `httpHeaderAuth` với Channel Access Token của LINE Bot.
- **Upload image to Google Drive (`googleDrive`):** 
  - Kết nối tài khoản Google Drive thông qua `googleDriveOAuth2Api`.
  - Chọn thư mục đích để lưu trữ toàn bộ ảnh biên lai khách gửi nhằm dễ dàng đối soát sau này.
- **Send Image URL to OCR Space for Text Extraction (`httpRequest`):** 
  - Cấu hình API endpoint của OCR Space: `https://api.ocr.space/parse/imageurl?apikey=YOURAPI&language=tha&isOverlayRequired=false&OCREngine=2&filetype=JPG&url=xxx`
  - Nhớ thay `YOURAPI` bằng khóa API thực tế của các sếp và thiết lập ngôn ngữ tiếng Thái (`language=tha`).
- **Extract Transaction Details (`code`):** 
  - Node JavaScript tùy chỉnh giúp bóc tách các trường dữ liệu quan trọng (số tiền, tên người gửi/nhận, thời gian giao dịch) từ chuỗi văn bản thô mà OCR trả về.
- **Record in Google Sheets (`googleSheets`):** 
  - Chọn tài khoản Google Sheets (`googleSheetsOAuth2Api`), trỏ tới file Google Sheets quản lý doanh thu.
  - Thiết lập operation là `append` để thêm dòng mới chứa thông tin giao dịch mỗi khi có khách chuyển khoản thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một ảnh biên lai mẫu vào LINE Bot để kiểm tra xem dữ liệu có được đẩy lên Google Sheets chuẩn chỉnh hay chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau Google Sheets để bắn thông báo "Ting ting" về nhóm nội bộ mỗi khi có khách thanh toán thành công.
- **Xử lý ngoại lệ (Error Handling):** Thêm nhánh Error Trigger để cảnh báo nếu ảnh khách gửi quá mờ, OCR không đọc được dữ liệu, giúp nhân viên chủ động liên hệ lại khách hàng.
- **Tự động phản hồi:** Thêm bước gửi tin nhắn tự động cảm ơn khách hàng qua LINE ngay sau khi ghi nhận giao dịch thành công.

### 📌 Kết luận
Việc tự động hóa khâu kiểm tra biên lai chuyển khoản ngân hàng Thái Lan qua LINE chưa bao giờ dễ dàng đến thế với n8n. Hãy thiết lập ngay hôm nay để tiết kiệm hàng giờ đồng hồ kiểm tra thủ công mỗi ngày cho đội ngũ vận hành của các sếp!