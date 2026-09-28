---
title: "🚀 Tự động trích xuất hóa đơn vào Excel bằng Google Gemini, OCR và Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình đọc hóa đơn từ PDF hoặc hình ảnh gửi qua Telegram, dùng AI Google Gemini trích xuất dữ liệu và lưu thẳng vào Microsoft Excel."
slug: "tu-dong-trich-xuat-hoa-don-vao-excel-google-gemini-telegram"
tags: [n8n, automation, ai, google-gemini, telegram, microsoft-excel]
keywords: [n8n workflow, trích xuất hóa đơn, google gemini ai, ocr telegram excel, tự động hóa kế toán]
---

# 🚀 Tự động trích xuất hóa đơn vào Excel bằng Google Gemini, OCR và Telegram

Các sếp có bao giờ cảm thấy mệt mỏi mỗi cuối tháng khi phải ngồi "hoa mắt chóng mặt" nhập hàng trăm tờ hóa đơn, biên lai từ PDF hoặc ảnh chụp vào file Excel chưa? Sai sót con số là chuyện cơm bữa, chưa kể tốn rất nhiều thời gian quý báu đáng lẽ dùng để phát triển kinh doanh.

Đừng lo nữa các sếp! Hôm nay em xin giới thiệu một siêu phẩm workflow n8n được thiết kế bởi chuyên gia Ramdoni. Hệ thống này sẽ tự động hóa toàn bộ quy trình: Các sếp chỉ cần gửi ảnh hoặc file PDF hóa đơn qua **Telegram**, AI **Google Gemini** sẽ thông minh đọc hiểu, trích xuất toàn bộ thông tin chuẩn xác, và tự động lưu vào **Microsoft Excel** mà không cần đụng tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian nhập liệu:** Không còn cảnh gõ phím mỏi tay, dữ liệu tự động đồng bộ vào Excel ngay khi gửi ảnh lên Telegram.
- **Độ chính xác cực cao với AI:** Kết hợp sức mạnh của OCR (Tesseract) cho ảnh và công nghệ trích xuất ngữ nghĩa đỉnh cao từ Google Gemini.
- **Tương tác mượt mà qua chat:** Nhận thông báo trạng thái xử lý (đang xử lý, thành công, file lỗi) ngay trên Telegram cá nhân hoặc nhóm chat.
- **Hoạt động không nghỉ ngơi 24/7:** Sẵn sàng nhận hóa đơn bất cứ lúc nào, ở bất cứ đâu trên điện thoại hay máy tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản Self-hosted hoặc n8n Cloud).
- **Telegram Bot:** Tạo một bot qua [@BotFather](https://t.me/BotFather) để lấy API Token.
- **Google Gemini API Key:** Tài khoản Google AI Studio để sử dụng node Google Gemini phân tích dữ liệu.
- **Microsoft Excel (OneDrive / SharePoint):** Tài khoản Microsoft 365 để lưu file Excel.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc tải file về, sau đó chọn **Import from File** hoặc dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Telegram Trigger**: Kết nối với tài khoản Telegram Credentials của bot các sếp vừa tạo. Node này sẽ hứng sự kiện khi có file/ảnh gửi vào bot.
- **Get Image / Get PDF**: Cấu hình lấy file từ Telegram về n8n để xử lý tiếp.
- **Extract Text from Image (OCR)** (Sử dụng Tesseract) & **Extract PDF Text**: Đảm bảo trích xuất phần text thô từ ảnh hoặc file PDF đầu vào.
- **Extract Structured Data (AI)** (Google Gemini): Cấu hình Google Gemini Credentials và cung cấp Prompt chi tiết để ép AI trả về dữ liệu cấu trúc (tên nhà cung cấp, ngày tháng, tổng tiền, mã số thuế...).
- **Save Data to Excel** (Microsoft Excel): Chọn file Excel đích trên OneDrive/SharePoint và ánh xạ (map) các trường dữ liệu từ bước AI sang các cột tương ứng trong bảng tính của các sếp.
- **Các node Notifikasi / Send Success Notification**: Cấu hình Chat ID để bot Telegram gửi tin nhắn báo cáo kết quả về cho các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử gửi một tấm ảnh chụp hóa đơn bất kỳ vào Bot Telegram để test xem dữ liệu có bay thẳng vào file Excel không nhé.
- Nếu mọi thứ chạy trơn tru, hãy gạt công tắc sang **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì Microsoft Excel, các sếp có thể dễ dàng thay thế bằng Google Sheets chỉ bằng cách đổi node cuối cùng.
- **Thêm bước Phê duyệt (Approval):** Thêm node Telegram với các nút bấm "Duyệt / Từ chối" trước khi dữ liệu được ghi vào Excel chính thức.
- **Báo cáo tổng kết:** Thêm một lịch chạy định kỳ (Schedule Trigger) vào cuối tuần để bot Telegram tự động tổng hợp tổng chi phí tuần gửi cho sếp qua tin nhắn.

### 📌 Kết luận
Tự động hóa quy trình xử lý hóa đơn chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Hãy "lên đồ" ngay hôm nay để giải phóng sức lao động thủ công cho đội ngũ kế toán và kinh doanh của các sếp nhé!